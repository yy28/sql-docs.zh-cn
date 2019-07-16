---
title: sys.dm_hadr_availability_replica_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05964e0557cb08e874424af542b8fc8a57ce0835
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900629"
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为每个本地副本都返回一行，并为与本地副本位于同一 AlwaysOn 可用性组的每个远程副本都返回一行。 每一行都包含给定副本的状态信息。  
  
> [!IMPORTANT]  
>  若要获取有关给定的可用性组中的每个副本的信息，请查询**sys.dm_hadr_availability_replica_states**正在承载主副本的服务器实例上。 在对正在承载某一可用性组的辅助副本的服务器实例进行查询时，此动态管理视图仅返回该可用性组的本地信息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|副本的唯一标识符。|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符。|  
|**is_local**|**bit**|是否是本地的该副本之一：<br /><br /> 0 = 指示某一可用性组中其主副本由本地服务器实例承载的远程辅助副本。 此值仅在主副本位置上出现。<br /><br /> 1 = 指示本地副本。 在辅助副本上，这是副本所属的可用性组的唯一可用值。|  
|**角色**|**tinyint**|当前[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]的本地副本或已连接的远程副本，其中一个角色：<br /><br /> 0 = 正在解析<br /><br /> 1 = 主<br /><br /> 2 = 辅助<br /><br /> 有关 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 角色的详细信息，请参阅 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。|  
|**role_desc**|**nvarchar(60)**|说明**角色**、 一个的：<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|当前操作状态的副本，其中一个：<br /><br /> 0 = 挂起故障转移<br /><br /> 1 = 挂起<br /><br /> 2 = 联机<br /><br /> 3 = 脱机<br /><br /> 4 = 失败<br /><br /> 5 = 失败，无仲裁<br /><br /> NULL = 副本不在本地。<br /><br /> 有关详细信息，请参阅[角色和操作状态](#RolesAndOperationalStates)，本主题中更高版本。|  
|**operational\_state\_desc**|**nvarchar(60)**|说明**运营\_状态**、 一个的：<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**恢复\_运行状况**|**tinyint**|汇总**数据库\_状态**的列[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)动态管理视图。 以下是可能的值和及其说明。<br /><br /> 0:正在进行。  至少一个联接的数据库具有并非 ONLINE 的数据库状态 (**数据库\_状态**是不是 0)。<br /><br /> 1:联机。 所有联接的数据库已联机数据库状态 (**database_state**为 0)。<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|说明**recovery_health**、 一个的：<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**同步\_运行状况**|**tinyint**|反映数据库同步状态的汇总 (**synchronization_state**) 的所有可用性数据库都联接 (也称为*副本*) 和副本 （将可用性模式同步提交或异步提交模式）。 汇总将反映至少运行状况正常的累积的状态数据库副本上。 以下是可能的值及其说明。<br /><br /> 0:不正常。   至少有一个联接的数据库处于 NOT SYNCHRONIZING 状态。<br /><br /> 1:完全正常。 一些副本未处于目标同步状态：同步提交副本应已同步，异步提交副本应正在同步。<br /><br /> 2:正常运行。 所有副本均处于目标同步状态：同步提交副本已同步，异步提交副本正在同步。|  
|**synchronization_health_desc**|**nvarchar(60)**|说明**synchronization_health**、 一个的：<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|指示辅助副本当前是否连接到主副本。 可能的值如下所示使用及其说明。<br /><br /> 0:已断开连接。 可用性副本对于 DISCONNECTED 状态的响应取决于其角色：在主副本上辅助副本已断开连接，如果其辅助数据库将标记为 NOT SYNCHRONIZED 等待辅助副本重新连接; 在主副本上在辅助副本，一旦检测，它已断开连接，辅助副本会尝试重新连接到主副本。<br /><br /> 1:连接。<br /><br /> 每个主副本都会跟踪同一可用性组中每个辅助副本的连接状态。 辅助副本仅跟踪主副本的连接状态。|  
|**connected_state_desc**|**nvarchar(60)**|说明**connection_state**、 一个的：<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|上一个连接错误的编号。|  
|**last_connect_error_description**|**nvarchar(1024)**|文本**last_connect_error_number**消息。|  
|**last_connect_error_timestamp**|**datetime**|日期和时间的时间戳，用于指示何时**last_connect_error_number**出现错误。|  
  
##  <a name="RolesAndOperationalStates"></a> 角色和操作状态  
 该角色，**角色**，反映了某一给定的可用性副本的状态和操作的状态， **operational_state**，描述副本是否已准备好处理所有的客户端请求可用性副本的数据库。 下面是可以为每个角色的操作状态的摘要：RESOLVING、 的主副本和辅助数据库。  
  
 **解决：** 正在解析角色中可用性副本时，可能的操作状态将是下表中所示。  
  
|操作状态|描述|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|正在为可用性组处理故障转移命令。|  
|OFFLINE|可用性副本的所有配置数据都已在 WSFC 群集上更新，并且也在本地元数据中更新，但可用性组目前缺少主副本。|  
|FAILED|在试图从 WSFC 群集中检索信息时发生了读取失败。|  
|FAILED_NO_QUORUM|本地 WSFC 节点没有仲裁。 这是一种推断状态。|  
  
 **主：** 当可用性副本履行主角色时，它当前是主副本。 下表中列出了可能的操作状态。  
  
|操作状态|描述|  
|-----------------------|-----------------|  
|PENDING|这是一个临时状态，但是，如果工作线程无法处理请求，主副本可能会处于此状态。|  
|ONLINE|可用性组资源已处于联机状态，并且所有数据库工作线程均已选取。|  
|FAILED|可用性副本无法从 WSFC 群集读取和/或写入。|  
  
 **辅助数据库：** 当可用性副本履行辅助角色时，它当前是辅助副本。 下表中列出了可能的操作状态。  
  
|操作状态|描述|  
|-----------------------|-----------------|  
|ONLINE|本地辅助副本连接到主副本。|  
|FAILED|本地辅助副本无法从 WSFC 群集读取和/或写入。|  
|NULL|在主副本上，当行与某一辅助副本相关时，将返回该值。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
