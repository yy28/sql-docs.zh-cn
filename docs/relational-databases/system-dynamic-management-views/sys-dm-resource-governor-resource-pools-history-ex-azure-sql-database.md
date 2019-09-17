---
title: sys.databases _resource_governor_resource_pools_history_ex （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
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
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: f94cc3ccd0278a3ae2f46707f2680f8d198db58a
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873926"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>sys.databases _resource_governor_resource_pools_history_ex （Transact-sql）

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

返回一个 Azure SQL 数据库的资源池统计信息的持续时间为20秒的快照，最大为32分钟（128 recs）。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|INT|资源池的 ID。 不可为 null。
|**name**|sysname|资源池的名称。 不可为 null。|
|**snapshot_time**|datetime2|拍摄的资源池统计信息快照的日期时间|
|**duration_ms**|INT|当前快照与前一个快照之间的持续时间|
|**statistics_start_time**|datetime2|为该池重置统计信息的时间。 不可为 null。|
|**active_session_count**|INT|当前快照中的活动会话总数|
|**active_worker_count**|INT|当前快照中的总工作进程数|
|**delta_cpu_usage_ms**|INT|自上次拍摄快照以来的 CPU 使用率（以毫秒为单位）。 不可为 null。|
|**delta_cpu_usage_preemptive_ms**|INT|自上一个快照以来，SQL CPU RG 未控制抢先式 win32 调用|
|**used_data_space_kb**|BIGINT|与用户池关联的用户数据库中使用的总空间|
|**allocated_disk_space_kb**|BIGINT|与用户池关联的中的用户数据库的数据文件总大小|
|**target_memory_kb**|BIGINT|此资源池试图获取的目标内存量（以 KB 为单位）。 这取决于当前设置和服务器状态。 不可为 null。|
|**used_memory_kb**|BIGINT|此资源池已用的内存量（以 KB 为单位）。 不可为 null。|
|**cache_memory_kb**|BIGINT|当前的缓存内存总用量（以 KB 为单位）。 不可为 null。|
|**compile_memory_kb**|BIGINT|当前总的内存盗用量（以 KB 为单位）。 这部分内存主要用于编译和优化，但也可能包括其他内存使用者所用的内存量。 不可为 null。|
|**active_memgrant_count**|BIGINT|当前内存授予计数。 不可为 null。|
|**active_memgrant_kb**|BIGINT|当前内存授予总量（以 KB 为单位）。 不可为 null。|
|**used_memgrant_kb**|BIGINT|当前通过内存授予使用（盗用）的内存总量。 不可为 null。|
|**delta_memgrant_timeout_count**|INT|此资源池中此资源池中内存授予超时的计数。 不可为 null。|
|**delta_memgrant_waiter_count**|INT|内存授予过程中当前挂起的查询数。 不可为 null。|
|**delta_out_of_memory_count**|INT|自上一次快照以来，池中失败的内存分配数。 不可为 null。|
|**delta_read_io_queued**|INT|自上次拍摄快照以来排队的总读取 Io。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_io_issued**|INT|自上次拍摄快照以来发出的读取 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_io_completed**|INT|自上次拍摄快照以来完成的读取 Io 总数。 不可为 null。|
|**delta_read_io_throttled**|INT|自快照以来限制的读取 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_read_bytes**|BIGINT|自上次拍摄快照以来读取的总字节数。 不可为 null。|
|**delta_read_io_stall_ms**|INT|自上次快照以来读取 IO 到达和完成之间的总时间（毫秒）。 不可为 null。|
|**delta_read_io_stall_queued_ms**|INT|自上一次快照以来读取 IO 到达和出现问题之间的总时间（毫秒）。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。 非零 delta_read_io_stall_queued_ms 表示 IO 受到 RG 的影响。|
|**delta_write_io_queued**|INT|自上次拍摄快照以来排队的总写入 Io。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_write_io_issued**|INT|自上次拍摄快照以来发出的写入 Io 总数。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_write_io_completed**|INT|自上次快照以来完成的写入 Io 总数。 不可为 Null。|
|**delta_write_io_throttled**|INT|自上一次快照以来限制的写入 Io 总数。 不可为 Null。|
|**delta_write_bytes**|BIGINT|自上次拍摄快照以来写入的总字节数。 不可为 null。|
|**delta_write_io_stall_ms**|INT|自上次快照以来写入 IO 到达和完成之间的总时间（毫秒）。 不可为 null。|
|**delta_write_io_stall_queued_ms**|INT|自上一次快照以来写入 IO 到达和问题之间的总时间（毫秒）。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**delta_io_issue_delay_ms**|INT|自上次快照以来，计划的问题与 IO 的实际问题之间的总时间（毫秒）。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**max_iops_per_volume**|INT|此池的每个磁盘卷的最大 IO 数（IOPS）。 可以为 Null。 如果没有为 IO 调控资源池，则为 null。|
|**max_memory_kb**|BIGINT|该资源池可拥有的最大内存量（以 KB 为单位）。 这取决于当前设置和服务器状态。 不可为 null。
|**max_log_rate_kb**|BIGINT|资源池级别的最大日志速率（每秒千字节）。|
|**max_data_space_kb**|BIGINT|此弹性池的最大弹性池存储限制设置（以 kb 为单位）。|
|**max_session**|INT|池的会话限制|
|**max_worker**|INT|池的辅助角色限制|
|**min_cpu_percent**|INT|存在 CPU 争用时此资源池中所有请求有保障的平均 CPU 带宽的当前配置。 不可为 null。|
|**max_cpu_percent**|INT|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。 不可为 null。|
|**cap_cpu_percent**|INT|资源池中的所有请求都将收到的 CPU 带宽硬性上限。 将 CPU 最大带宽级别限制为指定的级别。 允许的值范围为 1 到 100。 不可为 null。|
|**min_vcores**|decimal （5，2）|存在 CPU 争用时此资源池中所有请求有保障的平均 CPU 带宽的当前配置。  以 Vcore 为单位|
|**max_vcores**|decimal （5，2）|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。  In Vcore|
|**cap_vcores**|decimal （5，2）|资源池中的所有请求都将收到的 CPU 带宽硬性上限。  在 Vcore 上的单元中|
|**instance_cpu_count**|INT|为实例配置的 CPU 数|
|**instance_cpu_percent|decimal （5，2）|为实例配置的 CPU 百分比|
|**instance_vcores**|decimal （5，2）|为实例配置的 Vcore 数|
|**delta_log_bytes_used**|decimal （5，2）|自上一次快照以来的池级别的总日志生成（以字节为单位）|
|**avg_login_rate_percent**|decimal （5，2）|自上一次快照以来的登录次数与登录限制|
|**delta_vcores_used**|decimal （5，2）|自上一次拍摄快照以来 Vcore 计数的计算利用率。|
|**cap_vcores_used_percent**|decimal （5，2）|平均计算使用率（以池限制的百分比表示）。|
|**instance_vcores_used_percent**|decimal （5，2）|平均计算使用率（以 SQL 实例限制的百分比表示）。|
|**avg_data_io_percent**|decimal （5，2）|平均 i/o 利用率（以百分比表示），基于池的限制。|
|**avg_log_write_percent**|decimal （5，2）|平均写入资源使用率（以池限制的百分比表示）。|
|**avg_storage_percent**|decimal （5，2）|池的存储限制的平均存储利用率（以百分比表示）。|
|**avg_allocated_storage_percent**|decimal （5，2）|弹性池中所有数据库分配的数据空间百分比。 这是为弹性池分配的数据空间与数据最大大小的比率。 有关详细信息，请参阅：SQL DB 中的文件空间管理|
|**max_worker_percent**|decimal （5，2）|以百分比表示的最大并发工作线程数（以百分比表示）。|
|**max_session_percent**|decimal （5，2）|基于池的限制的最大并发会话数（以百分比表示）。|
|||

## <a name="permissions"></a>权限

此视图需要 VIEW SERVER STATE 权限。

## <a name="remarks"></a>备注

用户可以使用此动态管理视图来监视用户工作负荷池的近乎实时的资源消耗以及 Azure SQL 数据库实例的系统内部池。

> [!IMPORTANT]
> 此 DMV 提供的大多数数据都适用于内部使用，并可能会发生更改。

## <a name="examples"></a>示例

下面的示例按用户池返回每个快照上的最大日志速率数据和消耗量  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

下面的示例返回的信息类似于 elastic_pool_resource_stats，无需连接到逻辑主节点

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

- [翻译日志率治理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [弹性池 DTU 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [弹性池 vCore 资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
