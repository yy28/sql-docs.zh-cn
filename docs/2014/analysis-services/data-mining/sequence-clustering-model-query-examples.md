---
title: 序列聚类分析模型查询示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8f5776d2a7523f4d56bb48926a8f0bf0929e87f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118117"
---
# <a name="sequence-clustering-model-query-examples"></a>顺序分析和聚类分析模型查询示例
  在对数据挖掘模型创建查询时，可以创建内容查询，也可以创建预测查询。内容查询提供有关模型中存储的信息的详细信息，预测查询使用模型中的模式并基于您提供的新数据进行预测。 对于顺序分析和聚类分析模型，内容查询通常会提供所发现的分类的更多详细信息，或这些分类中的转换。 您还可以使用查询来检索有关模型的元数据。  
  
 针对顺序分析和聚类分析模型的预测查询通常是基于序列和转换、基于模型中包含的非序列属性或基于序列属性和非序列属性的组合来提出建议。  
  
 本节说明如何为基于 Microsoft 顺序分析和聚类分析算法的模型创建查询。 有关创建查询的常规信息，请参阅 [数据挖掘查询](data-mining-queries.md)。  
  
 **内容查询**  
  
 [使用数据挖掘架构行集返回模型参数](#bkmk_Query1)  
  
 [获取某种状态的序列列表](#bkmk_Query2)  
  
 [使用系统存储过程](#bkmk_Query3)  
  
 **预测查询**  
  
 [预测后面的一种或多种状态](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> 查找有关顺序分析和聚类分析模型的信息  
 若要对挖掘模型的内容创建有意义的查询，您必须了解模型内容的结构以及哪些节点类型存储哪类信息。 有关详细信息，请参阅[顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-sequence-clustering-models.md)。  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用数据挖掘架构行集返回模型参数  
 通过查询数据挖掘架构行集，您可以找到关于模型的各类信息，包括基本元数据、模型的创建日期和时间、上次处理模型的日期和时间、模型所基于的挖掘结构的名称以及用作可预测属性的列。  
  
 下面的查询返回用于生成模型 `[Sequence Clustering]`和为其定型的参数。 您可以在 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)的第 5 课中创建此模型。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 示例结果：  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 请注意，此模型是使用默认值为 10 的 CLUSTER_COUNT 创建的。 当您为 CLUSTER_COUNT 指定的分类数不为零时，算法会将此数视为要查找的大致分类数。 但是，在分析的过程中，算法可能会找到多于或少于指定数的分类。 在本例中，算法发现 15 个分类与定型数据拟合最好。 因此，已完成模型的参数值列表将报告由算法确定的分类数，而不是创建模型时传入的值。  
  
 此行为与让算法确定最佳分类数有何不同呢？ 您可以试验一下，创建另一个使用相同数据的聚类分析模型，但将 CLUSTER_COUNT 设置为 0。 这样做的结果是，算法将检测到 32 个分类。 因此，CLUSTER_COUNT 的默认值使用 10 可以限制结果的数目。  
  
 默认值使用 10 是因为减少分类数更便于大多数人浏览并了解数据中的分组。 但是，每个模型和数据集是不同的。 您可以试用不同的分类数，从而发现哪个参数值能产生最精确的模型。  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：获取某种状态的序列列表  
 挖掘模型内容存储在定型数据中找到的序列，序列由第一种状态与所有相关第二种状态的列表组成。 第一种状态用作该序列的标签，相关的第二种状态称为转换。  
  
 例如，在序列分组到各分类中之前，下面的查询返回模型中第一种状态的完整列表。  获取此列表的方法是返回将模型根节点作为父节点 (PARENT_UNIQUE_NAME = 0) 的序列 (NODE_TYPE = 13) 的列表。 FLATTENED 关键字可使结果更易读。  
  
> [!NOTE]  
>  列的名称、PARENT_UNIQUE_NAME、Support 和 Probability 必须括在方括号内，以便将它们与同名的保留关键字区分开来。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 部分结果：  
  
|NODE_UNIQUE_NAME|Product 1|Sequence Support|Sequence Probability|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|（第 4-36 行省略）|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 模型中的序列列表始终按字母升序排序。 序列的排序非常重要，因为您可以通过查看序列的序号来查找相关转换。 `Missing`值始终为转换 0。  
  
 例如，在上面的结果中，产品“Women's Mountain Shorts”在模型中的序列号为 37。 您可以使用该信息来查看在购买“Women's Mountain Shorts”之后购买的所有产品。  
  
 为此，首先需要引用从上述查询中返回的 NODE_UNIQUE_NAME 值，以获取包含该模型所有序列的节点的 ID。 将此值作为父节点的 ID 传递给查询，这样将仅获取此节点中包含的转换，而此节点恰好包含该模型所有序列的列表。 但是，如果您希望查看特定分类的转换列表，则可传入群集节点的 ID，从而仅查看与该分类关联的序列。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 示例结果：  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 此 ID 表示的节点包含购买“Women's Mountain Shorts”产品之后的序列列表以及支持和概率值。  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 示例结果：  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|缺少|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 请注意，与 Women's Mountain Shorts 相关的各序列的支持在模型中为 506。 转换的支持值总计也为 506。 但是，这些支持数不是整数，如果您认为支持仅表示包含每个转换的事例计数，这似乎有些奇怪。 但是，由于用于创建分类的方法计算部分成员身份，因此某个分类中任一转换的概率必须由该转换属于该特定分类的概率来衡量。  
  
 例如，如果有 4 个分类，则特定序列可能有 40% 的几率属于分类 1、30% 的几率属于分类 2、20% 的几率属于分类 3 以及 10% 的几率属于分类 4。 在算法确定转换最有可能属于的分类后，它使用分类先验概率来衡量转换在该分类中的概率。  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：使用系统存储过程  
 从这些查询示例中，可以看到模型中存储的信息很复杂，您可能需要创建多个查询才能获取所需的信息。 不过，Microsoft 顺序分析和聚类分析查看器提供了一组功能强大的工具，可用于以图形方式浏览顺序分析和聚类分析模型中包含的信息，您还可以使用该查看器来查询和深化模型。  
  
 在大多数情况下，Microsoft 顺序分析和聚类分析查看器中显示的信息是使用 Analysis Services 系统存储过程来查询模型而创建的。 您也可以编写针对模型内容的数据挖掘扩展插件 (DMX) 查询来检索同一信息，但是对于浏览或测试模型，使用 Analysis Services 系统存储过程非常简便快捷。  
  
> [!NOTE]  
>  系统存储过程是 Microsoft 提供的与 Analysis Services 服务器进行交互的工具，可供服务器和客户端进行内部处理。 因此，Microsoft 保留随时更改它们的权利。 虽然为方便起见在此处介绍了系统存储过程，但不建议在生产环境中使用它们。 为了确保生产环境中的稳定性和兼容性，您应始终使用 DMX 编写您自己的查询。  
  
 本节提供了如何使用系统存储过程来创建针对顺序分析和聚类分析模型的查询的一些示例：  
  
#### <a name="cluster-profiles-and-sample-cases"></a>分类剖面图和样本事例  
 “分类剖面图”选项卡显示了一个列表，列出模型中的分类、每个分类的大小以及指示该分类中包含的状态的直方图。 您可在查询中使用两个系统存储过程来检索类似信息：  
  
-   `GetClusterProfile` 返回分类的特征以及在分类的 NODE_DISTRIBUTION 表中找到的所有信息。  
  
-   `GetNodeGraph` 返回可用于构造分类的数学图形表示形式的节点和边缘，这与您在“顺序分析和聚类分析”视图的第一个选项卡中所见的相对应。 节点代表分类，边缘代表权重或强度。  
  
 下例演示了如何使用系统存储过程 `GetClusterProfiles`来返回模型中的所有分类及其各自的剖面图。 此存储过程将执行一系列 DMX 语句，它们返回模型中完整的一组剖面图。 但是，若要使用此存储过程，您必须知道模型的地址。  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 下例演示了如何检索特定分类 Cluster 12 的剖面图，方法是使用系统存储过程 `GetNodeGraph`，然后指定分类 ID，该 ID 通常与分类名称中的数字相同。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 如果您如以下查询中所示省略分类 ID，则 `GetNodeGraph` 会返回所有分类剖面图的有序平展列表：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 **“分类剖面图”** 选项卡还显示了模型样本事例的直方图。 这些样本事例代表模型的理想化事例。 这些事例在模型中的存储方式与定型数据不同；您必须使用特殊的语法来检索模型的样本事例。  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 有关详细信息，请参阅 [SELECT FROM <模型>.SAMPLE_CASES (DMX)](/sql/dmx/select-from-model-dmx)。  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>分类特征和分类对比  
 **“分类特征”** 选项卡汇总了每个分类的主属性，按概率进行排序。 您可以查看属于一个分类的事例数，以及该分类中的事例分布情况：每个特征都有一定的支持。 若要查看特定分类的特征，您必须知道该分类的 ID。  
  
 以下示例使用系统存储过程 `GetClusterCharacteristics`返回概率值超过指定阈值 0.0005 的 Cluster 12 的所有特征。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 若要返回所有分类的特征，必须将分类 ID 保留为空。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 下例调用系统存储过程 `GetClusterDiscrimination` 来比较 Cluster 1 和 Cluster 12 的特征。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 如果您要使用 DMX 编写您自己的查询来比较两个分类，或将一个分类与其补进行比较，您必须首先检索一组特征，再检索您感兴趣的特定分类的特征，然后比较这两组特征。 这种情况更为复杂，通常需要某些客户端处理。  
  
#### <a name="states-and-transitions"></a>状态和转换  
 Microsoft 顺序分析和聚类分析的 **“状态转换”** 选项卡会在后端执行复杂的查询以检索并比较不同分类的统计信息。 重新生成这些结果需要更复杂的查询和一些客户端处理。  
  
 但是，可以使用 [内容查询](#bkmk_ContentQueries)部分的示例 2 中介绍的 DMX 查询来检索序列或各个转换的概率和状态。  
  
## <a name="using-the-model-to-make-predictions"></a>使用模型进行预测  
 针对顺序分析和聚类分析模型的预测查询可使用许多适用于其他聚类分析模型的预测函数。 此外，还可以使用特殊预测函数 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)建议或推测下一状态。  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：预测后面的一种或多种状态  
 在给定值的情况下，可以使用 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) 函数来预测下一个最可能的状态。 还可以预测多个下一状态：例如，可以返回客户可能购买的前三种产品，以提供一个建议列表。  
  
 下面的示例查询是一个单独预测查询，它将返回前 5 个预测及其概率。 由于该模型包含一个嵌套表，因此进行预测时必须将嵌套表 `[v Assoc Seq Line Items]`用作列引用。 此外，提供输入值时，必须联接事例表和嵌套表列，如嵌套 SELECT 语句所示。  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 示例结果：  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 尽管您可能仅需要一列，但结果中包含三列，因为查询会始终为事例表返回一列。 此处的结果是平展的；否则，查询将返回包含两个嵌套表列的单个列。  
  
 列 $sequence 是由 `PredictSequence` 函数默认返回的列，以对预测结果进行排序。 对模型中的序列键进行匹配时需要 `[Line Number]`列，但不输出这些序列键。  
  
 有趣的是，购买 All-Purpose Bike Stand 之后的最前面两个预测序列是 Cycling Cap 和 Cycling Cap。 这不是一个错误。 这种序列很可能出现，具体取决于向客户显示数据的方式以及为模型定型时数据的分组方式。 例如，客户可能购买一顶红色的自行车帽，再购买一顶蓝色的自行车帽，在无法指定数量的情况下，就会在一行中出现两次购买自行车帽。  
  
 第 6 行和第 7 行中的值为占位符。 当您到达可能的转换的链末尾，而不是终止预测结果时，作为输入传递的值将添加到结果中。 例如，如果将预测数增加到 20，则第 6 行到第 20 行的值是一样的，全部为 All-Purpose Bike Stand。  
  
## <a name="function-list"></a>函数列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 此外， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法还额外支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[群集&#40;DMX&#41;](/sql/dmx/cluster-dmx)|返回最可能包含输入事例的分类|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|返回输入事例与指定分类之间的距离；如果未指定分类，则返回输入事例与可能性最大的分类之间的距离。<br /><br /> 此函数可用于任何类型的聚类分析模型（EM、K-Means 等），但结果会因算法而异。|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|返回输入事例属于指定分类的概率。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指示指定的节点是否包含当前事例。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|返回指定状态调整后的概率。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|预测关联的成员身份。|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|返回输入事例适合现有模型的可能性。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|返回一个表示给定列预测的直方图的表。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|返回事例所属的节点的 Node_ID。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|返回指定状态的概率。|  
|[PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)|为一组指定的序列数据预测将来的序列值。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|返回指定列的预测标准偏差。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|返回指定状态的支持值。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|返回指定列的方差。|  
  
 有关所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都支持的通用函数的列表，请参阅[通用预测函数 (DMX)](/sql/dmx/general-prediction-functions-dmx)。 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询](data-mining-queries.md)   
 [Microsoft 序列聚类分析算法技术参考](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft 序列聚类分析算法](microsoft-sequence-clustering-algorithm.md)   
 [序列聚类分析模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
