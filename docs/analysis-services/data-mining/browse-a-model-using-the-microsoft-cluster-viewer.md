---
title: "使用 Microsoft 分类查看器浏览模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [Analysis Services]
- discrimination [Analysis Services]
- names [Analysis Services], clusters
- Microsoft Cluster Viewer
- mining model content, viewing
- comparing clusters
- viewing clusters
- displaying clusters
- data mining [Analysis Services], clusters
- Cluster Viewer [Analysis Services]
- mining models [Analysis Services], clusters
ms.assetid: 591fe30b-d88f-4a71-94d4-4a3907fc275d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 561b0d339a7de446e6c96f3848998dba44409769
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-cluster-viewer"></a>使用 Microsoft 分类查看器浏览模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 分类查看器显示使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法生成的挖掘模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法是一种分段算法，用于浏览数据以标识数据中的变体并创建预测。 有关此算法的详细信息，请参阅 [Microsoft Clustering Algorithm](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)。  
  
> [!NOTE]  
>  若要查看有关模型中使用的公式以及所发现的模式的详细信息，请使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
##  <a name="BKMK_ViewerTabs"></a> 查看器的选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分类查看器提供了以下选项卡，用于浏览聚类分析挖掘模型：  
  
-   [分类关系图](#BKMK_Diagram)  
  
-   [分类剖面图](#BKMK_Profile)  
  
-   [分类特征](#BKMK_Characteristics)  
  
-   [分类对比](#BKMK_Discrimination)  
  
###  <a name="BKMK_Diagram"></a> 分类关系图  
 **分类查看器的** “分类关系图” [!INCLUDE[msCoName](../../includes/msconame-md.md)] 选项卡可以显示挖掘模型中的所有分类。 两个分类之间连线的明暗度表示分类的相似程度。 如果明暗度较浅或无明暗度，则表示分类的相似程度较低。 连线的颜色越深，链接的相似性越强。 通过调整分类右侧的滑块，可以调整查看器显示的连线数。 降低滑块将只显示最强链接。  
  
 默认情况下，明暗度代表分类的总体。 通过使用“明暗度****变量”和“状态”选项，可以选择明暗度代表的属性和状态对。 明暗度越深，特定状态所对应的属性分布范围就越大。 明暗度越浅，分布范围就越小。  
  
 若要重命名某个群集，请右键单击其节点并选择“重命名群集”。 新名称会在服务器中永久保留。  
  
 若要将关系图的可见部分复制到剪贴板，请单击 **“复制图形视图”**。 若要复制完整的关系图，请单击 **“复制整个图形”**。 使用 **“放大”** 和 **“缩小”**可以放大或缩小关系图，使用 **“缩放关系图以适应窗口”**可以适应屏幕大小。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> 分类剖面图  
 **“分类剖面图”** 选项卡可以提供模型中的算法创建的分类的总体视图。 此视图显示了每个分类中的属性以及属性的分布情况。 每个单元的 InfoTip 显示分布统计信息，每个列标题的 InfoTip 显示分类的总体。 离散属性显示为彩条，连续属性显示为菱形图，表示每个分类中的平均偏差和标准偏差。 通过“直方图条”  选项，可以控制直方图中可见的条数。 如果存在的图条数多于您选择显示的图条数，则会保留重要性最高的那些图条，其余图条则组合到一个灰色的存储桶内。  
  
 您可以更改分类的默认名称，使名称更具描述性。 右键单击群集的列标题，再选择“重命名群集”，即可重命名群集。 也可以通过选择 **“隐藏列”**来隐藏分类。  
  
 若要打开一个窗口，以便为群集提供更大、更详细的视图，请双击“状态”列中的任一单元格，或双击查看器中的任一直方图。  
  
 单击列标题，可以将列中的属性按照其对分类的重要性来进行排序。 也可以在查看器中拖动列以将其重新排序。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 分类特征  
 若要使用“分类特征”  选项卡，请从“分类”  列表中选择一个分类。 选择分类后，可以检查特定分类的组成特征。 分类包含的属性列在 **“变量”** 列中，所列属性的状态列在 **“值”** 列中。 属性状态将按重要性顺序列出，重要性由这些状态会出现在分类中的概率表示。 概率显示在 **“概率”** 列中。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> 分类对比  
 可以使用 **“分类对比”** 选项卡来比较两个分类的属性。 使用 **“分类 1”** 和 **“分类 2”** 列表选择要比较的分类。 查看器将确定分类之间最为重要的一些差异，并按重要性顺序显示与这些差异关联的属性状态。 属性右侧的条表示属性状态所倾向的分类，条的大小则表示属性状态倾向于相应分类的程度。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Clustering Algorithm](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  

