---
title: sys.dm_tcp_listener_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f45c634b2a5ab057fd9c2ae878e544a6b7d84f7f
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671343"
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回包含各个 TCP 侦听器的动态信息的行。  
  
> [!NOTE]
> 可用性组侦听器可能侦听 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的侦听器所侦听的端口。 在这种情况下，将分别列出这些侦听器，这与 Service Broker 侦听器的情况相同。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|侦听器的内部 id。 不可为 null。<br /><br /> 主键。|  
|**ip_address**|**nvarchar(48)**|处于联机状态且当前正在侦听的侦听器 IP 地址。 同时允许 IPv4 和 IPv6 地址。 如果某个侦听器拥有这两类地址，则分开列出这些地址。 IPv4 通配符显示为"0.0.0.0"。 IPv6 通配符显示为"::"。<br /><br /> 不可为 null。|  
|**is_ipv4**|**bit**|IP 地址的类型<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|侦听器正在侦听的端口号。 不可为 null。|  
|**类型**|**tinyint**|侦听器类型，可为下列值之一：<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = 数据库镜像<br /><br /> 不可为 null。|  
|**type_desc**|**nvarchar(20)**|说明**类型**、 一个的：<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> 不可为 null。|  
|State|**tinyint**|可用性组侦听器的状态，可为下列值之一：<br /><br /> 1 = 联机。 侦听器正在侦听并处理请求。<br /><br /> 2 = 等待重新启动。 侦听器处于脱机状态，等待重新启动。<br /><br /> 如果可用性组侦听器正在侦听服务器实例所侦听的端口，这两个侦听器始终具有相同状态。<br /><br /> 不可为 null。<br /><br /> 注意：此列中的值来自 TSD_listener 对象。 列不支持脱机状态，因为 TDS_listener 脱机时，它无法查询状态。|  
|**state_desc**|**nvarchar(16)**|说明**状态**、 一个的：<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> 不可为 null。|  
|**start_time**|**datetime**|指示启动侦听器时的时间戳。 不可为 null。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Always On 可用性组动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
