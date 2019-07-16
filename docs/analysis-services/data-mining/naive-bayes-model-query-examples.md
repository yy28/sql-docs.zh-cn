---
title: Naive Bayes 模型查询示例 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f4ea8c07865980caa6f817e2920599d1a9003d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182533"
---
# <a name="naive-bayes-model-query-examples"></a>Naive Bayes 模型查询示例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在创建针对数据挖掘模型的查询时，您既可以创建内容查询，也可创建预测查询；内容查询提供有关分析过程中发现的模式的详细信息，而预测查询则使用模型中的模式来对新数据进行预测。 您还可以通过使用针对数据挖掘架构行集的查询来检索元数据。 本节说明如何创建针对基于 Microsoft Naive Bayes 算法的模型的查询。  
  
 **内容查询**  
  
 [使用 DMX 获取模型元数据](#bkmk_Query1)  
  
 [检索定型数据的摘要](#bkmk_Query2)  
  
 [查找有关属性的详细信息](#bkmk_Query3)  
  
 [使用系统存储过程](#bkmk_Query4)  
  
 **预测查询**  
  
 [使用单独查询预测结果](#bkmk_Query5)  
  
 [获取具有概率和支持值的预测](#bkmk_Query6)  
  
 [预测关联](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>查找有关 Naive Bayes 模型的信息  
 Naive Bayes 模型的模型内容可提供有关定型数据中值分布的聚合信息。 您还可以通过创建针对数据挖掘架构行集的查询来检索有关模型的元数据的信息。  
  
###  <a name="bkmk_Query1"></a> 示例查询 1:使用 DMX 获取模型元数据  
 通过查询数据挖掘架构行集，您可找到模型的元数据。 这包括模型创建时间、上次处理模型时间、模型所基于的挖掘结构的名称以及用作可预测属性的列的名称。 您还可以返回创建模型时所使用的参数。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 示例结果：  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 此示例所使用的模型基于您在 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中创建的 Naive Bayes 模型，但进行了修改，添加了第二个可预测属性，并对定型数据应用了筛选器。  
  
###  <a name="bkmk_Query2"></a> 示例查询 2:检索定型数据的摘要  
 在 Naive Bayes 模型中，有关定型数据中值分布的聚合信息存储在边际统计节点中。 该摘要获取方便，您不必创建针对定型数据的 SQL 查询，就可找到该摘要。  
  
 下面的示例使用 DMX 内容查询，从节点 (NODE_TYPE = 24) 检索数据。 由于统计信息存储在嵌套表中，因此，使用 FLATTENED 关键字是为了使结果更易查看。  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  您必须将列名 SUPPORT 和 PROBABILITY 括在括号中，以便将它们与同名的多维表达式 (MDX) 保留关键字区分开来。  
  
 部分结果：  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0.492736216|4|  
|TM_NaiveBayes|性别|Missing|0|0|1|  
|TM_NaiveBayes|性别|F|8656|0.495081217|4|  
|TM_NaiveBayes|性别|M|8828|0.504918783|4|  
  
 例如，这些结果告诉您每个离散值 (VALUETYPE = 4) 的定型事例的数量以及计算出的概率，其中进行了缺失值 (VALUETYPE = 1) 调整。  
  
 有关 Naive Bayes 模型中的 NODE_DISTRIBUTION 表所提供的值的定义，请参阅 [Naive Bayes 模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)。 有关缺失的值如何影响支持和概率计算的详细信息，请参阅[缺失值（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Query3"></a> 示例查询 3:查找有关属性的详细信息  
 由于 Naive Bayes 模型经常包含有关不同属性之间关系的复杂信息，因此，查看这些关系的最简便的方法是使用 [Microsoft Naive Bayes 查看器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)。 但您也可创建 DMX 查询来返回数据。  
  
 下面的示例演示如何从模型返回有关特定属性 `Region`的信息。  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 此查询返回两种类型的节点：表示输入属性 (NODE_TYPE = 10) 的节点和属性 (NODE_TYPE = 11) 的每个值的节点。 使用节点标题（而不是节点名称）来标识节点，是因为标题可同时显示属性名称和属性值。  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 节点中所存储的某些列与您可从边际统计信息获得的相同，如节点概率分数和节点支持值。 但 MSOLAP_NODE_SCORE 是特殊值，只提供给输入属性节点，指示此节点在模型中的相对重要性。 您可以在“依赖关系网络”窗格中查看更多同类信息，但不会提供分数。  
  
 下面的查询返回模型中所有属性的重要性分数：  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 示例结果：  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 通过在 [Microsoft 一般内容树查看器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中查看模型内容，您可以更好地了解统计信息所关注的内容。 这里演示了一些简单示例；更多时候，您可能需要执行多个示例，或者在客户端存储并处理结果。  
  
###  <a name="bkmk_Query4"></a> 示例查询 4:使用系统存储过程  
 除了编写自己的内容查询外，您还可以使用 Analysis Services 系统存储过程浏览结果。 若要使用系统存储过程，请为存储过程的名称加上 CALL 关键字前缀：  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 部分结果：  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  这些系统存储过程用于 Analysis Services 服务器与客户端之间的通信，请仅在开发和测试挖掘模型时使用它们，以为操作提供便利。 创建生产系统的查询时，请始终使用 DMX 编写您自己的查询。  
  
 有关 Analysis Services 系统存储过程的详细信息，请参阅[数据挖掘存储过程（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)。  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>使用 Naive Bayes 模型进行预测  
 和用于浏览输入属性与可预测属性之间的关系相比，Microsoft Naive Bayes 算法通常较少用于预测。 但模型支持使用预测函数进行预测和关联。  
  
###  <a name="bkmk_Query5"></a> 示例查询 5:使用单独查询预测结果  
 下面的查询使用单独查询提供新值，并基于模型预测具有这些特征的客户是否会购买自行车。 创建针对回归模型的查询的最简便方法是使用 **“单独查询输入”** 对话框。 例如，创建下面的 DMX 查询可以使用以下方法：依次选择 `TM_NaiveBayes` 模型、 **“单独查询”** ，然后从 `[Commute Distance]` 和 `Gender`的下拉列表中选择值。  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 示例结果：  
  
|表达式|  
|----------------|  
|0|  
  
 预测函数返回可能性最大的值，在本例中为 0，这意味着此种类型的客户不会购买自行车。  
  
###  <a name="bkmk_Query6"></a> 示例查询 6:获取具有概率和支持值的预测  
 除了预测结果外，您可能经常想知道概率的可靠性。 下面的查询使用与上一示例相同的单个查询，但另外添加了预测函数 [PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md)，以返回包含有关预测支持的统计信息的嵌套表。  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 示例结果：  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 表的最后一行显示对支持和概率的缺失值调整。 方差和标准偏差值始终为 0，因为 Naive Bayes 模型无法对连续值建立模型。  
  
###  <a name="bkmk_Query7"></a> 示例查询 7:预测关联  
 如果挖掘结构包含以可预测属性作为键的嵌套表，则不可将 Microsoft Naive Bayes 算法用于关联分析。 例如，可通过使用中创建的挖掘结构生成 Naive Bayes 模型[第 3 课：生成市场篮方案&#40;数据挖掘中级教程&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)的数据挖掘基础教程。 此示例中使用的模型经过修改，目的是向事例表中添加收入和客户区域。  
  
 下面的查询示例给出了一个单独查询，该查询预测购买产品 `'Road Tire Tube'`时还可能会购买产品。 您可使用这些信息，向特定类型的客户推荐产品。  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 部分结果：  
  
|“模型”|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>函数列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 此外， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 算法还额外支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[IsDescendant (DMX)](../../dmx/isdescendant-dmx.md)|确定一个节点是否是模型中另一个节点的子节点。|  
|[Predict (DMX)](../../dmx/predict-dmx.md)|返回指定列的一个预测值或一组值。|  
|[PredictAdjustedProbability (DMX)](../../dmx/predictadjustedprobability-dmx.md)|返回加权的概率。|  
|[PredictAssociation (DMX)](../../dmx/predictassociation-dmx.md)|预测关联数据集中的成员身份。|  
|[PredictNodeId (DMX)](../../dmx/predictnodeid-dmx.md)|返回每个事例的 Node_ID。|  
|[PredictProbability (DMX)](../../dmx/predictprobability-dmx.md)|返回预测值的概率。|  
|[PredictSupport (DMX)](../../dmx/predictsupport-dmx.md)|返回指定状态的支持值。|  
  
 若要查看特定函数的语法，请参阅[数据挖掘扩展插件 (DMX) 函数参考](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Naive Bayes 算法技术参考](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Microsoft Naive Bayes 算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Naive Bayes 模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
