---
title: PreConnect:Starting 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ae1972bde3d0d13a608f4583e88e2b649ab82be3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024829"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting 事件类
  PreConnect:Starting事件类指示 LOGON 触发器或资源调控器分类器函数开始执行的时间。  
  
## <a name="preconnectstarting-event-class-data-columns"></a>PreConnect:Starting 事件类数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|“否”|  
|SPID|`int`|激发此事件的服务器进程的 ID。|12|是|  
|EventSubClass|`int`|1 表示用户定义的分类器函数。|21|是|  
|StartTime|`datetime`|用户定义的分类器函数开始时间。|14|是|  
|ObjectID|`int`|用户定义的分类器对象的 ID。|22|是|  
|ObjectName|`nvarchar(256)`|用户定义的分类器函数的两部分名称。 例如，dbo.classifier。|34|是|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../extended-events/extended-events.md)   
 [PreConnect:Completed 事件类](preconnect-completed-event-class.md)   
 [资源调控器](../resource-governor/resource-governor.md)  
  
  