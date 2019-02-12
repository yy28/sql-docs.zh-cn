---
title: 时序预测使用替换数据 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c96b70775105ea9446810ac3b064ae7cb07d4337
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010229"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>使用替换数据进行时序预测（数据挖掘中级教程）
  在本任务中，您将基于全球范围内的销售额数据生成新模型。 然后，将创建一个将全球范围内的销售额模型应用于某个单独区域的预测查询。  
  
## <a name="building-a-general-model"></a>生成通用模型  
 记住您对原始挖掘模型的结果分析揭示在某些区域和产品系列上存在较大的差异。 例如，M200 型号在北美的销售很强，而 T1000 型号的销售则不是这样。 但是，分析被复杂，因为某些系列没有太多数据或在不同的点开始时间的数据。 还缺少一些数据。  
  
 ![时序预测 M200 和 T1000 数量](../../2014/tutorials/media/6series-defaultforecasting.gif "时序预测 M200 和 T1000 数量")  
  
 为了解决某些数据质量问题，您决定将全球范围内的销售额数据合并，并使用一般销售趋势集来生成可应用于预测任何区域未来销售额的模型。  
  
 创建预测时，您将使用通过定型全球范围内的销售额数据生成的模式，但是将用每个区域的销售额数据替换历史数据点。 那样就保留了趋势的形状，但是使预测值与每个区域和型号的历史销售额数字一致。  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>使用时序模型执行交叉预测  
 使用使用一个序列中的数据预测另一个序列中的趋势的过程称为交叉预测。 可以在很多方案中使用交叉预测：例如，您可能决定电话销售额是总体经济活动的合适预测因子，将对电视销售额定型的模型应用到一般经济数据。  
  
 通过使用中函数的实参 REPLACE_MODEL_CASES 参数在 SQL Server 数据挖掘，执行交叉预测[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
 在下一个任务中，您将学习如何使用 REPLACE_MODEL_CASES。 您将使用合并的全球范围内的销售额数据来生成模型，然后创建将通用模型映射到替换数据的预测查询。  
  
 假定您现在已熟悉如何生成数据挖掘模型，因此简化了生成模型的说明。  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>使用聚合数据生成挖掘结构和挖掘模型  
  
1.  在中**解决方案资源管理器**，右键单击**挖掘结构**，然后选择**新建挖掘结构**以启动数据挖掘向导。  
  
2.  在数据挖掘向导中，进行以下选择：  
  
    -   算法：Microsoft 时序  
  
    -   使用在此高级课程中早些时候生成的数据源作为模型的源。 请参阅[高级时序预测&#40;数据挖掘中级教程&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)。  
  
         数据源视图： `AllRegions`  
  
    -   为序列键和时间键选择以下列：  
  
         键时间：ReportingDate  
  
         密钥：地区  
  
    -   为 `Input` 和 `Predict` 选择以下列：  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   有关**挖掘结构名称**，类型： `All Regions`  
  
    -   有关**挖掘模型名称**，类型： `All Regions`  
  
3.  处理新结构和新模型。  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>生成预测查询并映射替换数据  
  
1.  如果模型尚未打开，双击 AllRegions 结构，并在数据挖掘设计器中，单击**挖掘模型预测**选项卡。  
  
2.  在中**挖掘模型**窗格中，模型 AllRegions 应该已处于选中状态。 如果不选择它，请单击**选择模型**，然后选择模型 AllRegions。  
  
3.  在中**选择输入表**窗格中，单击**选择事例表**。  
  
4.  在中**选择表**对话框中，更改数据源为 T1000 Pacific Region，然后单击**确定**。  
  
5.  右键单击挖掘模型和输入的数据之间的联接线并选择**修改连接**。 如下所示将数据源视图中的数据映射到模型：  
  
    1.  验证挖掘模型中的 ReportingDate 列映射到输入数据中的 ReportingDate 列。  
  
    2.  在**修改映射**下单击对话框中，在为模型列 AvgQty，行**表列**，然后选择 T1000 Pacific.Quantity。 单击“确定” 。  
  
         此步骤将在用于预测平均数量的模型中创建的列映射到用于销售数量的 T1000 系列的实际数据。  
  
    3.  没有映射到任何输入列的模型中的列区域。  
  
         因为该模型聚合所有系列上的数据，所以，对于 T1000 Pacific 之类的系列值没有匹配项，并且在预测查询运行时将引发错误。  
  
6.  现在，您将生成预测查询。  
  
     首先，将一个列添加到结果，这些结果输出模型的 AllRegions 标签以及预测。 这样您知道了结果基于通用模型。  
  
    1.  在网格中，单击第一个空行下,**源**，然后选择 AllRegions 挖掘模型。  
  
    2.  有关**字段**，选择区域。  
  
    3.  有关**别名**，类型**模型使用**。  
  
7.  接下来，向结果中添加另一个标签，以便您可以看到该预测针对哪个系列。  
  
    1.  单击一个空行，然后在**源**，选择**自定义表达式**。  
  
    2.  在中**别名**列中，键入**ModelRegion**。  
  
    3.  在中**条件/参数**列中，键入`'T1000 Pacific'`。  
  
8.  现在您将设置交叉预测函数。  
  
    1.  单击一个空行，然后在**源**，选择**预测函数**。  
  
    2.  在中**字段**列中，选择**PredictTimeSeries**。  
  
    3.  有关**别名**，类型**Predicted Values**。  
  
    4.  将字段 AvgQty 拖从**挖掘模型**到窗格**条件/参数**通过使用拖放操作的列。  
  
    5.  在中**条件/参数**列中，在该字段名称，键入以下文本： `,5, REPLACE_MODEL_CASES`  
  
         完整文本**条件/参数**文本框应按如下所示： `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. 单击**结果**。  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>在 DMX 中创建交叉预测查询  
 您可能注意到一个交叉预测问题：即要将通用模型应用到不同数据序列（如北美区域的 T1000 产品型号），必须为每个序列创建不同查询，以便您可以将每组输入映射到该模型。  
  
 但是，不用在设计器中生成查询，您可以切换到 DMX 视图并编辑创建的 DMX 语句。 例如，下面的 DMX 语句表示您刚创建的查询：  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 若要将此语句应用于其他模型，只需编辑查询语句，替换筛选条件和更新与每个结果关联的标签。  
  
 例如，如果通过将“Pacific”替换为“North America”来更改筛选条件和列标签，您将基于通用模型中的模式得到 T1000 产品在北美洲的预测。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [比较预测的预测模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries (DMX)](/sql/dmx/predicttimeseries-dmx)  
  
  
