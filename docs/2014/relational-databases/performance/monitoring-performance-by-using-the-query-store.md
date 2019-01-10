---
title: 使用查询存储监视性能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bfdce1925bc4c73894e1ff1a9bb0d69f6da94501
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756609"
---
# <a name="monitoring-performance-by-using-the-query-store"></a>Monitoring Performance By Using the Query Store
  查询存储功能让 DBA 可以探查查询计划选项和性能。 它让你可以快速找到查询计划中的更改所造成的性能差异，从而简化了性能疑难解答。 这一性能会自动捕获查询、计划和运行时统计信息的历史记录，并将其保留以供你查看。 它按时间窗口将数据分割开来，使你可以查看数据库使用情况模式并了解服务器上何时发生了查询计划更改。 可使用 [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) 选项来配置查询存储。  
  
||  
|-|  
|**适用对象**：[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([获取它](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。|  
  
> [!IMPORTANT]  
>  目前这是预览功能。 为了使用查询存储，你必须承认并同意查询存储的实现遵从你的许可协议的预览条款（如企业协议、Microsoft Azure 协议或 Microsoft 在线订阅协议），以及任何适用于 [Microsoft Azure 预览版的补充使用条款](http://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)。  
  
##  <a name="Enabling"></a> 启用查询存储  
 默认情况下，新数据库的查询存储处于非活动状态。  
  
#### <a name="by-using-the-query-store-page-in-management-studio"></a>通过使用 Management Studio 中的查询存储页  
  
1.  在对象资源管理器中，右键单击数据库，然后单击“属性” 。 （要求 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]2016 版。）  
  
2.  在“数据库属性”  对话框中，选择“查询存储”  页。  
  
3.  在“启用”  框中，选择“True” 。  
  
#### <a name="by-using-transact-sql-statements"></a>通过使用 Transact-SQL 语句  
  
1.  使用 `ALTER DATABASE` 语句来启用查询存储。 例如：  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     有关与查询存储相关的语法选项的详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
> [!NOTE]  
>  无法启用 master 数据库的查询存储。  
  

  
##  <a name="About"></a>查询存储中的信息  
 由于统计信息更改、架构更改、索引的创建/删除等多种不同原因，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中任何特定查询的执行计划通常会随着时间而改进。过程缓存（其中存储了缓存的查询计划）仅存储最近的执行计划。 还会由于内存压力从计划缓存中逐出计划。 因此，执行计划更改造成的查询性能回归可能非常重大，且长时间才能解决。  
  
 由于查询存储会保留每个查询的多个执行计划，因此它可以强制执行策略，以引导查询处理器对某个查询使用特定执行计划。 这称为“计划强制”。 查询存储中的计划强制是通过使用类似于 [USE PLAN](/sql/t-sql/queries/hints-transact-sql-query) 查询提示的机制来提供的，但它不需要在用户应用程序中进行任何更改。 计划强制可在非常短的时间内解决由计划更改造成的查询性能回归。  
  
 使用查询存储功能的常见方案为：  
  
-   快速查找并修复通过强制使用先前查询计划而造成的计划性能回归。 修复近期由于执行计划更改而出现性能回归的查询。  
  
-   确定在给定时间窗口中查询执行的次数，从而帮助 DBA 对性能资源问题进行故障排除。  
  
-   标识过去 *x* 小时内的前 *n* 个查询（按执行时间、内存占用等）。  
  
-   审核给定查询的查询计划历史记录。  
  
-   分析特定数据库的资源（CPU、I/O 和内存）使用模式。  
  
 查询存储包含两个存储；用于永久保存执行计划信息的 **计划存储** ，以及用于永久保存执行统计信息的 **运行时统计信息存储** 。 `max_plans_per_query` 配置选项限制了计划存储中查询可存储的唯一计划数。 为增强性能，通过异步方式向这两个存储写入信息。 为尽量减少空间使用量，将在按固定时间窗口上聚合运行时统计信息存储中的运行时执行统计信息。 可通过查询查询存储目录视图来查看这些存储中的信息。  
  
 以下查询返回查询存储中查询和计划的相关信息。  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  

  
## <a name="using-the-regressed-queries-feature"></a>使用回归查询功能  
 在启用查询存储后，刷新对象资源管理器的数据库部分，以添加“查询存储”  部分。  
  
 ![查询存储](../../database-engine/media/querystore.PNG "查询存储")  
  
 在选择“回归查询” 后，打开 **中的“回归查询”**[!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]窗格。 “回归查询”窗格将显示查询存储中的查询和计划。 借助顶部的下拉列表框，可基于各种条件选择查询。 选择某个计划以查看图形查询计划。 可使用按钮来查看源查询，强制执行和取消强制执行某一查询计划，以及刷新显示内容。  
  
 ![RegressedQueries](../../database-engine/media/regressedqueries.PNG "RegressedQueries")  
  
 若要强制执行某一计划，请选择查询和计划，然后单击“强制计划”  你只可以强制执行由查询计划功能保存且仍保留在查询计划缓存中的计划。  
  

  
##  <a name="Options"></a> 配置选项  
 OPERATION_MODE  
 可以为 READ_WRITE 或 READ_ONLY。  
  
 CLEANUP_POLICY  
 配置 STALE_QUERY_THRESHOLD_DAYS 参数，以指定数据在查询存储保留的天数。  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 确定写入到查询存储的数据保留到磁盘的频率。 为了优化性能，由查询存储收集的数据应以异步方式写入到磁盘。 通过 DATA_FLUSH_INTERVAL_SECONDS 配置此异步传输发生的频率。  
  
 MAX_SIZE_MB  
 配置查询存储的最大大小。 如果查询存储中的数据命中 MAX_SIZE_MB 限制，则查询存储会自动从读写状态更改为只读状态，并停止收集新数据。  
  
 INTERVAL_LENGTH_MINUTES  
 确定运行时执行统计数据聚合到查询存储中的时间间隔。 为了优化空间使用情况，将在固定时间窗口上聚合运行时统计信息存储中的运行时执行统计信息。 此固定时间窗口通过 INTERVAL_LENGTH_MINUTES 进行配置。  
  
 查询 `sys.database_query_store_options` 视图以确定查询存储的当前选项。  
  
 若要深入了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句来设置选项，请参阅 [选项管理](#OptionMgmt)。  
  
 
  
##  <a name="Related"></a> 相关视图、功能和过程  
 可通过 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 或使用以下视图和过程来查看和管理查询存储。  
  
-   [sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql)  
  
### <a name="query-store-catalog-views"></a>查询存储目录视图  
 7 个查询视图提供了查询存储的相关信息。  
  
-   [sys.database_query_store_options (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql)  
  
-   [sys.query_context_settings (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-context-settings-transact-sql)  
  
-   [sys.query_store_plan (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-store-plan-transact-sql)  
  
-   [sys.query_store_query (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-store-query-transact-sql)  
  
-   [sys.query_store_query_text (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql)  
  
-   [sys.query_store_runtime_stats (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql)  
  
-   [sys.query_store_runtime_stats_interval (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql)  
  
### <a name="query-store-stored-procedures"></a>查询存储存储过程  
 6 个存储过程配置了查询存储。  
  
-   [sp_query_store_flush_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql)  
  
-   [sp_query_store_reset_exec_stats (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql)  
  
-   [sp_query_store_force_plan (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql)  
  
-   [sp_query_store_unforce_plan (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql)  
  
-   [sp_query_store_remove_plan (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql)  
  
-   [sp_query_store_remove_query (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql)  
  

  
##  <a name="Scenarios"></a>键使用方案  
  
###  <a name="OptionMgmt"></a> 选项管理  
 本部分提供一些有关如何管理查询存储功能本身的准则。  
  
 **查询存储当前是否处于活动状态？**  
  
 查询存储将其数据存储在用户数据库内，正因为此，它具有大小限制（使用 `MAX_STORAGE_SIZE_MB` 进行配置）。 如果查询存储中的数据命中该限制，则查询存储将自动从读写状态更改为只读状态，并停止收集新数据。  
  
 执行以下脚本以确定查询存储当前是否处于活动状态，以及它目前是否在收集运行时统计信息。  
  
```  
DECLARE @x nvarchar(100) = CAST(newid() AS nvarchar(100));  
DECLARE @query nvarchar(max) =   
N'IF EXISTS  
(  
    SELECT *   
    FROM sys.query_store_query_text   
    WHERE query_sql_text LIKE ''%' + @x + N'%''  
)  
SELECT ''Query Store is active'' ;  
ELSE SELECT ''Query Store is NOT active''' ;  
EXEC sp_executesql @query;  
```  
  
 **获取查询存储选项**  
  
 若要了解查询存储状态的相关详细信息，请在用户数据库中执行以下操作。  
  
```  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **设置查询存储间隔**  
  
 你可以覆盖用于聚合查询运行时统计信息的时间间隔（默认值为 60 分钟）。  
  
```  
  
      USE master;  
GO  
  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 请注意，不允许使用任意值-应使用以下项之一：1、 5、 10、 15、 30 和 60。  
  
 通过 `sys.database_query_store_options` 视图公开时间间隔的新值。  
  
 如果查询存储已满，请使用以下语句来扩展存储。  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **设置所有查询存储选项**  
  
 你可以使用单个 ALTER DATABASE 语句同时设置多个查询存储选项。  
  
```  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY =   
    (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15  
);  
```  
  
 **清理空间**  
  
 查询存储时间间隔表是在数据库创建期间在 PRIMARY 文件组中创建的，且之后不可更改此配置。 如果空间不足，你可以要使用以下语句来清理旧的查询存储数据。  
  
```  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 或者，你可以只清理临时查询数据，因为此数据与查询优化和计划分析的相关性更低，但却占用了大量空间。  
  
 **删除临时查询** 这会删除只执行了一次且已超过 24 小时的查询。  
  
```  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 你可以使用其他逻辑来定义自己的过程，以清理对你而言不再重要的数据。  
  
 以上示例使用 `sp_query_store_remove_query` 扩展存储过程来删除不必要的数据。 你还可以使用其他两个过程。  
  
-   `sp_query_store_reset_exec_stats` -清除给定计划的运行时统计信息。  
  
-   `sp_query_store_remove_plan` -删除单个计划。  
  

  
###  <a name="Peformance"></a> 性能审核和疑难解答  
 因为查询存储保存了整个查询执行过程中的编译历史记录和运行时度量，因此你可以轻松回答很多与你的工作负荷相关的不同问题。  
  
 **最后一个*n*在数据库上执行的查询。**  
  
```  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **每个查询的次数。**  
  
```  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **与过去一小时内最长平均执行时间的查询数。**  
  
```  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **在过去 24 小时，在相应的平均行计数和执行计数中读取的具有最大平均物理 IO 的查询数。**  
  
```  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **具有多个计划的查询。** 这些查询特别有趣，因为计划选择更改可能造成它们的性能回归。 以下查询将这些查询和所有计划一同进行了标识：  
  
```  
WITH Query_MultPlans  
AS  
(  
    SELECT COUNT(*) AS cnt, q.query_id   
    FROM sys.query_store_query_text AS qt  
    JOIN sys.query_store_query AS q  
        ON qt.query_text_id = q.query_text_id  
    JOIN sys.query_store_plan AS p  
        ON p.query_id = q.query_id  
    GROUP BY q.query_id  
    HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject, query_sql_text,  
plan_id, p.query_plan AS plan_xml,  
p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **最近性能回归的查询 （对比不同点的时间）。** 以下查询示例返回了其执行时间因计划选择更改而在过去 48 小时内翻倍的所有查询。 并排查询所有的运行时统计信息时间间隔。  
  
```  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 如果你向查看所有性能回归（而不仅是计划选择更改造成的回归），只需从先前查询中删除条件 `AND p1.plan_id <> p2.plan_id` 。  
  
 **最近性能回归的查询 （对比近期执行和历史执行）。** 下一查询会根据执行时间段来比较查询执行。 在此特定示例中，查询对比了最近时期（1 小时）和历史时期（过去一天）中的执行，并标识了那些引入 additional_duration_workload 的查询。 此度量的计算方式是最近平均执行和历史平均执行之差，再乘以最近执行数量。 它实际上表示相对于历史记录，引入了多少额外的持续时间最近执行：  
  
```  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time <= @history_start_time AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time <= @history_end_time AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time <= @recent_start_time AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time <= @recent_end_time AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/recent.count_executions-hist.total_duration/hist.count_executions)*(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
  

  
###  <a name="Stability"></a> 维护查询性能稳定性  
 对于执行多次的查询，你可能注意到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用了会导致不同资源利用率和持续时间的不同计划。 借助查询存储，你可以轻松检测到查询性能何时回归，并确定在感兴趣的时间段内的最优计划。 然后你可以对未来查询执行强制执行此最优计划。  
  
 你还可以使用参数（自动参数化或手动参数化）来标识某一查询内不一致的查询性能。 你可以在不同计划中标识出对所有或大多数参数值而言足够快和最佳的计划，并强制执行此计划；为更大范围的用户方案保留可预测的性能。  
  
 **强制执行或计划查询（应用强制策略）。** 当向某一查询强制执行某个计划时，每次查询开始执行时其强制执行的计划都会随同一起执行。  
  
```  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 在使用 `sp_query_store_force_plan` 时，你只可以强制执行查询存储记录为该查询计划的那些计划。 换句话说，可用于查询的计划只有那些在查询存储处于活动状态时已使用执行 Q1 的哪些计划。  
  
 **删除强制执行查询的计划。** 若要再次依靠 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 查询优化器来计算最佳查询计划，请使用 `sp_query_store_unforce_plan` 来取消强制执行为查询选定的计划。  
  
```  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
  

  
## <a name="see-also"></a>请参阅  
 [监视和优化性能](../performance/monitor-and-tune-for-performance.md)   
 [性能监视和优化工具](../performance/performance-monitoring-and-tuning-tools.md)   
 [打开活动监视器 (SQL Server Management Studio)](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [活动监视器](../performance-monitor/activity-monitor.md)  
  
  
