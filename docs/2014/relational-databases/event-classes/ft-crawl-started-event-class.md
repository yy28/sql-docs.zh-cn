---
title: FT:Crawl Started 事件类 | Microsoft Docs
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
- Crawl Started event class
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d5cbfb6d0ec7cf057d4bf3c7edbc6d1735dbc47
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203607"
---
# <a name="ftcrawl-started-event-class"></a>FT:Crawl Started 事件类
  **FT:Crawl Started** 事件类指示全文爬网（填充）已开始。 使用此事件类来检查工作线程任务是否正在实际拾取爬网请求。  
  
## <a name="ft-crawl-started-event-class-data-columns"></a>FT: Crawl Started 事件类的数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|启动了全文爬网的数据库 ID。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|**EventClass**|**int**|事件类型 = 155。|27|否|  
|**EventSequence**|**int**|给定事件在请求中的顺序。|51|否|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|**Exchange Spill**|**int**|系统分配的对象 ID。 对关于此对象的全文索引启动了全文爬网。|22|用户帐户控制|  
|**SessionLoginName**|**nvarchar**|发起会话的用户的登录名。 例如，如果你使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录名。|64|用户帐户控制|  
|**SPID**|**int**|发生该事件的会话的 ID。|12|用户帐户控制|  
|**StartTime**|**datetime**|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|**TextData**|**ntext**|全文爬网类型。 该值可以是“完整”、“增量”、“手动”或“自动”。|1|用户帐户控制|  
|**TransactionID**|**bigint**|系统分配的事务 ID。|4|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
