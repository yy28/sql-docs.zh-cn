---
title: 使用替换数据 （中间数据挖掘教程） 的时序预测 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d5639aa63affadcdf79acc6029840e7025081245
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312465"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>使用替换数据进行时序预测（数据挖掘中级教程）
  在本任务中，您将基于全球范围内的销售额数据生成新模型。 然后，将创建一个将全球范围内的销售额模型应用于某个单独区域的预测查询。  
  
## <a name="building-a-general-model"></a>生成通用模型  
 记住您对原始挖掘模型的结果分析揭示在某些区域和产品系列上存在较大的差异。 例如，M200 型号在北美的销售很强，而 T1000 型号的销售则不是这样。 但是，分析是十分复杂的，因为某些系列没有太多数据，或者数据在不同的时间点开始。 还缺少一些数据。  
  
 ![序列预测 M200 和 T1000 数量](../../2014/tutorials/media/6series-defaultforecasting.gif "序列预测 M200 和 T1000 数量")  
  
 为了解决某些数据质量问题，您决定将全球范围内的销售额数据合并，并使用一般销售趋势集来生成可应用于预测任何区域未来销售额的模型。  
  
 创建预测时，您将使用通过定型全球范围内的销售额数据生成的模式，但是将用每个区域的销售额数据替换历史数据点。 那样就保留了趋势的形状，但是使预测值与每个区域和型号的历史销售额数字一致。  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>使用时序模型执行交叉预测  
 使用使用一个序列中的数据预测另一个序列中的趋势的过程称为交叉预测。 可以在很多方案中使用交叉预测：例如，您可能决定电话销售额是总体经济活动的合适预测因子，将对电视销售额定型的模型应用到一般经济数据。  
  
 你可以在 SQL Server 数据挖掘，来执行通过使用该函数的自变量中的参数 REPLACE_MODEL_CASES 跨预测[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
 在下一个任务中，您将学习如何使用 REPLACE_MODEL_CASES。 您将使用合并的全球范围内的销售额数据来生成模型，然后创建将通用模型映射到替换数据的预测查询。  
  
 假定您现在已熟悉如何生成数据挖掘模型，因此简化了生成模型的说明。  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>使用聚合数据生成挖掘结构和挖掘模型  
  
1.  在**解决方案资源管理器**，右键单击**挖掘结构**，然后选择**新挖掘结构**以启动数据挖掘向导。  
  
2.  在数据挖掘向导中，进行以下选择：  
  
    -   算法：Microsoft 时序  
  
    -   使用在此高级课程中早些时候生成的数据源作为模型的源。 请参阅[高级时序预测&#40;中间数据挖掘教程&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)。  
  
         数据源视图： `AllRegions`  
  
    -   为序列键和时间键选择以下列：  
  
         关键时间： ReportingDate  
  
         键： 区域  
  
    -   为 `Input` 和 `Predict` 选择以下列：  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   有关**挖掘结构名称**，类型： `All Regions`  
  
    -   有关**挖掘模型名称**，类型： `All Regions`  
  
3.  处理新结构和新模型。  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>生成预测查询并映射替换数据  
  
1.  如果模型未打开，双击 AllRegions 结构，并在数据挖掘设计器中，单击**挖掘模型预测**选项卡。  
  
2.  在**挖掘模型**窗格中，应已选择 AllRegions 的模型。 如果未选择，请单击**选择模型**，然后选择的模型，AllRegions。  
  
3.  在**选择输入表**窗格中，单击**选择事例表**。  
  
4.  在**选择表**对话框中，更改数据源到 T1000 太平洋区域，然后单击**确定**。  
  
5.  右键单击挖掘模型和输入的数据之间的联接线并选择**修改连接**。 如下所示将数据源视图中的数据映射到模型：  
  
    1.  验证挖掘模型中的 ReportingDate 列映射到输入数据中的 ReportingDate 列。  
  
    2.  在**修改映射**对话框中，为模型列 AvgQty，行中的单击下**表列**，然后选择 T1000 Pacific.Quantity。 单击“确定” 。  
  
         此步骤将在用于预测平均数量的模型中创建的列映射到用于销售数量的 T1000 系列的实际数据。  
  
    3.  不到任何输入列映射模型中的列区域。  
  
         因为该模型聚合所有系列上的数据，所以，对于 T1000 Pacific 之类的系列值没有匹配项，并且在预测查询运行时将引发错误。  
  
6.  现在，您将生成预测查询。  
  
     首先，将一个列添加到结果，这些结果输出模型的 AllRegions 标签以及预测。 这样您知道了结果基于通用模型。  
  
    1.  在网格中，单击第一个空行下,**源**，然后选择 AllRegions 挖掘模型。  
  
    2.  有关**字段**，选择区域。  
  
    3.  有关**别名**，类型**模型使用**。  
  
7.  接下来，向结果中添加另一个标签，以便您可以看到该预测针对哪个系列。  
  
    1.  单击某个空行，然后在**源**，选择**自定义表达式**。  
  
    2.  在**别名**列中，键入**ModelRegion**。  
  
    3.  在**条件/参数**列中，键入`'T1000 Pacific'`。  
  
8.  现在您将设置交叉预测函数。  
  
    1.  单击某个空行，然后在**源**，选择**预测函数**。  
  
    2.  在**字段**列中，选择**PredictTimeSeries**。  
  
    3.  有关**别名**，类型**预测值**。  
  
    4.  拖动字段 AvgQty 从**挖掘模型**到窗格**条件/参数**通过使用拖放操作的列。  
  
    5.  在**条件/参数**列中，在字段名之后键入以下文本： `,5, REPLACE_MODEL_CASES`  
  
         完整文本**条件/参数**文本框中应，如下所示： `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
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
 [比较用于预测模型的预测&#40;中间数据挖掘教程&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [时间时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
