---
title: 神经网络模型的挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- output neurons [Analysis Services]
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- hidden layer
- hidden neurons
- input layer [Data Mining]
- input neurons [Analysis Services]
- mining model content, neural network models
- neural network model [Analysis Services]
ms.assetid: ea21ff9d-857f-475c-bd3d-6d1405bad069
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e19dfcdc284f048cffbb3a95e076b6e3a57294d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083587"
---
# <a name="mining-model-content-for-neural-network-models-analysis-services---data-mining"></a>神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）
  本主题介绍使用 Microsoft 神经网络算法的模型特有的挖掘模型内容。 有关如何解释所有模型类型共享的统计信息和结构，以及与挖掘模型内容相关的常规术语定义的说明，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-neural-network-model"></a>了解神经网络模型的结构  
 每个神经网络模型都具有一个表示该模型及其元数据的单一父节点，以及一个提供有关输入属性的说明性统计信息的边际统计信息节点 (NODE_TYPE = 24)。 边际统计信息节点非常有用，它汇总了输入相关信息，因此您无需从各个节点查询数据。  
  
 在这两个节点下面，至少还有两个另外的节点，也可能有更多节点，具体取决于该模型所具有的可预测属性的数目。  
  
-   第一个节点 (NODE_TYPE = 18) 始终表示输入层的顶端节点。 在该顶端节点下，您可以找到包含实际输入属性及其值的输入节点 (NODE_TYPE = 21)。  
  
-   每个后续节点各包含一个不同的“子网”(NODE_TYPE = 17)。 每个子网始终包含一个隐藏层 (NODE_TYPE = 19) 以及该子网的输出层 (NODE_TYPE = 20)。  
  
 ![神经网络模型内容结构](../media/modelcontentstructure-nn.gif "的神经网络模型内容结构")  
  
 输入层中的信息简单明了：每个输入层的顶端节点 (NODE_TYPE = 18) 充当输入节点 (NODE_TYPE = 21) 集合的组织程序。 下表说明了输入节点的内容。  
  
 每个子网 (NODE_TYPE = 17) 表示输入层对特定可预测属性的影响的分析。 如果有多个可预测输出，则有多个子网。 每个子网的隐藏层都包含多个隐藏节点 (NODE_TYPE = 22)，这些节点包含有关在该特定隐藏节点结束的每个转换的权重的详细信息。  
  
 输出层 (NODE_TYPE = 20) 包含多个输出节点 (NODE_TYPE = 23)，每个输出节点包含可预测属性的非重复值。 如果可预测属性为连续数值数据类型，则该属性只有一个输出节点。  
  
> [!NOTE]  
>  逻辑回归算法使用的是一种特殊的神经网络，这种神经网络仅有一个可预测结果并可能有多个输入。 逻辑回归不使用隐藏层。  
  
 浏览输入和子网结构的最简便方式是使用 **Microsoft 一般内容树查看器**。 您可以单击并展开任何节点，查看其子节点，或者查看该节点中包含的权重和其他统计信息。  
  
 若要使用数据和查看模型如何将输入与输出关联，请使用 **Microsoft 神经网络查看器**。 使用此自定义查看器，您可以筛选输入属性及其值，并以图形方式查看它们如何影响输出。 查看器中的工具提示显示与每对输入和输出值关联的概率和提升。 有关详细信息，请参阅 [使用 Microsoft 神经网络查看器浏览模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
## <a name="model-content-for-a-neural-network-model"></a>神经网络模型的模型内容  
 本部分提供的详细信息和示例仅针对挖掘模型内容中与神经网络有特殊关系的列。 有关此处未涵盖的架构行集中的通用列（如 MODEL_CATALOG 和 MODEL_NAME）的信息或有关挖掘模型术语的说明，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
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
|隐藏节点|空白|  
|输出层|空白|  
|输出节点|输出属性名称|  
  
 NODE_NAME  
 节点的名称。 该列包含的值与 NODE_UNIQUE_NAME 列相同。  
  
 NODE_UNIQUE_NAME  
 节点的唯一名称。  
  
 有关名称和 ID 如何提供有关模型的结构信息的详细信息，请参阅 [使用节点名称和 ID](#bkmk_NodeIDs)部分。  
  
 NODE_TYPE  
 神经网络模型输出以下节点类型：  
  
|节点类型 ID|Description|  
|------------------|-----------------|  
|1|模型。|  
|17|子网的组织程序节点。|  
|18|输入层的组织程序节点。|  
|19|隐藏层的组织程序节点。|  
|20|输出层的组织程序节点。|  
|21|输入属性节点。|  
|22|隐藏层节点|  
|23|输出属性节点。|  
|24|边际统计信息节点。|  
  
 NODE_CAPTION  
 与节点关联的标签或标题。 在神经网络模型中，始终为空白。  
  
 CHILDREN_CARDINALITY  
 对节点所具有的子节点数的估计。  
  
|节点|内容|  
|----------|-------------|  
|模型根|指示子节点的计数，其中至少包括 1 个网络，1 个必需边际节点和 1 个必需输入层。 例如，如果值为 5，则具有 3 个子网。|  
|边际统计信息|始终为 0。|  
|输入层|指示模型使用的输入属性值对的数目。|  
|输入节点|始终为 0。|  
|隐藏层|指示该模型创建的隐藏节点的数目。|  
|隐藏节点|始终为 0。|  
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
|隐藏节点|指示该隐藏节点在隐藏节点列表中的顺序的整数。|  
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
|隐藏节点|指示该隐藏节点在隐藏节点列表中的顺序的整数。|  
|输出层|空白|  
|输出节点|包含与 NODE_DESCRIPTION 列相同的信息的 XML 片段。|  
  
 MARGINAL_RULE  
 对于神经网络模型，始终为空白。  
  
 NODE_PROBABILITY  
 与此节点相关联的概率。 对于神经网络模型，始终为 0。  
  
 MARGINAL_PROBABILITY  
 从父节点到达该节点的概率。 对于神经网络模型，始终为 0。  
  
 NODE_DISTRIBUTION  
 包含节点的统计信息的嵌套表。 有关该表中每个节点类型的内容的详细信息，请参阅 [了解 NODE_DISTRIBUTION 表](#bkmk_NodeDistTable)部分。  
  
 NODE_SUPPORT  
 对于神经网络模型，始终为 0。  
  
> [!NOTE]  
>  由于该模型类型的输出不是概率性的，因此支持概率始终为 0。 只有权重才对该算法有意义；因此，该算法不会计算概率、支持或方差。  
  
 若要获取定型事例中对特定值的支持信息，请参阅边际统计信息节点。  
  
 MSOLAP_MODEL_COLUMN  
 |节点|内容|  
|----------|-------------|  
|模型根|空白|  
|边际统计信息|空白|  
|输入层|空白|  
|输入节点|输入属性名称。|  
|隐藏层|空白|  
|隐藏节点|空白|  
|输出层|空白|  
|输出节点|输入属性名称。|  
  
 MSOLAP_NODE_SCORE  
 对于神经网络模型，始终为 0。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 对于神经网络模型，始终为空白。  
  
## <a name="remarks"></a>备注  
 定型神经网络模型的目的是确定与从输入到中点、再从中点到终结点的每个转换关联的权重。 因此，该模型的输入层的主要存在目的是存储用于生成该模型的实际值。 隐藏层存储计算的权重，并提供回指到输入属性的指针。 输出层存储可预测值，并提供回指到隐藏层的中点的指针。  
  
##  <a name="bkmk_NodeIDs"></a> 使用节点名称和 ID  
 神经网络模型中各节点的命名方式提供有关节点的类型的其他信息，以便于将隐藏层与输入层相关联，并将输出层与隐藏层相关联。 下表给出了为每层中的节点分配 ID 的约定。  
  
|节点类型|节点 ID 约定|  
|---------------|----------------------------|  
|模型根 (1)|00000000000000000.|  
|边际统计信息节点 (24)|10000000000000000|  
|输入层 (18)|30000000000000000|  
|输入节点 (21)|以 60000000000000000 作为开头|  
|子网 (17)|20000000000000000|  
|隐藏层 (19)|40000000000000000|  
|隐藏节点 (22)|以 70000000000000000 作为开头|  
|输出层 (20)|50000000000000000|  
|输出节点 (23)|以 80000000000000000 作为开头|  
  
 通过查看隐藏节点 (NODE_TYPE = 22) 中的 NODE_DISTRIBUTION 表，您可以确定哪些输入属性与特定隐藏层节点关联。 NODE_DISTRIBUTION 表的每个行包含输入属性节点的 ID。  
  
 类似地，通过查看输出节点 (NODE_TYPE = 23) 中的 NODE_DISTRIBUTION 表，您可以确定哪些隐藏层与输出属性关联。 NODE_DISTRIBUTION 表的每个行包含隐藏层节点的 ID 和相关系数。  
  
##  <a name="bkmk_NodeDistTable"></a> 解释 NODE_DISTRIBUTION 表中的信息  
 NODE_DISTRIBUTION 表在某些节点中可以为空。 但是，对于输入节点、隐藏层节点和输出节点，NODE_DISTRIBUTION 表存储模型的重要相关信息。 为帮助您解释该信息，NODE_DISTRIBUTION 表为每个行包含一个 VALUETYPE 列，指示 ATTRIBUTE_VALUE 列中的值是离散 (4)、离散化 (5) 还是连续 (3) 值。  
  
### <a name="input-nodes"></a>输入节点  
 输入层为模型中使用的属性的每个值各包含一个节点。  
  
 **离散属性：** 输入的节点存储属性和其值的名称仅在 ATTRIBUTE_NAME 和 ATTRIBUTE_VALUE 列中。 例如，如果列为 [Work Shift]，则为模型中使用的该列的每个值（例如 AM 和 PM）创建一个单独的节点。 每个节点的 NODE_DISTRIBUTION 表仅列出属性的当前值。  
  
 **离散化数值属性：** 输入的节点存储属性和值，该值可以是一个范围或特定值的名称。 所有值均通过表达式表示，例如将 [Time Per Issue] 的值表示为“77.4 - 87.4”或“< 64.0”。 每个节点的 NODE_DISTRIBUTION 表仅列出属性的当前值。  
  
 **连续属性：** 输入的节点存储属性的平均值。 每个节点的 NODE_DISTRIBUTION 表仅列出属性的当前值。  
  
### <a name="hidden-layer-nodes"></a>隐藏层节点  
 隐藏层包含可变数目的节点。 在每个节点中，NODE_DISTRIBUTION 表包含从隐藏层到输入层中的节点的映射。 ATTRIBUTE_NAME 列包含与输入层中的节点对应的节点 ID。 ATTRIBUTE_VALUE 列包含与输入节点和隐藏层节点的该组合关联的权重。 表中的最后一行包含表示隐藏层中的该隐藏节点的权重的系数。  
  
### <a name="output-nodes"></a>输出节点  
 输出层为模型中使用的每个输出值各包含一个输出节点。 在每个节点中，NODE_DISTRIBUTION 表包含从输出层到隐藏层中的节点的映射。 ATTRIBUTE_NAME 列包含与隐藏层中的节点对应的节点 ID。 ATTRIBUTE_VALUE 列包含与输出节点和隐藏层节点的该组合关联的权重。  
  
 NODE_DISTRIBUTION 表根据属性类型包含以下其他信息：  
  
 **离散属性：** NODE_DISTRIBUTION 表的最后两行包含该节点作为一个整体和该属性的当前值的系数。  
  
 **离散化数值属性：** 与离散属性相同，但该属性的值的值范围。  
  
 **连续属性：** NODE_DISTRIBUTION 表的最后两行包含属性的平均值、 整个节点的系数和系数的方差。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Microsoft 神经网络算法技术参考](microsoft-neural-network-algorithm-technical-reference.md)   
 [神经网络模型查询示例](neural-network-model-query-examples.md)  
  
  
