---
title: sys.availability_groups (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3874bde2c43ddcba3e0ef365ff371a54ffcb8ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysavailabilitygroups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回为其 SQL Server 的本地实例承载可用性副本的每个可用性组的行。 每一行都包含可用性组元数据的缓存的副本。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性组的唯一标识符 (GUID)。|  
|**名称**|**sysname**|可用性组的名称。 这是在 Windows Server 故障转移群集 (WSFC) 内必须唯一的用户指定的名称。|  
|**resource_id**|**nvarchar(40)**|WSFC 群集资源的资源 ID。|  
|**resource_group_id**|**nvarchar(40)**|可用性组的 WSFC 群集资源组的资源组 ID。|  
|**failure_condition_level**|**int**|用户定义的失败条件级别在其下必须触发自动故障转移，此表下面立即表所示的整数值之一。<br /><br /> 失败条件级别的范围 (1–5) 是从最少限制的级别 1 到最多限制的级别 5。 给定的条件级别包含所有限制较少的级别。 因此，最严格的条件级别 5 包含四个限制较少的级别 (1-4)，级别 4 包含级别 1-3，依此类推。<br /><br /> 若要更改此值，请使用 FAILURE_CONDITION_LEVEL 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**health_check_timeout**|**int**|等待的等待时间 （以毫秒为单位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程来恢复之前的服务器实例被假定为慢速或挂起的服务器运行状况信息。 默认值为 30000 毫秒（30 秒）。<br /><br /> 若要更改此值，请使用 HEALTH_CHECK_TIMEOUT 选项[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。|  
|**automated_backup_preference**|**tinyint**|用于对此可用性组中的可用性数据库执行备份的首选位置。 以下是可能的值以及及其说明。<br /><br /> <br /><br /> 0： 主。 备份应该始终在主副本上发生。<br /><br /> 1： 仅辅助。 首选是对辅助副本执行备份。<br /><br /> 2： 优先辅助。 首选是对辅助副本执行备份，但如果没有可用于备份操作的辅助副本，对主副本执行备份是可接受的。 这是默认行为。<br /><br /> 3： 任何副本。 没有是对主副本执行备份还是对辅助副本执行备份的优先选择。<br /><br /> <br /><br /> 有关详细信息，请参阅 [活动辅助副本：辅助副本备份（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)概念。|  
|**automated_backup_preference_desc**|**nvarchar(60)**|说明**automated_backup_preference**、 一个的：<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> 无|  
|**version**|**int**|可用性组元数据存储在 Windows 故障转移群集版本。 当添加新功能，即会递增此版本号。|  
|**basic_features**|**bit**|指定这是否为基本可用性组。 有关详细信息，请参阅[基本可用性组（Always On 可用性组）](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。|  
|**dtc_support**|**bit**|指定是否已为此可用性组启用了 DTC 支持。 **DTC_SUPPORT**选项**CREATE AVAILABILITY GROUP**控制此设置。|  
|**db_failover**|**bit**|指定是否则可用性组支持故障转移的数据库运行状况条件。 **DB_FAILOVER**选项**CREATE AVAILABILITY GROUP**控制此设置。|  
|**is_distributed**|**bit**|指定这是否是分布式的可用性组。 有关详细信息，请参阅[分布式可用性组&#40;Always On 可用性组&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。|  
  
## <a name="failure-condition-level--values"></a>失败条件级别值  
 下表描述的可能的故障条件级别**failure_condition_level**列。  
  
|“值”|失败条件|  
|-----------|-----------------------|  
|1|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> <br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务已关闭。<br /><br /> 的因为从服务器实例接收不到任何 ACK 连接到 WSFC 故障转移群集的可用性组租期到期。 有关详细信息，请参阅 [工作原理：SQL Server AlwaysOn 租约超时](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)。|  
|2|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> <br /><br /> -实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会连接到群集，并指定用户**health_check_timeout**超过了可用性组的阈值。<br /><br /> 可用性副本处于失败状态。|  
|3|指定在发生了严重的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时应启动自动故障转移。<br /><br /> 这是默认值。|  
|4|指定在发生了中等程度的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部资源池中出现持久的内存不足情况）时应启动自动故障转移。|  
|5|指定在出现任何符合的失败条件时应启动自动故障转移，这些失败条件包括：<br /><br /> <br /><br /> -SQL 引擎工作线程耗尽。<br /><br /> 无法解决的死锁的检测。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器实例的 VIEW ANY DEFINITION 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.availability_replicas (Transact-SQL)](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [监视可用性组 & #40;Transact SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [监视可用性组 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
