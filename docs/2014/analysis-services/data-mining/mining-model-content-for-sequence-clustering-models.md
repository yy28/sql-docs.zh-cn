---
title: 序列聚类分析模型的挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, sequence clustering models
- sequence clustering algorithms [Analysis Services]
ms.assetid: 68e1934a-e147-4d53-b122-fa15e3fd5485
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12aad369e9a8614041bccaa08ee507d723c6c51f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083567"
---
# <a name="mining-model-content-for-sequence-clustering-models-analysis-services---data-mining"></a>顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）
  本主题介绍使用 Microsoft 顺序分析和聚类分析算法的模型特有的挖掘模型内容。 有关与适用于所有模型类型的挖掘模型内容相关的常规术语和统计术语的说明，请参阅[挖掘模型内容 （Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-sequence-clustering-model"></a>了解顺序分析和聚类分析模型的结构  
 顺序分析和聚类分析模型具有表示该模型及其元数据的单一父节点 (NODE_TYPE = 1)。 标记为“(全部)”的父节点具有相关的序列节点 (NODE_TYPE = 13)，用于列出在定型数据中检测到的所有转换。  
  
 ![序列聚类分析模型的结构](../media/modelcontent-seqclust.gif "序列聚类分析模型的结构")  
  
 根据在数据中找到的转换以及在创建模型时包括的任何其他输入属性（例如客户人口统计信息等），该算法还会创建大量分类。 每个分类 (NODE_TYPE = 5) 都包含其自己的序列节点 (NODE_TYPE = 13)，用于仅列出在生成该特定分类时所使用的转换。 通过序列节点，您可以深化以查看各状态转换 (NODE_TYPE = 14) 的详细信息。  
  
 有关序列和状态转换的说明和示例，请参阅 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)。  
  
## <a name="model-content-for-a-sequence-clustering-model"></a>顺序分析和聚类分析模型的模型内容  
 本节提供挖掘模型内容中与顺序分析和聚类分析有特殊关系的列的其他信息。  
  
 MODEL_CATALOG  
 存储模型的数据库的名称。  
  
 MODEL_NAME  
 模型的名称。  
  
 ATTRIBUTE_NAME  
 始终为空白。  
  
 NODE_NAME  
 节点的名称。 当前包含的值与 NODE_UNIQUE_NAME 列相同。  
  
 NODE_UNIQUE_NAME  
 节点的唯一名称。  
  
 NODE_TYPE  
 顺序分析和聚类分析模型输出以下节点类型：  
  
|节点类型 ID|Description|  
|------------------|-----------------|  
|1（模型）|模型的根节点|  
|5（分类）|包含分类中的转换计数、属性列表以及描述分类中的值的统计信息。|  
|13（序列）|包含分类中包含的转换列表。|  
|14（转换）|以表的形式说明事件的序列，该表的第一行包含起始状态，所有其他行包含后续状态以及支持和概率统计信息。|  
  
 NODE_GUID  
 空白。  
  
 NODE_CAPTION  
 与节点关联的标签或标题，用于显示目的。  
  
 使用模型时可以重命名分类标题；但是，如果关闭该模型，则不会保存新名称。  
  
 CHILDREN_CARDINALITY  
 对节点所具有的子节点数的估计。  
  
 **模型根** 基数值等于分类数加 1。 有关详细信息，请参阅 [基数](#bkmk_cardinality)。  
  
 **群集节点** 基数始终为 1，因为每个分类只有一个包含该分类中的序列列表的子节点。  
  
 **序列节点** 基数指示该分类中包含的转换数。 例如，模型根的序列节点的基数指出在整个模型中找到的转换数。  
  
 PARENT_UNIQUE_NAME  
 节点的父节点的唯一名称。  
  
 根级别上的任何节点均返回 NULL。  
  
 NODE_DESCRIPTION  
 与节点标题相同。  
  
 NODE_RULE  
 始终为空白。  
  
 MARGINAL_RULE  
 始终为空白。  
  
 NODE_PROBABILITY  
 **模型根** 始终为 0。  
  
 **群集节点** 模型中调整后的分类概率。 调整后的概率总和不等于 1，因为在顺序分析和聚类分析中使用的聚类分析方法允许在多个分类中使用部分成员身份。  
  
 **序列节点** 始终为 0。  
  
 **转换节点** 始终为 0。  
  
 MARGINAL_PROBABILITY  
 **模型根** 始终为 0。  
  
 **群集节点** 其值与 NODE_PROBABILITY 的值相同。  
  
 **序列节点** 始终为 0。  
  
 **转换节点** 始终为 0。  
  
 NODE_DISTRIBUTION  
 包含概率和其他信息的表。 有关详细信息，请参阅 [NODE_DISTRIBUTION 表](#bkmk_NODEDIST)。  
  
 NODE_SUPPORT  
 支持该节点的转换的数目。 因此，如果定型数据中有 30 个“产品 A 后跟产品 B”序列示例，则支持总数为 30。  
  
 **模型根** 模型中的转换的总数。  
  
 **群集节点** 对分类的原始支持，表示向该分类提供事例的定型事例的数目。  
  
 **序列节点** 始终为 0。  
  
 **转换节点** 分类中表示某一特定转换的事例的百分比。 它可以为 0，也可以为正值。 其计算方法是用群集节点的原始支持乘以该分类的概率。  
  
 通过此值，您可以知道向转换提供了多少个定型事例。  
  
 MSOLAP_MODEL_COLUMN  
 不适用。  
  
 MSOLAP_NODE_SCORE  
 不适用。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 与 NODE_DESCRIPTION 相同。  
  
## <a name="understanding-sequences-states-and-transitions"></a>了解序列、状态和转换  
 顺序分析和聚类分析模型具有一个唯一的结构，用于组合以下两种具有完全不同的信息类型的对象：其中一种是分类，另一种是状态转换。  
  
 顺序分析和聚类分析算法创建的分类与 Microsoft 聚类分析算法创建的分类类似。 每个分类都具有一个配置文件和相应特征。 但是，在顺序分析和聚类分析算法中，每个分类还另外包括一个列出该分类中的序列的子节点。 每个序列节点包含多个说明状态转换详细信息以及概率的子节点。  
  
 模型中的序列数几乎始终多于在任何单个事例中找到的序列数，这是因为序列可以链接在一起。 Microsoft Analysis Services 将指针从一种状态存储到另一种状态，以便计算每个转换的出现次数。 此外，您还可以查找序列的出现次数的相关信息，并度量该序列相较于整个被观察状态集的出现概率。  
  
 下表概述如何在模型中存储信息以及如何将节点关联起来。  
  
|节点|具有的子节点|NODE_DISTRIBUTION 表|  
|----------|--------------------|------------------------------|  
|模型根|多个群集节点<br /><br /> 具有整个模型的序列的节点|列出模型中的所有产品以及支持和概率。<br /><br /> 由于聚类分析方法允许在多个分类中使用部分成员身份，因此支持和概率的值可以为小数。 也就是说，每个事例可以潜在属于多个分类，而不会一次记为一个事例。 因此，在确定最终分类成员身份后，该值可通过该分类的概率进行调整。|  
|模型的序列节点|多个转换节点|列出模型中的所有产品以及支持和概率。<br /><br /> 由于已知模型的序列数，因此在该级别中，很容易计算支持和概率：<br /><br /> 支持 = 事例计数<br /><br /> 概率 = 模型中每个序列的原始概率。 所有概率的总和应为 1。|  
|单个的群集节点|仅具有该分类的序列的节点|列出分类中的所有产品，但仅提供作为分类特征的产品的支持和概率值。<br /><br /> 支持表示该分类中每个事例的调整后的支持值。 概率值是调整后的概率。|  
|各分类的序列节点|仅具有该分类中的序列的转换的多个节点|其信息与单个的群集节点中的信息完全相同。|  
|转换|无子节点|列出第一个相关状态的转换。<br /><br /> 支持是调整后的支持值，指示参与每个转换的事例。 概率是调整后的概率，以百分比表示。|  
  
###  <a name="bkmk_NODEDIST"></a> NODE_DISTRIBUTION 表  
 NODE_DISTRIBUTION 表提供特定分类的转换和序列的概率和支持详细信息。  
  
 将始终向转换表添加一行，表示可能的 `Missing` 值。 有关内容信息`Missing`值的含义以及它如何影响计算，请参阅[缺失值&#40;Analysis Services-数据挖掘&#41;](missing-values-analysis-services-data-mining.md)。  
  
 支持和概率的计算各不相同，这取决于计算是应用于定型事例还是完成的模型。 其原因在于默认聚类分析方法 Expectation Maximization (EM) 假定任何事例均可以属于多个分类。 计算模型中事例的支持时，可以使用原始计数和原始概率。 但是，分类中任何特定序列的概率必须通过所有可能的序列和分类组合之和进行权衡。  
  
###  <a name="bkmk_cardinality"></a> 基数  
 在聚类分析模型中，父节点的基数通常将告诉您该模型中具有多少个分类。 但是，顺序分析和聚类分析模型具有两种分类级别节点：其中一种节点包含分类，而另一种节点包含整个模型的序列列表。  
  
 因此，若要得出模型中的分类数，可以用（全部）节点的 NODE_CARDINALITY 值减 1。 例如，如果模型创建了 9 个分类，则模型根的基数为 10。 这是因为该模型包含 9 个群集节点，每个都具有其自己的序列节点，加上一个额外的标记为分类 10 的序列节点，该节点表示模型的序列。  
  
## <a name="walkthrough-of-structure"></a>结构演练  
 使用示例可以阐明如何存储信息以及如何解释信息。 例如，通过使用以下查询，您可以在基础 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 数据中查找最大订单，即被观察链最长的订单：  
  
```  
USE AdventureWorksDW2012  
SELECT DISTINCT OrderNumber, Count(*)  
FROM vAssocSeqLineItems  
GROUP BY OrderNumber  
ORDER BY Count(*) DESC  
```  
  
 通过这些结果，您可以发现订单号“SO72656”、“SO58845”和“SO70714”包含的序列最大，每个序列各包含 8 个产品。 利用订单 ID 可以查看特定订单的详细信息，以便了解购买了哪些产品及其购买顺序。  
  
|OrderNumber|LineNumber|“模型”|  
|-----------------|----------------|-----------|  
|SO58845|1|Mountain-500|  
|SO58845|2|LL Mountain Tire|  
|SO58845|3|Mountain Tire Tube|  
|SO58845|4|Fender Set - Mountain|  
|SO58845|5|Mountain Bottle Cage|  
|SO58845|6|Water Bottle|  
|SO58845|7|Sport-100|  
|SO58845|8|Long-Sleeve Logo Jersey|  
  
 但是，购买 Mountain-500 的某些客户可能会购买其他产品。 通过查看模型中的序列列表，可以查看在 Mountain-500 之后购买的所有产品。 以下过程将引导您使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中提供的两个查看器查看这些序列：  
  
#### <a name="to-view-related-sequences-by-using-the-sequence-clustering-viewer"></a>使用顺序分析和聚类分析查看器查看相关序列  
  
1.  在对象资源管理器中，右键单击 [Sequence Clustering] 模型，再选择“浏览”。  
  
2.  在顺序分析和聚类分析查看器中，单击 **“状态转换”** 选项卡。  
  
3.  在“分类”下拉列表中，确保选中“总体(全部)”。  
  
4.  将窗格左侧的滑动条一直移动到顶部，以显示所有链接。  
  
5.  在关系图中，找到 **Mountain-500**并单击此关系图中的节点。  
  
6.  突出显示的线条指向下一状态（在 Mountain-500 后购买的产品），而数字则指示概率。 请将其与一般模型内容查看器中的结果比较。  
  
#### <a name="to-view-related-sequences-by-using-the-generic-model-content-viewer"></a>使用一般模型内容查看器查看相关序列  
  
1.  在对象资源管理器中，右键单击 [Sequence Clustering] 模型，再选择“浏览”。  
  
2.  在查看器下拉列表中，选择 **Microsoft 一般内容树查看器**。  
  
3.  在 **“节点标题”** 窗格中，单击名为 **“分类 16 的序列级别”** 的节点。  
  
4.  在“节点详细信息”窗格中，找到 NODE_DISTRIBUTION 行，并单击嵌套表中的任意位置。  
  
     顶部的行始终用于缺少值。 该行为序列状态 0。  
  
5.  按向下键或者使用滚动条在嵌套表中向下移动，直到看到 Mountain-500 行为止。  
  
     该行为序列状态 20。  
  
    > [!NOTE]  
    >  您可以通过编程方式获取特定序列状态的行号，但是如果您只是为了浏览，最简单的方法是将嵌套表复制到 Excel 工作簿中。  
  
6.  返回到“节点标题”窗格，展开 **“分类 16 的序列级别”** 节点（如果尚未展开）。  
  
7.  在其子节点中查找 **“序列状态 20 的转换行”**。 单击该转换节点。  
  
8.  NODE_DISTRIBUTION 嵌套表包含下列产品和概率。 请将其与顺序分析和聚类分析查看器的 **“状态转换”** 选项卡中的结果进行比较。  
  
 下表显示了 NODE_DISTRIBUTION 表的结果以及图形查看器中所显示的舍入概率值。  
  
|产品|支持（NODE_DISTRIBUTION 表）|概率（NODE_DISTRIBUTION 表）|概率（源自图形）|  
|-------------|------------------------------------------|------------------------------------------------|--------------------------------|  
|Missing|48.447887|0.138028169|（未显示）|  
|Cycling Cap|10.876056|0.030985915|0.03|  
|Fender Set - Mountain|80.087324|0.228169014|0.23|  
|Half-Finger Gloves|0.9887324|0.002816901|0.00|  
|Hydration Pack|0.9887324|0.002816901|0.00|  
|LL Mountain Tire|51.414085|0.146478873|0.15|  
|Long-Sleeve Logo Jersey|2.9661972|0.008450704|0.01|  
|Mountain Bottle Cage|87.997183|0.250704225|0.25|  
|Mountain Tire Tube|16.808451|0.047887324|0.05|  
|Short-Sleeve Classic Jersey|10.876056|0.030985915|0.03|  
|Sport-100|20.76338|0.05915493|0.06|  
|Water Bottle|18.785915|0.053521127|0.25|  
  
 对于我们最初从定型数据中选择的事例，尽管其包含的“Mountain-500”产品后面紧跟着“LL Mountain Tire”，但是您可以发现这两种产品之间还有很多其他可能的序列。 若要查找任何特定分类的详细信息，必须重复从分类的序列列表深化到每种状态或产品的实际转换的过程。  
  
 您可以从一个特定分类中列出的序列跳至转换行中。 通过该转换行，可以确定下一个产品，并跳回到序列列表中的该产品。 通过对第一种和第二种状态的每种状态重复此过程，您可以处理较长的状态链。  
  
## <a name="using-sequence-information"></a>使用序列信息  
 顺序分析和聚类分析的一种常见应用场景是跟踪用户在某个网站上的点击。 例如，如果数据源自 Adventure Works 电子商务网站上的客户购买记录，则所生成的顺序分析和聚类分析模型可用于推断用户行为，以便重新设计该电子商务网站，进而解决导航问题或增加销售额。  
  
 例如，分析可能显示用户始终追随某一特定产品链，而不管人口统计信息如何。 此外，您可能还会发现用户在单击某一特定产品后频繁退出该网站。 根据此发现，您可能会问还可以向用户提供哪些其他路径，从而使用户继续访问该网站。  
  
 如果在对用户分类时没有要使用的其他信息，则可以仅使用序列信息收集有关导航的数据，以便更好地理解总体行为。 但是，如果可以收集客户相关信息并将该信息与客户数据库相匹配，则可以对序列组合使用聚类分析和预测功能，以便根据用户需要或可能根据当前页的导航路径提供相应建议。  
  
 顺序分析和聚类分析模型编译的大量状态和转换信息的另一个用途是确定从不使用的可能路径。 例如，如果有很多访问者访问第 1 至 4 页，但访问者从不继续访问第 5 页，您可能会调查是否有任何问题妨碍导航到第 5 页。 您可以通过查询模型内容并将其与可能的路径列表进行比较来实现此目的。  可以通过编程方式或使用多种站点分析工具来创建显示网站中所有导航路径的图形。  
  
 若要了解如何通过查询模型内容来获取被观察路径的列表，并查看针对顺序分析和聚类分析模型的其他查询示例，请参阅 [顺序分析和聚类分析模型查询示例](clustering-model-query-examples.md)。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)   
 [顺序分析和聚类分析模型查询示例](clustering-model-query-examples.md)  
  
  
