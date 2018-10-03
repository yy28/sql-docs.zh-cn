---
title: Algorithm 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Algorithm Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb2ab30f6abd753f0c954ef41ad26d0af9dcda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149777"
---
# <a name="algorithm-element-assl"></a>Algorithm 元素 (ASSL)
  定义使用的算法[MiningModel](../objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModel](../objects/miningmodel-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Algorithm` 元素的值为标识算法的字符串。 例如，该字符串可为*Microsoft_Naive_Bayes*， *Microsoft_Decision_Trees*，或*Microsoft_Clustering。* 该字符串标识由提供的算法[!INCLUDE[msCoName](../../../includes/msconame-md.md)]和自定义算法的用户提供的。 可用值`Algorithm`元素可以从的 SERVICE_NAME 列检索[DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md)架构行集。  
  
 父级对应的元素`Algorithm`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MiningModel>。 在 AMO 对象模型中，紧密相关的元素为 <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>。  
  
## <a name="see-also"></a>请参阅  
 [AlgorithmParameter 元素&#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters 元素&#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
