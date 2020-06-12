---
title: 决策树模型查询示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- decision tree algorithms [Analysis Services]
- content queries [DMX]
- decision trees [Analysis Services]
ms.assetid: ceaf1370-9dd1-4d1a-a143-7f89a723ef80
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7a6b158a42c9ca90bf2cfd2e9b981a1e2a735ccc
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522711"
---
# <a name="decision-trees-model-query-examples"></a>决策树模型查询示例
  在创建针对数据挖掘模型的查询时，您既可以创建内容查询，也可以创建预测查询。内容查询提供有关分析过程中发现的模式的详细信息，而预测查询则使用模型中的模式对新数据进行预测。 例如，决策树模型的内容查询可能提供有关树在每个级别上的事例数的统计信息或者区分事例的规则。 而预测查询则是将模型映射到新数据，以生成建议、分类等等。 您还可以使用查询来检索有关模型的元数据。  
  
 本节说明如何为基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法的模型创建查询。  
  
 **内容查询**  
  
 [通过数据挖掘架构行集检索模型参数](#bkmk_Query1)  
  
 [使用 DMX 获取与模型中的树有关的详细信息](#bkmk_Query2)  
  
 [从模型中检索子树](#bkmk_Query3)  
  
 **预测查询**  
  
 [返回具有概率的预测](#bkmk_Query4)  
  
 [根据决策树模型预测关联](#bkmk_Query5)  
  
 [从决策树模型中检索回归公式](#bkmk_Query6)  
  
##  <a name="finding-information-about-a-decision-trees-model"></a><a name="bkmk_top2"></a>查找有关决策树模型的信息  
 若要针对决策树模型内容创建有意义的查询，您应该了解模型内容的结构以及哪些节点类型存储哪类信息。 有关详细信息，请参阅 [决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
###  <a name="sample-query-1-retrieving-model-parameters-from-the-data-mining-schema-rowset"></a><a name="bkmk_Query1"></a>示例查询1：从数据挖掘架构行集中检索模型参数  
 通过查询数据挖掘架构行集，您可以找到有关模型的元数据，如模型创建时间、上次处理模型的时间、模型基于的挖掘结构的名称以及用作可预测属性的列的名称。 您还可以返回首次创建模型时所使用的参数。  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 示例结果：  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="sample-query-2-returning-details-about-the-model-content-by-using-dmx"></a><a name="bkmk_Query2"></a>示例查询2：使用 DMX 返回有关模型内容的详细信息  
 下面的查询返回有关在 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)中生成模型时创建的决策树的一些基本信息。 每个树状结构都存储在自己的节点中。 由于此模型包含单个可预测属性，因此只有一个树节点。 但是，如果使用决策树算法创建关联模型，则可能有成百上千的树，每种产品对应一个树。  
  
 此查询返回类型 2 的所有节点，这些节点是表示特定可预测属性的树的顶级节点。  
  
> [!NOTE]  
>  必须将 `CHILDREN_CARDINALITY` 列括在括号中，以便将它与同名的 MDX 保留关键字区分开来。  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 示例结果：  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|全部|12939|5|  
  
 这些结果是什么意思？ 在决策树模型中，特定节点的基数指明该节点有多少个直属子级。 此节点的基数是 5，这意味着该模型将潜在的自行车购买者的目标总体分成了 5 个子组。  
  
 下面的相关查询返回这 5 个子组的子级以及子节点中属性和值的分布。 由于统计信息（如支持、概率和方差）存储在嵌套表 `NODE_DISTRIBUTION`中，因此本示例使用 `FLATTENED` 关键字输出嵌套表列。  
  
> [!NOTE]  
>  必须将嵌套表列 `SUPPORT` 括在括号中，以便将它与同名保留关键字区分开来。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 示例结果：  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|Support|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 根据这些结果，你可以判断买了自行车的客户（ `[Bike Buyer]` = 1），1067的客户有0个汽车，473个客户有3辆车。  
  
###  <a name="sample-query-3-retrieving-subtrees-from-the-model"></a><a name="bkmk_Query3"></a>示例查询3：从模型中检索子树  
 假定您希望查找有关购买了自行车的客户的更多信息。 你可以通过在查询中使用 [IsDescendant (DMX)](/sql/dmx/isdescendant-dmx) 函数来查看任何子树的其他详细信息，如下面的示例所示。 通过从包含 42 岁以上的客户的树中检索叶节点 (NODE_TYPE = 4)，查询将返回自行车购买者的计数。 查询将嵌套表中的行限定为其中 Bike Buyer = 1 的行。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 示例结果：  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>使用决策树模型进行预测  
 由于决策树可用于各种任务（包括分类、回归以及关联），因此，在针对决策树模型创建预测查询时，您可以使用许多选项。 必须了解创建模型的目的才能明白预测的结果。 以下查询示例说明了三种不同的情况：  
  
-   返回分类模型的预测以及正确预测的概率，然后根据该概率筛选结果；  
  
-   创建一个单独查询来预测关联；  
  
-   检索部分决策树的回归公式，其中输入和输出之间的关系是线性的。  
  
###  <a name="sample-query-4-returning-predictions-with-probabilities"></a><a name="bkmk_Query4"></a>示例查询4：返回具有概率的预测  
 下面的示例查询使用在 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)中创建的决策树模型。 该查询在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW 的表 dbo.ProspectiveBuyers 中遍历新的示例数据集，以便预测新数据集中的哪些客户将购买自行车。  
  
 查询使用预测函数 [PredictHistogram (DMX)](/sql/dmx/predicthistogram-dmx)，该函数返回一个嵌套表，其中包含有关该模型发现的概率的有用信息。 该查询的最后的 WHERE 子句将筛选结果，以便仅返回预测购买自行车的概率大于 0% 的那些潜在客户。  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将返回具有列标签 **Expression**的嵌套表。 可通过对返回的列使用别名来更改此标签。 如果使用别名，则该别名（本例中为 **Results**）将用作嵌套表中的列标题和值。 必须展开嵌套表才能查看结果。  
  
 自行车购买者 = 1 的示例结果：  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 如果提供程序不支持分层行集（如此处显示的结果），则可以在查询中使用 FLATTENED 关键字将结果返回为包含 Null（替代重复的列值）的表。 有关详细信息，请参阅[嵌套表（Analysis Services - 数据挖掘）](nested-tables-analysis-services-data-mining.md)或[了解 DMX Select 语句](/sql/dmx/understanding-the-dmx-select-statement)。  
  
###  <a name="sample-query-5-predicting-associations-from-a-decision-trees-model"></a><a name="bkmk_Query5"></a>示例查询5：根据决策树模型预测关联  
 下面的示例查询基于关联挖掘结构。 为了按照此示例内容进行操作，您可以在此挖掘结构中添加一个新模型，并且选择 Microsoft 决策树作为算法。 有关如何创建关联挖掘结构的详细信息，请参阅[第 3 课：生成市场篮方案（数据挖掘中级教程）](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)。  
  
 以下示例查询是一个单独查询，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中轻松创建该查询，方法是选择字段，然后从下拉列表中选择这些字段的值。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 预期的结果：  
  
|型号|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 结果告诉您要向已购买 Patch Kit 产品的客户推荐的三款最佳产品。 也可以在您进行推荐时提供多款产品作为输入，方法是键入值，或使用 **“单独查询输入”** 对话框，然后添加或删除值。 以下示例查询演示如何提供用来进行预测的多个值。 这些值用定义输入值的 SELECT 语句中的 UNION 子句来连接。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 预期的结果：  
  
|型号|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="sample-query-6-retrieving-a-regression-formula-from-a-decision-trees-model"></a><a name="bkmk_Query6"></a>示例查询6：从决策树模型中检索回归公式  
 在创建包含连续属性的回归的决策树模型时，可以使用回归公式进行预测，也可以提取有关回归公式的信息。 有关回归模型的查询的详细信息，请参阅 [线性回归模型查询示例](linear-regression-model-query-examples.md)。  
  
 如果决策树模型由回归节点和根据离散属性或范围进行拆分的节点混合组成，则可以创建仅返回回归节点的查询。 NODE_DISTRIBUTION 表包含回归公式的详细信息。 在本示例中，对列进行了平展，对 NODE_DISTRIBUTION 表使用了别名，以便于查看。 但在此模型中，找不到将 Income 与其他连续属性相关联的回归量。 在这些情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将返回属性的平均值和模型中该属性的总体方差。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 示例结果：  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 有关回归模型中使用的值类型和统计信息的详细信息，请参阅[线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
## <a name="list-of-prediction-functions"></a>预测函数的列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法还支持下表中列出的其他函数。  
  
|||  
|-|-|  
|预测函数|使用情况|  
|[IsDescendant (DMX)](/sql/dmx/isdescendant-dmx)|确定一个节点是否是模型中另一个节点的子节点。|  
|[IsInNode (DMX)](/sql/dmx/isinnode-dmx)|指示指定的节点是否包含当前事例。|  
|[PredictAdjustedProbability (DMX)](/sql/dmx/predictadjustedprobability-dmx)|返回加权的概率。|  
|[PredictAssociation (DMX)](/sql/dmx/predictassociation-dmx)|预测关联数据集中的成员身份。|  
|[PredictHistogram (DMX)](/sql/dmx/predicthistogram-dmx)|返回与当前预测值相关的值的表。|  
|[PredictNodeId (DMX)](/sql/dmx/predictnodeid-dmx)|返回每个事例的 Node_ID。|  
|[PredictProbability (DMX)](/sql/dmx/predictprobability-dmx)|返回预测值的概率。|  
|[PredictStdev (DMX)](/sql/dmx/predictstdev-dmx)|返回指定列的预测标准偏差。|  
|[PredictSupport (DMX)](/sql/dmx/predictsupport-dmx)|返回指定状态的支持值。|  
|[PredictVariance (DMX)](/sql/dmx/predictvariance-dmx)|返回指定列的方差。|  
  
 有关所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都支持的通用函数的列表，请参阅[通用预测函数 (DMX)](/sql/dmx/general-prediction-functions-dmx)。 有关特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘查询](data-mining-queries.md)   
 [Microsoft 决策树算法](microsoft-decision-trees-algorithm.md)   
 [Microsoft 决策树算法技术参考](microsoft-decision-trees-algorithm-technical-reference.md)   
 [决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
