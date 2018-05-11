---
title: SPID 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2c665e40334710a631d10e236b26360a87277de
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="spid-element-xmla"></a>SPID 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  标识对其执行父活动服务器进程标识符 (SPID)[取消](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[取消](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **SPID**元素表示服务器进程 ID (SPID) 用于指定会话的实例上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [CancelAssociated 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)   
 [ConnectionID 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
