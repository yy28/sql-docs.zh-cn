---
title: Audit Add Role 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Add Role event class
ms.assetid: 4ea55922-608c-4db2-8b3f-873862755bba
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5db5acd9d3c883b03a5565c56220a4229a2eb1e8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43089996"
---
# <a name="audit-add-role-event-class"></a>Audit Add Role 事件类
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  当向数据库中添加角色或从中删除角色时，将发生 **Audit Add Role** 事件类。 此事件类用于 **sp_addrole** 和 **sp_droprole** 存储过程。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未来版本中可能会删除此事件类。 建议使用 **Audit Database Principal Management** 事件类。  
  
## <a name="audit-add-role-event-class-data-columns"></a>Audit Add Role 事件类的数据列  
  
|数据列名称|数据类型|描述|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|**ClientProcessID**|**int**|主机为运行该客户端应用程序的进程分配的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|用户帐户控制|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|**DatabaseName**|**nvarchar**|正在其中运行用户语句的数据库的名称。|35|用户帐户控制|  
|**DBUserName**|**nvarchar**|颁发者在数据库中的用户名。|40|用户帐户控制|  
|**EventClass**|**int**|事件类型 = 111。|27|否|  
|**EventSequence**|**int**|给定事件在请求中的顺序。|51|否|  
|**EventSubClass**|**int**|事件子类的类型。<br /><br /> 1 = 添加<br /><br /> 2 = 删除|21|用户帐户控制|  
|**HostName**|**nvarchar**|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|**LoginName**|**nvarchar**|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|用户帐户控制|  
|**LoginSid**|**图像**|登录用户的安全标识号 (SID)。 你可以在 **sys.server_principals** 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|用户帐户控制|  
|**NTUserName**|**nvarchar**|Windows 用户名。|6|用户帐户控制|  
|**RequestID**|**int**|包含该语句的请求的 ID。|49|用户帐户控制|  
|**RoleName**|**nvarchar**|添加或删除的数据库角色的名称。|38|用户帐户控制|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SessionLoginName**|**Nvarchar**|发起会话的用户的登录名。 例如，如果你使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|用户帐户控制|  
|**SPID**|**int**|发生该事件的会话的 ID。|12|用户帐户控制|  
|**StartTime**|**datetime**|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|**成功**|**int**|1 = 成功。 0 = 失败。 例如，值为 1 时表示权限检查成功；值为 0 时表示权限检查失败。|23|用户帐户控制|  
|**TransactionID**|**bigint**|系统分配的事务 ID。|4|用户帐户控制|  
|**XactSequence**|**bigint**|用于说明当前事务的标记。|50|用户帐户控制|  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_addrole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [sp_droprole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [Audit Database Principal Management 事件类](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)  
  
  
