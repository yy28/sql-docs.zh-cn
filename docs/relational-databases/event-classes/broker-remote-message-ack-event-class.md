---
title: Broker:Remote Message Ack 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6193e937af7e678fdc69f674b263c02a37ee7f55
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078129"
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack 事件类
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发送或接收消息确认时， **将生成** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] 事件。  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Broker:Remote Message Ack 事件类的数据列  
  
|数据列|类型|描述|列号|可筛选|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名称填充。|10|用户帐户控制|  
|**BigintData1**|**bigint**|包含确认的消息序列号。|52|否|  
|**BigintData2**|**bigint**|确认后的消息的序列号。|53|否|  
|**ClientProcessID**|**int**|由主机分配给正在运行客户端应用程序的进程的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|用户帐户控制|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID。 如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|用户帐户控制|  
|**EventClass**|**int**|捕获的事件类的类型。 对于 **Broker:Message Ack** 始终是 **149**。|27|否|  
|**EventSequence**|**int**|此事件的序列号。|51|否|  
|**EventSubClass**|**nvarchar**|事件子类的类型，提供有关每个事件类的详细信息。 此列可能包含以下值：<br /><br /> **已发送带有确认的消息**：<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 已将确认作为已编序的正常消息的一部分发送。<br /><br /> **已发送确认**：<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 已发送确认，但该确认不包括在已编序的正常消息内。<br /><br /> **已收到带有确认的消息**：<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 已收到确认，该确认包括在已编序的正常消息内。<br /><br /> **已收到确认**：<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 已收到确认，但该确认不在已编序的正常消息内。|21|用户帐户控制|  
|**GUID**|**uniqueidentifier**|对话的会话 ID。 此标识符将作为消息的一部分进行传输，并在会话双方之间共享。|54|否|  
|**HonorBrokerPriority**|**Int**|数据库 HONOR_BROKER_PRIORITY 选项的当前值：0 = OFF、1 = ON。|32|用户帐户控制|  
|**HostName**|**nvarchar**|正在运行客户端程序的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|用户帐户控制|  
|**IntegerData**|**int**|包含确认的消息的片段号。|25|否|  
|**IntegerData2**|**int**|正在进行确认的消息的片段号。|55|否|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。<br /><br /> 0 = 用户<br /><br /> 1 = 系统|60|否|  
|**LoginSid**|**图像**|已登录用户的安全标识号 (SID)。 服务器中的每个登录名都具有唯一的 SID。|41|用户帐户控制|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|用户帐户控制|  
|**NTUserName**|**nvarchar**|拥有生成此事件的连接的用户的名称。|6|用户帐户控制|  
|**Priority**|**int**|会话的优先级。|5|用户帐户控制|  
|**RoleName**|**nvarchar**|正在确认消息的实例的角色。 这可以是 **initiator** 或 **target**。|38|否|  
|**ServerName**|**nvarchar**|正在跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为客户端所关联的进程分配的服务器进程 ID。|12|用户帐户控制|  
|**StartTime**|**datetime**|事件（如果有）的开始时间。|14|用户帐户控制|  
|**StarvationElevation**|**int**|消息发送的优先级高于为会话配置的优先级：0 = false、1 = true。|33|用户帐户控制|  
|**TransactionID**|**bigint**|系统为事务分配的 ID。|4|否|  
  
  
