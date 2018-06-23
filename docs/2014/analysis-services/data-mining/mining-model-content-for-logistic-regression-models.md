---
title: 逻辑回归模型的挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logistic regression [Analysis Services]
- mining model content, logistic regression models
- regression algorithms [Analysis Services]
ms.assetid: 69cc0b86-e8bc-4d6c-903e-85724f5c0396
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e9846361e76eac9f4ad61edde10c0fda20f4f546
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014206"
---
# <a name="mining-model-content-for-logistic-regression-models-analysis-services---data-mining"></a>逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）
  本主题介绍使用 Microsoft 逻辑回归算法的模型特有的挖掘模型内容。 有关如何解释所有模型类型共享的统计信息和结构，以及与挖掘模型内容相关的常规术语定义的说明，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-logistic-regression-model"></a>了解逻辑回归模型的结构  
 逻辑回归模型是使用带有约束模型以消除隐藏节点的参数的 Microsoft 神经网络算法创建的。 因此，逻辑回归模型的总体结构几乎与神经网络的总体结构相同：每个模型都具有一个表示该模型及其元数据的单一父节点，以及一个提供有关在该模型中使用的输入的说明性统计信息的特殊边际统计信息节点 (NODE_TYPE = 24)。  
  
 此外，该模型还包含每个可预测属性的子网 (NODE_TYPE = 17)。 和在神经网络模型中一样，每个子网始终包含两个分支：其中一个分支用于输入层，而另一个分支则包含网络的隐藏层 (NODE_TYPE = 19) 和输出层 (NODE_TYPE = 20)。 如果将多个属性指定为仅预测，则可以对这些属性使用相同的子网。 同时作为输入的可预测属性可能不会显示在相同子网中。  
  
 但是，在逻辑回归模型中，表示隐藏层的节点为空，该节点没有任何子级。 因此，该模型包含表示单个输出 (NODE_TYPE = 23) 和单个输入 (NODE_TYPE = 21) 的节点，但不包含任何单个隐藏节点。  
  
 ![logisitc 回归模型的内容的结构](../media/skt-modelcontentstructure-logregc.gif "logisitc 回归模型的内容的结构")  
  
 默认情况下，逻辑回归模型在 **Microsoft 神经网络查看器**中显示。 使用此自定义查看器，您可以筛选输入属性及其值，并以图形方式查看它们如何影响输出。 查看器中的工具提示显示与每对输入和输出值关联的概率和提升。 有关详细信息，请参阅 [使用 Microsoft 神经网络查看器浏览模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 若要浏览输入和子网的结构，并查看详细统计信息，您可以使用 Microsoft 一般内容树查看器。 您可以单击并展开任何节点，查看其子节点，或者查看该节点中包含的权重和其他统计信息。  
  
## <a name="model-content-for-a-logistic-regression-model"></a>逻辑回归模型的模型内容  
 本部分提供的详细信息和示例仅针对挖掘模型内容中与逻辑回归有特殊关系的列。 模型内容与神经网络模型的内容几乎相同，但是为方便起见，此表可能将重复应用于神经网络模型的说明。  
  
 有关此处未涵盖的架构行集中的通用列（如 MODEL_CATALOG 和 MODEL_NAME）的信息或有关挖掘模型术语的说明，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
 MODEL_CATALOG  
 存储模型的数据库的名称。  
  
 MODEL_NAME  
 模型的名称。  
  
 ATTRIBUTE_NAME  
 与此节点对应的属性的名称。  
  
|节点|内容|  
|----------|-------------|  
|模型根|空白|  
|边际统计信息|空白|  
|输入层|空白|  
|输入节点|输入属性名称|  
|隐藏层|空白|  
|输出层|空白|  
|输出节点|输出属性名称|  
  
 NODE_NAME  
 节点的名称。 当前，该列包含的值与 NODE_UNIQUE_NAME 的值相同，但是这一情况在以后的版本中可能会发生变化。  
  
 NODE_UNIQUE_NAME  
 节点的唯一名称。  
  
 有关名称和 ID 如何提供有关模型的结构信息的详细信息，请参阅 [使用节点名称和 ID](#bkmk_NodeIDs)部分。  
  
 NODE_TYPE  
 逻辑回归模型输出以下节点类型：  
  
|节点类型 ID|Description|  
|------------------|-----------------|  
|@shouldalert|模型。|  
|17|子网的组织程序节点。|  
|18|输入层的组织程序节点。|  
|19|隐藏层的组织程序节点。 隐藏层为空。|  
|20|输出层的组织程序节点。|  
|21|输入属性节点。|  
|23|输出属性节点。|  
|24|边际统计信息节点。|  
  
 NODE_CAPTION  
 与节点关联的标签或标题。 在逻辑回归模型中，始终为空白。  
  
 CHILDREN_CARDINALITY  
 对节点所具有的子节点数的估计。  
  
|节点|内容|  
|----------|-------------|  
|模型根|指示子节点的计数，其中至少包括 1 个网络，1 个必需边际节点和 1 个必需输入层。 例如，如果值为 5，则具有 3 个子网。|  
|边际统计信息|始终为 0。|  
|输入层|指示模型使用的输入属性值对的数目。|  
|输入节点|始终为 0。|  
|隐藏层|在逻辑回归模型中，始终为 0。|  
|输出层|指示输出值的数目。|  
|输出节点|始终为 0。|  
  
 PARENT_UNIQUE_NAME  
 节点的父节点的唯一名称。 根级别上的任何节点均返回 NULL。  
  
 有关名称和 ID 如何提供有关模型的结构信息的详细信息，请参阅 [使用节点名称和 ID](#bkmk_NodeIDs)部分。  
  
 NODE_DESCRIPTION  
 节点的用户友好说明。  
  
|节点|内容|  
|----------|-------------|  
|模型根|空白|  
|边际统计信息|空白|  
|输入层|空白|  
|输入节点|输入属性名称|  
|隐藏层|空白|  
|输出层|空白|  
|输出节点|如果输出属性是连续的，则包含输出属性的名称。<br /><br /> 如果输出属性是离散或离散化属性，则包含属性的名称和值。|  
  
 NODE_RULE  
 嵌入节点的规则的 XML 说明。  
  
|节点|内容|  
|----------|-------------|  
|模型根|空白|  
|边际统计信息|空白|  
|输入层|空白|  
|输入节点|包含与 NODE_DESCRIPTION 列相同的信息的 XML 片段。|  
|隐藏层|空白|  
|输出层|空白|  
|输出节点|包含与 NODE_DESCRIPTION 列相同的信息的 XML 片段。|  
  
 MARGINAL_RULE  
 对于逻辑回归模型，始终为空白。  
  
 NODE_PROBABILITY  
 与此节点相关联的概率。 对于逻辑回归模型，始终为 0。  
  
 MARGINAL_PROBABILITY  
 从父节点到达该节点的概率。 对于逻辑回归模型，始终为 0。  
  
 NODE_DISTRIBUTION  
 包含节点的统计信息的嵌套表。 此表，以便每个节点类型的内容的详细信息，请参阅部分，了解 NODE_DISTRIBUTION 表中[挖掘模型内容神经网络模型的&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 NODE_SUPPORT  
 对于逻辑回归模型，始终为 0。  
  
> [!NOTE]  
>  由于该模型类型的输出不是概率性的，因此支持概率始终为 0。 对算法有意义的唯一项是权重；因此，算法不会计算概率、支持或方差。  
  
 若要获取定型事例中对特定值的支持信息，请参阅边际统计信息节点。  
  
 MSOLAP_MODEL_COLUMN  
 |节点|内容|  
|----------|-------------|  
|模型根|空白|  
|边际统计信息|空白|  
|输入层|空白|  
|输入节点|输入属性名称。|  
|隐藏层|空白|  
|输出层|空白|  
|输出节点|输入属性名称。|  
  
 MSOLAP_NODE_SCORE  
 在逻辑回归模型中，始终为 0。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 在逻辑回归模型中，始终为空白。  
  
##  <a name="bkmk_NodeIDs"></a> 使用节点名称和 ID  
 逻辑回归模型中各节点的命名方式提供该模型中各节点之间的关系的其他相关信息。 下表给出了为每层中的节点分配 ID 的约定。  
  
|节点类型|节点 ID 约定|  
|---------------|----------------------------|  
|模型根 (1)|00000000000000000.|  
|边际统计信息节点 (24)|10000000000000000|  
|输入层 (18)|30000000000000000|  
|输入节点 (21)|以 60000000000000000 作为开头|  
|子网 (17)|20000000000000000|  
|隐藏层 (19)|40000000000000000|  
|输出层 (20)|50000000000000000|  
|输出节点 (23)|以 80000000000000000 作为开头|  
  
 通过查看输出节点的 NODE_DISTRIBUTION 表，您可以使用这些 ID 确定输出属性如何与特定输入层属性关联。 该表中的每一行都包含一个会指到特定输入属性节点的 ID。 NODE_DISTRIBUTION 表还包含该输入-输出对的系数。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 逻辑回归算法](microsoft-logistic-regression-algorithm.md)   
 [神经网络模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [逻辑回归模型查询示例](logistic-regression-model-query-examples.md)   
 [Microsoft 逻辑回归算法技术参考](microsoft-logistic-regression-algorithm-technical-reference.md)  
  
  