---
title: 序列聚类分析群集特征选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.characteristics.f1
ms.assetid: 3a9e8a0c-7d03-47cc-8625-e68d73a8c947
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2119013c1c735c9b35a3790fedbf1ac114e9964a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196853"
---
# <a name="sequence-clustering-cluster-characteristics-tab-mining-model-viewer"></a>顺序分析和聚类分析的“分类特征”选项卡（挖掘模型查看器）
  **“Microsoft 顺序分析和聚类分析查看器”** 中的 **“分类特征”** 选项卡提供了定义序列分类的特征的详细列表。 这些特征可包括简单属性-值对以及状态间的转换。  
  
 可以使用此顺序分析和聚类分析模型视图，来深化到分类内容并查看代表分类的序列。  
  
 **有关详细信息，请参阅** [Microsoft 顺序分析和聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)和[使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览选定挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **Cluster**  
 选择要查看的分类。  
  
 **特征\<群集 >**  
 此表提供已分配给当前分类的序列的列表（按概率排序）。 请记住，序列基本上是一个属性-值对，后跟一个或多个其他的属性-值对。 序列及其概率的组合定义了每个分类的特征。  
  
 例如，在基于市场篮分析的顺序分析和聚类分析模型中，一个分类可以让客户选择销售项，然后在不再购买其他项的情况下结束事务（这是此模型最主要的特点）。 在试图分析服务器失败的顺序分析和聚类分析模型中，分类的主要特征可能是一系列高频率错误事件。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**变量**|此列指示特征是一个值还是一个转换。<br /><br /> 如果特征是一个值，**变量**列会包含属性名称。<br /><br /> 如果特征表示一个状态转换，**变量**列包含文本"转换"。|  
|**值**|此列的值取决于特征是一个简单属性-值对，还是一个表示项或事件的常见序列的状态转换。<br /><br /> 如果特征是一个值，**值**列会包含状态。<br /><br /> 如果特征表示一个状态转换，**值**列会包含状态转换的说明。|  
|**概率**|该列会显示一个栏，用于指示此特征（简单属性-值对或某些状态组合）是当前分类的成员的相对概率。<br /><br /> 可以将鼠标悬停在该栏的上方，来显示特征的频率值。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
