---
title: sys.dm_exec_query_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
caps.latest.revision: 64
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f758b902012ecbc3f13921fccd0326ec94fc918a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34468223"
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回缓存的查询计划中的聚合性能统计信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 缓存计划中的每个查询语句在该视图中对应一行，并且行的生存期与计划本身相关联。 在从缓存删除计划时，也将从该视图中删除对应行。  
  
> [!NOTE]
> 初始查询**sys.dm_exec_query_stats**可能会产生不准确的结果，如果没有在服务器上当前正在执行的工作负荷。 可以通过重新运行查询来确定更准确的结果。  
  
> [!NOTE]
> 若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_query_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |表示包含查询的批查询或存储过程的标记。<br /><br /> **sql 句柄**以及**statement_start_offset**和**语句结束偏移量**，可以用于检索查询的 SQL 文本通过调用**sys.dm_exec_sql_文本**动态管理函数。|  
|**statement_start_offset**|**int**|指示行所说明的查询在其批查询或持久化对象文本中的开始位置（以字节为单位，从 0 开始）。|  
|**statement_end_offset**|**int**|指示行所说明的查询在其批查询或持久化对象文本中的结束位置（以字节为单位，从 0 开始）。 之前的版本为[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，值为-1 指示批处理的末尾。 不再包括尾随的注释。|  
|**plan_generation_num**|**bigint**|可用于在重新编译后区分不同计划实例的序列号。|  
|**plan_handle**|**varbinary(64)**|表示查询所属的已编译计划的标记。 此值可以传递给[sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)动态管理函数来获取查询计划。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0x000。|  
|**creation_time**|**datetime**|编译计划的时间。|  
|**last_execution_time**|**datetime**|上次开始执行计划的时间。|  
|**execution_count**|**bigint**|计划自上次编译以来所执行的次数。|  
|**total_worker_time**|**bigint**|此计划自编译以来执行所用的 CPU 时间总量（以微秒为单位报告，但仅精确到毫秒）。<br /><br /> 对于本机编译的存储过程，如果许多执行所用的时间都不到 1 毫秒，则 **total_worker_time** 可能不精确。|  
|**last_worker_time**|**bigint**|上次执行计划所用的 CPU 时间（以微秒为单位报告，但仅精确到毫秒）。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|此计划在单次执行期间所用的最小 CPU 时间（以微秒为单位报告，但仅精确到毫秒）。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|此计划在单次执行期间所用的最大 CPU 时间（以微秒为单位报告，但仅精确到毫秒）。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|此计划自编译后在执行期间所执行的物理读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_physical_reads**|**bigint**|上次执行计划时所执行的物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_physical_reads**|**bigint**|此计划在单个执行期间所执行的最少物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_physical_reads**|**bigint**|此计划在单个执行期间所执行的最多物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_writes**|**bigint**|此计划自编译后在执行期间所执行的逻辑写入总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_writes**|**bigint**|上次执行计划时变脏的缓冲池页数。 如果页已变脏（已修改），则不计入写次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_writes**|**bigint**|此计划在单个执行期间所执行的最少逻辑写入次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_writes**|**bigint**|此计划在单个执行期间所执行的最多逻辑写入次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_reads**|**bigint**|此计划自编译后在执行期间所执行的逻辑读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_reads**|**bigint**|上次执行计划时所执行的逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_reads**|**bigint**|此计划在单个执行期间所执行的最少逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_reads**|**bigint**|此计划在单个执行期间所执行的最多逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_clr_time**|**bigint**|时间以微秒为单位 （但仅精确到毫秒） 内用报告[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR) 对象所执行的此计划自编译后。 CLR 对象可以是存储过程、函数、触发器、类型和聚合。|  
|**last_clr_time**|**bigint**|时间以微秒为单位 （但仅精确到毫秒） 内的执行所用的报告[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]期间一次执行此计划的 CLR 对象。 CLR 对象可以是存储过程、函数、触发器、类型和聚合。|  
|**min_clr_time**|**bigint**|此计划在单次执行期间在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 对象内所用的最小时间（以微秒为单位报告，但仅精确到毫秒）。 CLR 对象可以是存储过程、函数、触发器、类型和聚合。|  
|**max_clr_time**|**bigint**|此计划在单次执行期间在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 内所用的最大时间（以微秒为单位报告，但仅精确到毫秒）。 CLR 对象可以是存储过程、函数、触发器、类型和聚合。|  
|**total_elapsed_time**|**bigint**|上次完成执行此计划所用的总时间（以微秒为单位报告，但仅精确到毫秒）。|  
|**last_elapsed_time**|**bigint**|最近一次完成执行此计划所用的时间（以微秒为单位报告，但仅精确到毫秒）。|  
|**min_elapsed_time**|**bigint**|任何一次完成执行此计划所用的最小时间（以微秒为单位报告，但仅精确到毫秒）。|  
|**max_elapsed_time**|**bigint**|任何一次完成执行此计划所用的最大时间（以微秒为单位报告，但仅精确到毫秒）。|  
|**query_hash**|**Binary(8)**|对查询计算的二进制哈希值，用于标识具有类似逻辑的查询。 可以使用查询哈希确定仅仅是文字值不同的查询的聚合资源使用情况。|  
|**query_plan_hash**|**binary(8)**|对查询执行计划计算的二进制哈希值，用于标识类似的查询执行计划。 可以使用查询计划哈希查找具有类似执行计划的查询的累积成本。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0x000。|  
|**total_rows**|**bigint**|查询返回的总行数。 不能为 Null。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0。|  
|**last_rows**|**bigint**|上一次执行查询返回的行数。 不可为 null。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0。|  
|**min_rows**|**bigint**|最小曾经在一个执行期间由查询返回的行数。 不可为 null。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0。|  
|**max_rows**|**bigint**|在一个执行期间曾返回查询的行的最大数量。 不可为 null。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0。|  
|**statement_sql_handle**|**varbinary(64)**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 仅当启用查询存储区使用非 NULL 值填充并收集有关该特定查询的统计信息。|  
|**statement_context_id**|**bigint**|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 仅当启用查询存储区使用非 NULL 值填充并收集有关该特定查询的统计信息。|  
|**total_dop**|**bigint**|并行度的总和自编译后使用此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_dop**|**bigint**|在执行此计划的最后一次时的并行度。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_dop**|**bigint**|最小的并行度此计划曾经使用一次执行中。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_dop**|**bigint**|最大并行度此计划曾经使用一次执行中。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_grant_kb**|**bigint**|保留内存的总量 (KB) 中授予自编译后以后接收此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_grant_kb**|**bigint**|在执行上一次此计划时，则将授予的保留的内存量以 kb 为单位。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_grant_kb**|**bigint**|最小保留内存量 (KB) 中授予在一个执行期间曾收到此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_grant_kb**|**bigint**|最大保留的内存量 (KB) 中授予在一个执行期间曾收到此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_used_grant_kb**|**bigint**|保留内存的总量 (KB) 中授予此计划自编译后使用。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_used_grant_kb**|**bigint**|以 kb 为单位在执行此计划的最后一次时使用的内存授予量。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_used_grant_kb**|**bigint**|最小已用内存量 (KB) 中授予一次执行中曾经使用此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_used_grant_kb**|**bigint**|已用内存的最大量授予一次执行中曾经使用此计划以 kb 为单位。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_ideal_grant_kb**|**bigint**|以 kb 为单位估计的此计划自编译后的理想内存授予的总量。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_ideal_grant_kb**|**bigint**|在执行上一次此计划时，则将授予的理想内存量以 kb 为单位。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_ideal_grant_kb**|**bigint**|在一个执行期间曾估计此计划 (KB) 中授予的最小理想内存量。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_ideal_grant_kb**|**bigint**|在一个执行期间曾估计此计划 (KB) 中授予的最大理想内存量。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_reserved_threads**|**bigint**|保留的并行的总和线程曾经使用自编译后此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_reserved_threads**|**bigint**|在执行此计划的最后一次时的保留并行线程数。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_reserved_threads**|**bigint**|最小保留并行数线程一次执行中曾经使用此计划。  它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_reserved_threads**|**bigint**|最大的保留的并行线程数一次执行中曾经使用此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_used_threads**|**bigint**|总和使用并行线程曾经使用自编译后此计划。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_used_threads**|**bigint**|在执行此计划的最后一次时使用的并行线程数。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_used_threads**|**bigint**|使用此计划曾经使用一次执行中的并行线程中最小的数。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_used_threads**|**bigint**|使用一次执行中曾经使用此计划的并行线程的最大数目。 它将始终为 0 表示查询的内存优化表。<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_columnstore_segment_reads**|**bigint**|读取查询的列存储段的总和。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**last_columnstore_segment_reads**|**bigint**|列存储段读取上一次执行的查询数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**min_columnstore_segment_reads**|**bigint**|读过查询一次执行中的列存储段中最小的数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**max_columnstore_segment_reads**|**bigint**|读过查询一次执行中的列存储段中最大的数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**total_columnstore_segment_skips**|**bigint**|查询已跳过的列存储段的总和。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**last_columnstore_segment_skips**|**bigint**|列存储段跳过上一次执行的查询数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**min_columnstore_segment_skips**|**bigint**|曾经通过跳过查询一次执行中的列存储段中最小的数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**max_columnstore_segment_skips**|**bigint**|曾经通过跳过查询一次执行中的列存储段中最大的数。 不可为 null。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|
|**total_spills**|**bigint**|自编译后，通过执行此查询溢出的页的总数。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|总页数溢出的上次执行查询时。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|此查询在单个执行期间曾溢出的页中最小的数。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|最大页数单次执行期间曾溢出此查询。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**pdw_node_id**|**int**|此分布的节点标识符。<br /><br /> **适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 

> [!NOTE]
> <sup>1</sup>对于本机编译存储过程启用统计信息收集后，工作线程时间收集以毫秒为单位。 如果查询执行小于一毫秒，值将为 0。  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
   
## <a name="remarks"></a>注释  
 查询完成后，将更新该视图中的统计信息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-finding-the-top-n-queries"></a>A. 查找 TOP N 查询  
 以下示例按平均 CPU 时间返回排名前五个的查询的相关信息。 此示例将根据查询的查询哈希对查询进行聚合，以便按照查询的累积资源消耗来分组在逻辑上等效的查询。  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. 对查询返回行计数聚合  
 以下示例返回查询的行计数聚合信息（总行数、最小行数、最大行数和上一次行数）。  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>另请参阅  
[执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_procedure_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


