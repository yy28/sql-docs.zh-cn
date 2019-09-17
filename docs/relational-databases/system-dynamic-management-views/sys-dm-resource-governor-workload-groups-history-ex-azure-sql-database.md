---
title: sys.databases _resource_governor_workload_groups_history_ex （Azure SQL 数据库） |Microsoft Docs
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
ms.openlocfilehash: 5fea5badf14ce9863f07dff189f1665788ec5fb6
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873770"
---
# <a name="sysdm_resource_governor_workload_groups_history_ex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回一个 Azure SQL 数据库的资源池统计信息的持续时间为20秒的快照，最大为32分钟（128 recs）。
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**| INT |资源池的 ID。 不可为 null。|
|**group_id**| INT |工作负荷组的 ID。 不可为 null。|
|**name**| nvarchar(256) |工作负荷组的名称。 不可为 null。|
|**snapshot_time**| DATETIME |拍摄的资源组统计快照的日期时间。|
|**duration_ms**| INT |当前快照与前一个快照之间的持续时间。|
|**active_worker_count**| INT |当前快照中的总工作进程数。|
|**active_request_count**| INT |当前请求计数。 不可为 null。|
|**active_session_count**| INT |当前快照中的活动会话总数。|
|**total_request_count**| BIGINT |工作负荷组中已完成请求的累计计数。 不可为 null。|
|**delta_request_count**| INT |自上次快照以来工作负荷组中的已完成请求计数。 不可为 null。|
|**total_cpu_usage_ms**| BIGINT |此工作负荷组的累计 CPU 使用情况，以毫秒为单位。 不可为 null。|
|**delta_cpu_usage_ms**| INT |自上次拍摄快照以来的 CPU 使用率（以毫秒为单位）。 不可为 null。|
|**delta_cpu_usage_preemptive_ms**| INT |自上次拍摄快照以来，SQL CPU RG 不会控制抢先式 win32 调用。|
|**delta_reads_reduced_memgrant_count**| INT |自上次快照以来，已达到最大查询大小限制的内存授予数。 不可为 null。|
|**reads_throttled**| INT |已限制的读取总次数。|
|**delta_reads_queued**| INT |自上次拍摄快照以来排队的总读取 Io。 可以为 Null。 如果资源组不属于 IO，则为 Null。|
|**delta_reads_issued**| INT |自上次拍摄快照以来发出的读取 Io 总数。 可以为 Null。 如果资源组不属于 IO，则为 Null。|
|**delta_reads_completed**| INT |自上次拍摄快照以来完成的读取 Io 总数。 不可为 null。|
|**delta_read_bytes**| BIGINT |自上次拍摄快照以来读取的总字节数。 不可为 null。|
|**delta_read_stall_ms**| INT |自上次快照以来读取 IO 到达和完成之间的总时间（毫秒）。 不可为 null。|
|**delta_read_stall_queued_ms**| INT |自上一次快照以来读取 IO 到达和出现问题之间的总时间（毫秒）。 可以为 Null。 如果资源组不属于 IO，则为 Null。 非零 delta_read_stall_queued_ms 表示 IO 受到 RG 的影响。|
|**delta_writes_queued**| INT |自上次拍摄快照以来排队的总写入 Io。 可以为 Null。 如果资源组不属于 IO，则为 Null。|
|**delta_writes_issued**| INT |自上次拍摄快照以来发出的写入 Io 总数。 可以为 Null。 如果资源组不属于 IO，则为 Null。|
|**delta_writes_completed**| INT |自上次快照以来完成的写入 Io 总数。 不可为 null。|
|**delta_writes_bytes**| BIGINT |自上次拍摄快照以来写入的总字节数。 不可为 null。|
|**delta_write_stall_ms**| INT |自上次快照以来写入 IO 到达和完成之间的总时间（毫秒）。 不可为 null。|
|**delta_background_writes**| INT |自上一次快照以来后台任务执行的总写入数。|
|**delta_background_write_bytes**| BIGINT |自上一次快照以来后台任务所执行的总写入大小（以字节为单位）。|
|**delta_log_bytes_used**| BIGINT |自上次快照以来使用的日志（字节）。|
|**delta_log_temp_db_bytes_used**| BIGINT |自上次快照以来使用的 Tempdb 日志（字节）。|
|**delta_query_optimizations**| BIGINT |自上一次快照以来此工作负荷组中的查询优化数。 不可为 null。|
|**delta_suboptimal_plan_generations**| BIGINT |由于自上次拍摄快照以来的内存压力导致此工作负荷组中发生的不理想计划生成的计数。 不可为 null。
|**max_memory_grant_kb**| BIGINT |组的最大内存授予（KB）。|
|**max_request_cpu_msec**| BIGINT |单个请求的最大 CPU 使用情况，以毫秒为单位。 不可为 null。|
|**max_concurrent_request**| INT |并发请求最大数的当前设置。 不可为 null。|
|**max_io**| INT |组的最大 IO 限制。|
|**max_global_io**| INT |标识为仅供参考。 不受支持。 不保证以后的兼容性。
|**max_queued_io**| INT |标识为仅供参考。 不受支持。 不保证以后的兼容性。|
|**max_log_rate_kb**| BIGINT |资源组级别的最大日志速率（每秒千字节）。|
|**max_session**| INT |组的会话限制。|
|**max_worker**| INT |组的辅助角色限制。|
|||

## <a name="permissions"></a>权限

此视图需要 VIEW SERVER STATE 权限。

## <a name="remarks"></a>备注

用户可以使用此动态管理视图来监视用户工作负荷池的近乎实时的资源消耗以及 Azure SQL 数据库实例的系统内部池。

> [!IMPORTANT]
> 此 DMV 提供的大多数数据都适用于内部使用，并可能会发生更改。

## <a name="examples"></a>示例

下面的示例按用户池返回每个快照上的最大日志速率数据和使用量：

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

- [翻译日志率治理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [弹性池 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [弹性池 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
