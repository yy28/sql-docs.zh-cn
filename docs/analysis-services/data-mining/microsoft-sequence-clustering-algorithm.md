---
title: "Microsoft 序列聚类分析算法 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
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
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 375e6c59c38d7bcf4eb270c6b007d2fca16d119c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 顺序分析和聚类分析算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)]序列聚类分析算法是一种结合顺序分析群集的唯一算法。 你可以使用该算法来研究包含可在“顺序”中链接的事件的数据。 该算法可查找最常见的顺序，并且通过执行聚类分析来查找相似的顺序。 下面的示例说明了可以将其作为机器学习的数据捕获的顺序类型，从而提供有关常见问题或业务方案的建议：  
  
-   用户在导航或浏览网站时生成的点击流或单击路径  
  
-   列出发生事故（如硬盘故障或服务器死锁）之前的事件的日志  
  
-   说明客户将商品添加到在线购物车中的顺序的事务记录  
  
-   根据一段时间内客户或患者的互动来预测服务取消或其他不良结果的记录  
  
 该算法在许多方面都类似于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法。 不过， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法不是查找包含类似属性的事例的分类，而是查找顺序中包含类似路径的事例的分类。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 网站收集有关站点用户访问哪些页面以及页面访问顺序的信息。 因为该公司提供在线订购，所以用户必须登录到此站点。 这可以为该公司的各个客户配置文件提供点击信息。 通过对此数据使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法，该公司可以查找具有相同的点击模式或点击顺序的客户组或分类。 然后，该公司可以使用这些分类来分析用户如何在网站中移动，来识别哪些页面与特定商品的销售关系最密切及预测接下来哪些页面最有可能被访问。  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法是一种混合算法，它综合了聚类分析方法和 Markov 链分析，以识别分类及其顺序。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法的特点之一是使用顺序数据。 此数据通常表示数据集中状态之间的一系列事件或转换，例如，特定用户的一系列产品购买或 Web 点击操作。 该算法会检查所有转换概率，并测量数据集中所有可能顺序之间的差异或距离，以确定最好使用哪些顺序作为聚类分析的输入。 在创建候选顺序列表后，该算法通过期望最大化 (EM) 将该顺序信息用作聚类分析的输入。  
  
 有关实现的详细说明，请参阅 [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-sequence-clustering-models"></a>顺序分析和聚类分析模型所必需的数据  
 准备用于定型顺序分析和聚类分析模型的数据时，应理解特定算法的要求，其中包括所需要的数据量以及使用数据的方式。  
  
 顺序分析和聚类分析模型的要求如下：  
  
-   **单个键列** 顺序分析和聚类分析模型需要一个用于标识记录的键。  
  
-   **顺序列** 对于顺序数据，模型必须具有包含顺序 ID 列的嵌套表。 顺序 ID 可以为任何可排序的数据类型。 例如，可以使用数据类型为网页标识符、整数或文本字符串的列，只要该列可以标识顺序中的事件。 每个顺序只允许有一个顺序标识符，且每个模型中只允许有一种类型的顺序。  
  
-   **可选的非顺序属性** 该算法支持添加与顺序无关的其他属性。 这些属性可以包含嵌套列。  
  
 例如，在前面引用的 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 网站的示例中，顺序分析和聚类分析模型可以包含订单信息（作为事例表）、每个订单的具体客户的人口统计数据（作为非顺序属性）以及包含客户浏览网站和将商品放入购物车的顺序的嵌套表（作为顺序信息）。  
  
 有关顺序分析和聚类分析模型支持的内容类型和数据类型的详细信息，请参阅 [Microsoft 顺序分析和聚类分析算法技术参考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)的“要求”一节。  
  
## <a name="viewing-a-sequence-clustering-model"></a>查看顺序分析和聚类分析模型  
 该算法创建的挖掘模型在数据中包含了最常见顺序的说明。 若要浏览该模型，可以使用 **Microsoft 序列分类查看器**。 查看顺序分析和聚类分析模型时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 显示包含多个转换的分类。 您还可以查看相关的统计信息。 有关详细信息，请参阅 [使用 Microsoft 序列分类查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
 如果希望了解更多详细信息，可在 [Microsoft 一般内容树查看器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中浏览该模型。 为该模型存储的内容包括每个节点中所有值的分布情况、每个分类的概率以及有关转换的详细信息。 有关详细信息，请参阅[顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 对模型进行定型后，结果将存储为一组模式。 您可以使用数据中最常见顺序的说明来预测新顺序的下一个可能步骤。 但是，因为该算法包括了其他列，所以您可以使用得到的模型来识别顺序数据和非顺序输入之间的关系。 例如，您可以向模型添加客户的人口统计数据，还可以进行针对特定客户群体的预测。 可以自定义预测查询，以便返回数目可变的预测或返回说明性的统计信息。  
  
 有关如何创建针对数据挖掘模型的查询的信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。 有关如何针对顺序分析和聚类分析模型使用查询的示例，请参阅 [顺序分析和聚类分析模型查询示例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)。  
  
## <a name="remarks"></a>注释  
  
-   不支持使用预测模型标记语言 (PMML) 创建挖掘模型。  
  
-   支持钻取。  
  
-   支持使用 OLAP 挖掘模型和创建数据挖掘维度。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 顺序分析算法技术参考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [序列聚类分析模型查询示例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [使用 Microsoft 序列分类查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
