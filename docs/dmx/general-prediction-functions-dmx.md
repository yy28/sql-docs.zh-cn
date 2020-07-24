---
title: 一般预测函数（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cde2fe9da61ca9d877f0c905609d8baf832ea509
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971665"
---
# <a name="general-prediction-functions-dmx"></a>通用预测函数 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  您可以使用数据挖掘扩展插件（DMX）中的**SELECT**语句创建不同类型的查询。 查询可用于返回挖掘模型本身的信息，创建新预测，或者通过使用新数据对模型进行定型来改变模型。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供各种专用函数，这些函数可控制在查询中返回的信息的类型。 通过将这些函数添加到 DMX 查询中，可以检索更多统计信息或数据列。 但是，每个查询类型和每个模型类型都仅仅支持某些函数。  
  
## <a name="common-functions"></a>常见函数  
 可以使用函数来扩展挖掘模型返回的结果。 对于返回表表达式的任何**SELECT**语句，您可以使用以下函数：  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict (DMX)](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 此外，几乎所有模型类型都支持下列函数：  
  
-   [存在 &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant (DMX)](../dmx/isdescendant-dmx.md)  
  
-   [则 istestcase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [则 istrainingcase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict (DMX)](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 个别算法可能还支持其他的函数。 有关每种模型类型支持的函数列表，请参阅[数据挖掘查询](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)。  
  
## <a name="functions-specific-to-select-syntax"></a>特定于 SELECT 语法的函数  
 下表列出了可用于每种类型的**SELECT**语句的函数。  
  
 有关 DMX 中函数的常规信息，请参阅[数据挖掘扩展插件 &#40;dmx&#41; 函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
|查询类型|支持的函数|备注|  
|----------------|-------------------------|-------------|  
|[选择 DISTINCT FROM\<model>](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|这些函数可用于为包含数值数据类型的任何列提供最大值、最小值和平均值，而无需考虑该列是连续的还是离散化的。|  
|[选择 "从" \<model> 。CONTENT](../dmx/select-from-model-content-dmx.md)<br /><br /> or<br /><br /> [选择 "从" \<model> 。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant (DMX)](../dmx/isdescendant-dmx.md)|此函数检索模型中的指定节点的子节点，并且可用于（举例而言）循环访问挖掘模型内容中的节点。 节点在挖掘模型内容中的排列取决于模型类型。 有关每个挖掘模型类型的结构的信息，请参阅[挖掘模型内容 &#40;Analysis Services 数据挖掘&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)。<br /><br /> 如果您已将挖掘模型内容另存为一个维度，则还可以使用其他多维表达式 (MDX) 函数，这些函数可用于查询属性层次结构。|  
|[选择 "从" \<model> 。这](../dmx/select-from-model-cases-dmx.md)|[IsInNode (DMX)](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag 类](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [则 istrainingcase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [则 istestcase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|仅时序模型支持 Lag 函数。<br /><br /> 基于使用维持选项创建的结构的模型支持则 istestcase 函数，以创建测试数据集。 如果模型不是基于具有维持测试集的结构，则所有事例都将被视为定型事例。|  
|[选择 "从" \<model> 。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode (DMX)](../dmx/isinnode-dmx.md)|在这种情况下，IsInNode 函数返回属于一组理想化示例事例的事例。|  
|选择 "从" \<model> 。PMML|不适用。 请改用 XML 查询函数。|仅下列模型类型支持 PMML 表示形式：<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析|  
|[SELECT FROM \<model> 预测联接](../dmx/select-from-model-prediction-join-dmx.md)|专门用于生成模型所用的算法的预测函数。|有关每种模型类型的预测函数的列表，请参阅[数据挖掘查询](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)。|  
|[选择来源\<model>](../dmx/select-from-model-dmx.md)|专门用于生成模型所用的算法的预测函数。|有关每种模型类型的预测函数的列表，请参阅[数据挖掘查询](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)。|  
  
## <a name="see-also"></a>另请参阅  
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
