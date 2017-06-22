---
title: "Broker:Message Classify 事件类 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2bf30690ffcd48df2aedf00bad6c1124c0a555f0
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify 事件类
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将生成 **Broker:Message Classify** 事件。  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Broker:Message Classify 事件类的数据列  
  
|数据列|数据类型|说明|列号|可筛选|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|是|  
|**ClientProcessID**|**int**|由主机分配给正在运行客户端应用程序的进程的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|是|  
|**EventClass**|**int**|捕获的事件类的类型。 **Broker:Message Classify** 始终为 **141**。|27|是|  
|**EventSequence**|**int**|此事件的序列号。|51|是|  
|**EventSubClass**|**nvarchar**|事件子类的类型，提供有关每个事件类的进一步信息。 此列可能包含以下值：<br /><br /> **Local**：所选路由具有 LOCAL 地址。<br /><br /> **Remote**：所选路由具有非 LOCAL 地址。<br /><br /> **Delayed**：由于禁止转发或者没有出现匹配的路由，因此消息被延迟。|21|是|  
|**FileName**|**nvarchar**|消息定向到的服务名称。|36|是|  
|**GUID**|**uniqueidentifier**|对话的会话 ID。 此标识符将作为消息的一部分进行传输，并在会话双方之间共享。|54|是|  
|**HostName**|**nvarchar**|正在运行客户端程序的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|是|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|是|  
|**LoginSid**|**图像**|已登录用户的安全标识号 (SID)。 服务器中的每个登录名都具有唯一的 SID。|41|是|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|是|  
|**NTUserName**|**nvarchar**|拥有生成此事件的连接的用户的名称。|6|是|  
|**OwnerName**|**nvarchar**|消息要定向到的 Broker 标识符。|37|是|  
|**RoleName**|**nvarchar**|指明该消息是从网络中收到的，还是在此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中产生的。|38|是|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|是|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为客户端所关联的进程分配的服务器进程 ID。|12|是|  
|**Start Time**|**datetime**|事件（如果有）的开始时间。|14|是|  
|**TargetUserName**|**nvarchar**|下一个跃点中介器的网络地址。|39|是|  
|**TransactionID**|**bigint**|系统为事务分配的 ID。|4|是|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
