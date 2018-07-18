---
title: 序列聚类分析群集配置文件选项卡 (挖掘模型查看器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.profiles.f1
ms.assetid: 44230895-0a42-4032-8d6c-0cdb8a2dbb8c
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b69066bd09f74fddd0fc7151eae216b74444e8f0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323127"
---
# <a name="sequence-clustering-cluster-profiles-tab-mining-model-viewer"></a>顺序分析和聚类分析的“分类配置文件”选项卡（挖掘模型查看器）
  “Microsoft 顺序分析和聚类分析查看器”中的“分类剖面图”提供每个分类中包含的序列的具有颜色编码的视图。  
  
 可以使用此顺序分析和聚类分析模型视图，来快速查看模型所找到的序列的分组方式。 您将对长序列的数目和短序列的数目一目了然。 还可以单击分类并显示 **“挖掘图例”** ，来准确了解每个序列中的各种颜色所表示的状态。  
  
 **有关详细信息：**[Microsoft 序列聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)，[使用 Microsoft 序列分类查看器浏览模型  ](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>“常规”  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览选定挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **显示图例**  
 选择此选项可显示一个图例，该图例说明了分类剖面图中显示的颜色与状态的文本值之间的相关性。  
  
 **直方图条数**  
 使用此选项可更改直方图中包含的彩色条的数量。 如果存在的图条数多于您选择显示的图条数，则会保留重要性最高的那些图条，其余图条则组合到 **“其他”** 中。  
  
 **属性** 和 **分类剖面图**  
 图表的此部分列出了在模型中找到的序列的分类。  
  
 使用您在选项 **“直方图条数”** 中选定的状态数来显示每个序列分类。  
  
 为模型中的每个分类显示两组直方图，每个组位于图形中不同的行上：  
  
-   **\<属性名称 >.samples**： 此行中的直方图显示代表每个分类的项的序列。 在 DMX 术语中，它们是每个分类的示例事例。  
  
-   **\<属性名称 >**： 此行中的直方图介绍分类包含的所有项及其总体分布。 在 **“挖掘图例”** 可见时单击直方图，这将显示每个项的数值  
  
 **状态**  
 此列在图表中是可选的，并且可以选择“显示图例”选项来显示或删除它。 **“状态”** 列就对应的分类直方图中的哪种颜色表示哪种状态提供了指导。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 序列聚类分析算法](data-mining/microsoft-sequence-clustering-algorithm.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)   
 [使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
