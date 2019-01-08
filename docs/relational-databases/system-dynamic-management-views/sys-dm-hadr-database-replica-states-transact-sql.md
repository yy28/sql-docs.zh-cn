---
title: sys.dm_hadr_database_replica_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_states_TSQL
- sys.dm_hadr_database_states
- dm_hadr_database_states
- dm_hadr_database_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_database_replica_states dynamic management view
ms.assetid: 1a17b0c9-2535-4f3d-8013-cd0a6d08f773
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 94c9258ff71454134c5ff2023e174a0811d7afe6
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52159085"
---
# <a name="sysdmhadrdatabasereplicastates-transact-sql"></a>sys.dm_hadr_database_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为其返回 Always On 可用性组中的参与每个数据库的行的本地实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正承载其可用性副本。 此动态管理视图公开与主副本和辅助副本有关的状态信息。 在辅助副本上，此视图为服务器实例上的每个辅助数据库都返回一行。 在主副本上，此视图为每个主数据库都返回一行，并且为相应的辅助数据库另外返回一行。  
  
> [!IMPORTANT]
> 根据操作和更高级别的状态，数据库状态信息可能不可用或过期。 此外，这些值仅具有本地相关性。 例如，在主副本的值**last_hardened_lsn**列反映到主副本当前可用的给定辅助数据库有关的信息，不实际强制写入的 LSN 值辅助副本当前可能具有。  
   
|列名|数据类型|说明（针对主副本）|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|数据库的标识符，在 SQL Server 的实例内是唯一的。 这是相同的值中所示[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。|  
|**group_id**|**uniqueidentifier**|数据库所属的可用性组的标识符。|  
|**replica_id**|**uniqueidentifier**|可用性组内可用性副本的标识符。|  
|**group_database_id**|**uniqueidentifier**|可用性组内数据库的标识符。 在此数据库联接到的每个副本上，该标识符都是相同的。|  
|**is_local**|**bit**|可用性数据库是否是本地的，可以是下列值之一：<br /><br /> 0 = 数据库对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例而言不是本地的。<br /><br /> 1 = 数据库对于服务器实例而言是本地的。|  
|**is_primary_replica**|**bit**|如果副本是主要副本则返回 1；如果副本是辅助副本则返回 0。<br /><br />适用范围：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**synchronization_state**|**tinyint**|数据移动状态，以下值之一。<br /><br /> 0 = 未同步。 对于某一主数据库，指示该数据库未做好将其事务日志与相应的辅助数据库同步的准备。 对于辅助数据库，指示数据库由于连接问题而未开始日志同步，正被挂起，或者在启动或角色切换过程中正在转换状态。<br /><br /> 1 = 正在同步。 对于主数据库，指示此数据库已做好接受来自辅助数据库的扫描请求的准备。 对于辅助数据库，指示对于该数据库正在发生活动数据移动。<br /><br /> 2 = 已同步。 主数据库显示 SYNCHRONIZED 来代替 SYNCHRONIZING。 同步提交辅助数据库在以下情况下将显示已同步：本地缓存指示数据库副本可供故障转移并且数据库正在同步。<br /><br /> 3 = 恢复。 指示撤消进程中辅助数据库主动从主数据库获取页时的阶段。<br />**注意：** 当辅助副本上的数据库处于 REVERTING 状态时，强制故障转移到辅助副本将使数据库处于该数据库不能作为主数据库启动的状态。 该数据库将需要作为辅助数据库重新连接，或者您需要应用来自日志备份的新日志记录。<br /><br /> 4 = 正在初始化。 指示在正在辅助副本上传送和强制写入辅助数据库跟上撤消 LSN 所需的事务日志时的撤消阶段。<br />**注意：** 当辅助副本上的数据库处于 INITIALIZING 状态时，强制故障转移到辅助副本将使数据库处于在其中它不能启动作为主数据库的状态。 该数据库将需要作为辅助数据库重新连接，或者您需要应用来自日志备份的新日志记录。|  
|**synchronization_state_desc**|**nvarchar(60)**|数据移动状态的说明，可以是下列值之一：<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = 就此数据库而言，事务提交未同步。<br /><br /> 1 = 就此数据库而言，事务提交同步。<br /><br /> 对于异步提交可用性副本上的数据库，该值始终为 0。<br /><br /> 对于同步提交可用性副本上的数据库，该值仅在主数据库上是准确的。|  
|**synchronization_health**|**tinyint**|反映联接到可用性副本上的可用性组的数据库的同步状态和可用性副本 （同步提交或异步提交模式） 之一的可用性模式的交集以下值。<br /><br /> 0 = 不正常。 **Synchronization_state**数据库是 0 (NOT SYNCHRONIZING)。<br /><br /> 1 = 不完全正常。 同步提交可用性副本上的数据库被视为完全正常如果**synchronization_state**为 1 (SYNCHRONIZING)。<br /><br /> 2 = 正常。 同步提交可用性副本上的数据库被视为正常如果**synchronization_state**为 2 (SYNCHRONIZED) 和异步提交可用性副本上的数据库被视为正常如果**synchronization_state**为 1 (SYNCHRONIZING)。|  
|**synchronization_health_desc**|**nvarchar(60)**|说明**synchronization_health**的可用性数据库。<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = 联机<br /><br /> 1 = 正在还原<br /><br /> 2 = 正在恢复<br /><br /> 3 = 恢复挂起<br /><br /> 4 = 可疑<br /><br /> 5 = 紧急<br /><br /> 6 = 脱机<br /><br /> **注意：** 与相同**状态**sys.databases 中的列。|  
|**database_state_desc**|**nvarchar(60)**|说明**database_state**的可用性副本。<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **注意：** 与相同**state_desc** sys.databases 中的列。|  
|**is_suspended**|**bit**|数据库状态，可以是下列值之一：<br /><br /> 0 = 已恢复<br /><br /> 1 = 已挂起|  
|**suspend_reason**|**tinyint**|如果数据库处于已挂起状态，则为已挂起状态的原因，可以是下列值之一：<br /><br /> 0 = 用户操作<br /><br /> 1 = 挂起来自伙伴<br /><br /> 2 = 重做<br /><br /> 3 = 捕获<br /><br /> 4 = 应用<br /><br /> 5 = 重新启动<br /><br /> 6 = 撤消<br /><br /> 7 = 重新验证<br /><br /> 8 = 计算辅助副本同步点时出错|  
|**suspend_reason_desc**|**nvarchar(60)**|数据库挂起状态的原因的说明，可以是下列值之一：<br /><br /> SUSPEND_FROM_USER = 用户手动挂起的收据移动<br /><br /> SUSPEND_FROM_PARTNER = 在强制故障转移后挂起数据库副本<br /><br /> SUSPEND_FROM_REDO = 在重做阶段中出错<br /><br /> SUSPEND_FROM_APPLY = 在将日志写入文件时出错（请参阅错误日志）<br /><br /> SUSPEND_FROM_CAPTURE = 在捕获主副本上的日志时出错<br /><br /> SUSPEND_FROM_RESTART = 在重新启动数据库前挂起数据库副本（请参阅错误日志）<br /><br /> SUSPEND_FROM_UNDO = 在撤消阶段中出错（请参阅错误日志）<br /><br /> SUSPEND_FROM_REVALIDATION = 在重新连接时检测到了日志更改不匹配（请参阅错误日志）<br /><br /> SUSPEND_FROM_XRF_UPDATE = 找不到公共日志点（请参阅错误日志）|  
|**recovery_lsn**|**numeric(25,0)**|在主副本上，在恢复或故障转移之后、在主数据库写入任何新日志记录之前事务日志的结尾。 对于给定的辅助数据库，如果该值小于当前硬化的 LSN (last_hardened_lsn)，则 recovery_lsn 是此辅助数据库需要重新同步的值（即要恢复到和重新初始化的值）。 如果该值大于或等于当前硬化 LSN，重新同步将没有必要且不会发生。<br /><br /> **recovery_lsn**反映了用零填充的日志块 ID。 它不是实际的日志序列号 (LSN)。 有关如何派生此值的信息，请参阅[了解 LSN 列值](#LSNcolumns)，本主题中更高版本。|  
|**truncation_lsn**|**numeric(25,0)**|在主副本上，对于主数据库，反映了所有相应辅助数据库中的最小日志截断 LSN。 如果阻止本地日志截断（例如由备份操作阻止），则该 LSN 可能高于本地截断 LSN。<br /><br /> 对于给定的辅助数据库，反映了该数据库的截断点。<br /><br /> **truncation_lsn**反映了用零填充的日志块 ID。 它不是实际的日志序列号。|  
|**last_sent_lsn**|**numeric(25,0)**|指示一个点（在该点前的所有日志块都已由主数据库发送）的日志块标识符。 该标识符是将发送的下一日志块的 ID，而非最近发送的日志块的 ID。<br /><br /> **last_sent_lsn**反映了日志块 ID 用零填充，它不是实际的日志序列号。|  
|**last_sent_time**|**datetime**|发送最后一个日志块的时间。|  
|**last_received_lsn**|**numeric(25,0)**|标识一个点的日志块 ID，在该点之前，所有日志块都已由承载此辅助数据库的辅助副本接收。<br /><br /> **last_received_lsn**反映了用零填充的日志块 ID。 它不是实际的日志序列号。|  
|**last_received_time**|**datetime**|在辅助副本上读取最后接收的消息中的日志块 ID 的时间。|  
|**last_hardened_lsn**|**numeric(25,0)**|包含辅助数据库上最后强制写入的 LSN 的日志记录的日志块开头。<br /><br /> 在异步提交主数据库上或其当前策略为“延迟”的同步提交数据库上，该值为 NULL。 对于其他同步提交主数据库， **last_hardened_lsn**指示所有辅助数据库中的强制的 LSN 的最小值。<br /><br /> **注意： last_hardened_lsn**反映了用零填充的日志块 ID。 它不是实际的日志序列号。 有关详细信息，请参阅[了解 LSN 列值](#LSNcolumns)，本主题中更高版本。|  
|**last_hardened_time**|**datetime**|辅助数据库上最后一个日志块标识符的时间强制写入的 LSN (**last_hardened_lsn**)。 在主数据库上，反映了与最小强制写入的 LSN 相对应的时间。|  
|**last_redone_lsn**|**numeric(25,0)**|在辅助数据库上重做的上一个日志记录的实际日志序列号。 **last_redone_lsn**是始终小于**last_hardened_lsn**。|  
|**last_redone_time**|**datetime**|在辅助数据库上重做最后一个日志记录的时间。|  
|**log_send_queue_size**|**bigint**|主数据库中尚未发送到辅助数据库的日志记录量 (KB)。|  
|**log_send_rate**|**bigint**|在最后一个活动期间，以千字节 (KB) 的平均主副本发送实例数据的速率/秒。|  
|**redo_queue_size**|**bigint**|辅助副本的日志文件中尚未重做的日志记录量 (KB)。|  
|**redo_rate**|**bigint**|平均千字节 (KB) 中的给定辅助数据库做的日志记录速率 / 秒。|  
|**filestream_send_rate**|**bigint**|FILESTREAM 文件传送到辅助副本的速率（KB/秒）。|  
|**end_of_log_lsn**|**numeric(25,0)**|日志 LSN 的本地结尾。 与主数据库和辅助数据库上日志缓存中的最后一个日志记录相对应的实际 LSN。 在主副本上，辅助行反映了辅助副本已发送到主副本的最新进度消息中日志 LSN 的结尾。<br /><br /> **end_of_log_lsn**反映了用零填充的日志块 ID。 它不是实际的日志序列号。 有关详细信息，请参阅[了解 LSN 列值](#LSNcolumns)，本主题中更高版本。|  
|**last_commit_lsn**|**Numeric(25,0)**|与事务日志中的最后提交的记录相对应的实际日志序列号。<br /><br /> 主数据库上，这对应于上次处理的提交记录。 辅助数据库的行显示辅助副本已发送到主副本的日志序列号。<br /><br /> 在辅助副本上，这是已重做的最后一个提交记录。|  
|**last_commit_time**|**datetime**|与最后一个提交记录对应的时间。<br /><br /> 在辅助数据库上，此时间与主数据库上的时间相同。<br /><br /> 在主副本上，每个辅助数据库行都显示承载该辅助数据库的辅助副本报告回主副本的时间。 主数据库行和给定的辅助数据库行之间的时间差异表示大约恢复点目标 (RPO)，假定，重做进程并且进度已到主副本返回报告由辅助副本。|  
|**low_water_mark_for_ghosts**|**bigint**|针对数据库的单调递增的数字，指示主数据库上虚影清除使用的低水印。 如果这个数字没有随着时间的推移而增加，则意味着虚影清除可能未发生。 为了确定要清除的虚影行，主副本会在所有可用性副本（包括主副本）上将该列的最小值用于此数据库。|  
|**secondary_lag_seconds**|**bigint**|在同步期间，辅助副本是主副本的秒数。<br /><br />适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
##  <a name="LSNcolumns"></a> 了解 LSN 列值  
 值**end_of_log_lsn**， **last_hardened_lsn**， **last_received_lsn**， **last_sent_lsn**，**恢复_lsn**，并**truncation_lsn**列不是实际的日志序列号 (Lsn)。 上述各值反映了用零填充的日志块 ID。  
  
 **end_of_log_lsn**， **last_hardened_lsn**，和**recovery_lsn**是刷新 Lsn。 例如， **last_hardened_lsn**指示越过已位于磁盘的块的下一个块的开头。  因此任何 LSN < 的值**last_hardened_lsn**磁盘上。  不刷新 >= 此值的 LSN。  
  
 返回的 LSN 值**sys.dm_hadr_database_replica_states**，则只**last_redone_lsn**是真实的 LSN。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [监视可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
