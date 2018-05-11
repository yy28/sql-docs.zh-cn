---
title: NotifyTableChange 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 125cea75f5c892cd30e3f346c0b755ab8de55ae5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  通知的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]到指定的数据源中的表已发生更改。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)， [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **NotifyTableChange**命令允许客户端的应用程序显式通知[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，其中一个或多个数据源中包含的表已更改。 对于主动缓存，此通知指示应该查看并更新基于这些表的关系 OLAP (ROLAP) 对象。  
  
 此方法通知最适用的 ROLAP 对象基于视图或命名查询定义为其更改可能很难检测和跟踪数据源视图中。  
  
 **对象**元素必须引用中的数据源[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 如果**对象**元素引用的对象以外的数据源，发生错误。  
  
 有关主动缓存的详细信息，请参阅[主动缓存（分区）](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="see-also"></a>另请参阅  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
