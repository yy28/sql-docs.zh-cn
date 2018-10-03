---
title: Session 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Session Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2f18754a2ef7d44a2a85bb9da78378bc631ecd0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080387"
---
# <a name="session-element-xmla"></a>Session 元素 (XMLA)
  使用 SOAP 标头的 SOAP 请求消息中标识的实例上的现有显式会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|SessionId|标识要使用的会话的必需的 `String` 属性。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用全局唯一标识符 (GUID) 识别会话。|  
  
## <a name="remarks"></a>备注  
 `Session` 标头元素标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有显式启动的会话。 `Session` 元素是以下消息类型中的 SOAP 标头的一部分：  
  
-   SOAP 响应，其中包含[BeginSession](session-element-xmla.md) SOAP 标头元素。  
  
-   SOAP 请求来标识在其上运行的会话[Discover](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法。  
  
 会话标识符并不保证会话保持有效。 `Session` 元素中指定的会话会过期。 例如，如果会话超时或与会话相关联的连接断开，则该会话将过期。 如果会话过期并且不再有效，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将结束该会话并回滚当前正在处理的所有事务。 使用不再有效的会话标识符发送的任何 SOAP 消息将失败，相应 SOAP 错误指示找不到指定的会话。  
  
 如果没有将 `Session` 元素作为 SOAP 请求的一部分发送，则在 `Discover` 或 `Execute` 方法调用期间，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例将隐式开始一个会话，然后在方法调用完成后结束该会话。  
  
## <a name="see-also"></a>请参阅  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
