---
title: sys.dm_resource_governor_workload_groups_history_ex （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
ms.openlocfilehash: ac776813cb817d1357948091bfc48c981fa8e730
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053258"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回快照在 15 秒间隔过去 30 分钟的资源池统计信息为 Azure SQL 数据库。
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**| INT |资源池的 ID。 不可为 null。|
|**group_id**| INT |工作负荷组的 ID。 不可为 null。|
|**name**| nvarchar(256) |工作负荷组的名称。 不可为 null。|
|**snapshot_time**| DATETIME |拍摄的资源组统计信息快照的日期时间。|
|**duration_ms**| INT |当前和以前的快照之间的持续时间。|
|**active_worker_count**| INT |当前快照中的总工作线程。|
|**active_request_count**| INT |当前请求计数。 不可为 null。|
|**active_session_count**| INT |当前快照中的活动会话总数。|
|**total_request_count**| BIGINT |工作负荷组中已完成请求的累计计数。 不可为 null。|
|**delta_request_count**| INT |自上一个快照以来工作负荷组中的已完成请求的计数。 不可为 null。|
|**total_cpu_usage_ms**| BIGINT |此工作负荷组的累计 CPU 使用情况，以毫秒为单位。 不可为 null。|
|**delta_cpu_usage_ms**| INT |自上一个快照以来的毫秒的 CPU 使用率。 不可为 null。|
|**delta_cpu_usage_preemptive_ms**| INT |抢先式的 win32 调用不管理方法是 SQL CPU RG 自上次快照。|
|**delta_reads_reduced_memgrant_count**| INT |自上一个快照以来达到的最大查询大小限制的内存授予数。 不可为 null。|
|**reads_throttled**| INT |限制读取的总次数。|
|**delta_reads_queued**| INT |自上一个快照以来的读取 IOs 排入队列的总数。 可以为 Null。 如果没有为 IO 调控资源组，则为 null。|
|**delta_reads_issued**| INT |读取自上一个快照以来发出的 Io 总数。 可以为 Null。 如果没有为 IO 调控资源组，则为 null。|
|**delta_reads_completed**| INT |读取自上一个快照以来完成的 Io 总数。 不可为 null。|
|**delta_read_bytes**| BIGINT |自上一个快照以来读取的字节总数。 不可为 null。|
|**delta_read_stall_ms**| INT |读的 IO 到达和完成自上一个快照之间 （以毫秒为单位） 的总时间。 不可为 null。|
|**delta_read_stall_queued_ms**| INT |读 IO 到达和发出自上一个快照之间 （以毫秒为单位） 的总时间。 可以为 Null。 如果没有为 IO 调控资源组，则为 null。 非零 delta_read_stall_queued_ms 意味着 IO 受 RG。|
|**delta_writes_queued**| INT |自上一个快照以来的写入 IOs 排入队列的总数。 可以为 Null。 如果没有为 IO 调控资源组，则为 null。|
|**delta_writes_issued**| INT |写入自上一个快照以来发出的 Io 总数。 可以为 Null。 如果没有为 IO 调控资源组，则为 null。|
|**delta_writes_completed**| INT |写入自上一个快照以来完成的 Io 总数。 不可为 null。|
|**delta_writes_bytes**| BIGINT |自上一个快照以来写入的字节总数。 不可为 null。|
|**delta_write_stall_ms**| INT |写 IO 到达和完成自上一个快照之间 （以毫秒为单位） 的总时间。 不可为 null。|
|**delta_background_writes**| INT |自上一个快照以来所执行的后台任务的总写入。|
|**delta_background_write_bytes**| BIGINT |总写入执行后台任务，因为上一个快照，以字节为单位的大小。|
|**delta_log_bytes_used**| BIGINT |以字节为单位的上一个快照以来使用的日志。|
|**delta_log_temp_db_bytes_used**| BIGINT |以字节为单位的上一个快照以来使用 Tempdb 日志。|
|**delta_query_optimizations**| BIGINT |自上一个快照以来此工作负荷组中的查询优化数。 不可为 null。|
|**delta_suboptimal_plan_generations**| BIGINT |自上一个快照以来发生由于内存压力而导致此工作负荷组中的不理想计划生成的计数。 不可为 null。
|**max_memory_grant_kb**| BIGINT |最大内存授予以 kb 为单位的组。|
|**max_request_cpu_msec**| BIGINT |单个请求的最大 CPU 使用情况，以毫秒为单位。 不可为 null。|
|**max_concurrent_request**| INT |并发请求最大数的当前设置。 不可为 null。|
|**max_io**| INT |组的的最大 IO 限制。|
|**max_global_io**| INT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。
|**max_queued_io**| INT |标识为仅供参考。 不提供支持。 不保证以后的兼容性。|
|**max_log_rate_kb**| BIGINT |在资源组级别的最大日志速率 （每秒千字节）。|
|**max_session**| INT |会话组的限制。|
|**max_worker**| INT |辅助角色组的限制。|
|||

## <a name="permissions"></a>权限

此视图需要 VIEW SERVER STATE 权限。

## <a name="remarks"></a>备注

用户可以访问此动态管理视图来监视近乎实时的用户工作负荷池，以及 Azure SQL 数据库实例的系统内部池的资源消耗。

> [!IMPORTANT]
> 此 dmv 显示的数据的大多数专供内部使用，可能会发生更改。

## <a name="examples"></a>示例

下面的示例返回按用户池最大日志速率数据和在每个快照的使用：

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>请参阅

- [转换日志速率调控](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [弹性池 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [弹性池 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
