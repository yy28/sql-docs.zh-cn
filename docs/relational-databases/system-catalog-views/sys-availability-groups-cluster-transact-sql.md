---
title: sys.availability_groups_cluster (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1173764b8726aebc2e53cef103f341b95e8c82fa
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511077"
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
|**failure_condition_level**|**int**|必须按其触发自动故障转移的用户定义的失败条件级别，可为以下整数值之一：<br /><br /> 1：指定在发生以下任何情况时应启动自动故障转移： <br />-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务已关闭。<br />的因为任何确认不收到从服务器实例连接到 WSFC 故障转移群集的可用性组租期到期。 有关详细信息，请参阅[工作方式：SQL Server Alwayson 租约超时](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)。<br /><br /> 2：指定在发生以下任何情况时应启动自动故障转移：  <br />的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会连接到群集和用户指定**health_check_timeout**超出了阈值的可用性组。 <br />可用性副本处于失败状态。 <br />3：指定在发生了严重的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时应启动自动故障转移。 这是默认值。 <br />4：指定在发生了中等程度的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部资源池中出现持久的内存不足情况）时应启动自动故障转移。<br />5：指定在出现任何符合的失败条件时应启动自动故障转移，这些失败条件包括：<br />-的 SQL 引擎工作线程耗尽。 <br />-无法解决的死锁检测。<br /><br /> 失败条件级别的范围 (1-5) 是从最少限制的级别 1 到最多限制的级别 5。 给定的条件级别包含所有限制较少的级别。 因此，最严格的条件级别 5 包含四个限制较少的级别 (1-4)，级别 4 包含级别 1-3，依此类推。<br /><br /> 若要更改此值，请使用 FAILURE_CONDITION_LEVEL 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**health_check_timeout**|**int**|等待时间 （以毫秒为单位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程返回服务器运行状况信息，在服务器实例被假定为较慢或挂起之前。 默认值为 30000 毫秒（30 秒）。<br /><br /> 若要更改此值，请使用 HEALTH_CHECK_TIMEOUT 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**automated_backup_preference**|**tinyint**|用于对此可用性组中的可用性数据库执行备份的首选位置。 可以是以下值之一：<br /><br /> 0:主副本。 备份应该始终在主副本上发生。<br />1：仅限辅助副本。 首选是对辅助副本执行备份。<br />2：辅助副本优先。 首选是对辅助副本执行备份，但如果没有可用于备份操作的辅助副本，对主副本执行备份是可接受的。 这是默认行为。<br />3：任何副本。 没有是对主副本执行备份还是对辅助副本执行备份的优先选择。<br /><br /> 有关详细信息，请参阅[活动次要副本：在辅助副本上备份&#40;Always On 可用性组&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|说明**automated_backup_preference**、 一个的：<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 无|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器实例的 VIEW ANY DEFINITION 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.availability_replicas (Transact-SQL)](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
