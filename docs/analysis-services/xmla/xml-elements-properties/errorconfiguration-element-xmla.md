---
title: ErrorConfiguration 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 488ace059e2dc7d3ec1d1ed09df3895147b48aec
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指定有关的处理过程中可能出现的错误设置[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)操作。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)，[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|[KeyDuplicate](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md)， [KeyErrorAction](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md)， [KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)， [KeyErrorLimitAction](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md)， [KeyErrorLogFile](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md)， [KeyNotFound](../../../analysis-services/scripting/properties/keynotfound-element-assl.md)， [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)， [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 此元素的结构是相同的结构**ErrorConfiguration**元素在 Analysis Services 脚本语言 (ASSL)。 有关详细信息**ErrorConfiguration**元素，请参阅[ErrorConfiguration 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
