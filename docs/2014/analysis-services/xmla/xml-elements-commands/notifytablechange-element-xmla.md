---
title: NotifyTableChange 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NotifyTableChange Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25d060b73f7fb5999d4eb04faaa209eb7713f9d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224427"
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 元素 (XMLA)
  通知的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]到指定的数据源中的表发生更改。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../xml-elements-properties/object-element-xmla.md)， [TableNotifications](../xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `NotifyTableChange` 命令允许客户端应用程序显式通知 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例数据源中包含的一个或多个表发生了更改。 对于主动缓存，此通知指示应该查看并更新基于这些表的关系 OLAP (ROLAP) 对象。  
  
 这种通知方法最好使用 ROLAP 对象基于视图或命名查询中为其更改可能很难检测和跟踪的数据源视图定义。  
  
 `Object` 元素必须引用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库中的数据源。 如果 `Object` 元素引用对象而非数据源，则会发生错误。  
  
 有关主动缓存的详细信息，请参阅[主动缓存（分区）](../../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="see-also"></a>请参阅  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
