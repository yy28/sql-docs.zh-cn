---
title: "监视本机编译的存储过程的执行 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 监视本机编译的存储过程的执行
  本主题论述如何监视本机编译的存储过程的性能  
  
## 使用扩展事件  
 使用 **sp_statement_completed** 扩展事件可以跟踪查询的执行情况。 使用此事件或者可以选择使用针对某一特定本机编译的存储过程的 object_id 的筛选器创建一个扩展事件会话。在执行各查询后引发该扩展事件。 该扩展事件报告的 CPU 时间和持续时间指示该查询占用了多少 CPU 以及执行时间。 占用大量 CPU 时间的本机编译的存储过程可能具有性能问题。  
  
 **line_number**，连同扩展事件中的 **object_id** 可用于调查该查询。 可以使用以下查询检索过程定义。 可以使用行号标识该定义内的查询：  
  
```tsql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 有关 **sp_statement_completed** 扩展事件的详细信息，请参阅[如何检索导致了事件的语句](http://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx)。  
  
## 使用数据管理视图  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持在过程级别和查询级别收集本机编译的存储过程的执行统计信息。 由于对性能的影响，默认不启用收集执行统计信息。  
  
 可使用 [sys.sp_xtp_control_proc_exec_stats (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) 对本机编译的存储过程启用和禁用统计信息收集。  
  
 通过 [sys.sp_xtp_control_proc_exec_stats (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) 启用统计信息收集后，你可以使用 [sys.dm_exec_procedure_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 监视本机编译存储过程的性能。  
  
 通过 [sys.sp_xtp_control_query_exec_stats (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 启用统计信息收集后，你可以使用 [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 监视本机编译存储过程的性能。  
  
 在收集开始时，启用统计信息收集。 然后，执行本机编译的存储过程。 在收集结束时，禁用统计信息收集。 然后，对 DMV 返回的执行统计信息进行分析。  
  
 在你收集统计信息后，可以使用 [sys.dm_exec_procedure_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 针对某一过程查询本机编译的存储过程的执行统计信息，以及使用 [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 针对查询来查询本机编译的存储过程的执行统计信息。  
  
> [!NOTE]  
>  对于启用统计信息收集时的本机编译的存储过程，以毫秒为单位收集工作线程时间。 如果查询执行不到 1 毫秒，则该值将为 0。 对于本机编译的存储过程，如果许多执行所用的时间都不到 1 毫秒，则 **total_worker_time** 可能不精确。  
  
 下面的查询在统计信息收集后返回当前数据库中本机编译的存储过程的过程名称和执行统计信息：  
  
```tsql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 下面的查询按总工作线程时间的降序返回当前数据库中已为其收集了统计信息的本机编译的存储过程中所有查询的查询文本以及执行统计信息：  
  
```tsql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 本机编译的存储过程支持 SHOWPLAN_XML（估计的执行计划）。 可以使用该估计的执行计划检查查询计划，以便找到任何错误计划问题。 错误计划的常见原因是：  
  
-   在创建过程前未更新统计信息。  
  
-   缺失索引  
  
 通过执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)]获取 Showplan XML：  
  
```tsql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 或者，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，选择过程名称并且单击 **“显示估计的执行计划”**。  
  
 本机编译的存储过程的估计的执行计划显示过程中查询的查询运算符和表达式。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 对于本机编译的存储过程，并不支持所有 SHOWPLAN_XML 属性。 例如，与查询优化器开销相关的属性不是针对过程的 SHOWPLAN_XML 的一部分。  
  
## 另请参阅  
 [本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  