---
title: "使用 Microsoft 关联规则查看器浏览模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- itemsets [Analysis Services]
- mining models [Analysis Services], associations
- mining model content, viewing
- rules [Data Mining]
- Association Rules Viewer [Analysis Services]
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- Microsoft Association Rules Viewer
- dependencies [Analysis Services]
ms.assetid: 538fc01b-8eb1-467a-9b66-3cd57cf7489f
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a30bdbe56a78d1bb9b09f0ff179646496bb4afdd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="browse-a-model-using-the-microsoft-association-rules-viewer"></a>使用 Microsoft 关联规则查看器浏览模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)]关联规则查看器中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]显示由生成的挖掘模型[!INCLUDE[msCoName](../../includes/msconame-md.md)]关联算法。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法是用于创建可用于市场篮分析的数据挖掘模型的关联算法。 有关此算法的详细信息，请参阅 [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md)。  
  
 以下是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法的主要原因：  
  
-   查找对通常能在一个事务中找到的项进行说明的项集。  
  
-   发现根据现有项预测事务中存在其他项的规则。  
  
> [!NOTE]  
>  若要查看有关模型中使用的公式以及所发现的模式的详细信息，请使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
 有关如何创建、浏览和使用关联挖掘模型的详细信息，请参阅[第 3 课：生成市场篮方案（数据挖掘中级教程）](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)。  
  
##  <a name="BKMK_ViewerTabs"></a> 查看器的选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则查看器包括以下选项卡：  
  
-   [项集](#BKMK_Itemsets)  
  
-   [规则](#BKMK_Rules)  
  
-   [依赖关系网络](#BKMK_Dependency)  
  
 每个选项卡都包含 **“显示长名称”** 复选框，可以使用此复选框来显示或隐藏在规则或项集中所以生成项集的表。  
  
###  <a name="BKMK_Itemsets"></a> 项集  
 **“项集”** 选项卡显示被模型识别为经常发现一起出现的项集的列表。 该选项卡显示的网格有以下列： **“支持”**、 **“大小”**和 **“项集”**。 有关支持的详细信息，请参阅 [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md)。 **“大小”** 列显示项集中的项的数量。 **“项集”** 列显示模型发现的实际项集。 可以使用 **“显示”** 列表控制项集的格式，可将格式设置为以下选项：  
  
-   **显示属性名称和值**  
  
-   **仅显示属性值**  
  
-   **仅显示属性名称**  
  
 可以使用 **“最低支持”** 和 **“最小项集大小”**来筛选选项卡中显示的项集数量。 还可使用 **“筛选项集”** 并输入必须存在的项集特征，来进一步限制项集的显示数量。 例如，如果键入 Water Bottle = existing，则可将项集限制为仅包含 water bottle 的那些项集。 **“筛选项集”** 选项还会显示您以前使用过的筛选器列表。  
  
 通过单击列标题，可以对网格中的行进行排序。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> 规则  
 **“规则”** 选项卡显示关联算法发现的规则。 **“规则”** 选项卡包括的网格包含以下列： **“概率”**、 **“重要性”**和 **“规则”**。 概率说明出现规则结果的可能性。 重要性用于度量规则的用途。 尽管规则出现的概率可能很高，但规则自身的用途可能并不重要。 重要性列就是说明这一情况的。 例如，如果每个项集都包含属性的某个特定状态，那么，即使概率非常高，预测状态的规则也并不重要。 重要性越高，规则越重要。  
  
 可以使用 **“最小概率”** 和 **“最低重要性”** 来筛选规则，此操作类似于可在 **“项集”** 选项卡中进行的筛选。您也可以使用 **“筛选规则”** ，根据属性包含的状态来筛选规则。  
  
 通过单击列标题，可以对网格中的行进行排序。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> 依赖关系网络  
 **“依赖关系网络”** 选项卡包括一个依赖关系网络查看器。 查看器中的每个节点代表一个项，如 state = WA。 节点间的箭头代表项之间有关联。 箭头的方向表示按照算法发现的规则确定的项之间的关联。 例如，如果查看器包含三个项 A、B 和 C，并且 C 是根据 A 和 B 预测的，那么，选择了节点 C 时，则有两个箭头指向节点 C，即 A 到 C 和 B 到 C。  
  
 查看器左边的滑块可当作与规则的概率关联的筛选器使用。 降低滑块将只显示最强链接。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Association Algorithm](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
