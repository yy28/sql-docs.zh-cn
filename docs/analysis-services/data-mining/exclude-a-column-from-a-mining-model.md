---
title: "从挖掘模型中排除列 | Microsoft Docs"
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
  - "排除挖掘模型列"
  - "挖掘模型 [Analysis Services], 列"
  - "列 [数据挖掘], 排除"
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 29
---
# 从挖掘模型中排除列
  在创建新的挖掘模型时，您可能不希望使用模型基于的挖掘结构中存在的所有列。 例如，您可能添加了一个客户名称列来用于钻取，但不想将该列用于建模。 或者，您可能决定为一个列创建具有不同离散化的多个副本，并且在每个模型中仅使用这些副本中的一个，而忽略其余副本。 您还可以有选择地在若干不同模型中添加输入列，看看所添加的变量是如何影响输出列的。  
  
 您不需要为每个列组合都创建新的挖掘结构；相反，您只需将某个列标记为不在特定的模型中使用。  
  
### 从挖掘模型中排除列  
  
1.  在 **中的数据挖掘设计器的** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，在有关的挖掘模型下，选择与要排除的列相对应的单元。  
  
2.  从下拉列表框中选择“忽略”。  
  
## 另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  