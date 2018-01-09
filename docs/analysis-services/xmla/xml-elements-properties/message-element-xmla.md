---
title: "消息元素 (XMLA) |Microsoft 文档"
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
apiname: Message Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords: Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4bc4844a7187448bb9d44b47aee4d6c1bef8509d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="message-element-xmla"></a>Message 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含从实例返回一条消息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]通过[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Messages>  
   ...  
   <Message>  
      <Error>...</Error>  
      <!-- or -->  
      <Warning>...</Warning>  
   </Message>  
   ...  
</Messages>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[消息](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|子元素|[错误](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)，[警告](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 在 **Discover** 方法调用中的单个 XMLA 命令或 **Execute** 方法调用成功完成，但是带有错误或警告的情况下使用此元素。 在这种情况下，**消息**元素添加到的根元素后所有其他元素，后者又包含一个或多个**消息**元素。 每个**消息**元素表示单个消息，出现错误或警告，由[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
