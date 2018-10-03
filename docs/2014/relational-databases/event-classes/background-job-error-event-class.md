---
title: Background Job Error 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d997265cd0e6ac0f471376c68bc7525c7ce7a5ad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198567"
---
# <a name="background-job-error-event-class"></a>Background Job Error 事件类
  当后台作业异常终止时，会发生 **Background Job Error** 事件类。 这种情况可能需要引起系统管理员的注意。  
  
## <a name="background-job-error-event-class-data-columns"></a>Background Job Error 事件类的数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|作业指定的数据库的 ID。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|**DatabaseName**|**nvarchar**|正在其中运行用户语句的数据库的名称。|35|用户帐户控制|  
|**错误**|**int**|上次尝试使用的错误号（仅限**EventSubClass** 1）。|31|用户帐户控制|  
|**EventClass**|**int**|事件类型 = 193。|27|否|  
|**EventSequence**|**int**|特定事件在请求中的顺序。|51|否|  
|**EventSubClass**|**int**|事件子类的类型。<br /><br /> 1 = 失败之后放弃的后台作业。<br /><br /> 2 = 已删除的后台作业 - 队列已满。<br /><br /> 3 = 返回一个错误的后台作业。|21|用户帐户控制|  
|**IndexID**|**int**|受事件影响的对象的索引的 ID。 若要确定对象的索引的 ID，请使用 **sysindexes** 系统表的 **indid** 列。|24|用户帐户控制|  
|**IntegerData**|**int**|作业尝试的次数（仅限**EventSubClass** 1）。|25|用户帐户控制|  
|**IntegerData2**|**int**|作业序列号。|55|用户帐户控制|  
|**Exchange Spill**|**int**|系统分配的对象 ID。|22|用户帐户控制|  
|**SessionLoginName**|**nvarchar**|发起会话的用户的登录名。 例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录名。|64|用户帐户控制|  
|**Severity**|**int**|上次尝试中出现的错误的严重级别（仅限**EventSubClass** 1）。|20|用户帐户控制|  
|**StartTime**|**datetime**|创建作业的时间。|14|用户帐户控制|  
|**State**|**int**|上次尝试中出现的错误状态（仅限**EventSubClass** 1）。|30|用户帐户控制|  
|**TextData**|**ntext**|事件子类值的文本说明。|1|用户帐户控制|  
|**类型**|**int**|作业类型。|57|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../extended-events/extended-events.md)   
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Auto Stats 事件类](auto-stats-event-class.md)  
  
  
