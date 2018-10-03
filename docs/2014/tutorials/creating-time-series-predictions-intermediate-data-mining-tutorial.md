---
title: 创建时序预测 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 109c4eb07dd34aa5ef3e41d794edfc39ffffcac8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119867"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>创建时序预测（数据挖掘中级教程）
  在本课前面的任务中，您已经创建了时序模型并浏览了结果。 默认情况下，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将始终为一个时序模型创建一组五 (5) 个预测，并将预测值作为预测图的一部分显示。 但是，也可以通过生成数据挖掘扩展插件 (DMX) 预测查询，来创建预测。  
  
 在本任务中，您将创建一个预测查询，该查询生成的预测就是您在查看器中看到的同一预测。 该任务假定您已经学完了“数据挖掘基础教程”中的课程，并且熟悉如何使用预测查询生成器。 现在，您将学习如何创建特定于时序模型的查询。  
  
## <a name="creating-time-series-predictions"></a>创建时序预测  
 一般来说，创建预测查询的第一步是选择挖掘模型和输入表。 但是，时序模型不需要为常规预测进行额外输入。 因此，您在进行预测时并不需要指定新数据源，除非您要将数据添加到模型或替换数据。  
  
 在本课程中，您必须指定预测步骤数。 可以指定序列名称来获取针对产品和区域的特定组合的预测。  
  
#### <a name="to-select-a-model-and-input-table"></a>选择模型和输入表  
  
1.  上**挖掘模型预测**数据挖掘设计器选项卡，在**挖掘模型**框中，单击**选择模型**。  
  
2.  在中**选择挖掘模型**对话框框中，展开预测结构，选择**Forecasting**从列表中，模型，然后单击**确定**。  
  
3.  忽略**选择输入表**框。  
  
    > [!NOTE]  
    >  对于时序模型，并不需要指定单独的输入，除非您要进行交叉预测。  
  
4.  在中**源**上的网格中列**挖掘模型预测**选项卡上，单击第一个空行中的单元格，然后选择**预测挖掘模型**。  
  
5.  在中**字段**列中，选择**Model Region**。  
  
     此操作可将序列标识符添加到预测查询中，以指示预测适用于的型号和区域的组合。  
  
6.  单击下一步中的空行**源**列，，然后选择**预测函数**。  
  
7.  在中**字段**列中，选择**PredictTimeSeries**。  
  
    > [!NOTE]  
    >  此外可以使用`Predict`使用时序模型的函数。 但在默认情况下，预测函数只为每个时序创建一个预测。 因此，若要指定多个预测步骤，必须使用**PredictTimeSeries**函数。  
  
8.  在中**挖掘模型**窗格中，选择挖掘模型列**量。** 将 Amount 拖到**条件/参数**框**PredictTimeSeries**前面添加的函数。  
  
9. 单击**条件/参数**框，然后键入一个逗号后, 跟**5**，在该字段名称。  
  
     中的文本**条件/参数**框现在应显示以下：  
  
     `[Forecasting].[Amount],5`  
  
10. 在中**别名**列中，键入`PredictAmount`。  
  
11. 单击下一步中的空行**源**列，，然后选择**预测函数**试。  
  
12. 在中**字段**列中，选择**PredictTimeSeries**。  
  
13. 在中**挖掘模型**窗格中，选择的列数量，然后将其拖到**条件/参数**第二个框**PredictTimeSeries**函数。  
  
14. 单击**条件/参数**框，然后键入一个逗号后, 跟**5**，在该字段名称。  
  
     中的文本**条件/参数**框现在应显示以下：  
  
     `[Forecasting].[ Quantity],5`  
  
15. 在中**别名**列中，键入`PredictQuantity`。  
  
16. 单击**切换到查询结果视图**。  
  
     查询结果以表格形式显示。  
  
 请记住，您在查询生成器中创建了三个不同类型的结果，一个结果使用列中的值，另两个结果从预测函数中获取预测值。 因此，查询结果包含三个单独的列。 第一列包含产品和区域组合的列表。 第二列和第三列都包含预测结构的嵌套表。 每个嵌套表都包含时间步长和预测值，如下表所示：  
  
 示例结果（金额被截断为两位小数）：  
  
 **M200 Europe PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|2008 年 7 月 25 日|99978.00|  
|2008 年 8 月 25 日|145575.07|  
|2008 年 9 月 25 日|116835.19|  
|2008 年 10 月 25 日|116537.38|  
|2008 年 11 月 25 日|107760.55|  
  
 **M200 Europe PredictQuantity**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|2008 年 7 月 25 日|52|  
|2008 年 8 月 25 日|67|  
|2008 年 9 月 25 日|58|  
|2008 年 10 月 25 日|57|  
|2008 年 11 月 25 日|54|  
  
 **M200 North America-PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|2008 年 7 月 25 日|348533.93|  
|2008 年 8 月 25 日|340097.98|  
|2008 年 9 月 25 日|257986.19|  
|2008 年 10 月 25 日|374658.24|  
|2008 年 11 月 25 日|379241.44|  
  
 **M200 North America-PredictQuantity**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|2008 年 7 月 25 日|272|  
|2008 年 8 月 25 日|152|  
|2008 年 9 月 25 日|250|  
|2008 年 10 月 25 日|181|  
|2008 年 11 月 25 日|290|  
  
> [!WARNING]  
>  在示例数据库中使用的日期对于此版本已更改。 如果您在使用较早版本的示例数据，则可能会看到不同的结果。  
  
## <a name="saving-the-prediction-results"></a>保存预测结果  
 对于使用预测结果，有几个不同的选项可供您选择。 您可以平展结果，从“结果”视图复制数据，然后将数据粘贴到 Excel 工作表或其他文件中。  
  
 为了简化保存结果的过程，数据挖掘设计器还提供将数据保存到数据源视图的功能。 将结果保存到数据源视图的功能仅在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中提供。 结果只能以平展格式存储。  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>在“结果”窗格中平展结果  
  
1.  在预测查询生成器中，单击**切换到查询设计视图**。  
  
     该视图发生变化，允许手动编辑 DMX 查询文本。  
  
2.  在 `FLATTENED` 关键字后键入 `SELECT` 关键字。 完整的查询文本应该如下所示：  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  或者，您可以键入一个子句来限制结果，如下面的示例所示：  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  单击**切换到查询结果视图**。  
  
#### <a name="to-export-prediction-query-results"></a>导出预测查询结果  
  
1.  单击**保存查询结果**。  
  
2.  在中**保存数据挖掘查询结果**对话框中，对于**数据源**，选择[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。 如果您希望将数据保存到不同的关系数据库，也可以创建数据源。  
  
3.  在中**表名称**列中，键入新的临时表名，如**Test Predictions**。  
  
4.  单击 **“保存”**。  
  
    > [!NOTE]  
    >  若要查看您创建的表，请创建与您保存数据的实例的数据库引擎的连接，然后创建查询。  
  
## <a name="conclusion"></a>结语  
 您学习了如何生成基本时序模型、解释预测和创建预测。  
  
 本教程中的其余任务是可选的，它们介绍高级时序预测。 如果您决定继续，将学习如何将新数据添加到模型并基于扩展的序列创建预测。 您还将学习如何通过使用模型中的趋势但是使用新数据序列替换模型中的数据来执行交叉预测。  
  
## <a name="next-lesson"></a>下一课  
 [高级时序预测&#40;数据挖掘中级教程&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
