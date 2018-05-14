---
title: EndSession 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d086e93de6030621356271582d8162e58fcabe4f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="endsession-element-xmla"></a>EndSession 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  使用在 SOAP 请求消息的 SOAP 标头来结束的实例上的现有会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>語法  
  
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
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|SessionId|所需**字符串**标识要结束的会话的属性。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用全局唯一标识符 (GUID) 识别会话。|  
  
## <a name="remarks"></a>注释  
 **EndSession**标头元素是向现有的显式启动会话发送的 SOAP 请求的一部分[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果**EndSession**标头元素，不会发送，但包含将不再有效的会话标识符、 SOAP 错误返回一个指示找不到该会话。  
  
## <a name="see-also"></a>另请参阅  
 [BeginSession 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [会话元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [管理连接和会话 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
