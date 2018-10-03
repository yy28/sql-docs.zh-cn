---
title: BeginSession 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BeginSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9194333e376dc8ab685057847c3f4156330d5dfa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180057"
---
# <a name="beginsession-element-xmla"></a>BeginSession 元素 (XMLA)
  使用 SOAP 请求消息中的 SOAP 标头的实例上启动新会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
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
  
## <a name="remarks"></a>备注  
 `BeginSession` 标头元素是发送到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的 SOAP 请求的一部分，可在该实例上显式启动新会话。 返回的 SOAP 响应的 SOAP 标头包含[会话](session-element-xmla.md)标识新会话的元素。 可以通过使用 `Session` 标头元素，将该新会话标识符存储到后续 SOAP 请求中，并发送该标识符。  
  
 如果不发送 `BeginSession` 标头，则不会显式启动会话。 如果不显式启动会话，则将无法管理该会话上的事务。 换而言之，不能使用以下 XML for Analysis (XMLA) 命令： [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md)，并[RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)。 显式启动的会话上执行的所有 XMLA 方法和命令均视为原子事务。  
  
## <a name="see-also"></a>请参阅  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [Session 元素&#40;XMLA&#41;](session-element-xmla.md)   
 [管理连接和会话&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
