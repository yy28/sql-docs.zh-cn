---
title: "更改挖掘模型中列的离散化 | Microsoft Docs"
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
  - "离散化 [Analysis Services]"
  - "挖掘结构 [Analysis Services], 操作指南主题"
  - "离散化列 [数据挖掘]"
  - "存入桶问题 [Analysis Services]"
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 14
---
# 更改挖掘模型中列的离散化
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在某些情况下会自动离散化值，也就是说，它会在数字列中保存值。 例如，如果数据包含连续数值数据，并且创建了决策树模型，则将依据数据的分布，自动将连续数据的所有列都存入 bin 目录中。 如果要控制数据的离散化方式，则必须更改挖掘结构列的属性，这些属性可控制数据在模型中的使用方式。  
  
 有关如何在挖掘模型中设置属性的常规信息，请参阅[挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### 显示挖掘模型列的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击包含挖掘模型名称的列标题，或者网格中包含挖掘算法名称的行，然后选择“属性”。  
  
     **“属性”** 窗口将显示与挖掘模型相关联的所有属性。  
  
2.  在靠近屏幕左侧的 **“结构”** 列中，单击包含要离散化的连续数值数据的列。  
  
     **“属性”** 窗口更改为只显示与该列相关联的属性。  
  
### 更改离散化方法  
  
1.  在 **“挖掘属性”** 窗口中，单击 **“内容”**旁的文本框，然后从下拉列表中选择 **Discretized** 。  
  
     <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 属性现已启用。  
  
2.  在“属性”窗口中，单击 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 旁的文本框，然后选择下列值之一：**Automatic**、**EqualAreas** 或 **Cluster**。  
  
    > [!NOTE]  
    >  如果列的用法设置为 **Ignore**，则列的“属性”窗口将为空白。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
3.  在“属性”窗口，单击 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 旁的文本框，然后键入一个数值。  
  
    > [!NOTE]  
    >  如果更改这些属性，则必须重新处理该结构以及要对其使用新设置的所有模型。  
  
## 另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  