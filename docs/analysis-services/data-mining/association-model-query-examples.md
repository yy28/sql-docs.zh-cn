---
title: "关联模型查询示例 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1313c2933ba37f161edd4980a6b931388f60e13b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="association-model-query-examples"></a>关联模型查询示例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在对数据挖掘模型创建查询时，可以创建内容查询，也可创建预测查询。内容查询提供有关在分析过程中发现的规则和项集的详细信息，预测查询使用在数据中发现的关联来做出预测。 对于关联模型来说，预测通常基于规则且可用来给出建议，而内容查询通常用于浏览项集之间的关系。 此外，还可检索有关模型的元数据。  
  
 本节讲述如何为基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则的算法的模型创建这些类型的查询。  
  
 **内容查询**  
  
 [使用 DMX 获取模型元数据](#bkmk_Query1)  
  
 [从架构行集中获取元数据](#bkmk_Query2)  
  
 [检索模型的原始参数](#bkmk_Query3)  
  
 [检索项集和产品列表](#bkmk_Query4)  
  
 [返回排在前 10 位的项集](#bkmk_Query5)  
  
 **预测查询**  
  
 [预测关联项](#bkmk_Query6)  
  
 [确定相关项集的置信度](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> 查找有关模型的信息  
 所有挖掘模型都公开算法根据标准化架构（即挖掘模型架构行集）所了解的内容。 可以使用建数据挖掘扩展插件 (DMX) 语句或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储过程来对挖掘模型架构行集创建查询。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，还可使用类似 SQL 的语法，直接将架构行集作为系统表来查询。  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用 DMX 获取模型元数据  
 以下查询返回有关关联模型 `Association`的基本元数据，例如模型名称、存储模型的数据库以及模型中子节点的数目。 此查询使用 DMX 内容查询从模型的父节点中检索元数据：  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  必须将列名 CHILDREN_CARDINALITY 括在括号中，以便将它与同名的 MDX 保留关键字区分开来。  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_CATALOG|Association Test|  
|MODEL_NAME|关联|  
|NODE_CAPTION|Association Rules Model|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 有关这些列在关联模型中含义的定义，请参阅 [关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：从架构行集中获取其他元数据  
 通过查询数据挖掘架构行集，可以找到在 DMX 内容查询中返回的相同信息。 不过，架构行集还提供其他一些列，例如上次处理模型的日期、挖掘结构和用作可预测属性的列的名称。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|关联|  
|SERVICE_NAME|Association Rules Model|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|关联|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：检索模型的原始参数  
 以下查询返回一个列，该列包含有关创建模型时使用的参数设置的详细信息。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 示例结果：  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [返回页首](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>查找有关规则和项集的信息  
 关联模型有两个常见用途：查找有关常见项集的信息以及提取有关特定规则和项集的详细信息。 例如，您可能希望提取评为当前特别受关注的规则的列表，或创建最常见项集的列表。 您可以使用 DMX 内容查询来检索此类信息， 也可使用 **“Microsoft 关联查看器”**浏览该信息。  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：检索项集和产品列表  
 以下查询检索全部项集，同时还将检索列出每个项集中包含的产品的嵌套表。 NODE_NAME 列包含模型内项集的唯一 ID，而 NODE_CAPTION 给出项目的文本说明。 本例中对嵌套表进行了平展处理，这样，包含两个产品的项集在结果中生成了两行。 如果客户端支持分层数据，则可以忽略 FLATTENED 关键字。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 示例结果：  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> 示例查询 5：返回排在前 10 位的项集  
 本例演示如何使用 DMX 在默认情况下提供的某些分组和排序函数。 当按照每个节点的支持对项集排序时，该查询返回排在前 10 位的项集。 请注意，无需对结果进行显式分组，这与 Transact-SQL 中不同。不过，只能在每个查询中使用一个聚合函数。  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 示例结果：  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [返回页首](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>使用模型进行预测  
 关联规则模型通常用于生成建议，这些建议基于在项集中发现的相关性。 因此，基于关联规则模型创建预测查询时，您通常使用模型中的规则基于新数据进行猜测。  [PredictAssociation (DMX)](../../dmx/predictassociation-dmx.md) 是返回建议的函数，它包含几个可用于自定义查询结果的参数。  
  
 另一个说明对关联模型的查询非常有用的示例是返回各种规则和项集的置信度，以便可以比较不同跨区销售策略的有效性。 以下示例说明如何创建这些查询。  
  
###  <a name="bkmk_Query6"></a> 示例查询 6：预测关联项目  
 此示例使用在[数据挖掘中级教程（Analysis Services - 数据挖掘）](http://msdn.microsoft.com/library/404b31d5-27f4-4875-bd60-7b2b8613eb1b)中创建的关联模型。 它演示如何创建一个预测查询，该查询告诉您应向已购买某种特定产品的客户推荐哪些产品。 此种类型的查询称为单独查询，在该查询中，使用 **SELECT…UNION** 语句向模型提供所需的值。 由于对应于新值的可预测模型列为嵌套表，因此必须使用某一 **SELECT** 子句将新值映射到嵌套表列 `[Model]`，再使用另一 **SELECT** 子句将嵌套表列映射到事例级别列 `[v Assoc Seq Line Items]`。 如果在该查询中添加 INCLUDE-STATISTICS 关键字，则可看到推荐的概率和支持。  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 示例结果：  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> 示例查询 7：确定相关项集的置信度  
 尽管规则可用于生成建议，但在对数据集内的模式的更深入分析中，项集作用更大。 例如，如果对前面示例查询返回的建议不满意，则可以检查包含产品 A 的其他项集，以更好地了解是否产品 A 是人们在购买各种产品时倾向于购买的附件，或者是否产品 A 与购买特定产品有很强的关联性。 浏览这些关系的最简单方法是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联查看器中筛选项集，但也可使用查询检索这些信息。  
  
 以下示例查询返回包含 Water Bottle 项目（包括单项 Water bottle）的所有项集。  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 示例结果：  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 该查询不仅返回嵌套表中符合此条件的行，还返回嵌套表外部或事例表中的所有行。 因此，必须添加一个条件来消除对目标属性名称具有 Null 值的事例表行。  
  
 [返回页首](#bkmk_top2)  
  
## <a name="function-list"></a>函数列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法还支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[IsDescendant &#40; DMX &#41;](../../dmx/isdescendant-dmx.md)|确定一个节点是否是神经网络图中另一个节点的子节点。|  
|[IsInNode &#40; DMX &#41;](../../dmx/isinnode-dmx.md)|指示指定的节点是否包含当前事例。|  
|[PredictAdjustedProbability &#40; DMX &#41;](../../dmx/predictadjustedprobability-dmx.md)|返回加权的概率。|  
|[PredictAssociation &#40; DMX &#41;](../../dmx/predictassociation-dmx.md)|预测关联数据集中的成员身份。|  
|[PredictHistogram &#40; DMX &#41;](../../dmx/predicthistogram-dmx.md)|返回与当前预测值相关的值的表。|  
|[PredictNodeId &#40; DMX &#41;](../../dmx/predictnodeid-dmx.md)|返回每个事例的 Node_ID。|  
|[PredictProbability &#40; DMX &#41;](../../dmx/predictprobability-dmx.md)|返回预测值的概率。|  
|[PredictSupport &#40; DMX &#41;](../../dmx/predictsupport-dmx.md)|返回指定状态的支持值。|  
|[PredictVariance &#40; DMX &#41;](../../dmx/predictvariance-dmx.md)|返回预测值的方差。|  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 关联算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Microsoft 关联算法技术参考](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)   
 [关联模型 &#40; 的挖掘模型内容Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
