---
title: "在数据挖掘设计器中创建单独查询 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dfbb55881c274dee8560cbba14319bcc831b38c2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>在数据挖掘设计器中创建单独查询
  如果需要为单个事例创建预测，单独查询是非常有用的。 有关单独查询的详细信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。  
  
 在数据挖掘设计器的 **“挖掘模型预测”** 选项卡中，可以创建许多不同类型的查询。 可以通过使用设计器或者通过键入数据挖掘扩展插件 (DMX) 语句来创建查询。 还可以从设计器开始工作，并通过更改 DMX 语句或者通过添加 WHERE 或 ORDER BY 子句来修改它所创建的查询。  
  
 若要在查询设计视图和查询文本视图之间切换，请单击工具栏上的第一个按钮。 在查询文本视图中，可以查看预测查询生成器创建的 DMX 代码。 您还可以运行查询，修改查询，并运行修改后的查询。 但是，如果切换回查询设计视图，则修改后的查询将不再继续运行。  
  
 下面的代码演示一个对目标邮件模型 TM_Decision_Tree 的单独查询的示例。  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 下列步骤说明如何创建该预测查询。  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>使用数据挖掘设计器创建单独查询  
  
1.  在数据挖掘设计器中，单击 **“挖掘模型预测”** 选项卡。  
  
2.  在 **“挖掘模型”** 表中，单击 **“选择模型”** 。  
  
     此时将打开 **“选择挖掘模型”** 对话框，以显示当前项目中存在的所有挖掘结构。  
  
     选择要用于创建预测的模型。  
  
     例如，若要创建本主题开头所显示的示例代码，请选择 TM_Decision_Tree，再单击“确定”。  
  
3.  在 **“挖掘模型预测”** 选项卡中，单击工具栏上的 **“单独查询”** 。  
  
     该选项卡中将出现 **“单独查询输入”** 表，该表中的各列自动映射到 **“挖掘模型”** 表中的各列。  
  
4.  在 **“单独查询输入”** 表中，选择 **“值”** 列中的值，用以说明要为其创建预测的事例。  
  
     例如，选择 **2** 作为 **Number Children At Home**，然后键入 **45** 作为 **Age**。  
  
5.  将一个可预测列从 **“挖掘模型”** 表拖到该选项卡底部的 **“源”** 列中。还可以根据需要键入该列的别名。  
  
     例如，将 **Bike Buyer** 拖到 **“源”** 列。  
  
6.  通过在“源”列的下拉列表中选择“预测函数”或“自定义表达式”，向查询中添加其他函数。  
  
     例如，单击 **“预测函数”**，再选择 **PredictProbability**。  
  
7.  在 **PredictProbability** 行中单击“条件/参数”，键入要预测的列的名称，还可以选择键入要预测的特定值。  
  
     例如，键入 **[Bike Buyer], 1**。  
  
8.  在 **PredictProbability** 行中单击 **“别名”** 框，再键入一个表示新列的名称。  
  
     例如，键入 **ProbableBuyer**。  
  
9. 在 **“挖掘模型预测”** 选项卡的工具栏上，单击 **“切换到查询结果视图”** 。  
  
     此时将出现一个新屏幕，显示查询的结果。 若要查看刚创建的 DMX 语句，请单击 **SQL**。  
  
## <a name="see-also"></a>另请参阅  
 [预测查询（数据挖掘）](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  

