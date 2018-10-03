---
title: 聚类分析模型查询示例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b716b3854ec2fbf931facf3aa224a04055e9f73e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087487"
---
# <a name="clustering-model-query-examples"></a>聚类分析模型查询示例
  依据数据挖掘模型创建查询时，可以检索有关模型的元数据，或者创建内容查询以提供有关分析时发现的模式的详细信息。 或者，可以创建预测查询，以使用模型中的模式来对新数据进行预测。 每一类查询都提供不同的信息。 例如，内容查询可能提供有关发现的分类的更多详细信息，而预测查询可能指出新数据点最有可能属于哪个分类。  
  
 本节说明如何为基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法的模型创建查询。  
  
 **内容查询**  
  
 [使用 DMX 获取模型元数据](#bkmk_Query1)  
  
 [从架构行集中检索模型元数据](#bkmk_Query2)  
  
 [返回分类或分类列表](#bkmk_Query3)  
  
 [返回分类的属性](#bkmk_Query4)  
  
 [使用系统存储过程返回分类配置文件](#bkmk_Query5)  
  
 [查找分类的对比因子](#bkmk_Query6)  
  
 [返回属于分类的事例](#bkmk_Query7)  
  
 **预测查询**  
  
 [从聚类分析模型中预测结果](#bkmk_Query8)  
  
 [确定分类成员身份](#bkmk_Query9)  
  
 [返回具有概率和距离的所有可能分类](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a> 查找有关模型的信息  
 所有挖掘模型都公开算法根据标准化架构（即挖掘模型架构行集）学习的内容。 可以使用数据挖掘扩展插件 (DMX) 语句来针对挖掘模型架构行集创建查询。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，还可以直接将架构行集作为系统表来查询。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用 DMX 获取模型元数据  
 下面的查询返回您在基本数据挖掘教程中创建的聚类分析模型 `TM_Clustering`的基本元数据。 聚类分析模型的父节点中可用的元数据包括模型的名称、存储模型的数据库以及模型中的子节点数目。 此查询使用 DMX 内容查询从模型的父节点中检索元数据：  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  必须将列名 CHILDREN_CARDINALITY 括在括号中，以便将它与同名的多维表达式 (MDX) 保留关键字区分开来。  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Cluster Model|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|All|  
  
 有关这些列在聚类分析模型中的含义的定义，请参阅[聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-clustering-models-analysis-services-data-mining.md)。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：从架构行集中检索模型元数据  
 通过查询数据挖掘架构行集，可以找到在 DMX 内容查询中返回的相同信息。 但是，架构行集还提供一些额外的列。 这包括创建模型时使用的参数、上次处理模型的日期和时间以及模型的所有者。  
  
 下面的示例返回创建、修改和上次处理模型的日期，以及用于生成模型的聚类分析参数和定型集的大小。 这些信息对于模型的归档或者确定使用了哪些聚类分析选项来创建现有模型很有用。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [返回页首](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>查找有关分类的信息  
 聚类分析模型中最有用的内容查询通常返回与使用 **“分类查看器”** 可浏览的信息同类的信息。 这包括分类配置文件、分类特征以及分类对比。 本节提供检索这些信息的查询示例。  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：返回分类或分类列表  
 因为所有分类的节点类型都为 5，所以通过仅仅查询该类型的节点的模型内容可轻松地检索分类的列表。 您还可以筛选按概率或支持所返回的节点，如下例所示。  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 示例结果：  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Cluster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 定义分类的属性可以在数据挖掘架构行集中的两列找到。  
  
-   NODE_DESCRIPTION 列包含逗号分隔的属性列表。 请注意，为便于显示，可能对属性列表进行了缩略。  
  
-   NODE_DISTRIBUTION 列中的嵌套表包含分类的属性的完整列表。 如果您的客户端不支持分层行集，可以通过在 SELECT 列列表前添加 FLATTENED 关键字来返回嵌套表。 有关 FLATTENED 关键字的使用的详细信息，请参阅 [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx)。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：返回分类的属性  
 对于每个分类， **“分类查看器”** 都显示列出属性及其值的配置文件。 此查看器还显示一个直方图，以显示当模型中完全填充了事例时值的分布。 如果您是在查看器中浏览模型，则可以轻松地将直方图从挖掘图例复制并粘贴到 Excel 或 Word 文档。 您还可以使用查看器的“分类特征”窗格以图形方式比较不同分类的属性。  
  
 但是，如果您必须一次获取多个分类的值，则查询模型更容易。 例如，浏览模型时，您可能注意到最上面的两个分类在属性 `Number Cars Owned`上存在不同。 因此，您需要提取每个分类的值。  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 代码的第一行指定您只需要最上面的两个分类。  
  
> [!NOTE]  
>  默认情况下，分类按支持排序。 因此，NODE_SUPPORT 列可以忽略。  
  
 代码的第二行添加仅仅从嵌套表列返回某些列的嵌套 Select 语句。 此外，它将嵌套表中的行限定为与目标属性 `Number Cars Owned`有关的那些行。 为了简化显示，使用嵌套表的别名。  
  
> [!NOTE]  
>  嵌套表列 `PROBABILITY`必须括在括号中，因为它也是保留的 MDX 关键字的名称。  
>   
>  示例结果：  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> 示例查询 5：使用系统存储过程返回分类配置文件  
 作为一种快捷方式，您还可以调用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用来处理分类的系统存储过程，而不是使用 DMX 编写自己的查询。 下面的示例说明如何使用内部存储过程来返回 ID 为 002 的分类的配置文件。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 同样，可以使用系统存储过程来返回特定分类的特征，如下面的示例所示：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 示例结果：  
  
|属性|值|频率|支持|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|地区|North America|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  数据挖掘系统存储过程仅供内部使用， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 保留根据需要更改它们的权利。 如果用于生产，建议您使用 DMX、AMO 或 XMLA 来创建查询。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a> 示例查询 6：查找分类的对比因子  
 使用**分类查看器**的“分类对比”选项卡，可以轻松地将一个分类与另一个分类进行比较，或者将一个分类与其余所有事例（分类的补充）进行比较。  
  
 但是，创建查询来返回这些信息很复杂，您可能需要在客户端上进行一些额外的处理来存储临时结果并比较两个或更多查询的结果。 作为一种快捷方式，可以使用系统存储过程。  
  
 下面的查询返回一个表，该表指示节点 ID 分别为 009 和 007 的两个分类之间的主对比因子。 具有正值的属性有利于分类 009，而具有负值的属性则有利于分类 007。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 示例结果：  
  
|属性|值|分数|  
|----------------|------------|-----------|  
|地区|North America|100|  
|English Occupation|技术工人|94.9003803898654|  
|地区|Europe|-72.5041051379789|  
|English Occupation|Manual|-69.6503163202722|  
  
 这与当你从第一个下拉列表中选择分类 9，从第二个下拉列表中选择分类 7 时， **分类对比** 查看器的图中所显示的信息相同。 若要将分类 9 与其补数进行比较，应在第二个参数中使用空字符串，如下面的示例所示：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  数据挖掘系统存储过程仅供内部使用， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 保留根据需要更改它们的权利。 如果用于生产，建议您使用 DMX、AMO 或 XMLA 来创建查询。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> 示例查询 7：返回属于分类的事例  
 如果对挖掘模型启用了钻取，则可以创建查询来返回有关在模型中使用的事例的详细信息。 此外，如果对挖掘结构启用了钻取，则可以通过使用 [StructureColumn （DMX）](/sql/dmx/structurecolumn-dmx) 函数来包括基础结构中的列。  
  
 下面的示例返回模型中使用的两列 Age 和 Region，以及模型中未使用的一列 First Name。 此查询仅仅返回归为分类 1 的事例。  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 若要返回属于某个分类的事例，必须知道该分类的 ID。 可以通过在某个查看器中浏览模型来获取分类的 ID。 或者，为便于引用，可以重命名分类，之后，即可使用名称来代替 ID 号。 但要注意的是，在重新处理模型后，您分配给分类的名称将会丢失。  
  
 [返回页首](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>使用模型进行预测  
 尽管聚类分析通常用于描述和了解数据，但是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 实现使您还可以对分类成员身份进行预测，并返回与预测关联的概率。 本节提供关于如何在聚类分析模型上创建预测查询的示例。 您可以通过指定表格格式数据源来针对多个事例进行预测，或者可以通过创建单独查询来一次提供一个新的值。 为清楚起见，本节中的示例均为单独查询。  
  
 有关如何使用 DMX 创建预测查询的详细信息，请参阅[数据挖掘查询接口](data-mining-query-tools.md)。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a> 示例查询 8：从聚类分析模型中预测结果  
 如果您创建的聚类分析模型包含可预测的属性，则可以使用该模型来对结果进行预测。 但是，模型处理可预测属性以不同的方式根据是否将可预测列设置为`Predict`或`PredictOnly`。 如果设置为列的用法`Predict`，该属性的值添加到聚类分析模型，并在完成的模型中显示为属性。 但是，如果将列的用法设置为 `PredictOnly`，则值不会用于创建分类。 相反，模型完成后，聚类分析算法创建的新值`PredictOnly`属性基于每个事例所属的分类。  
  
 下面的查询向模型提供一个新事例，在该模型中，有关该事例的唯一信息是年龄和性别。 SELECT 语句指定你关注的可预测属性/值对，而 [PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx) 函数则指出具有这些属性的事例具有目标结果的概率。  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 用法设置为时的结果示例`Predict`:  
  
|Bike Buyer|表达式|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 用法设置为 `PredictOnly` 且模型重新处理时的结果示例：  
  
|Bike Buyer|表达式|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 在本示例中，模型中的区别不是很明显。 但是，有时可能必须检测出值的实际分布与模型所预测的情况之间的区别。 在这种情况下 [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 函数很有用，因为它可指出事例适用于模型的可能性。  
  
 PredictCaseLikelihood 函数返回的数是概率，因此总是在 0 和 1 之间，值 .5 表示随机结果。 因此，小于 .5 的分数意味着预测的事例不太可能适用于此模型，而大于 .5 的分数则意味着预测的事例适用于模型的可能性比不适用于模型的可能性大。  
  
 例如，下面的查询返回两个值，这两个值指出新示例事例的可能性。 非规范化值表示适用于当前模型的概率。 使用 NORMALIZED 关键字时，此函数返回的可能性分数是用“有模型的概率”除以“没有模型的概率”来得到的。  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 示例结果：  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8.65459953145182E-68|  
  
 请注意这些结果中的数是用科学记数法来表示的。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a> 示例查询 9：确定分类成员身份  
 本示例使用 [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) 函数来返回新事例最有可能属于的分类，并使用 [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx) 函数来返回该分类中的成员身份的概率。  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 示例结果：  
  
|$CLUSTER|表达式|  
|--------------|----------------|  
|Cluster 2|0.397918596951617|  
  
 **请注意**默认情况下，`ClusterProbability`函数将返回最可能分类的概率。 但是，您可以通过使用语法 `ClusterProbability('cluster name')`来指定另一分类。 如果这样做，请注意每个预测函数的结果都独立于其他结果。 因此，第二列中的概率分数可能引用另一个分类，而不是第一列中所指定的分类。  
  
 [返回页首](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a> 示例查询 10：返回具有概率和距离的所有可能分类  
 在上一个示例中，概率分数不是非常高。 若要确定是否存在更好的分类，可以将 [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) 函数与 [Cluster &#40;DMX&#41;](/sql/dmx/cluster-dmx) 函数一起使用，以返回包括所有可能的分类以及新事例属于每个分类的概率的嵌套表。 FLATTENED 关键字用于将分层行集改为平面表，以便于查看。  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Cluster 2|0.602081403048383|0.397918596951617|  
|分类 10|0.719691686785675|0.280308313214325|  
|分类 4|0.867772590378791|0.132227409621209|  
|分类 5|0.931039872200985|0.0689601277990149|  
|分类 3|0.942359230072167|0.0576407699278328|  
|分类 6|0.958973668972756|0.0410263310272437|  
|分类 7|0.979081275926724|0.0209187240732763|  
|分类 1|0.999169044818624|0.000830955181376364|  
|分类 9|0.999831227795894|0.000168772204105754|  
|分类 8|1|0|  
  
 默认情况下，结果按概率进行排序。 结果指出，尽管分类 2 的概率非常低，分类 2 仍然最适合于新数据点。  
  
 **注意** 额外的一列 `$DISTANCE`表示从数据点到分类的距离。 默认情况下， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法使用可缩放的 EM 聚类分析，此类分析为每个数据点分配多个分类，并对可能的分类进行排序。  但是，如果您使用 K-means 算法来创建聚类分析模型，则只能为每个数据点分配一个分类，并且此查询仅仅返回一行。 了解这些区别对于解释 [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 函数来包括基础结构中的列。 有关 EM 与 K-means 聚类分析之间的区别的详细信息，请参阅 [Microsoft 聚类分析算法技术参考](microsoft-clustering-algorithm-technical-reference.md)。  
  
 [返回页首](#bkmk_top2)  
  
## <a name="function-list"></a>函数列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 不过，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法生成的模型还支持下表中列出的其他函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[群集&#40;DMX&#41;](/sql/dmx/cluster-dmx)|返回最可能包含输入事例的分类。|  
|[ClusterDistance &#40;DMX&#41;](/sql/dmx/clusterdistance-dmx)|返回输入事例与指定分类之间的距离；如果未指定分类，则返回输入事例与可能性最大的分类之间的距离。<br /><br /> 返回输入事例属于指定分类的概率。|  
|[ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx)|返回输入事例属于指定分类的概率。|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|确定一个节点是否是模型中另一个节点的子节点。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指示指定的节点是否包含当前事例。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|返回加权的概率。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|预测关联数据集中的成员身份。|  
|[PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx)|返回输入事例适合现有模型的可能性。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|返回与当前预测值相关的值的表。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|返回每个事例的 Node_ID。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|返回预测值的概率。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|返回指定列的预测标准偏差。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|返回指定状态的支持值。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|返回指定列的方差。|  
  
 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询](data-mining-queries.md)   
 [Microsoft 聚类分析算法技术参考](microsoft-clustering-algorithm-technical-reference.md)   
 [Microsoft 聚类分析算法](microsoft-clustering-algorithm.md)  
  
  
