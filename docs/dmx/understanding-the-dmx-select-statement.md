---
description: 了解 DMX Select 语句
title: 了解 DMX Select 语句 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 93744da59ad7149203da8fd14179045b63dc798f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395213"
---
# <a name="understanding-the-dmx-select-statement"></a>了解 DMX Select 语句
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [SELECT](../dmx/select-dmx.md)语句是您在中 (DMX) 创建的大多数查询的基础 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 该语句可以执行多种任务，例如对数据挖掘模型进行浏览和预测。  
  
 下面是可以使用 **SELECT** 语句完成的任务：  
  
-   浏览数据挖掘模型。 架构行集可以定义模型的结构。  
  
-   发现挖掘模型列可能有的值。  
  
-   浏览分配给挖掘模型中节点的事例，或获取有代表性的事例。  
  
-   使用各种输入创建预测。  
  
-   复制挖掘模型。  
  
 其中每个任务都使用一组不同的数据，我们将调用一个 *数据域*。 在语句的 **FROM** 子句中定义数据域。  
  
-   您需要在数据挖掘模型自身中查找对象，例如，用于定义一组数据的规则或用于进行预测的公式。  
  
     在这种情况下，您需要查看存储在模型自身中的元数据。 因此，数据域就是数据挖掘架构行集中的列。  
  
-   您需要从用于生成模型的这些事例获取详细信息。  
  
     在这种情况下，您需要钻取到作为数据域的挖掘结构，并查看列中的各行，如“Gender”、“Bike Buyer”等。  
  
 **重要提示：** 表达式列表或 **WHERE** 子句中包含的所有内容都必须来自 **from** 子句定义的数据域。 您不能将数据域混用。  
  
##  <a name="select-types"></a><a name="Select_Types"></a> 选择类型  
 **SELECT**语句的语法支持许多不同的任务。 使用下列模式来执行这些任务：  
  
-   [预测](#Predicting)  
  
-   [浏览](#Browsing)  
  
-   [复制](#Copying)  
  
-   [钻取](#Drillthrough)  
  
###  <a name="predicting"></a><a name="Predicting"></a> 预测  
 通过使用下列查询类型，您可以根据挖掘模型执行预测。  
  
 可以在预测联接**SELECT**语句的**FROM**和**WHERE**子句内包含任何浏览或预测**SELECT**语句。  
  
|查询类型|描述|  
|----------------|-----------------|  
|从 [自然] 预测联接中选择|返回一个预测，该预测是通过将挖掘模型中的列与内部数据源中的列联接而创建的。<br /><br /> 此查询类型的域是来自模型的可预测列和来自输入数据源的列。<br /><br /> [从 &#60;模型中选择&#62; 预测联接 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [预测查询（数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|选择来源 *\<model>*|仅根据挖掘模型返回可预测列的最可能状态。 该查询类型是使用空预测联接创建预测的快捷方式。<br /><br /> 该查询类型的域是来自模型的可预测列。<br /><br /> [从 &#60;模型中选择&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [预测查询（数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [返回到选择类型](#Select_Types)  
  
###  <a name="browsing"></a><a name="Browsing"></a> 浏览  
 通过使用下列查询类型，可以浏览挖掘模型的内容。  
  
|查询类型|描述|  
|----------------|-----------------|  
|选择 DISTINCT FROM *\<model>*|为指定的列返回所有来自挖掘模型的状态值。<br /><br /> 此查询类型的数据域是数据挖掘模型。<br /><br /> [选择 "与 &#60;模型不同" &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [内容查询（数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|选择 "从" *\<model>* 。CONTENT|返回说明挖掘模型的内容。<br /><br /> 此查询类型的数据域是内容架构行集。<br /><br /> [从 &#60;模型&#62; 中进行选择。内容 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [内容查询（数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|选择 "从" *\<model>* 。DIMENSION_CONTENT|返回说明挖掘模型的内容。<br /><br /> 此查询类型的数据域是内容架构行集。<br /><br /> [从 &#60;模型&#62; 中进行选择。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|选择 "从" *\<model>* 。PMML|返回挖掘模型的预测模型标记语言 (PMML) 表示形式，用于支持该功能的算法。<br /><br /> 该查询类型的域是 PMML 架构行集。<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126283(v=sql.110))|  
  
 [返回到选择类型](#Select_Types)  
  
###  <a name="copying"></a><a name="Copying"></a> 复制  
 可以将挖掘模型及其关联的挖掘结构复制到新模型中，然后在语句中重命名模型。  
  
|查询类型|描述|  
|----------------|-----------------|  
|选择加入 *\<new model>*|创建挖掘模型的副本。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [返回到选择类型](#Select_Types)  
  
###  <a name="drillthrough"></a><a name="Drillthrough"></a> 钻  
 通过使用下列查询类型，可以浏览用于为模型定型的事例或事例的表示形式。  
  
|查询类型|描述|  
|----------------|-----------------|  
|选择 "从" *\<model>* 。这|返回用于为挖掘模型定型的事例。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [从 &#60;模型&#62; 中进行选择。DMX&#41;&#40;情况 ](../dmx/select-from-model-cases-dmx.md)<br /><br /> [使用 DMX 来创建钻取查询](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|选择 "从" *\<model>* 。SAMPLE_CASES|返回一个示例事例，该事例代表用于为挖掘模型定型的事例。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [从 &#60;模型&#62; 中进行选择。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|选择 "从" *\<structure>* 。 这|从基础挖掘结构返回详细数据行，即使某些详细信息并未用于对该挖掘模型定型。<br /><br /> [从 &#60;结构&#62; 中进行选择。这](../dmx/select-from-structure-cases.md)<br /><br /> [钻取查询（数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [返回到选择类型](#Select_Types)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;DMX&#41; 的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
