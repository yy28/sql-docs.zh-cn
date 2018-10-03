---
title: AlgorithmParameter 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AlgorithmParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AlgorithmParameter
helpviewer_keywords:
- AlgorithmParameter element
ms.assetid: 73211495-065c-43c6-a486-be6044617263
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8eb25678d58f676ee10ef488b376c8331c59e15
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109957"
---
# <a name="algorithmparameter-element-assl"></a>AlgorithmParameter 元素 (ASSL)
  定义了一个参数使用的算法[MiningModel](miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AlgorithmParameters>  
   <AlgorithmParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </AlgorithmParameter>  
</AlgorithmParameters>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AlgorithmParameters](../collections/algorithmparameters-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 `AlgorithmParameter` 是挖掘模型算法的参数。 `AlgorithmParameter` 将此参数表示为名称/值对。 `AlgorithmParameter` 可表示的适用参数集依算法而定。 有关给定算法的算法参数的详细信息，请参阅该算法的相应文档。  
  
 可用算法参数，包括验证和显示信息可以从检索[DMSCHEMA_MINING_SERVICE_PARAMETERS](../../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)架构行集。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AlgorithmParameter>。  
  
## <a name="see-also"></a>请参阅  
 [MiningModel 元素&#40;ASSL&#41;](miningmodel-element-assl.md)   
 [Algorithm 元素&#40;ASSL&#41;](../properties/algorithm-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
