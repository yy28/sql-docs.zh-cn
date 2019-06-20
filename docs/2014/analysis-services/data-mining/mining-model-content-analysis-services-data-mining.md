---
title: 挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- standard deviation
- confidence scores [data mining]
- mining models [Analysis Services]
- variance
- machine learning algorithms [Analysis Services]
- model content
- support [data mining]
- node distribution
ms.assetid: e7c039f6-3266-4d84-bfbd-f99b6858acf4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d09f32cb21762ca56eab156701ee013ef2c03ec3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083775"
---
# <a name="mining-model-content-analysis-services---data-mining"></a>挖掘模型内容（Analysis Services - 数据挖掘）
  使用基础挖掘结构中的数据设计并处理挖掘模型后，该挖掘模型就已完成，包含有“  挖掘模型内容”。 可以使用此内容来预测或分析您的数据。  
  
 挖掘模型内容包含关于模型的元数据、关于数据的统计信息以及挖掘算法发现的模式。 模型内容可能包括回归公式、规则和项集的定义或权重和其他统计信息，具体取决于所使用的算法。  
  
 不论使用的是哪种算法，挖掘模型内容都是以标准结构呈现的。 你可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]提供的 Microsoft 一般内容树查看器中浏览结构，然后切换到自定义查看器之一，以查看如何针对每种模型类型以图形方式解释和显示信息。 还可以使用支持 MINING_MODEL_CONTENT 架构行集的任意客户端创建针对该挖掘模型内容的查询。 有关详细信息，请参阅 [数据挖掘查询任务和操作指南](data-mining-query-tasks-and-how-tos.md)。  
  
 本节介绍为所有的挖掘模型类型提供的基本内容结构。 还说明了所有挖掘模型内容所通用的节点类型，并提供了关于如何解释这些信息的指南。  
  
 [挖掘模型内容的结构](#bkmk_Structure)  
  
 [模型内容中的节点](#bkmk_Nodes)  
  
 [按算法类型列出挖掘模型内容](#bkmk_AlgoType)  
  
 [查看挖掘模型内容的工具](#bkmk_Viewing)  
  
 [查询挖掘模型内容的工具](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> 挖掘模型内容的结构  
 每个模型的内容均显示为一系列“节点  ”。 节点是挖掘模型内的对象，包含该模型某一部分的元数据或信息。 节点按层次结构排列。 层次结构中节点的准确排列以及层次结构的含义取决于您使用的算法。 例如，如果您创建一个决策树模型，该模型可以包含多个树，并且所有树均连接到模型根；如果您创建一个神经网络模型，则该模型可能包含一个或多个网络，外加一个统计信息节点。  
  
 每个模型中的第一个节点都称为“  根节点”或“模型父节点  ”。 每个模型都有一个根节点 (NODE_TYPE = 1)。 根节点通常包含关于模型的某些元数据以及子节点的数目，但是几乎没有关于该模型发现的模式的其他信息。  
  
 根据您用来创建模型的算法，根节点的子节点的数量会有所不同。 子节点具有不同的含义，包含不同的内容，具体取决于算法以及数据的深度和复杂性。  
  
##  <a name="bkmk_Nodes"></a> 挖掘模型内容中的节点  
 在挖掘模型中，每个节点都是一个常规用途的容器，用于存储关于整个模型或它的一部分的一段信息。 每个节点的结构始终是相同的，并包含数据挖掘架构行集定义的列。 有关详细信息，请参阅 [DMSCHEMA_MINING_MODEL_CONTENT 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
 每个节点都包含关于该节点的元数据，包括在每个模型中唯一的标识符、父节点的 ID 以及该节点具有的子节点数量。 元数据标识节点属于哪个模型以及存储该特定模型的数据库目录。 节点中提供的其他内容根据您用来创建模型的算法类型的不同而不同，可能包含：  
  
-   支持特定的预测值的定型数据中的事例计数。  
  
-   统计信息，如平均值、标准偏差或方差。  
  
-   系数和公式。  
  
-   规则和横向指针的定义。  
  
-   XML 片段，用于描述该模型的一部分。  
  
### <a name="list-of-mining-content-node-types"></a>挖掘内容节点类型的列表  
 下表列出了可以在数据挖掘模型中输出的各种类型的节点。 由于每种算法处理信息的方式不同，因此每个模型仅生成几种特定类型的节点。 如果您更改算法，节点的类型可能也会更改。 此外，如果您重新处理模型，每个节点的内容可能也会更改。  
  
> [!NOTE]  
>  如果你使用的数据挖掘服务不是由 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]提供的，或者你创建自己的插件算法，则可能还有更多自定义节点类型。  
  
|NODE_TYPE ID|节点标签|节点内容|  
|-------------------|----------------|-------------------|  
|1|“模型”|元数据和根内容节点。 适用于所有模型类型。|  
|2|树|分类树的根节点。 适用于决策树模型。|  
|3|Interior|树中的内部拆分节点。 适用于决策树模型。|  
|4|Distribution|树的终端节点。 适用于决策树模型。|  
|5|分类|算法检测到的分类。 适用于聚类分析模型以及顺序分析和聚类分析模型。|  
|6|Unknown|未知节点类型。|  
|7|ItemSet|算法检测到的项集。 适用于关联模型或顺序分析和聚类分析模型。|  
|8|AssociationRule|算法检测到的关联规则。 适用于关联模型或顺序分析和聚类分析模型。|  
|9|PredictableAttribute|可预测属性。 适用于所有模型类型。|  
|10|InputAttribute|输入属性。 适用于决策树和 Naïve Bayes 模型。|  
|11|InputAttributeState|有关输入属性状态的统计信息。 适用于决策树和 Naïve Bayes 模型。|  
|13|序列|序列分类的 Markov 模型组件的顶端节点。 适用于顺序分析和聚类分析模型。|  
|14|Transition|Markov 转换矩阵。 适用于顺序分析和聚类分析模型。|  
|15|TimeSeries|时序树的非根节点。 仅适用于时序模型。|  
|16|TsTree|对应于可预测时序的时序树的根节点。 适用于时序模型，并仅限于使用 MIXED 参数创建的模型。|  
|17|NNetSubnetwork|一个子网络。 适用于神经网络模型。|  
|18|NNetInputLayer|包含输入层的节点的组。 适用于神经网络模型。|  
|19|NNetHiddenLayer|包含描述隐藏层的节点的组。 适用于神经网络模型。|  
|21|NNetOutputLayer|包含输出层的节点的组。 适用于神经网络模型。|  
|21|NNetInputNode|将输入属性与对应状态相匹配的输入层中的节点。 适用于神经网络模型。|  
|22|NNetHiddenNode|隐藏层中的节点。 适用于神经网络模型。|  
|23|NNetOutputNode|输出层中的节点。 此节点通常将输出属性与对应的状态相匹配。 适用于神经网络模型。|  
|24|NNetMarginalNode|关于定型集的边际统计信息。 适用于神经网络模型。|  
|25|RegressionTreeRoot|回归树的根。 适用于线性回归模型以及包含连续的输入属性的决策树模型。|  
|26|NaiveBayesMarginalStatNode|关于定型集的边际统计信息。 适用于 Naïve Bayes 模型。|  
|27|ArimaRoot|ARIMA 模型的根节点。 仅适用于那些使用 ARIMA 算法的时序模型。|  
|28|ArimaPeriodicStructure|ARIMA 模型中的周期性结构。 仅适用于那些使用 ARIMA 算法的时序模型。|  
|29|ArimaAutoRegressive|ARIMA 模型中的单个字词的自动回归系数。<br /><br /> 仅适用于那些使用 ARIMA 算法的时序模型。|  
|30|ArimaMovingAverage|ARIMA 模型中单个字词的移动平均值系数。 仅适用于那些使用 ARIMA 算法的时序模型。|  
|1000|CustomBase|自定义节点类型的起始点。 自定义节点类型必须是值大于此常量的整数。 适用于通过使用自定义插件算法创建的模型。|  
  
### <a name="node-id-name-caption-and-description"></a>节点 ID、名称、标题和说明  
 任何模型的根节点始终具有值为 0 的唯一 ID (**NODE_UNIQUE_NAME**)。 所有节点 ID 自动由 Analysis Services 分配，无法修改。  
  
 每个模型的根节点还包含有关模型的一些基本的元数据。 这些元数据包括存储模型的 Analysis Services 数据库 (**MODEL_CATALOG**)、架构 (**MODEL_SCHEMA)** 和模型的名称 (**MODEL_NAME)** 。 不过，这些信息在模型的所有节点中都是重复的，因此您无需查询根节点来获取这些元数据。  
  
 除了用作唯一标识符的名称，每个节点还具有一个名称(**NODE_NAME**)  。 此名称是算法自动创建的，用于显示目的，不能进行编辑。  
  
> [!NOTE]  
>  Microsoft 聚类分析算法允许用户为每个分类指定友好名称。 不过，这些友好名称在服务器上不是持久性的，如果您重新处理模型，算法将重新生成新的分类名称。  
  
 每个节点的“标题  ”和“说明  ”都是由算法自动生成的，用作标签，可以帮助您了解节点的内容。 为每个字段生成的文本取决于模型类型。 某些情况下，名称、标题和说明可能包含完全相同的字符串，但是在某些模型中，说明还可能包含更多信息。 请参阅各个模型类型的主题，了解有关实现的详细信息。  
  
> [!NOTE]  
>  Analysis Services 服务器支持重命名节点，前提是您的模型是使用实现重命名的自定义插件算法生成的。 若要启用重命名，必须在创建插件算法时覆盖方法。  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>父节点、子节点和节点基数  
 树结构中父节点和子节点之间的关系是由 PARENT_UNIQUE_NAME 列的值决定的。 该值存储在子节点，指示父节点的 ID。 下面给出了说明此信息的含义的示例：  
  
-   为 NULL 的 PARENT_UNIQUE_NAME 表示此节点是模型的顶端节点。  
  
-   如果 PARENT_UNIQUE_NAME 的值为 0，则此节点一定是模型中顶端节点的直接后代。 这是因为根节点的 ID 始终为 0。  
  
-   您可以在数据挖掘扩展插件 (DMX) 查询内使用函数来查找特定节点的后代或父级。 有关在查询中使用函数的详细信息，请参阅[数据挖掘查询](data-mining-queries.md)。  
  
 “  基数”是指集中的项数。 在处理的挖掘模型的上下文中，基数会指示特定节点中子级的数量。 例如，如果某个决策树模型有一个 [Yearly Income] 节点，并且该节点有两个子节点，一个针对条件 [Yearly Income] = High，一个针对条件 [Yearly Income] = Low，则 [Yearly Income] 节点的 CHILDREN_CARDINALITY 值将为 2。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，当计算节点的基数时，仅统计直接的子节点。 不过，如果您创建了一个自定义插件算法，则可以重载 CHILDREN_CARDINALITY，从而按不同的方式统计基数。 这种做法可能会很有用，例如，如果您希望统计后代的总数，而不仅仅是直接子级的数量。  
  
 尽管对于所有模型来说统计基数的方法都是相同的，但是根据模型类型的不同，解释或使用基数值的方式会有所不同。 例如，在聚类分析模型中，顶端节点的基数会指示已找到的分类总数。 在其他类型的模型中，基数可能始终有一个设定的值（取决于节点类型）。 有关如何解释基数的详细信息，请参阅有关各个模型类型的主题。  
  
> [!NOTE]  
>  有些模型（例如，由 Microsoft 神经网络算法创建的模型）另外还包含一个特殊的节点类型，该类型提供关于整个模型的定型数据的描述性统计信息。 根据定义，这些节点永远不会具有子节点。  
  
### <a name="node-distribution"></a>节点分布  
 NODE_DISTRIBUTION 列包含一个嵌套表，在许多节点中这个表都提供有关算法所发现的模式的重要而详细的信息。 根据模型类型、节点在树中的位置以及此可预测属性是连续数值还是离散值，该表中所提供的准确统计信息会有所变化；不过，它们可以包括属性的最小值和最大值、分配给值的权重、节点中事例的数量、回归公式中使用的系数以及诸如标准偏差和方差等统计度量值。 有关如何解释节点分布的详细信息，请参阅对应于您所使用的特定模型类型的主题。  
  
> [!NOTE]  
>  NODE_DISTRIBUTION 表可能为空，具体取决于节点类型。 例如，某些节点仅用于组织子节点的集合，包含详细统计信息的是子节点。  
  
 嵌套表 NODE_DISTRIBUTION 始终包含以下列。 每个列的内容会有所不同，具体取决于模型类型。 有关特定模型类型的详细信息，请参阅 [按算法类型列出挖掘模型内容](#bkmk_AlgoType)。  
  
 ATTRIBUTE_NAME  
 内容随算法的不同而变化。 可以是列的名称，例如可预测属性、规则、项集或算法内部的一条信息（如公式的一部分）。  
  
 此列还可以包含一个属性/值对。  
  
 ATTRIBUTE_VALUE  
 在 ATTRIBUTE_NAME 中指定的属性的值。  
  
 如果属性名称为列，则在最简单的事例中，ATTRIBUTE_VALUE 包含该列的离散值之一。  
  
 根据算法处理值的方式，ATTRIBUTE_VALUE 还可能包含一个标志，用于指示该属性是存在一个值 (`Existing`) 还是值为 Null (`Missing`)。  
  
 例如，如果将模型设置为查找至少购买过一次某个特定商品的客户，ATTRIBUTE_NAME 列可能包含属性/值对，用于定义所关注的商品（如 `Model = 'Water bottle'`），并且 ATTRIBUTE_VALUE 列将仅仅包含关键字 `Existing` 或 `Missing`。  
  
 Support  
 具有此属性/值对或包含此项集或规则的事例的计数。  
  
 通常，每个节点的支持值会指示定型集中有多少事例包含在当前节点中。 在大多数模型类型中，支持代表的是事例的准确计数。 支持值很有用，这是因为它使得您无需查询定型数据，就可以查看定型事例内的数据分布。 Analysis Services 服务器还使用这些存储值来计算存储概率与以前的概率之比，以确定推导是强还是弱。  
  
 例如，在分类树中，支持值指示具有所描述的属性组合的事例数。  
  
 在决策树中，树中每个级别的支持的总数等于其父节点的支持数。 例如，如果包含 1200 个事例的模型按性别，并且再平分由三个值的收入低、 中和高的子节点的节点 (2) 节点 (4)，(5) 和 (6)，始终等于相同数量的情况下为节点 (2)。  
  
|节点 ID 和节点属性|支持计数|  
|---------------------------------|-------------------|  
|(1) 模型根|1200|  
|(2) Gender = Male<br /><br /> (3) Gender = Female|600<br /><br /> 600|  
|(4) Gender = Male 并且 Income = High<br /><br /> (5) Gender = Male 并且 Income = Medium<br /><br /> (6) Gender = Male 并且 Income = Low|200<br /><br /> 200<br /><br /> 200|  
|(7) Gender = Female 并且 Income = High<br /><br /> (8) Gender = Female 并且 Income = Medium<br /><br /> (9) Gender = Female 并且 Income = Low|200<br /><br /> 200<br /><br /> 200|  
  
 对于聚类分析模型，支持的数量可以加权，以包括属于多个分类的概率。 多重分类成员身份是默认的聚类分析方法。 在这种情况下，由于每个事例不必属于一个且仅一个分类，因此这些模型中的支持在所有分类中可能不会合计达 100%。  
  
 PROBABILITY  
 指示在整个模型中此特定节点的概率。  
  
 通常，概率代表对此特定值的支持除以节点内的事例总数 (NODE_SUPPORT)。  
  
 但是，概率会略有调整以消除数据中缺失的值所造成的偏差。  
  
 例如，如果 [Total Children] 的当前值为 'One' 和 'Two'，则您会希望避免创建预测出不可能没有孩子或有三个孩子的模型。 若要确保缺失值是不可能的（而是完全可能），则算法会始终为任何属性的实际值的计数加 1。  
  
 例如：  
  
 [Total Children = One] 的概率 = [Total Children = One 的事例数] + 1/[所有事例数] + 3  
  
 [Total Children = Two] 的概率 = [Total Children = Two 的事例数] +1/[所有事例数] +3  
  
> [!NOTE]  
>  调整值 3 是通过将现有值的总数 n 加 1 而计算得来的。  
  
 调整后，所有值的概率相加仍为 1。 没有数据的值的概率（在此示例中，[Total Children = 'Zero'、'Three' 或其他某个值]）是从一个很低的非零级别开始，并随着事例数的增加而缓慢上升。  
  
 方差  
 指示节点中值的方差。 根据定义，对于离散值，方差始终为 0。 如果模型支持连续值，则方差是使用分母 n 或节点中的事例数计算为 σ (sigma) 的。  
  
 一般有两个定义用来表示标准偏差 (`StDev`)。 计算标准偏差的一个方法是考虑偏差，另一个方法是不使用偏差计算标准偏差。 一般情况下，Microsoft 数据挖掘算法在计算标准偏差时不使用偏差。  
  
 NODE_DISTRIBUTION 表中显示的值是所有离散和离散化属性的实际值以及连续值的平均值。  
  
 VALUE_TYPE  
 指示值或属性的数据类型以及值的用法。 某些值类型仅适用于某些特定的模型类型：  
  
|VALUE_TYPE ID|值标签|值类型名称|  
|--------------------|-----------------|---------------------|  
|1|Missing|指示事例数据不包含此属性的值。 `Missing` 状态与具有值的属性是分开计算的。|  
|2|Existing|指示事例数据包含此属性的值。|  
|3|连续|指示此属性的值是一个连续数值，因此可以由平均值以及偏差和标准偏差表示。|  
|4|离散|指示值（数字或文本）被视为离散值。<br /><br /> **注意** 离散值也可能处于缺失状态；不过，在进行计算时，它们的处理方式不同。 有关信息，请参阅[缺失值（Analysis Services - 数据挖掘）](missing-values-analysis-services-data-mining.md)。|  
|5|离散化|指示该属性包含已离散化的数值。 该值将是一个带格式的字符串，描述离散化存储桶。|  
|6|Existing|指示属性具有连续数值，并且这些值已经在数据中提供（与缺失或推导的值不同）。|  
|7|系数|指示一个表示系数的数值。<br /><br /> 系数是一个在计算依赖变量的值时要应用的值。 例如，如果您的模型创建了一个基于年龄预测收入的回归公式，则在将年龄与收入相关联的公式中将使用系数。|  
|8|得分|指示表示某个属性的得分的数值。|  
|9|统计信息|指示表示回归量的统计信息的数值。|  
|10|节点唯一名称|指示该值不应处理为数字或字符串，而是应处理为模型中另一内容节点的唯一标识符。<br /><br /> 例如，在神经网络模型中，ID 提供从输出层中节点至隐藏层中节点的指针，以及从隐藏层中节点至输入层中节点的指针。|  
|11|截距|表示数值，代表回归公式中的截距。|  
|12|周期|指示该值表示模型中的周期性结构。<br /><br /> 仅适用于包含 ARIMA 模型的时序模型。<br /><br /> 注意：Microsoft 时序算法自动检测到周期性结构根据定型数据。 因而，最终模型中的周期包括的周期值可能不是您在创建模型时作为参数提供的。|  
|13|自动回归阶数|指示一个值，该值表示自动回归序列的数目。<br /><br /> 适用于使用 ARIMA 算法的时序模型。|  
|14|移动平均值阶数|表示一个值，该值表示一个序列中的移动平均值数。<br /><br /> 适用于使用 ARIMA 算法的时序模型。|  
|15|差分阶数|指示一个值，用于表示差分时序的次数。<br /><br /> 适用于使用 ARIMA 算法的时序模型。|  
|16|Boolean|表示布尔型。|  
|17|其他|表示一个由该算法定义的自定义值。|  
|18|预呈现的字符串|表示一个由算法作为字符串呈现的自定义值。 对象模型不应用格式。|  
  
 值类型是从 ADMOMD.NET 枚举派生的。 有关详细信息，请参阅 <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>。  
  
### <a name="node-score"></a>节点分数  
 根据模型类型的不同，节点分数的含义也不同，也可以特定于节点类型。 有关如何为每个模型和节点类型计算 NODE_SCORE 的信息，请参阅 [按算法类型列出挖掘模型内容](#bkmk_AlgoType)。  
  
### <a name="node-probability-and-marginal-probability"></a>节点概率和边际概率  
 所有模型类型的挖掘模型架构行集均包括列 NODE_PROBABILITY 和 MARGINAL_PROBABILITY。 这些列仅在那些概率值有意义的节点中包含值。 例如，模型的根节点永远不会包含一个概率分数。  
  
 在那些提供概率分数的节点中，节点概率和边际概率表示不同的计算。  
  
-   **边际概率** 是指从其父节点到达该节点的概率。  
  
-   **节点概率** 是指从根节点到达该节点的概率。  
  
-   **节点概率** 始终小于或等于 **边际概率**。  
  
 例如，如果决策树中所有客户的总人数按性别平分（并且没有值缺失），则子节点的概率应为 .5。 但是，假设根据收入级别的每个性别节点也同样划分-High、 Medium 和 Low。 这种情况下，每个子节点的 MARGINAL_PROBABILITY 分数应始终为 .33，而 NODE_PROBABILTY 值将是指向该节点的所有概率的乘积，因此始终小于 MARGINAL_PROBABILITY 值。  
  
|节点/属性和值的级别|边际概率|节点概率|  
|----------------------------------------|--------------------------|----------------------|  
|模型根<br /><br /> 所有目标客户|1|1|  
|按性别平分目标客户|.5|.5|  
|按性别平分目标客户，然后按三种收入级别平分|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>节点规则和边际规则  
 所有模型类型的挖掘模型架构行集也均包括列 NODE_RULE 和 MARGINAL_RULE。 这些列包含 XML 片段，可以用于对模型进行序列化，或表示模型结构的某一部分。 如果某个值毫无意义，则某些节点的这些列可能为空。  
  
 提供两种类型的 XML 规则，与两种类型的概率值相似。 MARGINAL_RULE 中的 XML 片段用于定义当前节点的属性和值，而 NODE_RULE 中的 XML 片段用于描述从模型根至当前节点的路径。  
  
##  <a name="bkmk_AlgoType"></a> 按算法类型列出挖掘模型内容  
 每个算法将不同类型的信息作为其内容架构的一部分存储。 例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法会生成许多子节点，每个节点代表一个可能的分类。 每个群集节点都包含一些规则，这些规则描述该分类中各个项所共有的特征。 相反， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法不包含任何子节点；而模型的父节点包含的公式用于说明分析所发现的线性关系。  
  
 下表提供了指向每种算法的主题的链接：  
  
-   **模型内容主题：** 说明每种算法类型，每个节点类型的含义，并提供有关哪些节点最感兴趣的特定模型类型中的指导。  
  
-   **查询主题：** 提供了有关如何解释结果的针对特定模型类型和指南的查询的示例。  
  
|算法或模型类型|模型内容|查询挖掘模型|  
|-----------------------------|-------------------|----------------------------|  
|关联规则模型|[关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-association-models-analysis-services-data-mining.md)|[关联模型查询示例](association-model-query-examples.md)|  
|聚类分析模型|[决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[聚类分析模型查询示例](clustering-model-query-examples.md)|  
|决策树模型|[决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[决策树模型查询示例](decision-trees-model-query-examples.md)|  
|线性回归模型|[线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[线性回归模型查询示例](linear-regression-model-query-examples.md)|  
|逻辑回归模型|[逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-logistic-regression-models.md)|[线性回归模型查询示例](linear-regression-model-query-examples.md)|  
|Naïve Bayes 模型|[Naive Bayes 模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Naive Bayes 模型查询示例](naive-bayes-model-query-examples.md)|  
|神经网络模型|[神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[神经网络模型查询示例](neural-network-model-query-examples.md)|  
|顺序分析和聚类分析|[顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-sequence-clustering-models.md)|[顺序分析和聚类分析模型查询示例](sequence-clustering-model-query-examples.md)|  
|时序模型|[时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[时序模型查询示例](time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> 查看挖掘模型内容的工具  
 当在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中浏览模型时，可以使用 **Microsoft 一般内容树查看器**查看信息， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中均提供了此查看器。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容查看器通过使用挖掘模型内容架构行集中可用的同一信息，来显示模型中的列、规则、属性 (property)、属性 (attribute)、节点以及其他内容。 内容架构行集是用于呈现数据挖掘模型内容详细信息的通用框架。 您可以在任何支持分层行集的客户端中查看模型内容。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的此查看器在 HTML 表查看器中呈现这些信息，这些信息将以一致的格式表示所有模型，使得您所创建模型的结构更易于理解。 有关详细信息，请参阅 [使用 Microsoft 一般内容树查看器浏览模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
##  <a name="bkmk_Querying"></a> 查询挖掘模型内容的工具  
 若要检索挖掘模型内容，您必须针对数据挖掘模型创建一个查询。  
  
 创建内容查询的最简便方法就是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中执行以下 DMX 语句：  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 有关详细信息，请参阅 [数据挖掘查询](data-mining-queries.md)。  
  
 还可以通过使用数据挖掘架构行集来查询挖掘模型内容。 架构行集是标准的架构，客户端可以用来发现、浏览和查询有关挖掘结构和模型的信息。 您可以通过使用 XMLA、Transact-SQL 或 DMX 语句来查询架构行集。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您还可以通过启动与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的连接并查询系统表来访问数据挖掘架构行集中的信息。 有关详细信息，请参阅[查询数据挖掘架构行集&#40;Analysis Services-数据挖掘&#41;](data-mining-schema-rowsets-ssas.md)。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 一般内容树查看器（数据挖掘）](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
