---
title: SP:Starting 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:Starting event class
ms.assetid: ef55e579-080d-4650-a7fc-4dd03ed8e391
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 252370327d85401acb6142c2253750535dc080b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693575"
---
# <a name="spstarting-event-class"></a>SP:Starting 事件类
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SP:Starting 事件类指示存储过程将要开始执行。  
  
## <a name="spstarting-event-class-data-columns"></a>SP:Starting 事件类的数据列  
  
|数据列名称|数据类型|描述|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|ClientProcessID|**int**|主机为运行该客户端应用程序的进程分配的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|用户帐户控制|  
|DatabaseID|**int**|正在运行存储过程的数据库的 ID。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|DatabaseName|**nvarchar**|正在运行存储过程的数据库的名称。|35|用户帐户控制|  
|EventClass|**int**|事件类型 = 42。|27|否|  
|EventSequence|**int**|给定事件在请求中的顺序。|51|否|  
|GroupID|**int**|在其中激发 SQL 跟踪事件的工作负荷组的 ID。|66|用户帐户控制|  
|HostName|**nvarchar**|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|IsSystem|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|LineNumber|**int**|显示调用此存储过程的 execute 语句的行号。|5|用户帐户控制|  
|LoginName|**nvarchar**|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|用户帐户控制|  
|LoginSid|**图像**|登录用户的安全标识号 (SID)。 您可以在 sys.server_principals 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|NestLevel|**int**|存储过程的嵌套级别。|29|用户帐户控制|  
|NTDomainName|**nvarchar**|用户所属的 Windows 域。|7|用户帐户控制|  
|NTUserName|**nvarchar**|Windows 用户名。|6|用户帐户控制|  
|ObjectID|**int**|系统分配的存储过程 ID。|22|用户帐户控制|  
|ObjectName|**nvarchar**|将要开始的存储过程的名称。|34|用户帐户控制|  
|ObjectType|**int**|将要开始的存储过程的类型。 此值对应于 sys.objects 目录视图中的类型列。 有关值的信息，请参阅 [ObjectType 跟踪事件列](../../relational-databases/event-classes/objecttype-trace-event-column.md)。|28|用户帐户控制|  
|RequestID|**int**|包含该语句的请求的 ID。|49|用户帐户控制|  
|ServerName|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|SessionLoginName|**nvarchar**|发起会话的用户的登录名。 例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 SessionLoginName 将显示 Login1，而 LoginName 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|用户帐户控制|  
|SourceDatabaseID|**int**|对象所在数据库的 ID。|62|用户帐户控制|  
|SPID|**int**|发生该事件的会话的 ID。|12|用户帐户控制|  
|StartTime|**datetime**|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|TextData|**ntext**|过程调用的文本。|1|用户帐户控制|  
|TransactionID|**bigint**|系统分配的事务 ID。|4|用户帐户控制|  
|XactSequence|**bigint**|用于说明当前事务的标记。|50|用户帐户控制|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
