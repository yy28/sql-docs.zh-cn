---
title: sys.dm_db_xtp_checkpoint_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2f425607b124b90859368d71775fa988a6e286b3
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  返回与当前数据库中的内存中 OLTP 检查点操作有关的统计信息。 如果数据库中没有内存中 OLTP 对象，则返回空结果集。  
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 与较新版本具有显著差异和更低时在主题中讨论[SQL Server 2014](#bkmk_2014)。**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本  
 下表介绍中的列`sys.dm_db_xtp_checkpoint_stats`开头**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|控制器观察到的最后一个 LSN。|  
|end_of_log_lsn|**numeric(38)**|日志末尾 LSN。|  
|bytes_to_end_of_log|**bigint**|日志未处理的控制器，对应于之间的字节的字节数`last_lsn_processed`和`end_of_log_lsn`。|  
|log_consumption_rate|**bigint**|事务日志使用情况 （以 KB/秒） 的控制器的速率。|  
|active_scan_time_in_ms|**bigint**|通过主动扫描事务日志中的控制器所用的时间。|  
|total_wait_time_in_ms|**bigint**|不扫描日志时的控制器的累积等待时间。|  
|waits_for_io|**bigint**|等待日志 IO 引起控制器线程数。|  
|io_wait_time_in_ms|**bigint**|等待日志 IO 控制器线程所用的累计时间。|  
|waits_for_new_log_count|**bigint**|等待引起新的日志要生成的控制器线程数。|  
|new_log_wait_time_in_ms|**bigint**|按控制器线程等待新的日志所用的累计时间。|  
|idle_attempts_count|**bigint**|控制器转换为空闲状态的次数。|  
|tx_segments_dispatched|**bigint**|控制器观察到且分派给序列化程序的段的数。 段是日志的一个连续部分的窗体，序列化的一个单元。 它的当前大小为 1 MB 大小，但可以在将来更改。|  
|segment_bytes_dispatched|**bigint**|由于数据库重新启动调度到序列化程序，在控制器的字节的总字节数。|  
|bytes_serialized|**bigint**|由于数据库重新启动，序列化的字节总数。|  
|serializer_user_time_in_ms|**bigint**|通过在用户模式下的序列化程序所花费的时间。|  
|serializer_kernel_time_in_ms|**bigint**|通过在内核模式下的序列化程序所花费的时间。|  
|xtp_log_bytes_consumed|**bigint**|总消耗自数据库重新启动以来的日志字节数。|  
|checkpoints_closed|**bigint**|由于数据库重新启动已关闭的检查点计数。|  
|last_closed_checkpoint_ts|**bigint**|最后一个已关闭检查点的时间戳。|  
|hardened_recovery_lsn|**numeric(38)**|从此 LSN 开始将恢复。|  
|hardened_root_file_guid|**uniqueidentifier**|由于最后一个已完成的检查点强制写入的根文件 GUID。|  
|hardened_root_file_watermark|**bigint**|**内部仅**。 距离是有效的最多读取的根文件 （这是内部相关类型仅 – 调用 BSN）。|  
|hardened_truncation_lsn|**numeric(38)**|截断点 LSN。|  
|log_bytes_since_last_close|**bigint**|从上一个字节关闭到日志的当前末尾。|  
|time_since_last_close_in_ms|**bigint**|自上次关闭的检查点以来的时间。|  
|current_checkpoint_id|**bigint**|当前新的段正在分配给此检查点。 检查点系统是一种管道。 在当前检查点是从日志段分配给。 一旦它已达到限制，该检查点将由控制器和一个新创建为当前释放。|  
|current_checkpoint_segment_count|**bigint**|段中当前检查点的计数。|  
|recovery_lsn_candidate|**bigint**|**内部唯一**。 地选取作为 recoverylsn current_checkpoint_id 关闭时的候选。|  
|outstanding_checkpoint_count|**bigint**|等待要关闭管道中的检查点数目。|  
|closing_checkpoint_id|**bigint**|关闭检查点的 ID。<br /><br /> 序列化程序并行工作的因此它们完成后检查点是由关闭线程关闭的候选对象。 关闭线程可以仅关闭一次一个地，但必须是按顺序，因此关闭检查点是关闭线程正在处理的一个。|  
|recovery_checkpoint_id|**bigint**|要恢复中使用的检查点的 ID。|  
|recovery_checkpoint_ts|**bigint**|恢复检查点的时间戳。|  
|bootstrap_recovery_lsn|**numeric(38)**|引导的恢复 LSN。|  
|bootstrap_root_file_guid|**uniqueidentifier**|Bootstrap 的根文件 GUID。|  
|internal_error_code|**bigint**|归任何控制器、 序列化程序，关闭和合并线程时出错。|
|bytes_of_large_data_serialized|**bigint**|序列化的数据量。 |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 下表介绍中的列`sys.dm_db_xtp_checkpoint_stats`，为**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|该线程的当前日志序列号 (LSN) 和日志结尾之间的日志字节数。|  
|total_log_blocks_processed|**bigint**|自服务器启动以来处理的日志块总数。|  
|total_log_records_processed|**bigint**|自服务器启动以来处理的日志记录总数。|  
|xtp_log_records_processed|**bigint**|自服务器启动以来处理的内存中 OLTP 日志记录总数。|  
|total_wait_time_in_ms|**bigint**|累计等待时间（毫秒）。|  
|waits_for_io|**bigint**|日志 IO 的等待数。|  
|io_wait_time_in_ms|**bigint**|等待日志 IO 所用的累计时间。|  
|waits_for_new_log|**bigint**|生成新日志的等待数。|  
|new_log_wait_time_in_ms|**bigint**|等待新日志所用的累计时间。|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|自上一个内存中 OLTP 检查点以来生成的日志量。|  
|ms_since_last_checkpoint|**bigint**|自上一个内存中 OLTP 检查点以来的时间量（毫秒）。|  
|checkpoint_lsn|**numeric (38)**|与上次完成的内存中 OLTP 检查点关联的恢复日志序列号 (LSN)。|  
|current_lsn|**numeric (38)**|当前正在处理的日志记录的 LSN。|  
|end_of_log_lsn|**numeric (38)**|日志结尾的 LSN。|  
|task_address|**varbinary(8)**|SOS_Task 的地址。 联接到 sys.dm_os_tasks 以查找其他信息。|  
  
## <a name="permissions"></a>权限  
 要求具有对服务器的 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
