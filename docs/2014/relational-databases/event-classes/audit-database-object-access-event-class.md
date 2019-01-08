---
title: Audit Database Object Access 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Database Object Access event class
ms.assetid: 0294ba51-6085-4de2-a52d-dac1a87fbd4d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 62a6b3a1f92723d43fde32060c6d4ccbbfc14a98
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52798829"
---
# <a name="audit-database-object-access-event-class"></a>Audit Database Object Access 事件类
  在访问数据库对象（如架构）时，会发生 **Audit Database Object Access** 事件类。  
  
## <a name="audit-database-object-access-event-class-data-columns"></a>Audit Database Object Access 事件类的数据列  
  
|数据列名称|数据类型|Description|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|**DatabaseName**|**nvarchar**|正在其中运行用户语句的数据库的名称。|35|用户帐户控制|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户名。|40|用户帐户控制|  
|**EventSequence**|**int**|给定事件在请求中的顺序。|51|否|  
|**HostName**|**nvarchar**|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|**LoginName**|**nvarchar**|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|用户帐户控制|  
|**LoginSid**|**image**|登录用户的安全标识号 (SID)。 你可以在 **sys.server_principals** 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|用户帐户控制|  
|**NTUserName**|**nvarchar**|Windows 用户名。|6|用户帐户控制|  
|**ObjectName**|**nvarchar**|引用的对象名。|34|用户帐户控制|  
|**ObjectType**|**int**|表示事件中涉及的对象类型的值。 此值对应于 **sys.objects** 目录视图中的类型列。 有关值的信息，请参阅 [ObjectType 跟踪事件列](objecttype-trace-event-column.md)。|28|用户帐户控制|  
|**OwnerName**|**nvarchar**|对象所有者的数据库用户名。|37|用户帐户控制|  
|**权限**|**bigint**|表示所检查的权限类型的整型值。<br /><br /> 1 = SELECT ALL<br /><br /> 2 = UPDATE ALL<br /><br /> 4 = REFERENCES ALL<br /><br /> 8 = INSERT<br /><br /> 16 = DELETE<br /><br /> 32 = EXECUTE（仅限于过程）|19|用户帐户控制|  
|**RequestID**|**int**|包含该语句的请求的 ID。|49|用户帐户控制|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SessionLoginName**|**nvarchar**|发起会话的用户的登录名。 例如，如果你使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|用户帐户控制|  
|**SPID**|**int**|发生该事件的会话的 ID。|12|用户帐户控制|  
|**StartTime**|**datetime**|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|**成功**|**int**|1 = 成功。 0 = 失败。 例如，值为 1 时表示权限检查成功；值为 0 时表示权限检查失败。|23|用户帐户控制|  
|**TextData**|**ntext**|依赖于跟踪中捕获的事件类的文本值。|1|用户帐户控制|  
|**TransactionID**|**bigint**|系统分配的事务 ID。|4|用户帐户控制|  
|**XactSequence**|**bigint**|用于说明当前事务的标记。|50|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
