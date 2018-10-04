---
title: 系统视图中，内存中 OLTP 的存储过程、 Dmv 和等待类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04b2d0fdd00d9f3001ce1687744a9ecd992f44dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144617"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>系统视图、存储过程、内存中 OLTP 的 DMV 和等待类型
  本主题提供针对许多支持内存中 OLTP 的数据库对象的简短描述，以及指向它们的链接。  
  
### <a name="system-views"></a>系统视图  
  
|系统视图|Description|内存中 OLTP 功能|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|检查文件组是否包含内存优化的数据。|以下各列显示其他的值：**类型**并**type_desc**。|  
|[sys.indexes (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|检查内存优化表中是否存在索引。|以下各列显示其他的值：**类型**并**type_desc**。|  
|[sys.parameters (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|检查参数是否非 Null（这样可更高效地执行本机编译存储过程）。|**is_nullable**列。|  
|[sys.all_sql_modules &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|检查存储过程是否是本机编译存储过程。|**uses_native_compilation**列。|  
|[sys.sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|检查存储过程是否是本机编译存储过程。|**uses_native_compilation**列。|  
|[sys.table_types &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|检查表是否经过内存优化。|**is_memory_optimized**列。|  
|[sys.tables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|检查表是否经过内存优化，并检查表的持续性设置。|**持续性**， **durability_desc**，和**is_memory_optimized**列。|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|显示内存优化表的哈希索引。|特定的内存中 OLTP。|  
  
### <a name="metadata-functions"></a>元数据函数  
  
|元数据函数|Description|内存中 OLTP 功能|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX (Transact-SQL)](/sql/t-sql/functions/objectproperty-transact-sql)|检查数据库对象是否经过内存优化。|**ExecIsWithNativeCompilation**并**TableIsMemoryOptimized**属性。<br /><br /> **IsSchemaBound**属性支持过程对象类型 （返回 0 表示过程而不是 NULL）。|  
|[SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)|检查服务器是否支持内存中 OLTP。|**IsXTPSupported**属性。|  
  
### <a name="system-stored-procedures"></a>系统存储过程  
  
|存储过程|Description|  
|----------------------|-----------------|  
|[sys.sp_xtp_bind_db_resource_pool &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|将内存中 OLTP 数据库绑定至资源池。|  
|[sys.sp_xtp_checkpoint_force_garbage_collection &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|启动内存中 OLTP 数据库的垃圾回收。|  
|[sys.sp_xtp_control_proc_exec_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|允许对本机编译的存储过程收集统计信息。|  
|[sys.sp_xtp_control_query_exec_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|允许根据查询对本机编译的存储过程收集统计信息。|  
|[sys.sp_xtp_merge_checkpoint_files &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|合并数据和差异文件。|  
|[sys.sp_xtp_unbind_db_resource_pool &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|删除数据库和资源池之间的绑定。|  
  
## <a name="dynamic-management-views-dmvs"></a>动态管理视图 (DMV)  
 存在几个适用于内存优化表的 DMV。  
  
 有关详细信息，请参阅[内存优化表动态管理视图&#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql)。  
  
## <a name="wait-types"></a>等待类型  
 存在几个支持内存中 OLTP 的等待类型。  
  
 有关详细信息，请参阅等待都带有前缀的类型**WAIT_XTP**，并**XTPPROC**中[sys.dm_os_wait_stats &#40;-&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)主题。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [对内存中 OLTP 的 Transact-SQL 支持](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
