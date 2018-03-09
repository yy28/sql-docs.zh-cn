---
title: "sys.availability_groups_cluster (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d2b47abb7cba870e3d697a3e679d646e7f83b9c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysavailabilitygroupscluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回每个 Always On 可用性组的行在 Windows Server 故障转移群集 (WSFC)。 每一行都包含 WSFC 群集的可用性组元数据。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符 (GUID)。|  
|**名称**|**sysname**|可用性组的名称。 这是在 Windows Server 故障转移群集 (WSFC) 内必须唯一的用户指定的名称。|  
|**resource_id**|**nvarchar(40)**|WSFC 群集资源的资源 ID。|  
|**resource_group_id**|**nvarchar(40)**|可用性组的 WSFC 群集资源组的资源组 ID。|  
|**failure_condition_level**|**int**|必须按其触发自动故障转移的用户定义的失败条件级别，可为以下整数值之一：<br /><br /> 1： 指定应启动自动故障转移出现任何以下： <br />-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务已关闭。<br />的因为从服务器实例接收不到任何 ACK 连接到 WSFC 故障转移群集的可用性组租期到期。 有关详细信息，请参阅 [工作原理：SQL Server AlwaysOn 租约超时](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)。<br /><br /> 2： 指定应启动自动故障转移出现任何以下：  <br />-实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会连接到群集，并指定用户**health_check_timeout**超过了可用性组的阈值。 <br />可用性副本处于失败状态。 <br />3： 指定应按关键启动自动故障转移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部错误，如孤立的自旋锁、 严重的写访问冲突或过多的转储。 这是默认值。 <br />4： 指定应在中等启动这些自动故障转移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部错误，例如在永久性内存不足情况[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部资源池。<br />5： 指定应在任何限定的失败条件，包括启动这些自动故障转移：<br />-SQL 引擎工作线程耗尽。 <br />无法解决的死锁的检测。<br /><br /> 失败条件级别的范围 (1–5) 是从最少限制的级别 1 到最多限制的级别 5。 给定的条件级别包含限制较少的级别的所有。 因此，最严格的条件级别 5 包含四个限制较少的级别 (1-4)，级别 4 包含级别 1-3，依此类推。<br /><br /> 若要更改此值，请使用 FAILURE_CONDITION_LEVEL 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**health_check_timeout**|**int**|等待的等待时间 （以毫秒为单位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程来恢复之前的服务器实例被假定为慢速或挂起的服务器运行状况信息。 默认值为 30000 毫秒（30 秒）。<br /><br /> 若要更改此值，请使用 HEALTH_CHECK_TIMEOUT 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**automated_backup_preference**|**tinyint**|用于对此可用性组中的可用性数据库执行备份的首选位置。 可以是以下值之一：<br /><br /> 0： 主。 备份应该始终在主副本上发生。<br />1： 仅辅助。 首选是对辅助副本执行备份。<br />2： 优先辅助。 首选是对辅助副本执行备份，但如果没有可用于备份操作的辅助副本，对主副本执行备份是可接受的。 这是默认行为。<br />3： 任何副本。 没有是对主副本执行备份还是对辅助副本执行备份的优先选择。<br /><br /> 有关详细信息，请参阅 [活动辅助副本：辅助副本备份（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)概念。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|说明**automated_backup_preference**、 一个的：<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 无|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器实例的 VIEW ANY DEFINITION 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [监视可用性组 &#40;Transact SQL &#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [监视可用性组 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
