---
title: "会话元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Session Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords: Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c033153f19ce1456b0558a95a85ad6caab778be5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="session-element-xmla"></a>Session 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]使用在 SOAP 请求消息的 SOAP 标头来标识实例上的现有的显式会话[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|SessionId|所需**字符串**标识要使用的会话的属性。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用全局唯一标识符 (GUID) 识别会话。|  
  
## <a name="remarks"></a>Remarks  
 **会话**标头元素标识的现有的显式启动的会话上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 **会话**元素是在以下类型的消息的 SOAP 标头的一部分：  
  
-   包含的 SOAP 响应[BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) SOAP 标头元素。  
  
-   SOAP 请求来标识在其上运行会话[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
 会话标识符并不保证会话保持有效。 在指定的会话**会话**元素可能会过期。 例如，如果会话超时或与会话相关联的连接断开，则该会话将过期。 如果会话过期并且不再有效，则 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将结束该会话并回滚当前正在处理的所有事务。 使用不再有效的会话标识符发送的任何 SOAP 消息将失败，相应 SOAP 错误指示找不到指定的会话。  
  
 如果**会话**元素不会发送 SOAP 请求的一部分[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例隐式开始的会话的持续时间**发现**或**执行**方法调用，然后结束完成方法调用后该会话。  
  
## <a name="see-also"></a>另请参阅  
 [EndSession 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [管理连接和会话 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [标头 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
