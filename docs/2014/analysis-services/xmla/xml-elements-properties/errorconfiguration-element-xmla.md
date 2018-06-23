---
title: ErrorConfiguration 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ErrorConfiguration Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorConfiguration
- urn:schemas-microsoft-com:xml-analysis#ErrorConfiguration
- microsoft.xml.analysis.errorconfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: 5e350f5f-3a14-49b4-80c0-208c61f336d5
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1ce9cf2dc862f187c1a9f9cb9e3403e01ade0cfa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027748"
---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 元素 (XMLA)
  指定有关的处理过程中可能出现的错误设置[批处理](../xml-elements-commands/batch-element-xmla.md)或[过程](../xml-elements-commands/process-element-xmla.md)操作。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Batch> <!-- or Process -->  
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
</Batch>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../xml-elements-commands/batch-element-xmla.md)，[过程](../xml-elements-commands/process-element-xmla.md)|  
|子元素|[KeyDuplicate](../../scripting/properties/keyduplicate-element-assl.md)， [KeyErrorAction](../../scripting/objects/action-element-assl.md)， [KeyErrorLimit](../../scripting/properties/keyerrorlimit-element-assl.md)， [KeyErrorLimitAction](../../scripting/properties/keyerrorlimitaction-element-assl.md)， [KeyErrorLogFile](../../scripting/objects/file-element-assl.md)， [KeyNotFound](../../scripting/properties/keynotfound-element-assl.md)， [NullKeyConvertedToUnknown](../../scripting/properties/nullkeyconvertedtounknown-element-assl.md)， [NullKeyNotAllowed](../../scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 此元素的结构与 Analysis Services 脚本语言 (ASSL) 中的 `ErrorConfiguration` 元素的结构相同。 有关详细信息`ErrorConfiguration`元素，请参阅[ErrorConfiguration 元素&#40;ASSL&#41;](../../scripting/objects/errorconfiguration-element-assl.md)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  