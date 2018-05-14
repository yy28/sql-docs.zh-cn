---
title: 消息元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90579f9204a263b4b2366e4b1eeab714676a4be7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="messages-element-xmla"></a>Messages 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一套[消息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)元素返回的实例从[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]通过[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
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
|父元素|[结果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|子元素|[消息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 在 **Discover** 方法调用中的单个 XMLA 命令或 **Execute** 方法调用成功完成，但是带有错误或警告的情况下使用此元素。 在这种情况下，**消息**元素添加到[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)所有其他元素之后, 的元素，后者又包含一个或多个**消息**元素。 每个**消息**元素表示单个消息，出现错误或警告，由[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
