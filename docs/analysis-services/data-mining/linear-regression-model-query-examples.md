---
title: "线性回归模型查询示例 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- content queries [DMX]
ms.assetid: fd3cf312-57a1-44b6-b772-fce6fc1c26d7
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 36f1f595cd087ff05582250c205681b2b7794702
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="linear-regression-model-query-examples"></a>线性回归模型查询示例
  在创建针对数据挖掘模型的查询时，您既可以创建内容查询，也可以创建预测查询。内容查询提供有关分析过程中发现的模式的详细信息，而预测查询则使用模型中的模式对新数据进行预测。 例如，内容查询可能会提供有关回归公式的更多详细信息，而预测查询则可能会告诉您新数据点是否适合模型。 您还可以使用查询来检索有关模型的元数据。  
  
 本节介绍如何针对基于 Microsoft 线性回归算法的模型创建查询。  
  
> [!NOTE]  
>  由于线性回归基于 Microsoft 决策树算法的特殊情况，因而会存在诸多相似性，且某些使用连续可预测属性的决策树模型可包含回归公式。 有关详细信息，请参阅 [Microsoft 决策树算法技术参考](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)。  
  
 **内容查询**  
  
 [使用数据挖掘架构行集确定用于模型的参数](#bkmk_Query1)  
  
 [使用 DMX 返回模型的回归公式](#bkmk_Query2)  
  
 [仅返回模型的系数](#bkmk_Query3)  
  
 **预测查询**  
  
 [使用单独查询预测收入](#bkmk_Query4)  
  
 [对回归模型使用预测函数](#bkmk_Query5)  
  
##  <a name="bkmk_top"></a> 查找有关线性回归模型的信息  
 线性回归模型的结构极其简单：挖掘模型将数据表示为定义回归公式的单个节点。 有关详细信息，请参阅 [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
 [返回页首](#bkmk_top)  
  
###  <a name="bkmk_Query1"></a> 示例查询 1：使用数据挖掘架构行集确定用于模型的参数  
 通过查询数据挖掘架构行集，您可找到模型的元数据。 这包括模型创建时间、上次处理模型时间、模型所基于的挖掘结构的名称以及指定为可预测属性的列的名称。 您还可以返回首次创建模型时所使用的参数。  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 示例结果：  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT=10,<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  参数设置“`FORCE_REGRESSOR =` ”指示参数 FORCE_REGRESSOR 的当前值为 Null。  
  
 [返回页首](#bkmk_top)  
  
###  <a name="bkmk_Query2"></a> 示例查询 2：检索模型的回归公式  
 下面的查询返回一个线性回归模型的挖掘模型内容，该回归模型是通过使用 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中使用的目标邮件数据源创建的。 此模型基于年龄预测客户收入。  
  
 查询返回包含回归公式的节点的内容。 所有变量和系数均存储在嵌套表 NODE_DISTRIBUTION 的单独行中。 如果要查看完整的回归公式，请使用 [Microsoft 树查看器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)，单击“(全部)”节点，然后打开“挖掘图例”。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  如果通过使用查询（如 `SELECT <column name> from NODE_DISTRIBUTION`）来引用嵌套表的单个列，则必须将某些列（如 **SUPPORT** 或 **PROBABILITY**）用括号括起来，以将它们与同名的保留字区分开。  
  
 预期的结果：  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|缺少|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|年龄|471.687717702463|0|0|126.969442359327|7|  
|年龄|234.680904692439|0|0|0|8|  
|年龄|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 我们来做个比较，在 **“挖掘图例”**中，该回归公式显示如下：  
  
 `Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)`  
  
 可看出在“挖掘图例”中，对某些数值进行了舍入；但 NODE_DISTRIBUTION 表与“挖掘图例”实际上包含的是相同的值。  
  
 VALUETYPE 列中的值可告诉您每一行所包含的信息的类型，这在以编程方式处理结果时很有用。 下表给出了一个线性回归公式的输出值的类型。  
  
|VALUETYPE|  
|---------------|  
|1（缺失）|  
|3（连续）|  
|7（系数）|  
|8（得分）|  
|9（统计信息）|  
|7（系数）|  
|8（得分）|  
|9（统计信息）|  
|11（截距）|  
  
 有关回归模型每个值类型含义的详细信息，请参阅 [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
 [返回页首](#bkmk_top)  
  
###  <a name="bkmk_Query3"></a> 示例查询 3：仅返回模型的系数  
 通过使用 VALUETYPE 枚举，您可以仅返回回归公式的系数，如下面的查询所示：  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 此查询返回两行：一行来自挖掘模型内容，另一行来自包含系数的嵌套表。 此处未包括 ATTRIBUTE_NAME 列，因为对于系数，该列始终为空。  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793.5477381267|11|  
  
 [返回页首](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>根据线性回归模型进行预测  
 您可以使用数据挖掘设计器中的“挖掘模型预测”选项卡来生成针对线性回归模型的预测查询。 您可从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用预测查询生成器。  
  
> [!NOTE]  
>  此外，还可以通过使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Excel 数据挖掘外接插件或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Excel 数据挖掘外接插件来创建针对回归模型的查询。 即使 Excel 数据挖掘外接插件无法创建回归模型，您也可以浏览并查询 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例中所存储的所有模型。  
  
 [返回页首](#bkmk_top)  
  
###  <a name="bkmk_Query4"></a> 示例查询 4：使用单独查询预测收入  
 创建针对回归模型的单个查询的最简便方法是使用 **“单独查询输入”** 对话框。 例如，生成下面的 DMX 查询可以使用以下方法：先选择相应的回归模型，再选择“单独查询” ，然后在 **Age** 中键入 **20**。  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 示例结果：  
  
|Yearly Income|  
|-------------------|  
|45227.302092176|  
  
 [返回页首](#bkmk_top)  
  
###  <a name="bkmk_Query5"></a> 示例查询 5：对回归模型使用预测函数  
 您可以对线性回归模型使用许多标准预测函数。 下面的示例演示如何向预测查询结果中添加说明性统计信息。 您可以从这些结果发现此模型的均值的偏差非常大。  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 示例结果：  
  
|Yearly Income|StDev1|  
|-------------------|------------|  
|45227.302092176|31827.1726561396|  
  
 [返回页首](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>预测函数的列表  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法均支持一组通用的函数。 此外， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法还额外支持下表中列出的函数。  
  
|||  
|-|-|  
|预测函数|用法|  
|[IsDescendant (DMX)](../../dmx/isdescendant-dmx.md)|确定一个节点是否是模型中另一个节点的子节点。|  
|[IsInNode (DMX)](../../dmx/isinnode-dmx.md)|指示指定的节点是否包含当前事例。|  
|[PredictHistogram (DMX)](../../dmx/predicthistogram-dmx.md)|返回指定列的一个预测值或一组值。|  
|[PredictNodeId (DMX)](../../dmx/predictnodeid-dmx.md)|返回每个事例的 Node_ID。|  
|[PredictStdev (DMX)](../../dmx/predictstdev-dmx.md)|返回预测值的标准偏差。|  
|[PredictSupport (DMX)](../../dmx/predictsupport-dmx.md)|返回指定状态的支持值。|  
|[PredictVariance (DMX)](../../dmx/predictvariance-dmx.md)|返回指定列的方差。|  
  
 有关对所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 算法都通用的函数列表，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。 有关如何使用这些函数的详细信息，请参阅[数据挖掘扩展插件 (DMX) 函数引用](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 线性回归算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 线性回归算法技术参考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  

