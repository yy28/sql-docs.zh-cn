---
title: TransactionLog 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TransactionLog event class
ms.assetid: bbcf09c6-3128-4775-b3de-e986a70411e0
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 2f68f588aa603e1ff022669a8e1bebd06f9b7c9b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533487"
---
# <a name="transactionlog-event-class"></a>TransactionLog 事件类
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 TransactionLog 事件类可以监视 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的事务日志中的活动。  
  
## <a name="transactionlog-event-class-data-columns"></a>TransactionLog 事件类的数据列  
  
|数据列名称|数据类型|描述|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|用户帐户控制|  
|BinaryData|**图像**|与在跟踪中捕获的事件类相关的二进制值。|2|用户帐户控制|  
|ClientProcessID|**int**|主机为运行该客户端应用程序的进程分配的 ID。 如果客户端提供客户端进程，则填充此数据列。|9|用户帐户控制|  
|DatabaseID|**int**|记录数据的数据库的 ID。|3|用户帐户控制|  
|DatabaseName|**nvarchar**|正在其中运行用户语句的数据库的名称。|35|用户帐户控制|  
|EventClass|**int**|事件类型 = 54。|27|否|  
|EventSequence|**int**|给定事件在请求中的顺序。|51|否|  
|EventSubClass|**int**|事件子类的类型。|21|用户帐户控制|  
|GroupID|**int**|在其中激发 SQL 跟踪事件的工作负荷组的 ID。|66|用户帐户控制|  
|HostName|**nvarchar**|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|IndexID|**int**|受事件影响的对象的索引的 ID。 若要确定对象的索引 ID，请使用 sys.indexes 目录视图的 index_id 列。|24|用户帐户控制|  
|IntegerData|**int**|与在跟踪中捕获的事件类相关的整型值。|25|用户帐户控制|  
|IsSystem|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|用户帐户控制|  
|LoginName|**nvarchar**|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|用户帐户控制|  
|LoginSid|**图像**|已登录的用户的安全标识符 (SID)。 您可以在 sys.server_principals 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|NTDomainName|**nvarchar**|用户所属的 Windows 域。|7|用户帐户控制|  
|NTUserName|**nvarchar**|Windows 用户名。|6|用户帐户控制|  
|ObjectID|**int**|系统分配的对象 ID。|22|用户帐户控制|  
|RequestID|**int**|包含该语句的请求的 ID。|49|用户帐户控制|  
|ServerName|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|SessionLoginName|**nvarchar**|发起会话的用户的登录名。 例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 SessionLoginName 将显示 Login1，而 LoginName 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|用户帐户控制|  
|SPID|**int**|发生该事件的会话的 ID。|12|用户帐户控制|  
|StartTime|**datetime**|该事件（如果存在）的启动时间。|14|用户帐户控制|  
|TransactionID|**bigint**|系统分配的事务 ID。|4|用户帐户控制|  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
