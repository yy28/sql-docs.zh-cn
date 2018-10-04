---
title: sys.dm_db_xtp_checkpoint_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 216b04e58d741d3c44cd187ba94eaac7ee791762
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837795"
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  返回与当前数据库中的内存中 OLTP 检查点操作有关的统计信息。 如果数据库中没有内存中 OLTP 对象，则返回空结果集。  
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 大大不同于较新版本和更低时在主题中讨论[SQL Server 2014](#bkmk_2014)。**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本  
 下表介绍中的列`sys.dm_db_xtp_checkpoint_stats`开头**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|控制器检测到的最后一个 LSN。|  
|end_of_log_lsn|**numeric(38)**|日志结尾 LSN。|  
|bytes_to_end_of_log|**bigint**|记录未处理的控制器，对应于之间字节的字节数`last_lsn_processed`和`end_of_log_lsn`。|  
|log_consumption_rate|**bigint**|事务日志消耗的控制器 （以 KB/秒） 的速率。|  
|active_scan_time_in_ms|**bigint**|通过主动扫描事务日志中的控制器所用的时间。|  
|total_wait_time_in_ms|**bigint**|累计等待时间为控制器的时不会扫描日志。|  
|waits_for_io|**bigint**|日志 IO 所产生的控制器线程的等待数。|  
|io_wait_time_in_ms|**bigint**|等待日志 IO 由控制器线程所用的累计时间。|  
|waits_for_new_log_count|**bigint**|所产生的新的日志要生成的控制器线程的等待数。|  
|new_log_wait_time_in_ms|**bigint**|由控制器线程等待新日志所用的累计时间。|  
|idle_attempts_count|**bigint**|在控制器转换为空闲状态次数。|  
|tx_segments_dispatched|**bigint**|控制器检测到并分派到序列化程序的段的数目。 段是日志的连续窗体序列化的单元部分。 它当前的大小为 1 mb 以内，但可以在将来的更改。|  
|segment_bytes_dispatched|**bigint**|由于数据库重新启动调度到序列化程序，控制器字节的总字节数。|  
|bytes_serialized|**bigint**|由于数据库重新启动序列化的字节总数。|  
|serializer_user_time_in_ms|**bigint**|序列化程序在用户模式下花费的时间。|  
|serializer_kernel_time_in_ms|**bigint**|序列化程序在内核模式下花费的时间。|  
|xtp_log_bytes_consumed|**bigint**|使用自该数据库重新启动以来的日志字节数的总计数。|  
|checkpoints_closed|**bigint**|由于数据库重新启动已关闭的检查点计数。|  
|last_closed_checkpoint_ts|**bigint**|最后一个已关闭检查点的时间戳。|  
|hardened_recovery_lsn|**numeric(38)**|从此 LSN 开始将恢复。|  
|hardened_root_file_guid|**uniqueidentifier**|强制写入的最后一个已完成检查点的结果的根文件的 GUID。|  
|hardened_root_file_watermark|**bigint**|**内部仅**。 延伸的范围是有效的最多读取的根文件 （这是在内部相关类型仅 – 调用 BSN）。|  
|hardened_truncation_lsn|**numeric(38)**|截断点的 LSN。|  
|log_bytes_since_last_close|**bigint**|从上一个字节接近当前日志的结尾。|  
|time_since_last_close_in_ms|**bigint**|自最后关闭的检查点的时间。|  
|current_checkpoint_id|**bigint**|要分配给此检查点的当前新段。 检查点系统是一个管道。 当前检查点是在日志中的段分配给。 一旦它已达到限制，检查点是由控制器和一个新创建的新发布。|  
|current_checkpoint_segment_count|**bigint**|当前检查点中的段的计数。|  
|recovery_lsn_candidate|**bigint**|**在内部仅**。 若要被挑选为 recoverylsn current_checkpoint_id 关闭时的候选项。|  
|outstanding_checkpoint_count|**bigint**|等待要关闭管道中的检查点的数目。|  
|closing_checkpoint_id|**bigint**|关闭检查点的 ID。<br /><br /> 序列化程序并行工作的因此一旦它们达到完成检查点是关闭线程即将关闭的候选版本。 但关闭线程可以仅关闭一次一个地，必须是按顺序，因此关闭检查点是关闭线程所处理的。|  
|recovery_checkpoint_id|**bigint**|若要在恢复中使用的检查点的 ID。|  
|recovery_checkpoint_ts|**bigint**|恢复检查点的时间戳。|  
|bootstrap_recovery_lsn|**numeric(38)**|有关 bootstrap 的恢复 LSN。|  
|bootstrap_root_file_guid|**uniqueidentifier**|Bootstrap 的根文件的 GUID。|  
|internal_error_code|**bigint**|看到的任何控制器、 序列化程序，关闭和合并线程时出错。|
|bytes_of_large_data_serialized|**bigint**|已序列化的数据量。 |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 下表介绍中的列`sys.dm_db_xtp_checkpoint_stats`，对于**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**。  
  
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
  
## <a name="permissions"></a>Permissions  
 要求具有对服务器的 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>请参阅  
 [内存优化表动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
