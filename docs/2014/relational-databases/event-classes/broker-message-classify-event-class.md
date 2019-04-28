---
title: Broker:Message Classify 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4398085227952f30e4df7d54ac78c1aef1355173
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664046"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify 事件类
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将生成 **Broker:Message Classify** 事件。  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Broker:Message Classify 事件类的数据列  
  
|数据列|数据类型|Description|列号|可筛选|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|是|  
|**ClientProcessID**|**int**|由主机分配给正在运行客户端应用程序的进程的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 数据列而且服务器可用，则 **ServerName** 将显示数据库名。 可使用 DB_ID 函数来确定数据库的值。|3|是|  
|**EventClass**|**int**|捕获的事件类的类型。 **Broker:Message Classify** 始终为 **141**。|27|否|  
|**EventSequence**|**int**|此事件的序列号。|51|否|  
|**EventSubClass**|**nvarchar**|事件子类的类型，提供有关每个事件类的进一步信息。 此列可能包含下列值：<br /><br /> **本地**:所选路由具有 LOCAL 地址。<br /><br /> **远程**:所选路由具有非 LOCAL 地址。<br /><br /> **延迟**:消息被延迟，因为禁止转发或者没有匹配的路由。|21|是|  
|**FileName**|**nvarchar**|消息定向到的服务名称。|36|否|  
|**GUID**|**uniqueidentifier**|对话的会话 ID。 此标识符将作为消息的一部分进行传输，并在会话双方之间共享。|54|否|  
|**HostName**|**nvarchar**|正在运行客户端程序的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|是|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|否|  
|**LoginSid**|**image**|已登录用户的安全标识号 (SID)。 服务器中的每个登录名都具有唯一的 SID。|41|是|  
|**NTDomainName**|**nvarchar**|用户所属的 Windows 域。|7|是|  
|**NTUserName**|**nvarchar**|拥有生成此事件的连接的用户的名称。|6|是|  
|**OwnerName**|**nvarchar**|消息要定向到的 Broker 标识符。|37|否|  
|**RoleName**|**nvarchar**|指明该消息是从网络中收到的，还是在此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中产生的。|38|否|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为客户端所关联的进程分配的服务器进程 ID。|12|是|  
|**Start Time**|**datetime**|事件（如果有）的开始时间。|14|是|  
|**TargetUserName**|**nvarchar**|下一个跃点中介器的网络地址。|39|否|  
|**TransactionID**|**bigint**|系统为事务分配的 ID。|4|否|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
