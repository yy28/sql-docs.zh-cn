---
title: "内容查询 （数据挖掘） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4f4a5a8-a230-4222-bece-9d563501f65f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d45986f9907903c6ccdf4d7b1c6bfe5d22eee78
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="content-queries-data-mining"></a>内容查询（数据挖掘）
  内容查询是一种提取有关内部统计信息以及挖掘模型结构信息的一种方式。 有时，内容查询可提供在查看器中不易查看的详细信息。 您还可以使用内容查询的结果以编程方式提取信息以供他用。  
  
 本节提供有关可以使用内容查询检索的信息类型的常规信息，以及用于内容查询的一般 DMX 语法。  
  
 [基本内容查询](#bkmk_ContentQuery)  
  
-   [针对结构和事例数据的查询](#bkmk_Structure)  
  
-   [针对模型模式的查询](#bkmk_Patterns)  
  
 [示例](#bkmk_Examples)  
  
-   [针对关联模型的内容查询](#bkmk_Assoc)  
  
-   [针对决策树模型的内容查询](#bkmk_DecTree)  
  
 [使用查询结果](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> 基本内容查询  
 您可以通过使用预测查询生成器来创建内容查询，使用在 SQL Server Management Studio 中提供的 DMX 内容查询模板，或者直接在 DMX 中撰写查询。 与预测查询不同，您无需联接外部数据，因此内容查询易于撰写。  
  
 本节概述了您可以创建的内容查询类型。  
  
-   通过针对挖掘结构或事例数据的查询，您可以查看用于定型的详细数据。  
  
-   针对模型的查询可以返回模式、属性列表、公式等等。  
  
###  <a name="bkmk_Structure"></a> 针对结构和事例数据的查询  
 DMX 支持对用于生成挖掘结构和模型的缓存数据进行查询。 默认情况下，在您定义挖掘结构时将创建此缓存，并且在您处理该结构或模型时填充此缓存。  
  
> [!WARNING]  
>  如果您需要将数据拆分为定型集和测试集，则不能清除或删除此缓存。 如果清除了缓存，则您无法查询事例数据。  
  
 以下示例演示了用于创建针对事例数据或挖掘结构中数据的查询的常用模式：  
  
 **获取模型的所有事例**  
 `SELECT FROM <model>.CASES`  
  
 使用此语句可以从用于生成模型的事例数据中检索指定列。 为运行此查询，您必须对模型具有钻取权限。  
  
 **查看在结构中包含的所有数据**  
 `SELECT FROM <structure>.CASES`  
  
 使用此语句可以查看结构中包含的所有数据，包括特定挖掘模型中不包括的列。 您必须对模型以及结构具有钻取权限，才能从挖掘结构中检索数据。  
  
 **获取值范围**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 使用此语句可以查找连续列或 DISCRETIZED 列的存储桶的最小值、最大值和平均值。  
  
 **获取非重复值**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 使用此语句可以检索 DISCRETE 列的所有值。  请勿针对 DISCRETIZED 列使用此语句；请改用 **RangeMin** 和 **RangeMax** 函数。  
  
 **查找用于对模型或结构定型的事例**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 使用此语句可获取用于对模型定型的完整数据集。  
  
 **查找用于测试模型或结构的事例**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 使用此语句可获取为测试与特定结构相关的挖掘模型而保留的数据。  
  
 **从特定的模型模式钻取到基础事例数据**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 使用此语句可从定型模型中检索详细事例数据。 您必须指定特定节点：例如，必须知道群集的节点 ID、决策树的特定分支，等等。此外，您还必须拥有对模型的钻取权限才能运行此查询。  
  
###  <a name="bkmk_Patterns"></a> 针对模型模式、统计信息和属性的查询  
 数据挖掘模型的内容有多种用途。 利用模型内容查询，您可以：  
  
-   提取公式或概率以便您自己来进行计算。  
  
-   对于关联模型，可检索用于生成预测的规则。  
  
-   检索特定规则的说明，以便您可以在自定义应用程序中使用这些规则。  
  
-   查看时序模型检测到的移动平均值。  
  
-   获取某段趋势线的回归公式。  
  
-   检索与标识为特定群集的一部分的客户有关的可行信息。  
  
 以下示例演示了一些用于创建针对模型内容的查询的常用模式：  
  
 **从模型中获取模式**  
 `SELECT FROM <model>.CONTENT`  
  
 使用此语句可以检索有关模型中特定节点的详细信息。 根据算法类型，该节点可包含规则和公式、支持和方差统计信息等。  
  
 **检索在定型模型中使用的属性**  
 `CALL System.GetModelAttributes(<model>)`  
  
 使用此存储过程可以检索已由某一模型使用的属性的列表。 例如，此信息可用于确定由于功能选择而清除的属性。  
  
 **检索在数据挖掘维度中存储的内容**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 使用此语句可以从数据挖掘维度中检索数据。  
  
 此查询类型主要供内部使用。 但是，并非所有算法都支持此功能。 是否支持将通过 MINING_SERVICES 架构行集中的一个标志来指示。  
  
 如果您开发自己的插件算法，则可使用此语句验证您的模型的内容以便进行测试。  
  
 **获取模型的 PMML 表示形式**  
 `SELECT * FROM <model>.PMML`  
  
 获取以 PMML 格式表示模型的 XML 文档。 并非支持所有模型类型。  
  
##  <a name="bkmk_Examples"></a> 示例  
 尽管某些模型内容在各算法中是标准的，但根据您用于生成模型的算法不同，内容的某些部分会大不相同。 因此，在创建内容查询时，必须了解模型中哪些信息对您的特定模型最有用。  
  
 本节提供了几个示例，用来演示选择的算法如何影响存储在模型中的信息类型。 有关挖掘模型内容以及每种模型类型特定的内容的详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Assoc"></a> 示例 1：针对关联模型的内容查询  
 `SELECT FROM <model>.CONTENT`语句返回不同种类的信息，具体取决于您正在查询的模型类型。 对于关联模型，“节点类型” 为一段关键信息。 节点类似于模型内容中的信息的容器。 在关联模型中，表示规则的节点的 NODE_TYPE 值为 8，而表示项集的节点的 NODE_TYPE 值为 7。  
  
 因此，以下查询将返回前 10 个项集，按照 SUPPORT 排序（默认排序）。  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 下面的查询构建于这些信息之上。 该查询返回三列：节点的 ID、完整规则以及项集右侧的产品（即，预测将作为项集的一部分与其他某些产品关联的产品）。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 FLATTENED 关键字表示嵌套行集应转换为平展表。 在规则右侧表示产品的属性包含在 NODE_DISTRIBUTION 表中；因此，我们通过添加长度大于 2 的要求来仅检索包含属性名的行。  
  
 使用一个简单的字符串函数从第三列中删除模型的名称。 （通常，模型名称作为嵌套列的值的前缀。）  
  
 WHERE 子句指定 NODE_TYPE 的值应当为 8，这表示仅仅检索规则。  
  
 有关更多示例，请参阅 [关联模型查询示例](../../analysis-services/data-mining/association-model-query-examples.md)。  
  
###  <a name="bkmk_DecTree"></a> 示例 2：针对决策树模型的内容查询  
 决策树模型可用于预测以及分类。  此示例假定您使用模型是为了预测结果，但同时也希望找出可以使用哪些因子或规则来对结果进行分类。  
  
 在决策树模型中，使用节点表示树和叶节点。 每个节点的标题包含指向结果的路径的说明。 因此，若要跟踪任一特定结果的路径，您需要确定包含该结果的节点，然后获取该节点的详细信息。  
  
 在预测查询中，可以添加预测函数 [PredictNodeId (DMX)](../../dmx/predictnodeid-dmx.md) 来获取相关节点的 ID，如以下示例所示：  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 一旦您有了包含结果的节点的 ID，就可以通过创建包含 NODE_CAPTION 的内容查询，来检索说明预测的规则或路径，如下所示：  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 有关更多示例，请参阅 [决策树模型查询示例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)。  
  
##  <a name="bkmk_Results"></a> 使用查询结果  
 如示例中所示，内容查询主要返回表格行集，但还可以包含来自嵌套列的信息。 您可以平展返回的行集，但这样做可能会导致对结果的使用更复杂。 特别是 NODE_DISTRIBUTION 节点的内容是嵌套的，但包含了大量有关模型的有用信息。  
  
 有关如何使用分层行集的详细信息，请参阅 MSDN 上的 OLEDB 规范。  
  
## <a name="see-also"></a>另请参阅  
 [了解 DMX Select 语句](../../dmx/understanding-the-dmx-select-statement.md)   
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
