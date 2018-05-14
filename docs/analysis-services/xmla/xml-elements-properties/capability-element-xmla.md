---
title: 功能元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 92e9fa83f19384276abd7401fd809a56187c75b7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="capability-element-xmla"></a>Capability 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指示支持的协议功能的父代中[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)标头元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **功能**元素指示包含的任一应用程序支持特定功能，如二进制或压缩， **ProtocolCapabilities**标头中的元素SOAP 标头的 SOAP 请求中，或由的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含**ProtocolCapabilities** SOAP 响应的 SOAP 标头中的标头元素。 值**功能**元素是支持的功能的名称。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持下表所列出的功能。  
  
|功能名称|Description|  
|---------------------|-----------------|  
|sx|二进制 XML 支持|  
|xpress|压缩支持|  
  
## <a name="see-also"></a>另请参阅  
 [管理连接和会话 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
