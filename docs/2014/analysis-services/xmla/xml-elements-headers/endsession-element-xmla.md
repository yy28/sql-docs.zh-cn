---
title: EndSession 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EndSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EndSession
- urn:schemas-microsoft-com:xml-analysis#EndSession
- microsoft.xml.analysis.endsession
helpviewer_keywords:
- EndSession element
ms.assetid: e64f1da4-5c83-40a2-b15e-837f5451bafa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 806b1dea9aeb9a4598b9516f8e7a953962307e65
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096897"
---
# <a name="endsession-element-xmla"></a>EndSession 元素 (XMLA)
  使用 SOAP 请求消息中的 SOAP 标头结束现有会话的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <EndSession  
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
|SessionId|标识要结束的会话的必需的 `String` 属性。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用全局唯一标识符 (GUID) 识别会话。|  
  
## <a name="remarks"></a>备注  
 `EndSession` 标头元素是发送到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例上的现有显式启动的会话的 SOAP 请求的一部分。 如果已发送 `EndSession` 标头元素，但是该元素包含一个不再有效的会话标识符，将返回一个指示不能找到该会话的 SOAP 错误。  
  
## <a name="see-also"></a>请参阅  
 [BeginSession 元素&#40;XMLA&#41;](session-element-xmla.md)   
 [Session 元素&#40;XMLA&#41;](session-element-xmla.md)   
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
