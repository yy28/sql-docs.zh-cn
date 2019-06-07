---
title: sys.dm_resource_governor_resource_pools_history_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: d585f1f1245457aa9051f25bca696cf4495d93ed
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66743924"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

返回快照在 15 秒间隔过去 30 分钟的资源池统计信息为 Azure SQL 数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|ssNoversion|资源池的 ID。 不可为 null。
|**名称**|sysname|资源池的名称。 不可为 null。|
|**snapshot_time**|datetime2|拍摄的资源池统计信息快照的日期时间|
|**duration_ms**|ssNoversion|当前和以前的快照之间的持续时间|
|**statistics_start_time**|datetime2|为该池重置统计信息的时间。 不可为 null。|
|**active_session_count**|ssNoversion|当前快照中的活动会话总数|
|**active_worker_count**|ssNoversion|当前快照中的工作线程总数|
|**delta_cpu_usage_ms**|ssNoversion|自上一个快照以来的毫秒的 CPU 使用率。 不可为 null。|
|**delta_cpu_usage_preemptive_ms**|ssNoversion|抢先式的 win32 调用不管理，方法是 SQL CPU RG 上一个快照以来|
|**used_data_space_kb**|BIGINT|将用于与用户池相关联的用户数据库中的总空间|
|**allocated_disk_space_kb**|BIGINT|总数据文件中关联的用户数据库的大小与用户池|
|**target_memory_kb**|BIGINT|此资源池试图获取的目标内存量（以 KB 为单位）。 这取决于当前设置和服务器状态。 不可为 null。|
|**used_memory_kb**|BIGINT|此资源池已用的内存量（以 KB 为单位）。 不可为 null。|
|**cache_memory_kb**|BIGINT|当前的缓存内存总用量（以 KB 为单位）。 不可为 null。|
|**compile_memory_kb**|BIGINT|当前总的内存盗用量（以 KB 为单位）。 这部分内存主要用于编译和优化，但也可能包括其他内存使用者所用的内存量。 不可为 null。|
|**active_memgrant_count**|BIGINT|当前内存授予计数。 不可为 null。|
|**active_memgrant_kb**|BIGINT|当前内存授予总量（以 KB 为单位）。 不可为 null。|
|**used_memgrant_kb**|BIGINT|当前通过内存授予使用（盗用）的内存总量。 不可为 null。|
|**delta_memgrant_timeout_count**|ssNoversion|在此期限内，计数的内存授予此资源池中的超时。 不可为 null。|
|**delta_memgrant_waiter_count**|ssNoversion|内存授予过程中当前挂起的查询数。 不可为 null。|
|**delta_out_of_memory_count**|ssNoversion|自上一个快照以来池中的失败的内存分配数。 不可为 null。|
|**delta_read_io_queued**|ssNoversion|自上一个快照以来的读取 IOs 排入队列的总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_io_issued**|ssNoversion|读取自上一个快照以来发出的 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_io_completed**|ssNoversion|读取自上一个快照以来完成的 Io 总数。 不可为 null。|
|**delta_read_io_throttled**|ssNoversion|读取自快照以来限制的 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_bytes**|BIGINT|自上一个快照以来读取的字节总数。 不可为 null。|
|**delta_read_io_stall_ms**|ssNoversion|读的 IO 到达和完成自上一个快照之间 （以毫秒为单位） 的总时间。 不可为 null。|
|**delta_read_io_stall_queued_ms**|ssNoversion|读 IO 到达和发出自上一个快照之间 （以毫秒为单位） 的总时间。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。 非零 delta_read_io_stall_queued_ms 意味着 IO 受 RG。|
|**delta_write_io_queued**|ssNoversion|自上一个快照以来的写入 IOs 排入队列的总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_write_io_issued**|ssNoversion|写入自上一个快照以来发出的 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_write_io_completed**|ssNoversion|写入自上一个快照以来完成的 Io 总数。 不可为 Null。|
|**delta_write_io_throttled**|ssNoversion|总写入自上一个快照以来限制 IOs。 不可为 Null。|
|**delta_write_bytes**|BIGINT|自上一个快照以来写入的字节总数。 不可为 null。|
|**delta_write_io_stall_ms**|ssNoversion|写 IO 到达和完成自上一个快照之间 （以毫秒为单位） 的总时间。 不可为 null。|
|**delta_write_io_stall_queued_ms**|ssNoversion|写 IO 到达和发出自上一个快照之间 （以毫秒为单位） 的总时间。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_io_issue_delay_ms**|ssNoversion|（以毫秒为单位） 的计划的问题和实际发出 IO 自上一个快照之间的总时间。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**max_iops_per_volume**|ssNoversion|最大每秒 I/O (操作数 IOPS) 每个磁盘卷设置为此池。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**max_memory_kb**|BIGINT|该资源池可拥有的最大内存量（以 KB 为单位）。 这取决于当前设置和服务器状态。 不可为 null。
|**max_log_rate_kb**|BIGINT|资源池级别的最大日志速率 （每秒千字节）。|
|**max_data_space_kb**|BIGINT|最大弹性池存储限制设置为以千字节此弹性池。|
|**max_session**|ssNoversion|池的会话数限制|
|**max_worker**|ssNoversion|辅助角色池的限制|
|**min_cpu_percent**|ssNoversion|存在 CPU 争用时此资源池中所有请求有保障的平均 CPU 带宽的当前配置。 不可为 null。|
|**max_cpu_percent**|ssNoversion|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。 不可为 null。|
|**cap_cpu_percent**|ssNoversion|资源池中的所有请求都将收到的 CPU 带宽硬性上限。 将 CPU 最大带宽级别限制为指定的级别。 允许的值范围为 1 到 100。 不可为 null。|
|**min_vcores**|decimal(5,2)|存在 CPU 争用时此资源池中所有请求有保障的平均 CPU 带宽的当前配置。  Vcore 为单位|
|**max_vcores**|decimal(5,2)|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。  中的 Vcore 单位|
|**cap_vcores**|decimal(5,2)|资源池中的所有请求都将收到的 CPU 带宽硬性上限。  在上个 Vcore 单元|
|**instance_cpu_count**|ssNoversion|为实例配置 CPU 的数目|
|**instance_cpu_percent|decimal(5,2)|为实例配置 CPU 百分比|
|**instance_vcores**|decimal(5,2)|为实例配置的 Vcore 数|
|**delta_log_bytes_used**|decimal(5,2)|总的日志 （以字节为单位） 池级生成自上一个快照以来|
|**avg_login_rate_percent**|decimal(5,2)|自上一个快照，登录限制进行比较的登录次数|
|**delta_vcores_used**|decimal(5,2)|计算资源使用率的 Vcore 计数自上一个快照。|
|**cap_vcores_used_percent**|decimal(5,2)|平均计算使用率百分比形式表示的池的限制。|
|**instance_vcores_used_percent**|decimal(5,2)|平均计算使用率百分比形式表示的 SQL 实例的限制。|
|**avg_data_io_percent**|decimal(5,2)|以基于池限制百分比表示的平均 I/O 使用率。|
|**avg_log_write_percent**|decimal(5,2)|平均写入资源使用率百分比形式表示的池的限制。|
|**avg_storage_percent**|decimal(5,2)|以池的存储限制的百分比表示的平均存储使用率。|
|**avg_allocated_storage_percent**|decimal(5,2)|分配的弹性池中所有数据库的数据空间的百分比。 这是分配给数据弹性池的最大大小的数据空间的比率。 有关详细信息，请参阅：SQL DB 中的文件空间管理|
|**max_worker_percent**|decimal(5,2)|最大并发辅助进程 （请求） 以基于池限制百分比表示。|
|**max_session_percent**|decimal(5,2)|以基于池限制百分比表示的最大并发会话。|
|||

## <a name="permissions"></a>权限

此视图需要 VIEW SERVER STATE 权限。

## <a name="remarks"></a>备注

用户可以访问此动态管理视图来监视近乎实时的用户工作负荷池，以及 Azure SQL 数据库实例的系统内部池的资源消耗。

> [!IMPORTANT]
> 此 dmv 显示的数据的大多数专供内部使用，可能会发生更改。

## <a name="examples"></a>示例

下面的示例返回按用户池的最大日志速率数据和在每个快照的使用情况  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

下面的示例返回类似信息作为 sys.elastic_pool_resource_stats 而无需连接到逻辑主服务器

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>请参阅

- [转换日志速率调控](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [弹性池 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [弹性池 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
