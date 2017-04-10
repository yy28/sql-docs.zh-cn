---
title: "更改挖掘模型的属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "挖掘模型 [Analysis Services], 属性"
  - "属性 [数据挖掘]"
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# 更改挖掘模型的属性
  某些挖掘模型属性应用于整个模型，而其他一些模型属性应用于单独的列。 例如， **Drillthrough** 属性就应用于整个模型，它指定事例数据是否应该可用于查询； **Description** 属性也是此类属性。 应用于列的属性包括 **Usage** 和 **ModelingFlags**；它们控制列中的数据在模型内的使用方式。  
  
 下面的模型属性具有可用于创建表达式或配置复杂模型属性的高级编辑器。 以下属性提供：  
  
-   **Filter** 属性：打开[“数据集筛选器或模型筛选器”对话框](../Topic/Data%20Set%20Filter%20or%20Model%20Filter%20Dialog%20Box.md)。  
  
-   **AlgorithmParameters** 属性：打开[“算法参数”对话框（“挖掘模型”视图）](../Topic/Algorithm%20Parameters%20Dialog%20Box%20\(Mining%20Models%20View\).md)。  
  
 有关如何在挖掘模型中设置属性的信息，请参阅[挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### 更改挖掘模型的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击包含挖掘模型名称的列标题，或者网格中包含挖掘算法名称的行，然后选择“属性”。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
### 更改挖掘模型列的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击网格中位于挖掘结构列与挖掘模型的交叉点处的单元格，然后选择“属性”。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
    > [!NOTE]  
    >  如果列的用法设置为 **Ignore**，则列的“属性”窗口将为空白。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
## 另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  