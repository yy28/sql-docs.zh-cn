---
title: 高级时序预测（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca144d1d473f7df49f73d5ed170052c61ce6107d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893692"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>高级时序预测（数据挖掘中级教程）
  通过浏览预测模型，您发现尽管大多数区域的销售额都遵循一个相似的模式，但是某些区域和某些型号（例如，太平洋地区的 M200 型号）却呈现出完全不同的趋势。 您对此并不感到惊奇，因为您知道区域之间的差异很常见，可以由多种因素引起，其中包括市场促销、错误的报告或地理政治事件。  
  
 但是，您的用户要求提供可在全球范围内应用的模型。 因此，为了将各个因素对预测所造成的影响降至最低，您决定生成一个基于全球范围内销售额的聚合度量值的模型。 然后，您可以使用此模型对每个区域进行预测。  
  
 在本任务中，您将生成所需的所有数据源以执行高级预测任务。 您将创建两个数据源视图用作预测查询的输入，一个数据源视图用于生成新模型。  
  
 **步骤**  
  
1.  [准备扩展的销售额数据（用于预测）](#bkmk_newExtendData)  
  
2.  [准备聚合数据（用于生成模型）](#bkmk_newReplaceData)  
  
3.  [准备序列数据（用于交叉预测）](#bkmk_CrossData2)  
  
4.  [使用 EXTEND 进行预测](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [创建交叉预测模型](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [使用 REPLACE 进行预测](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [查看新预测](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="creating-the-new-extended-sales-data"></a><a name="bkmk_newExtendData"></a>创建新的扩展销售数据  
 要更新您的销售额数据，您需要获取最新的销售额数字。 特别关注来自太平洋地区的数据，该地区启动了区域性促销以吸引新商店的关注并提升产品知名度。  
  
 对于此方案，我们假定已从 Excel 工作簿导入数据，该工作簿只包含几个月的新数据供几个区域使用。 您将使用 Transact-sql 脚本为数据创建一个表，然后定义要用于预测的数据源视图。  
  
#### <a name="create-the-table-with-new-sales-data"></a>使用新的销售额数据创建表  
  
1.  在 Transact-SQL 查询窗口中，执行以下语句以将销售额数据添加到 AdventureWorksDW 数据库（或者任何其他数据库）。  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  使用以下脚本插入新值。  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  引号用于货币值，以防止出现逗号分隔符和货币符号的问题。 您还可以采用以下格式传入货币值：`130170.22`  
    >   
    >  请注意，在示例数据库中使用的日期对于此版本已更改。 如果您使用较早版本的 AdventureWorks，则可能需要对插入的日期进行相应的调整。  
  
###  <a name="create-a-data-source-view-using-the-new-sales-data"></a><a name="bkmk_newReplaceData"></a>使用新的销售数据创建数据源视图  
  
1.  在**解决方案资源管理器**中，右键单击 "**数据源视图**"，然后选择 "**新建数据源视图**"。  
  
2.  在数据源视图向导中进行以下选择：  
  
     **数据源**：[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **选择表和视图**：选择刚刚创建的表 NewSalesData。  
  
3.  单击 **“完成”** 。  
  
4.  在数据源视图设计图面中，右键单击 NewSalesData，然后选择 "**浏览数据**" 以验证数据。  
  
> [!WARNING]  
>  您仅将此数据用于预测，因此数据是否完整并不重要。  
  
##  <a name="creating-the-data-for-the-cross-prediction-model"></a><a name="bkmk_CrossData2"></a>创建跨预测模型的数据  
 在原始预测模型中使用的数据已被视图 vTimeSeries 略微分组，它将几个自行车型号折叠为更少的类别，将几个国家/地区的结果合并为区域结果。 为了创建可用于全球范围内预测的模型，您将直接在数据源视图设计器中创建一些其他简单的聚合。 新的数据源视图将仅包含所有产品在各个区域的销售额的总和以及平均值。  
  
 创建了用于模型的数据源后，必须创建用于预测的新数据源视图。 例如，您要使用新的全球范围内模型预测欧洲的销售额，必须仅输入欧洲区域的数据。 因此，您将设置一个筛选原始数据的新数据源视图，并为每组预测查询更改筛选条件。  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>使用自定义数据源视图创建模型数据  
  
1.  在**解决方案资源管理器**中，右键单击 "**数据源视图**"，然后选择 "**新建数据源视图**"。  
  
2.  在向导的欢迎页上，单击 **“下一步”**。  
  
3.  在 **“选择数据源”** 页上，选择 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]，然后单击 **“下一步”**。  
  
4.  在 "**选择表和视图**" 页中，不添加任何表，只需单击 "**下一步**"。  
  
5.  在 "**完成向导**" 页上，键入名称`AllRegions`，然后单击 "**完成**"。  
  
6.  接下来，右键单击空白数据源视图设计图面，然后选择 "**新建命名查询**"。  
  
7.  在 "**创建命名查询**" 对话框中， **Name**为 "名称`AllRegions`" 键入，为 "**说明**" 键入**所有型号和区域的销售额的总和和平均值**。  
  
8.  在“SQL 文本”窗格中键入以下语句，然后单击“确定”：  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. 右键单击该表， `AllRegions`然后选择 "**浏览数据**"。  
  
###  <a name="to-create-the-series-data-for-cross-prediction"></a><a name="bkmk_CrossData"></a>创建用于交叉预测的序列数据  
  
1.  在**解决方案资源管理器**中，右键单击 "**数据源视图**"，然后选择 "**新建数据源视图**"。  
  
2.  在数据源视图向导中进行以下选择：  
  
     **数据源**：[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **选择表和视图**：不选择任何表  
  
     **名称**：`T1000 Pacific Region`  
  
3.  单击 **“完成”** 。  
  
4.  右键单击**T1000 太平洋 Region**的空设计图面，然后选择 "**新建命名查询**"。  
  
     **“创建命名查询”** 对话框随即出现。 重新键入名称，然后添加下面的说明：  
  
     **名称**：`T1000 Pacific Region`  
  
     **说明**：**按`vTimeSeries`区域和型号筛选**  
  
5.  在“文本”窗格中键入以下查询，然后单击“确定”：  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  由于需要单独为每个序列创建预测，您可能要复制查询文本并将其保存为文本文件，以便其他数据序列可以重用它。  
  
6.  在数据源视图设计图面中，右键单击 "T1000"，然后选择 "**浏览数据**" 以验证是否已正确筛选数据。  
  
     在创建交叉预测查询时，您将使用此数据作为模型的输入。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [使用更新的数据 &#40;中级数据挖掘教程的时序预测&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [多维模型中的数据源视图](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
