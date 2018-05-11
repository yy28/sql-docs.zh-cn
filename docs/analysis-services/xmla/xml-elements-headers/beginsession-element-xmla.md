---
title: BeginSession 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f369a963c287fd2bf1c2dc82a51bb285088c8b1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="beginsession-element-xmla"></a>BeginSession 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  使用在 SOAP 请求消息的 SOAP 标头的实例上启动新会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **BeginSession**标头元素是发送到的 SOAP 请求的一部分[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，并显式启动新会话的实例上。 SOAP 响应返回的 SOAP 标头包含[会话](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)标识新的会话的元素。 存储和后续使用的 SOAP 请求中发送此新的会话标识符**会话**标头元素。  
  
 如果**BeginSession**标头元素不会发送，尚未显式启动会话。 如果不显式启动会话，则将无法管理该会话上的事务。 换而言之，无法将以下 XML 用于 Analysis (XMLA) 命令： [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)。 显式启动的会话上执行的所有 XMLA 方法和命令均视为原子事务。  
  
## <a name="see-also"></a>另请参阅  
 [EndSession 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [会话元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [管理连接和会话 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
