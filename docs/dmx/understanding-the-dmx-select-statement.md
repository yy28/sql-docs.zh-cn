---
title: 了解 DMX Select 语句 |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- predictions [DMX]
- queries [DMX], Select statement
- SELECT statement [DMX]
- statements [DMX], SELECT statement
- copying mining models
ms.assetid: 61e97285-4a06-4434-9a40-38cde5af7c3f
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 84f8a735323fe347f97585f453527e9b55afe374
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-dmx-select-statement"></a>了解 DMX Select 语句
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [选择](../dmx/select-dmx.md)语句是创建与数据挖掘扩展插件 (DMX) 中的大多数查询的基础[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 该语句可以执行多种任务，例如对数据挖掘模型进行浏览和预测。  
  
 以下是你可以通过使用完成任务**选择**语句：  
  
-   浏览数据挖掘模型。 架构行集可以定义模型的结构。  
  
-   发现挖掘模型列可能有的值。  
  
-   浏览分配给挖掘模型中节点的事例，或获取有代表性的事例。  
  
-   使用各种输入创建预测。  
  
-   复制挖掘模型。  
  
 其中每个任务使用一组不同的数据，我们将调用*数据域*。 定义中的数据域**FROM**语句子句。  
  
-   您需要在数据挖掘模型自身中查找对象，例如，用于定义一组数据的规则或用于进行预测的公式。  
  
     在这种情况下，您需要查看存储在模型自身中的元数据。 因此，数据域就是数据挖掘架构行集中的列。  
  
-   您需要从用于生成模型的这些事例获取详细信息。  
  
     在这种情况下，您需要钻取到作为数据域的挖掘结构，并查看列中的各行，如“Gender”、“Bike Buyer”等。  
  
 **重要说明：**在表达式列表中或在包含的任何内容**其中**子句必须来自定义的数据域**FROM**子句。 您不能将数据域混用。  
  
##  <a name="Select_Types"></a> 选择类型  
 语法**选择**语句支持许多不同的任务。 使用下列模式来执行这些任务：  
  
-   [预测](#Predicting)  
  
-   [浏览](#Browsing)  
  
-   [复制](#Copying)  
  
-   [钻取](#Drillthrough)  
  
###  <a name="Predicting"></a> 预测  
 通过使用下列查询类型，您可以根据挖掘模型执行预测。  
  
 你可以浏览或预测的任何一个**选择**内的语句**FROM**和**其中**预测联接子句**选择**语句。  
  
|查询类型|Description|  
|----------------|-----------------|  
|从 [自然] 预测的选择加入|返回一个预测，该预测是通过将挖掘模型中的列与内部数据源中的列联接而创建的。<br /><br /> 此查询类型的域是来自模型的可预测列和来自输入数据源的列。<br /><br /> [SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [预测查询 & #40; 数据挖掘 & #41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
|SELECT FROM *\<模型 >*|仅根据挖掘模型返回可预测列的最可能状态。 该查询类型是使用空预测联接创建预测的快捷方式。<br /><br /> 该查询类型的域是来自模型的可预测列。<br /><br /> [SELECT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [预测查询 & #40; 数据挖掘 & #41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
  
 [返回以选择类型](#Select_Types)  
  
###  <a name="Browsing"></a> 浏览  
 通过使用下列查询类型，可以浏览挖掘模型的内容。  
  
|查询类型|Description|  
|----------------|-----------------|  
|SELECT DISTINCT FROM *\<模型 >*|为指定的列返回所有来自挖掘模型的状态值。<br /><br /> 此查询类型的数据域是数据挖掘模型。<br /><br /> [SELECT DISTINCT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [内容查询&#40;数据挖掘&#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM *\<模型 >*。内容|返回说明挖掘模型的内容。<br /><br /> 此查询类型的数据域是内容架构行集。<br /><br /> [SELECT FROM&#60;模型&#62;。内容&#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [内容查询&#40;数据挖掘&#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM *\<模型 >*。DIMENSION_CONTENT|返回说明挖掘模型的内容。<br /><br /> 此查询类型的数据域是内容架构行集。<br /><br /> [SELECT FROM&#60;模型&#62;。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|SELECT FROM *\<模型 >*。PMML|返回挖掘模型的预测模型标记语言 (PMML) 表示形式，用于支持该功能的算法。<br /><br /> 该查询类型的域是 PMML 架构行集。<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|  
  
 [返回以选择类型](#Select_Types)  
  
###  <a name="Copying"></a> 复制  
 可以将挖掘模型及其关联的挖掘结构复制到新模型中，然后在语句中重命名模型。  
  
|查询类型|Description|  
|----------------|-----------------|  
|SELECT INTO *\<新模型 >*|创建挖掘模型的副本。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [选择到&AMP;#40;DMX&AMP;#41;](../dmx/select-into-dmx.md)|  
  
 [返回以选择类型](#Select_Types)  
  
###  <a name="Drillthrough"></a> 钻取  
 通过使用下列查询类型，可以浏览用于为模型定型的事例或事例的表示形式。  
  
|查询类型|Description|  
|----------------|-----------------|  
|SELECT FROM *\<模型 >*。用例|返回用于为挖掘模型定型的事例。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [创建使用 DMX 的钻取查询](../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)|  
|SELECT FROM *\<模型 >*。SAMPLE_CASES|返回一个示例事例，该事例代表用于为挖掘模型定型的事例。<br /><br /> 该查询类型的域是内容架构行集。<br /><br /> [SELECT FROM&#60;模型&#62;。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|SELECT FROM *\<结构 >*。 用例|从基础挖掘结构返回详细数据行，即使某些详细信息并未用于对该挖掘模型定型。<br /><br /> [SELECT FROM&#60;结构&#62;。用例](../dmx/select-from-structure-cases.md)<br /><br /> [钻取查询 & #40; 数据挖掘 & #41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)|  
  
 [返回以选择类型](#Select_Types)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 & #40; DMX & #41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 & #40; DMX & #41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
