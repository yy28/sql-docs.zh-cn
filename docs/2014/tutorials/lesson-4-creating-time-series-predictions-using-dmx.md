---
title: 第 4 课： 创建使用 DMX 时序预测 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a345b37d13ade71baad6635cee0508e97d7755eb
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312405"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>第 4 课：使用 DMX 创建时序预测
  在本课程和下一课中，你将使用数据挖掘扩展插件 (DMX) 来创建不同类型的基于时序模型中创建的预测[第 1 课： 创建时序挖掘模型和挖掘结构](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)和[第 2 课： 将挖掘模型添加到时序挖掘结构](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)。  
  
 使用时序模型，可以通过许多选项来进行预测：  
  
-   使用挖掘模型中现有的模式和数据  
  
-   使用挖掘模型中的现有模式但提供新数据  
  
-   在模型中添加新数据或者更新模型。  
  
 下面概述了进行这些类型的预测所需的语法：  
  
 默认的序列预测  
 使用[PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)从定型的挖掘模型返回指定的数目的预测。  
  
 有关示例，请参阅[PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)或[时间 Series Model Query Examples](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)。  
  
 EXTEND_MODEL_CASES  
 使用[PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)使用 EXTEND_MODEL_CASES 参数时要添加新数据，扩展的序列，并创建基于更新的挖掘模型的预测。  
  
 本教程包含有关如何使用 EXTEND_MODEL_CASES 的示例。  
  
 REPLACE_MODEL_CASES  
 使用[PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)使用 REPLACE_MODEL_CASES 参数来将原始数据替换为新的数据序列，然后创建基于应用于新数据挖掘模型中的模式的预测系列。  
  
 有关如何使用 REPLACE_MODEL_CASES 的示例，请参阅[第 2 课： 生成预测方案&#40;中间 Data Mining Tutorial&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   创建一个查询，基于现有数据获得默认预测。  
  
 在下一课中，您将执行下列相关任务：  
  
-   创建一个查询，提供新数据并获得更新的预测。  
  
 除了使用 DMX 手动创建查询以外，还可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的预测查询生成器来创建预测。  
  
## <a name="simple-time-series-prediction-query"></a>简单的时序预测查询  
 第一步是结合使用 `SELECT FROM` 语句和 `PredictTimeSeries` 函数来创建时序预测。 时序模型支持一种简化的预测创建语法：您不必提供任何输入，而只需指定要创建的预测数。 下面是将您使用的语句的一般示例：  
  
```  
SELECT <select list>   
FROM [<mining model name>]   
WHERE [<criteria>]  
```  
  
 选择列表可以包含从模型的列，如产品的名称行要创建预测或预测函数，如[延隔时间&#40;DMX&#41; ](/sql/dmx/lag-dmx)或[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)，这是专门为时序挖掘模型。  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>创建简单的时序预测查询  
  
1.  在**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将该语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     使用：  
  
    ```  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    ```  
  
     第一行从挖掘模型中检索用来标识序列的值。  
  
     第二行和第三行使用 `PredictTimeSeries` 函数。 每一行都预测一个不同的属性（`[Quantity]` 或 `[Amount]`）。 可预测属性名称后面的数字指定要预测的时间步长量。  
  
     `AS` 子句用于为每个预测函数返回的列提供名称。 如果您不提供别名，则默认情况下将返回这两列，标签为 `Expression`。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  将  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     使用：  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    FROM   
    [Forecasting_MIXED]  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
6.  上**文件**菜单上，单击**DMXQuery1.dmx 另存为**。  
  
7.  在**另存为**对话框中，浏览到相应的文件夹，然后将该文件`SimpleTimeSeriesPrediction.dmx`。  
  
8.  在工具栏上，单击**执行**按钮。  
  
     该查询将针对在 `WHERE` 子句中指定的产品和地区的每个组合（共两个组合）返回 6 个预测。  
  
 在下一课中，您将创建一个为模型提供新数据的查询，并将该预测的结果与刚创建的预测进行比较。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [第 5 课：扩展时序模型](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>请参阅  
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)   
 [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)   
 [时间时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [第 2 课： 生成预测方案&#40;中间数据挖掘教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
