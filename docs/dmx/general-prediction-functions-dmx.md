---
title: 通用预测函数 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8de92033c58f2583fc7ba93e6c326d4a406c90a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985429"
---
# <a name="general-prediction-functions-dmx"></a>通用预测函数 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  可以使用**选择**语句中的数据挖掘扩展插件 (DMX) 创建不同类型的查询。 查询可用于返回挖掘模型本身的信息，创建新预测，或者通过使用新数据对模型进行定型来改变模型。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了多种专用函数可控制在查询中返回的信息的类型。 通过将这些函数添加到 DMX 查询中，可以检索更多统计信息或数据列。 但是，每个查询类型和每个模型类型都仅仅支持某些函数。  
  
## <a name="common-functions"></a>常见函数  
 可以使用函数来扩展挖掘模型返回的结果。 可以将以下函数用于任何**选择**返回表表达式的语句：  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[预测&#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 此外，几乎所有模型类型都支持下列函数：  
  
-   [存在&#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [预测&#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 个别算法可能还支持其他的函数。 每个模型类型支持的函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="functions-specific-to-select-syntax"></a>特定于 SELECT 语法的函数  
 下表列出了可用于每种类型的函数**选择**语句。  
  
 有关在 DMX 中的函数的常规信息，请参阅[数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
|查询类型|支持的函数|Remarks|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM\<模型 >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|这些函数可用于为包含数值数据类型的任何列提供最大值、最小值和平均值，而无需考虑该列是连续的还是离散化的。|  
|[SELECT FROM\<模型 >。内容](../dmx/select-from-model-content-dmx.md)<br /><br /> 或多个<br /><br /> [SELECT FROM\<模型 >。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|此函数检索模型中的指定节点的子节点，并且可用于（举例而言）循环访问挖掘模型内容中的节点。 节点在挖掘模型内容中的排列取决于模型类型。 为每个挖掘模型类型的结构有关的信息，请参阅[挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。<br /><br /> 如果您已将挖掘模型内容另存为一个维度，则还可以使用其他多维表达式 (MDX) 函数，这些函数可用于查询属性层次结构。|  
|[SELECT FROM\<模型 >。用例](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag 类](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Lag 函数仅支持时序模型。<br /><br /> 在对结构使用维持选项创建测试数据集创建基于模型中支持，则 IsTestCase 函数。 如果模型不是基于具有维持测试集的结构，则所有事例都将被视为定型事例。|  
|[SELECT FROM\<模型 >。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|在此上下文中，IsInNode 函数将返回属于一组理想化的示例用例的用例。|  
|SELECT FROM\<模型 >。PMML|不适用。 请改用 XML 查询函数。|仅下列模型类型支持 PMML 表示形式：<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析|  
|[SELECT FROM\<模型 > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|专门用于生成模型所用的算法的预测函数。|每个模型类型的预测函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。|  
|[SELECT FROM\<模型 >](../dmx/select-from-model-dmx.md)|专门用于生成模型所用的算法的预测函数。|每个模型类型的预测函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
