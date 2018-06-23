---
title: 会话元素 (XMLA) |Microsoft 文档
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
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4be4778be16da0271e2f46643a165864d679e8ff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027995"
---
# <a name="session-element-xmla"></a>Session 元素 (XMLA)
  使用在 SOAP 请求消息的 SOAP 标头来标识实例上的现有的显式会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|InclusionThresholdSetting|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|SessionId|标识要使用的会话的必需的 `String` 属性。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用全局唯一标识符 (GUID) 识别会话。|  
  
## <a name="remarks"></a>Remarks  
 `Session` 标头元素标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有显式启动的会话。 `Session` 元素是以下消息类型中的 SOAP 标头的一部分：  
  
-   包含的 SOAP 响应[BeginSession](session-element-xmla.md) SOAP 标头元素。  
  
-   SOAP 请求来标识在其上运行会话[发现](../xml-elements-methods-discover.md)或[执行](../xml-elements-methods-execute.md)方法。  
  
 会话标识符并不保证会话保持有效。 `Session` 元素中指定的会话会过期。 例如，如果会话超时或与会话相关联的连接断开，则该会话将过期。 如果会话过期并且不再有效，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将结束该会话并回滚当前正在处理的所有事务。 使用不再有效的会话标识符发送的任何 SOAP 消息将失败，相应 SOAP 错误指示找不到指定的会话。  
  
 如果没有将 `Session` 元素作为 SOAP 请求的一部分发送，则在 `Discover` 或 `Execute` 方法调用期间，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例将隐式开始一个会话，然后在方法调用完成后结束该会话。  
  
## <a name="see-also"></a>请参阅  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头&#40;XMLA&#41;](xml-elements-headers.md)  
  
  