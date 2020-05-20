---
title: sys. query_store_query （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 073c90b18d9f6fb8b75bf5da44f3d3817d8f296c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831404"
---
# <a name="sysquery_store_query-transact-sql"></a>sys. query_store_query （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关查询及其关联的总体运行时执行统计信息的信息。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|主密钥。|  
|**query_text_id**|**bigint**|外键。 联接到[sys.databases query_store_query_text &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|外键。 联接到[sys.databases&#41;的 query_context_settings &#40;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**object_id**|**bigint**|查询所属的数据库对象的 ID （存储过程、触发器、CLR UDF/UDAgg 等）。 如果查询不是作为数据库对象（即席查询）的一部分执行，则为0。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**batch_sql_handle**|**varbinary(64)**|查询所属的语句批处理的 ID。 仅当查询引用临时表或表变量时才填充。<br/>**注意：** Azure SQL 数据仓库将始终返回*NULL*。|  
|**query_hash**|**binary （8）**|基于逻辑查询树的单个查询的 MD5 哈希。 包含优化器提示。|  
|**is_internal_query**|**bit**|查询是在内部生成的。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**query_parameterization_type**|**tinyint**|参数化类型：<br /><br /> 0 - 无<br /><br /> 1-用户<br /><br /> 2-简单<br /><br /> 3-强制<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**query_parameterization_type_desc**|**nvarchar(60)**|参数化类型的文本说明。<br/>**注意：** Azure SQL 数据仓库将始终返回*None*。|  
|**initial_compile_start_time**|**datetimeoffset**|编译开始时间。|  
|**last_compile_start_time**|**datetimeoffset**|编译开始时间。|  
|**last_execution_time**|**datetimeoffset**|上次执行时间是指查询/计划的最后结束时间。|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|上次使用查询的 SQL 批处理的句柄。 可以将其作为输入提供给[sys. dm_exec_sql_text &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) ，以获取该批的完整文本。<br/>**注意：** Azure SQL 数据仓库将始终返回*NULL*。|  
|**last_compile_batch_offset_start**|**bigint**|可提供给 sys.databases dm_exec_sql_text 和 last_compile_batch_sql_handle 的信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**last_compile_batch_offset_end**|**bigint**|可提供给 sys.databases dm_exec_sql_text 和 last_compile_batch_sql_handle 的信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**count_compiles**|**bigint**|编译统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回一（1）。|  
|**avg_compile_duration**|**float**|编译统计信息（微秒）。|  
|**last_compile_duration**|**bigint**|编译统计信息（微秒）。|  
|**avg_bind_duration**|**float**|绑定统计信息（微秒）。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**last_bind_duration**|**bigint**|绑定统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**avg_bind_cpu_time**|**float**|绑定统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**last_bind_cpu_time**|**bigint**|绑定统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|  
|**avg_optimize_duration**|**float**|优化统计信息（微秒）。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**last_optimize_duration**|**bigint**|优化统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**avg_optimize_cpu_time**|**float**|优化统计信息（微秒）。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**last_optimize_cpu_time**|**bigint**|优化统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**avg_compile_memory_kb**|**float**|编译内存统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**last_compile_memory_kb**|**bigint**|编译内存统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**max_compile_memory_kb**|**bigint**|编译内存统计信息。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
|**is_clouddb_internal_query**|**bit**|在本地始终为 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br/>**注意：** Azure SQL 数据仓库将始终返回零（0）。|
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys. database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys. query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
