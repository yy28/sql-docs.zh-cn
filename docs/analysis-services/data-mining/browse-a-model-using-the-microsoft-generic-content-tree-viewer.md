---
title: "使用 Microsoft 一般内容树查看器浏览模型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dcb5c01581dd9d42e7504dc00f514544479b27fc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>使用 Microsoft 一般内容树查看器浏览模型
  通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般挖掘模型内容查看器，可以查看有关挖掘算法找到的模式的详细信息，以及访问在分析过程中生成的各种统计信息。 信息的数量和类型取决于使用的算法，但可包括以下几类：  
  
-   数据段及其特征。  
  
-   有关每个组或整个数据集的说明性统计信息。  
  
-   树中的分支或子节点的数目。  
  
-   对群集或整个数据集的计算，例如方差和平均值。  
  
 查看这些信息可帮助您更好地理解分析结果。 此外，您还可确定微调模型继而为模型重新定型的方法， 或者，您可决定使用其他算法重新定型。  
  
## <a name="viewing-mining-model-content"></a>查看挖掘模型内容  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容查看器显示挖掘模型的“内容架构行集”  中的列、规则、属性、特性、节点和其他内容。 内容架构行集是用于呈现数据挖掘模型内容详细信息的通用框架。  
  
 此详细信息包含在一个 HTML 表中，该表将模型中的模式、群集或树表示为节点。 您可以单击各节点，然后将其展开以便查看详细信息，例如针对数值属性的不同值的公式或计数。 您也可以浏览节点中的父子关系。  
  
 有关挖掘模型内容中所用术语的常规含义的详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。 本主题还包括指向特定类型模型的挖掘模型内容信息的链接。 每种挖掘模型包含的信息都是高度特定于数据中的算法和模式的，因此，我们建议您查阅每个模型类型的技术参考主题以全面了解各模型类型。  
  
## <a name="querying-mining-model-content"></a>查询挖掘模型内容  
 通过查询挖掘模型，同样可以获取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器提供的信息。 可以使用数据挖掘扩展插件 (DMX) 语句来创建针对挖掘模型内容的查询。 例如，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，可通过执行以下 DMX 语句来运行内容查询。  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 有关详细信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
