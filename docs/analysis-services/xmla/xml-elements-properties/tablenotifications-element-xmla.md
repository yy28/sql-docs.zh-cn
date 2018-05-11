---
title: TableNotifications 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 494652445c37b296d2cb4ad6e1cc3d40e78bff48
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tablenotifications-element-xmla"></a>TableNotifications 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一套[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)所使用的元素[NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<NotifyTableChange >  
   ...  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
   </TableNotifications>  
   ...  
</NotifyTableChange>  
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
|父元素|[NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|  
|子元素|[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
