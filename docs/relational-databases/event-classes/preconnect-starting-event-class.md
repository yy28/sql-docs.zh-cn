---
title: PreConnect:Starting 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e040b5676b6e620705c076e1174f16f93b7d02b4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073298"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting 事件类
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  PreConnect:Starting事件类指示 LOGON 触发器或资源调控器分类器函数开始执行的时间。  
  
## <a name="preconnectstarting-event-class-data-columns"></a>PreConnect:Starting 事件类数据列  
  
|数据列名称|数据类型|描述|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|否|  
|SPID|**int**|激发此事件的服务器进程的 ID。|12|用户帐户控制|  
|EventSubClass|**int**|1 表示用户定义的分类器函数。|21|用户帐户控制|  
|StartTime|**datetime**|用户定义的分类器函数开始时间。|14|用户帐户控制|  
|ObjectID|**int**|用户定义的分类器对象的 ID。|22|用户帐户控制|  
|ObjectName|**nvarchar(256)**|用户定义的分类器函数的两部分名称。 例如，dbo.classifier。|34|用户帐户控制|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed 事件类](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)  
  
  
