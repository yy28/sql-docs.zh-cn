---
title: Microsoft 一般内容树查看器 （数据挖掘） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: eb48d0ce455c41f6e684b54af86bb6ff5f8eddfb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026432"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Microsoft 一般内容树查看器（数据挖掘）
  **“Microsoft 一般内容树查看器”** 以标准化 HTML 表格式显示有关数据挖掘模式的内容的详细信息。 此视图很有用，因为它将公开模型的基础结构，以及有关系数、值的分布等项的详细信息。  
  
 表中显示的实际内容因使用的算法而异，可能包括列、规则、属性、特性、节点和公式。 有关模型内容以及如何解释每个模型类型信息的详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
 此查看器中显示的信息使用基于挖掘模型的内容架构行集的通用结构。 内容架构行集是用于存储数据挖掘模型的模式、统计信息和其他内容的通用框架。 有关挖掘模型的数据挖掘架构行集中的列的列表，请参阅 [DMSCHEMA_MINING_MODEL_CONTENT 行集](schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)。  
  
## <a name="options"></a>“常规”  
 **节点标题 (唯一 ID)**  
 此窗格显示所选挖掘模型中所有节点的列表。 节点在树中的排列方式随要查看的模型类型的不同而不同。  
  
 可以单击每个节点，在 **“节点详细信息”** 窗格中显示有关该节点的详细信息。  
  
 **节点的详细信息**  
 显示选定节点的内容的详细信息。 每个节点均以标准化格式存储其信息，但表中每个行的内容和基数取决于要查看的模型类型或节点类型。 例如，为表示关联模型中的规则的节点存储的信息不同于表示决策树模型中的树的节点中的信息。  
  
 有关如何解释特定模型类型的节点信息的信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘查询](data-mining/data-mining-queries.md)  
  
  