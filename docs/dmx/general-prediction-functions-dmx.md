---
title: 常规预测函数 (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- mapping functions to query types [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- SELECT statement [DMX]
- Data Mining Extensions [Analysis Services], functions
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: e128159a-0458-43c9-bfe9-129cb6cfbe1c
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5e767d0243a8600c0f20cffebebfa92baffc2fc4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="general-prediction-functions-dmx"></a>通用预测函数 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  你可以使用**选择**语句中数据挖掘扩展插件 (DMX) 来创建不同类型的查询。 查询可用于返回挖掘模型本身的信息，创建新预测，或者通过使用新数据对模型进行定型来改变模型。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供了各种专用控制查询中返回的信息的类型的函数。 通过将这些函数添加到 DMX 查询中，可以检索更多统计信息或数据列。 但是，每个查询类型和每个模型类型都仅仅支持某些函数。  
  
## <a name="common-functions"></a>常见函数  
 可以使用函数来扩展挖掘模型返回的结果。 你可以使用以下函数任何**选择**返回表表达式的语句：  
  
|||  
|-|-|  
|[BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40; DMX &#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40; DMX &#41;](../dmx/topcount-dmx.md)|  
|[预测 &#40; DMX &#41;](../dmx/predict-dmx.md)|[TopPercent &#40; DMX &#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)|[TopSum &#40; DMX &#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)||  
  
 此外，几乎所有模型类型都支持下列函数：  
  
-   [存在 &#40; DMX &#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40; DMX &#41;](../dmx/isdescendant-dmx.md)  
  
-   [则 IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)  
  
-   [则 IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md)  
  
-   [预测 &#40; DMX &#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40; DMX &#41;](../dmx/structurecolumn-dmx.md)  
  
 个别算法可能还支持其他的函数。 有关每个模型类型所支持的函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="functions-specific-to-select-syntax"></a>特定于 SELECT 语法的函数  
 下表列出可用于每种类型的函数**选择**语句。  
  
 有关在 DMX 中的函数的常规信息，请参阅[数据挖掘扩展插件 &#40; DMX &#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
|查询类型|支持的函数|Remarks|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM\<模型 >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)|这些函数可用于为包含数值数据类型的任何列提供最大值、最小值和平均值，而无需考虑该列是连续的还是离散化的。|  
|[SELECT FROM\<模型 >。内容](../dmx/select-from-model-content-dmx.md)<br /><br /> 或多个<br /><br /> [SELECT FROM\<模型 >。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40; DMX &#41;](../dmx/isdescendant-dmx.md)|此函数检索模型中的指定节点的子节点，并且可用于（举例而言）循环访问挖掘模型内容中的节点。 节点在挖掘模型内容中的排列取决于模型类型。 有关每个挖掘模型类型的结构的信息，请参阅[挖掘模型内容 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).<br /><br /> 如果您已将挖掘模型内容另存为一个维度，则还可以使用其他多维表达式 (MDX) 函数，这些函数可用于查询属性层次结构。|  
|[SELECT FROM\<模型 >。用例](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag 类](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [则 IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [则 IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)|Lag 函数仅支持时序模型。<br /><br /> 则 IsTestCase 函数支持基于使用创建维持选项，以创建测试数据集的结构的模型。 如果模型不是基于具有维持测试集的结构，则所有事例都将被视为定型事例。|  
|[SELECT FROM\<模型 >。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)|在此上下文中，一部分，则 IsInNode 函数将返回属于一组理想化的示例用例的用例。|  
|SELECT FROM\<模型 >。PMML|不适用。 请改用 XML 查询函数。|仅下列模型类型支持 PMML 表示形式：<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析|  
|[SELECT FROM\<模型 > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|专门用于生成模型所用的算法的预测函数。|有关每个模型类型的预测函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。|  
|[SELECT FROM\<模型 >](../dmx/select-from-model-dmx.md)|专门用于生成模型所用的算法的预测函数。|有关每个模型类型的预测函数的列表，请参阅[数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
