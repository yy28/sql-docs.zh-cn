---
title: 关联模型的挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- mining model content, association models
- rules [Data Mining]
- associations [Analysis Services]
ms.assetid: d5849bcb-4b8f-4f71-9761-7dc5bb465224
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a1e525d7b42d058343e41ea154f0687fb969839
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083690"
---
# <a name="mining-model-content-for-association-models-analysis-services---data-mining"></a>关联模型的挖掘模型内容（Analysis Services – 数据挖掘）
  本主题讲述使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法的模型特有的挖掘模型内容。 有关与适用于所有模型类型的挖掘模型内容相关的常规术语和统计术语的说明，请参阅 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-an-association-model"></a>了解关联模型的结构  
 关联模型结构非常简单。 每个模型均具有表示该模型及其元数据的单一父节点，且每个父节点均具有项集和规则的平面列表。 项集和规则不是按树组织的，它们的顺序是项集在先、规则在后，如下面的关系图所示。  
  
 ![关联模型的模型内容的结构](../media/modelcontentstructure-assoc.gif "的关联模型的模型内容结构")  
  
 每个项集均包含在其自己的节点中 (NODE_TYPE = 7)。 “节点  ”包含项集定义、含有此项集的事例的数目以及其他信息。  
  
 每个规则也包含在其自己的节点中 (NODE_TYPE = 8)。 “规则  ”说明项目关联方式的一般模式。 规则类似于 IF-THEN 语句。 规则左侧显示的是一个现有条件或条件集。 规则右侧显示的是数据集中的项，该项通常与左侧的条件相关联。  
  
 **注意** 如果要提取规则或项集，可使用查询仅返回需要的节点类型。 有关详细信息，请参阅 [关联模型查询示例](association-model-query-examples.md)  
  
## <a name="model-content-for-an-association-model"></a>关联模型的模型内容  
 本节仅针对与关联模型相关的挖掘模型内容中的列给出详细信息和示例。  
  
 有关架构行集中通用列（例如 MODEL_CATALOG 和 MODEL_NAME）的信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
 MODEL_CATALOG  
 存储模型的数据库的名称。  
  
 MODEL_NAME  
 模型的名称。  
  
 ATTRIBUTE_NAME  
 与此节点对应的属性的名称。  
  
 NODE_NAME  
 节点的名称。 对于关联模型，该列包含的值与 NODE_UNIQUE_NAME 列相同。  
  
 NODE_UNIQUE_NAME  
 节点的唯一名称。  
  
 NODE_TYPE  
 关联模型仅输出以下节点类型：  
  
|节点类型 ID|类型|  
|------------------|----------|  
|1（模型）|根节点或父节点。|  
|7（项集）|项集，或属性-值对的集合。 示例：<br /><br /> `Product 1 = Existing, Product 2 = Existing`<br /><br /> 或<br /><br /> `Gender = Male`。|  
|8（规则）|用于定义项相互关联的方式的规则。<br /><br /> 例如：<br /><br /> `Product 1 = Existing, Product 2 = Existing -> Product 3 = Existing`。|  
  
 NODE_CAPTION  
 与节点关联的标签或标题。  
  
 **项集节点** 逗号分隔的项列表。  
  
 **规则节点** 包含规则的左右两边。  
  
 CHILDREN_CARDINALITY  
 指示当前节点的子节点的数目。  
  
 **父节点** 指示项集与规则数目的总和。  
  
> [!NOTE]  
>  若要获取对项集和规则计数的明细，请参阅该模型根节点的 NODE_DESCRIPTION。  
  
 **项集或规则节点** 始终为 0。  
  
 PARENT_UNIQUE_NAME  
 节点的父节点的唯一名称。  
  
 **父节点** 始终为 NULL。  
  
 **项集或规则节点** 始终为 0。  
  
 NODE_DESCRIPTION  
 节点内容的用户友好说明。  
  
 **父节点** 包括一个逗号分隔列表，该列表包含有关该模型的以下信息：  
  
|项|Description|  
|----------|-----------------|  
|ITEMSET_COUNT|模型中所有项集的计数。|  
|RULE_COUNT|模型中所有规则的计数。|  
|MIN_SUPPORT|为任何单个项集找到的最小支持。<br /><br /> **注意** 值可能不同于为 *MINIMUM _SUPPORT* 参数设置的值。|  
|MAX_SUPPORT|为任何单个项集找到的最大支持。<br /><br /> **注意** 值可能不同于为 *MAXIMUM_SUPPORT* 参数设置的值。|  
|MIN_ITEMSET_SIZE|最小项集的大小，由项目的计数表示。<br /><br /> 值为 0 指示 `Missing` 状态被视为独立项目。<br /><br /> **注意** *MINIMUM_ITEMSET_SIZE* 参数的默认值为 1。|  
|MAX_ITEMSET_SIZE|指示找到的最大项集的大小。<br /><br /> **注意** 此值受创建模型时为 *MAX_ITEMSET_SIZE* 参数设置的值的约束。 该值永远不可大于、但可小于为该参数设置的值。 默认值为 3。|  
|MIN_PROBABILITY|为模型中的任何单个项集或规则检测到的最小概率。<br /><br /> 例如：0.400390625<br /><br /> **注意** 对于项集，此值始终大于创建模型时为 *MINIMUM_PROBABILITY* 参数设置的值。|  
|MAX_PROBABILITY|为模型中的任何单个项集或规则检测到的最大概率。<br /><br /> 例如：1<br /><br /> **注意** 没有参数来约束项集的最大概率。 若要消除出现过于频繁的项目，请改用 *MAXIMUM_SUPPORT* 参数。|  
|MIN_LIFT|该模型为任何项集提供的最小提升量。<br /><br /> 例如：0.14309369632511<br /><br /> 注意：了解最小提升可帮助您确定对任何一个项集的提升是否有效。|  
|MAX_LIFT|该模型为每个项集提供的最大提升量。<br /><br /> 例如：1.95758227647523**注意**了解最大提升可帮助您确定对任何一个项集的提升是否有效。|  
  
 **项集节点** 项集节点包含一个项目列表，该列表显示为一个以逗号分隔的文本字符串。  
  
 例如：  
  
 `Touring Tire = Existing, Water Bottle = Existing`  
  
 这表示同时购买了旅行车轮胎和水瓶。  
  
 **规则节点** 规则节点包含由箭头分隔的规则的左右两边。  
  
 例如： `Touring Tire = Existing, Water Bottle = Existing -> Cycling cap = Existing`  
  
 这意味着如果某人买了旅行车轮胎和水瓶，他还可能买了自行车运动帽。  
  
 NODE_RULE  
 描述节点中嵌套的规则或项集的 XML 片段。  
  
 **父节点** 空白。  
  
 **项集节点** 空白。  
  
 **规则节点** 包含关于规则的其他有用信息的 XML 片段，这些信息包括支持、置信度、项目数量以及表示规则左侧的节点的 ID 等。  
  
 MARGINAL_RULE  
 空白。  
  
 NODE_PROBABILITY  
 与项集或规则关联的概率或置信度分数。  
  
 **父节点** 始终为 0。  
  
 **项集节点** 项集的概率。  
  
 **规则节点** 规则的置信度值。  
  
 MARGINAL_PROBABILITY  
 与 NODE_PROBABILITY 相同。  
  
 NODE_DISTRIBUTION  
 根据节点是项集还是规则，该表包含的信息可能会有很大不同。  
  
 **父节点** 空白。  
  
 **项集节点** 列出了项集中的每个项目以及概率和支持值。 例如，如果项集包含两个产品，则将列出每个产品的名称，同时还会列出包括每个产品的事例的计数。  
  
 **规则节点** 包含两行。 第一行显示规则右侧（预测项目）所具有的属性以及置信度分数。  
  
 第二行为关联模型独有，包含一个指向位于规则右侧的项集的指针。 在 ATTRIBUTE_VALUE 列中，将该指针表示为仅包含右侧项目的项集的 ID。  
  
 例如，如果规则为 `If {A,B} Then {C}`，则该表包含项目 `{C}`的名称，以及含有项目 C 所在项集的节点的 ID。  
  
 在根据项集节点确定总共有多少个事例包含右侧产品时，该指针很有用处。 遵循 `If {A,B} Then {C}` 规则的事例是 `{C}`的项集中列出的事例的子集。  
  
 NODE_SUPPORT  
 支持此节点的事例的数目。  
  
 **父节点** 模型中的事例数。  
  
 **项集节点** 包含项集中所有项目的事例的数目。  
  
 **规则节点** 含有规则中包含的所有项目的事例的数目。  
  
 MSOLAP_MODEL_COLUMN  
 根据节点是项集还是规则，包含不同的信息。  
  
 **父节点** 空白。  
  
 **项集节点** 空白。  
  
 **规则节点** 包含规则左侧项目的项集的 ID。 例如，如果规则为 `If {A,B} Then {C}`，则该列包含仅含有 `{A,B}`的项集的 ID。  
  
 MSOLAP_NODE_SCORE  
 **父节点** 空白。  
  
 **项集节点** 项集的重要性分数。  
  
 **规则节点** 规则的重要性分数。  
  
> [!NOTE]  
>  项集和规则的重要性的计算方法不同。 有关详细信息，请参阅 [Microsoft 关联算法技术参考](microsoft-association-algorithm-technical-reference.md)。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 空白。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft 关联算法](microsoft-association-algorithm.md)   
 [关联模型查询示例](association-model-query-examples.md)  
  
  
