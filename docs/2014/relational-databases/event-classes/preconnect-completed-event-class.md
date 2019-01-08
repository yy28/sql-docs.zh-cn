---
title: PreConnect:Completed 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaad0a80fd77257c6e79e092733d75c0c8df5df5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52755979"
---
# <a name="preconnectcompleted-event-class"></a>PreConnect:Completed 事件类
  PreConnect:Completed 事件类指示何时 LOGON 触发器或资源调控器分类器函数结束执行。  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>PreConnect:Completed 事件类的数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|216|27|否|  
|SPID|`int`|激发此事件的服务器进程的 ID。|12|用户帐户控制|  
|EventSubClass|`int`|1 表示用户定义的分类器函数。|21|用户帐户控制|  
|StartTime|`datetime`|用户定义的分类器函数开始时间。|14|用户帐户控制|  
|EndTime|`datetime`|用户定义的分类器函数开始时间。|15|用户帐户控制|  
|Duration|`bigint`|分类器函数所用的时间，以微秒为单位。|13|用户帐户控制|  
|ObjectID|`int`|用户定义的分类器对象的 ID。|22|用户帐户控制|  
|CPU|`int`|CPU 使用率，以毫秒为单位。|18|用户帐户控制|  
|Reads|`int`|逻辑读取数。|16|用户帐户控制|  
|Writes|`int`|逻辑写入数。|17|用户帐户控制|  
|GroupID|`int`|分类工作负荷组的 ID。|66|用户帐户控制|  
|错误|`int`|如果用户定义的分类器函数无法执行，则为最后一个错误号。|31|用户帐户控制|  
|State|`int`|最后一个错误的状态。|30|用户帐户控制|  
|TargetUserName|`sysname`|如果系统无法找到相应的活动组，则为用户定义的分类器函数的返回值（工作负荷组名）。 否则，此列设为 NULL.|39|用户帐户控制|  
|ObjectName|`nvarchar(256)`|用户定义的分类器函数的两部分名称。 例如，dbo.classifier。|34|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../extended-events/extended-events.md)   
 [PreConnect:Starting 事件类](preconnect-starting-event-class.md)   
 [资源调控器](../resource-governor/resource-governor.md)  
  
  
