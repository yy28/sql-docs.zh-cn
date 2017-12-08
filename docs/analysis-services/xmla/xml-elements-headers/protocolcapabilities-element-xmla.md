---
title: "ProtocolCapabilities 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ProtocolCapabilities Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords: ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 42ff93dce6b71f7cfd69ed85d92c4c4f7912faee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 元素 (XMLA)
  使用在 SOAP 请求消息的 SOAP 标头来标识的实例之间的协议功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]和客户端应用程序。  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/engine`  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
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
|父元素|无|  
|子元素|[功能](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **ProtocolCapabilities**元素使客户端应用程序可以与协商协议功能，如二进制 XML 或压缩支持[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]在任何时候的实例。 协议协商包括以下步骤：  
  
1.  客户端应用程序通过发送在 SOAP 标头中包含 **ProtocolCapabilities** 元素的 SOAP 请求来标识其协议功能。  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例接收和处理 SOAP 请求。  
  
3.  如果[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例具有同样的协议功能作为请求，该实例发送包含相同的 SOAP 响应**ProtocolCapabilities**元素发送在 SOAP 请求中，并且已被协议已成功协商。 否则，协议功能协商不成功，该实例返回 SOAP 错误。  
  
 后成功协商协议功能，多长时间客户端应用程序和[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，请使用特定协议取决于会话是否显式或隐式：  
  
-   显式会话是指使用创建[BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)标头元素。 对于显式会话，在客户端应用程序发送新的 **ProtocolCapabilities** 元素或会话结束之前一直使用协商的协议。  
  
-   隐式会话是在提交 SOAP 请求时通过 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例创建的会话，并且不由客户端应用程序显式指定。 对于隐式会话，仅在 SOAP 请求完成之前使用协商的协议。  
  
 协议功能可以不显式协商。 即客户端应用程序不必在 SOAP 请求中包含 **ProtocolCapabilities** 元素。 如果 SOAP 请求不包括**ProtocolCapabilities**元素，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例响应 SOAP 请求为使用相同的格式。  
  
## <a name="see-also"></a>另请参阅  
 [管理连接和会话 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
