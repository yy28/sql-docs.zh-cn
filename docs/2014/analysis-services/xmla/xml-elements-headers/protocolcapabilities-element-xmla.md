---
title: ProtocolCapabilities 元素 (XMLA) |Microsoft Docs
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
- ProtocolCapabilities Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4183d90d07a54cf009daec59ca29ca802f2bf67
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295427"
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 元素 (XMLA)
  使用 SOAP 标头的 SOAP 请求消息中标识的实例之间的协议功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]和客户端应用程序。  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/engine  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[功能](../xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `ProtocolCapabilities` 元素可使客户端应用程序随时与 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例协商协议功能，如二进制 XML 或压缩支持。 协议协商包括以下步骤：  
  
1.  客户端应用程序通过发送包含的 SOAP 请求来标识其协议功能`ProtocolCapabilities`元素作为 SOAP 标头的一部分。  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例接收和处理 SOAP 请求。  
  
3.  如果 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例具有所请求的协议功能，则该实例将发送一个 SOAP 响应，该响应包含的 `ProtocolCapabilities` 元素与 SOAP 请求中发送的相同，此时协议协商成功。 否则，协议功能协商不成功，该实例返回 SOAP 错误。  
  
 在成功协商协议功能，多长时间客户端应用程序和[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，请使用特定协议取决于会话是显式或隐式：  
  
-   显式会话是指使用创建[BeginSession](session-element-xmla.md)标头元素。 对于显式会话，则使用协商的协议，直到客户端应用发送了一个新`ProtocolCapabilities`元素或会话结束。  
  
-   隐式会话是在提交 SOAP 请求时通过 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例创建的会话，并且不由客户端应用程序显式指定。 对于隐式会话，仅在 SOAP 请求完成之前使用协商的协议。  
  
 协议功能可以不显式协商。 也就是说，客户端应用程序不需要包括`ProtocolCapabilities`元素作为 SOAP 请求的一部分。 如果 SOAP 请求不包括 `ProtocolCapabilities` 元素，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例使用与 SOAP 请求相同的格式作出响应。  
  
## <a name="see-also"></a>请参阅  
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
