---
title: 消息元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21bb83be0940b806c071f305d75826ab65330c15
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054194"
---
# <a name="messages-element-xmla"></a>Messages 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一系列[消息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)由 Analysis Services 的实例中返回元素[Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[结果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|子元素|[Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 在 **Discover** 方法调用中的单个 XMLA 命令或 **Execute** 方法调用成功完成，但是带有错误或警告的情况下使用此元素。 在这种情况下，**消息**元素添加到[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)元素后的所有其他元素，其中又包含一个或多个**消息**元素。 每个**消息**元素表示一个返回消息，出现错误或警告，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
