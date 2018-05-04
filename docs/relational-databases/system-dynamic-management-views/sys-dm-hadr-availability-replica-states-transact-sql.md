---
title: sys.dm_hadr_availability_replica_states (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 65
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 49ed5ae45fcd3f5c760481a4dce85f8a5bd8e5a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在同一 Always On 可用性组作为本地副本中返回的行对于每个本地副本和一个行对于每个远程副本。 每一行都包含有关给定副本的状态信息。  
  
> [!IMPORTANT]  
>  若要获取有关给定的可用性组中每个副本的信息，请查询**sys.dm_hadr_availability_replica_states**正在承载主副本的服务器实例上。 在对正在承载某一可用性组的辅助副本的服务器实例进行查询时，此动态管理视图仅返回该可用性组的本地信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|副本的唯一标识符。|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符。|  
|**is_local**|**bit**|副本是本地，之一：<br /><br /> 0 = 指示某一可用性组中其主副本由本地服务器实例承载的远程辅助副本。 此值仅在主副本位置上出现。<br /><br /> 1 = 指示本地副本。 在辅助副本上，这是副本所属的可用性组的唯一可用值。|  
|**角色**|**tinyint**|当前[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]本地副本或连接的远程副本，其中一个的角色：<br /><br /> 0 = 正在解析<br /><br /> 1 = 主<br /><br /> 2 = 辅助<br /><br /> 有关 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 角色的详细信息，请参阅 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。|  
|**role_desc**|**nvarchar(60)**|说明**角色**、 一个的：<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|当前操作状态的副本，之一：<br /><br /> 0 = 挂起故障转移<br /><br /> 1 = 挂起<br /><br /> 2 = 联机<br /><br /> 3 = 脱机<br /><br /> 4 = 失败<br /><br /> 5 = 失败，无仲裁<br /><br /> NULL = 副本不在本地。<br /><br /> 有关详细信息，请参阅[角色和操作状态](#RolesAndOperationalStates)，本主题中更高版本。|  
|**operational\_state\_desc**|**nvarchar(60)**|说明**操作\_状态**、 一个的：<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**恢复\_运行状况**|**tinyint**|汇总的**数据库\_状态**列[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)动态管理视图。 以下是可能的值以及及其说明。<br /><br /> 0： 正在进行。  至少一个已联接的数据库已联机以外的数据库状态 (**数据库\_状态**是不是 0)。<br /><br /> 1： 联机。 所有已联接的数据库都有联机数据库状态 (**database_state**为 0)。<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|说明**recovery_health**、 一个的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**同步\_运行状况**|**tinyint**|反映的数据库同步状态的汇总 (**synchronization_state**) 的所有可用性数据库都联接 (也称为*副本*) 和副本 （可用性模式同步提交或异步提交模式）。 汇总将反映最累积的状态数据库副本上。 以下是可能的值以及及其说明。<br /><br /> 0： 不正常。   至少有一个联接的数据库处于 NOT SYNCHRONIZING 状态。<br /><br /> 1： 部分正常运行。 一些副本未处于目标同步状态：同步提交副本应已同步，异步提交副本应正在同步。<br /><br /> 2： 正常运行。 所有副本均处于目标同步状态：同步提交副本已同步，异步提交副本正在同步。|  
|**synchronization_health_desc**|**nvarchar(60)**|说明**synchronization_health**、 一个的：<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|辅助副本当前是否连接到主副本。 与及其说明下面显示了可能的值。<br /><br /> 0： 断开连接。 断开连接状态的可用性副本的响应取决于其角色： 的主副本上断开连接的辅助副本时，其辅助数据库被标记为未在主副本上，它会一直等待到辅助数据库的同步重新连接;在辅助副本上，一旦检测到其未连接，辅助副本会尝试重新连接到主副本。<br /><br /> 1： 连接。<br /><br /> 每个主副本都会跟踪同一可用性组中每个辅助副本的连接状态。 辅助副本仅跟踪主副本的连接状态。|  
|**connected_state_desc**|**nvarchar(60)**|说明**connection_state**、 一个的：<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|上一个连接错误的编号。|  
|**last_connect_error_description**|**nvarchar(1024)**|文本**last_connect_error_number**消息。|  
|**last_connect_error_timestamp**|**datetime**|日期和时间的时间戳，该值指示当**last_connect_error_number**出错。|  
  
##  <a name="RolesAndOperationalStates"></a> 角色和操作状态  
 该角色，**角色**，反映给定的可用性副本的状态和操作的状态， **operational_state**，描述副本是否已准备好要处理的所有客户端请求可用性副本的数据库。 以下是可用于每个角色的操作状态的摘要： 解决、 主和辅助。  
  
 **解决：**解析角色的可用性副本时，可能的操作状态包括下表中所示。  
  
|操作状态|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|正在为可用性组处理故障转移命令。|  
|OFFLINE|可用性副本的所有配置数据都已在 WSFC 群集上更新，并且也在本地元数据中更新，但可用性组目前缺少主副本。|  
|FAILED|在试图从 WSFC 群集中检索信息时发生了读取失败。|  
|FAILED_NO_QUORUM|本地 WSFC 节点没有仲裁。 这是一种推断状态。|  
  
 **主站点：**可用性副本正在执行的主角色，它是当前主副本。 可能的操作状态包括下表中所示。  
  
|操作状态|Description|  
|-----------------------|-----------------|  
|PENDING|这是一个临时状态，但是，如果工作线程无法处理请求，主副本可能会处于此状态。|  
|ONLINE|可用性组资源已处于联机状态，并且所有数据库工作线程均已选取。|  
|FAILED|可用性副本无法从 WSFC 群集读取和/或写入。|  
  
 **辅助：**可用性副本正在执行辅助角色，它是当前辅助副本。 可能的操作状态包括下表中所示。  
  
|操作状态|Description|  
|-----------------------|-----------------|  
|ONLINE|本地辅助副本连接到主副本。|  
|FAILED|本地辅助副本无法从 WSFC 群集读取和/或写入。|  
|NULL|在主副本上，当行与某一辅助副本相关时，将返回该值。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [监视可用性组 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
