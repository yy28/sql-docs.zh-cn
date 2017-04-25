---
title: "Broker:Message Drop 事件类 | Microsoft Docs"
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
- Broker:Message Drop event class
ms.assetid: f532b7c9-ca34-4bac-8dc3-53f9895fd6af
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 47fd82b02e3d808d2609e5c9830099d11627795f
ms.lasthandoff: 04/11/2017

---
# <a name="brokermessage-drop-event-class"></a>Broker:Message Drop 事件类
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成 **Broker:Message Drop** 事件。 对于应转发的消息，请参阅 [Broker:Forwarded Message Dropped 事件类](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)。  
  
## <a name="brokermessage-drop-event-class-data-columns"></a>Broker:Message Drop 事件类的数据列  
  
|数据列|类型|说明|列号|可筛选|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**应用程序名称**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|是|  
|**BigintData1**|**bigint**|已删除消息的序列号。|52|是|  
|**BigintData2**|**bigint**|成功确认的最后一条消息的序列号。|53|是|  
|**ClientProcessID**|**int**|由主机分配给正在运行客户端应用程序的进程的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|是|  
|**错误**|**int**|事件中文本的 **sys.messages** 的消息 ID 号。|31|是|  
|**EventClass**|**int**|捕获的事件类的类型。 对于 **Broker:MessageDrop** 始终为 **160**。|27|是|  
|**EventSequence**|**int**|此事件的序列号。|51|是|  
|**EventSubClass**|**nvarchar**|指明已删除的消息是否为已编序的消息。 两个值之一：<br /><br /> **已编序的消息**。 已删除的消息是已编序的消息。<br /><br /> **未编序的消息**。 已删除的消息不是已编序的消息。|21|是|  
|**GUID**|**uniqueidentifier**|已删除的消息所属的会话 ID。 此标识符将作为消息的一部分进行传输，并在会话双方之间共享。|54|是|  
|**HostName**|**nvarchar**|正在运行客户端程序的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|是|  
|**IntegerData**|**int**|已删除消息的片段数。|25|是|  
|**IntegerData2**|**int**|正在确认的已删除消息的片段数。|55|是|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|是|  
|**LoginName**|**nvarchar**|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录或 Windows 登录凭据，格式为域\用户名）。|11|是|  
|**LoginSid**|**图像**|已登录用户的安全标识号 (SID)。 服务器中的每个登录名都具有唯一的 SID。|41|是|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|是|  
|**NTUserName**|**nvarchar**|拥有生成此事件的连接的用户的名称。|6|是|  
|**ObjectName**|**nvarchar**|对话的会话句柄。|34|是|  
|**RoleName**|**nvarchar**|会话句柄的角色。 这可以是 **initiator** 或 **target**。|38|是|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|是|  
|**Severity**|**int**|事件中文本的严重级别号。|29|是|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为客户端所关联的进程分配的服务器进程 ID。|12|是|  
|**StartTime**|**datetime**|事件（如果有）的开始时间。|14|是|  
|**State**|**int**|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源代码中生成该事件的位置。 可能生成此事件的每个位置都有不同的状态代码。 Microsoft 支持工程师可以使用此状态代码查找生成事件的位置。|30|是|  
|**TextData**|**ntext**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 删除消息的原因。|1|是|  
|**TransactionID**|**bigint**|系统为事务分配的 ID。|4|是|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
