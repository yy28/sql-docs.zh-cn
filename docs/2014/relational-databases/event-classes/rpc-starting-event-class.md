---
title: RPC:Starting 事件类 | Microsoft Docs
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
- RPC:Starting event class
ms.assetid: 1d5c3e53-0104-41f7-ab8b-732462d859f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a162dc259e79c9704e30f251ce72c5f9c221601a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209167"
---
# <a name="rpcstarting-event-class"></a>RPC:Starting 事件类
  RPC:Starting 事件类指示远程过程调用已启动。  
  
## <a name="rpcstarting-event-class-data-columns"></a>RPC:Starting 事件类的数据列  
  
|数据列名称|`Data type`|Description|列 ID|可筛选|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|BinaryData|`image`|与在跟踪中捕获的事件类相关的二进制值。|2|用户帐户控制|  
|ClientProcessID|`int`|主机为运行该客户端应用程序的进程分配的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|用户帐户控制|  
|DatabaseID|`int`|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在跟踪中捕获 ServerName 数据列而且服务器可用，则将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|DatabaseName|`nvarchar`|正在其中运行用户语句的数据库的名称。|35|用户帐户控制|  
|EventClass|`int`|事件类型 = 11。|27|否|  
|EventSequence|`int`|给定事件在请求中的顺序。|51|否|  
|GroupID|`int`|在其中激发 SQL 跟踪事件的工作负荷组的 ID。|66|用户帐户控制|  
|HostName|`nvarchar`|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|IsSystem|`int`|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|LoginName|`nvarchar`|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|用户帐户控制|  
|LoginSid|`image`|登录用户的安全标识号 (SID)。 您可以在 sys.server_principals 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|NTDomainName|`nvarchar`|用户所属的 Windows 域。|7|用户帐户控制|  
|NTUserName|`nvarchar`|Windows 用户名。|6|用户帐户控制|  
|ObjectName|`nvarchar`|引用的对象名。|34|用户帐户控制|  
|RequestID|`int`|包含该语句的请求的 ID。|49|用户帐户控制|  
|ssSqlProfiler|`nvarchar`|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|SessionLoginName|`nvarchar`|发起会话的用户的登录名。 例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 SessionLoginName 将显示 Login1，而 LoginName 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|用户帐户控制|  
|SPID|`int`|发生该事件的会话的 ID。|12|用户帐户控制|  
|StartTime|`datetime`|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|TextData|`ntext`|远程过程调用的文本。|1|用户帐户控制|  
|TransactionID|`bigint`|系统分配的事务 ID。|4|用户帐户控制|  
|XactSequence|`bigint`|用于说明当前事务的标记。|50|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
