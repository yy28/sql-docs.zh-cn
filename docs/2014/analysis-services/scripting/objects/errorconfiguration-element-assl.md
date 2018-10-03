---
title: ErrorConfiguration 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ErrorConfiguration Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ErrorConfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: e8363ec2-fbbf-48f6-a55d-01793afa759c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 07b55794f3e5de70d4f515ed8f905e02a04787ee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225042"
---
# <a name="errorconfiguration-element-assl"></a>ErrorConfiguration 元素 (ASSL)
  指定在处理父元素时可能出现的错误的处理设置。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningStructure, Partition -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Cube >  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](cube-element-assl.md)，[维度](dimension-element-assl.md)， [MeasureGroup](group-element-assl.md)， [MiningStructure](miningstructure-element-assl.md)，[分区](partition-element-assl.md)|  
|子元素|[KeyDuplicate](../properties/keyduplicate-element-assl.md)， [KeyErrorAction](action-element-assl.md)， [KeyErrorLimit](../properties/keyerrorlimit-element-assl.md)， [KeyErrorLimitAction](../properties/keyerrorlimitaction-element-assl.md)， [KeyErrorLogFile](file-element-assl.md)， [KeyNotFound](../properties/keynotfound-element-assl.md)， [NullKeyConvertedToUnknown](../properties/nullkeyconvertedtounknown-element-assl.md)， [NullKeyNotAllowed](../properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ErrorConfiguration>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
