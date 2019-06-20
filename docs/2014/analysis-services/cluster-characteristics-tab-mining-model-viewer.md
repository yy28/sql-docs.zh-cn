---
title: 群集特征选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.characteristics.f1
ms.assetid: 8e33ed1d-1ce4-405d-895b-7e995b2c910d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0b4a798f9a395741ae831d3b22fc06a71f55607
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087992"
---
# <a name="cluster-characteristics-tab-mining-model-viewer"></a>“分类特征”选项卡（挖掘模型查看器）
  利用 **“分类特征”** 选项卡，可以浏览聚类分析模型中分类的特征或该模型中所有事例的集。 图形会将每个属性-值对的重要性显示为定义分类的特征（与其他分类相比）。  
  
 **有关详细信息：**[Microsoft 聚类分析算法](data-mining/microsoft-clustering-algorithm.md)，[使用 Microsoft 分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 挖掘模型将在自定义查看器中打开。  
  
 **Viewer**  
 选择用于浏览所选挖掘模型的查看器。 可以使用与此模型类型关联的自定义查看器或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用任何可用的插件查看器。  
  
 **Cluster**  
 选择要查看的分类，或选择“总体(全部)”以查看模型的属性的整体分布情况。  
  
 **特征\<群集 >**  
 图形包含以下列，这些列对所选分类的特征进行了说明。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**变量**|列出在所选分类中找到的挖掘模型中的属性。|  
|**值**|列出在当前所选分类中找到的当前属性的值。|  
|**概率**|条形指示属性-值对的强度作为此分类的显著特征。 如果您将鼠标指针悬停在条形上方，则可查看以百分比表示的概率值。 这表示，在任何特定事例中使用此属性和值组合时，该事例会归入此分类的概率。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
