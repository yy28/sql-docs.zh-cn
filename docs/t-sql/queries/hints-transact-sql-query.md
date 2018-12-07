---
title: 查询提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
- QUERY_PLAN_PROFILE query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42247b11f00524ba08dd74f41f11da35fdcb2026
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530359"
---
# <a name="hints-transact-sql---query"></a>提示 (Transact-SQL) - 查询
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  查询提示指定应在整个查询中使用指示的提示。 它们影响语句中的所有运算符。 如果主查询中涉及 UNION，则只有最后一个涉及 UNION 运算符的查询可以包含 OPTION 子句。 查询提示作为 [OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)的一部分指定。 如果一个或多个查询提示导致查询优化器不能生成有效计划，则引发 8622 错误。  
  
> [!CAUTION]  
> 由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器通常会为查询选择最佳执行计划，因此我们建议资深开发人员和数据库管理员只有在不得已时才可使用提示。  
  
 **适用范围：**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }   
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>参数  
 { HASH | ORDER } GROUP  
 指定在查询的 GROUP BY 或 DISTINCT 子句中所说明的聚合应使用哈希或排列。  
  
 { MERGE | HASH | CONCAT } UNION  
 指定所有 UNION 运算由合并、哈希或串联 UNION 集执行。 如果指定了多个 UNION 提示，查询优化器就会从这些指定的提示中选择开销最少的策略。  
  
 { LOOP | MERGE | HASH } JOIN  
 指定整个查询中的所有联接操作由 LOOP JOIN、MERGE JOIN 或 HASH JOIN 执行。 如果指定了多个联接提示，则优化器从允许的联接策略中选择开销最少的联接策略。  
  
 如果在同一查询中的 FROM 子句中还为一对特定的表指定了联接提示，则尽管仍须遵守查询提示，但该联接提示将优先联接这两个表。 因此，这对表的联接提示可能只限制选择查询提示中允许的联接方法。 有关详细信息，请参阅[联接提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-join.md)。  
  
 EXPAND VIEWS  
 指定展开索引视图，而且查询优化器不将任何索引视图看作是查询中任何部分的替代。 当视图名称由查询文本中的视图定义替换时，视图将展开。  
  
 实际上，该查询提示不允许在查询计划中直接使用索引视图和直接在索引视图上使用索引。  
  
 只有在查询的 SELECT 部分中直接引用视图，而且指定了 WITH (NOEXPAND) 或 WITH (NOEXPAND, INDEX( index_value [ ,...n ] ) ) 时，才不展开索引视图。 有关查询提示 WITH (NOEXPAND) 的详细信息，请参阅 [FROM](../../t-sql/queries/from-transact-sql.md)。  
  
 只有语句的 SELECT 部分中的视图（包括 INSERT、UPDATE、MERGE 和 DELETE 语句中的视图）才受提示影响。  
  
 FAST number_rows  
 指定对查询进行优化，以便快速检索第一个 number_rows。 该值是非负整数。 在返回第一个 number_rows 后，查询继续执行并生成完整的结果集。  
  
 FORCE ORDER  
 指定在查询优化过程中保持由查询语法指示的联接顺序。 使用 FORCE ORDER 不会影响查询优化器可能的角色逆转行为。  
  
> [!NOTE]  
> 在 MERGE 语句中，如果未指定 WHEN SOURCE NOT MATCHED 子句，则按照默认的联接次序，先访问源表再访问目标表。 如果指定 FORCE ORDER，则保留此默认行为。  
  
 { FORCE | DISABLE } EXTERNALPUSHDOWN  
 强制或禁用向下推送 Hadoop 中符合条件的表达式的计算。 仅适用于使用 PolyBase 的查询。 不会向下推送到 Azure 存储。  
  
 KEEP PLAN  
 强制查询优化器对查询放宽估计的重新编译阈值。 当通过运行 UPDATE、DELETE、MERGE 或 INSERT 语句对表进行的索引列更改数目达到估计数目时，会自动重新编译查询，该估计数目即为估计的重新编译阈值。 指定 KEEP PLAN 可确保当表有多个更新时不会频繁地对查询进行重新编译。  
  
 KEEPFIXED PLAN  
 强制查询优化器不因统计信息的更改而重新编译查询。 指定 KEEPFIXED PLAN 可确保仅当更改基础表的架构或在那些表上执行 sp_recompile 时才重新编译查询。  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止查询使用非聚集内存优化列存储索引。 如果查询包含避免使用列存储索引的查询提示，而又包含支持使用列存储索引的索引提示，那么这两个提示相互冲突，导致查询返回错误。  
  
 MAX_GRANT_PERCENT = percent  
 内存授予大小所占的最大百分比。 查询保证不会超过此限制。 如果 Resource Governor 设置低于此提示指定的值，则实际限制可能更低。 有效值介于 0.0 和 100.0 之间。  
  
**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MIN_GRANT_PERCENT = percent  
 内存授予大小所占的最小百分比 = 默认百分比限制。 查询保证会获取最大值（必需内存，最小授予），因为至少需要必需内存才能启动查询。 有效值介于 0.0 和 100.0 之间。  
  
**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MAXDOP number  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 对于指定了 max degree of parallelism 配置选项的查询，会覆盖 sp_configure 和 Resource Governor 的该选项。 MAXDOP 查询提示可以超出使用 sp_configure 配置的值。 如果 MAXDOP 超出使用 Resource Governor 配置的值，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]会使用 Resource Governor MAXDOP 值（如 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md) 中所述）。 使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
> [!WARNING]     
> 如果 MAXDOP 设置为零，服务器将选择最大并行度。  
  
 MAXRECURSION number     
 指定该查询允许的最大递归数。 number 是介于 0 至 32,767 之间的非负整数。 如果指定 0，则没有限制。 如果未指定此选项，则对服务器的默认限制为 100。  
  
 当在查询执行期间达到指定或默认的 MAXRECURSION 数量限制时，将结束查询并返回错误。  
  
 由于此错误，该语句的所有结果都被回滚。 如果该语句为 SELECT 语句，则可能会返回部分结果或不返回结果。 所返回的任何部分结果都可能无法包括超过指定最大递归级别的递归级别上的所有行。  
  
 有关详细信息，请参阅 [WITH common_table_expression (Transact-SQL)](../../t-sql/queries/with-common-table-expression-transact-sql.md)。     
  
 NO_PERFORMANCE_SPOOL    
 **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止将 spool 运算符添加到查询计划（需要 spool 保证更新语义有效的计划除外）。 在某些情况下，spool 运算符可能会降低性能。 例如，如果有大量查询与 spool 操作并发运行，spool 将使用 tempdb 并会出现 tempdb 争用。  
  
 OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )     
 在编译和优化查询时指示查询优化器对局部变量使用特定值。 仅在查询优化期间使用该值，在查询执行期间不使用该值。  
  
 *@variable_name*  
 在查询中使用的局部变量的名称，可以为其分配用于 OPTIMIZE FOR 查询提示的值。  
  
 UNKNOWN  
 指定查询优化器在查询优化期间使用统计数据而不是初始值来确定局部变量的值。  
  
 literal_constant  
 要分配给 @variable_name 并用于 OPTIMIZE FOR 查询提示的文字常量值。 literal_constant 只在查询优化期间使用，在查询执行期间不用作 @variable_name 的值。 literal_constant 可以是任意可用文字常量表示的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型。 literal_constant 的数据类型必须可隐式转换为查询中 @variable_name 所引用的数据类型。  
  
 OPTIMIZE FOR 可以抵消优化器的默认参数检测行为，也可在创建计划指南时使用。 有关详细信息，请参阅[重新编译存储过程](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。  
  
 OPTIMIZE FOR UNKNOWN  
 指示查询优化器在编译和优化查询时使用所有局部变量的统计数据而不是初始值，包括使用强制参数化创建的参数。  
  
 如果在同一查询提示中使用 OPTIMIZE FOR @variable_name = literal_constant 和 OPTIMIZE FOR UNKNOWN，则查询优化器对特定值使用指定的 literal_constant，而对其余变量值使用 UNKNOWN。 这些值仅用于查询优化期间，而不会用于查询执行期间。  
  
 PARAMETERIZATION { SIMPLE | FORCED }     
 指定在编译查询时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器应用于此查询的参数化规则。  
  
> [!IMPORTANT]  
> 只能在计划指南中指定 PARAMETERIZATION 查询提示，用于覆盖 PARAMETERIZATION 数据库 SET 选项的当前设置。 不能直接在查询中指定该查询提示。    
> 有关详细信息，请参阅[使用计划指南指定查询参数化行为](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。
  
 SIMPLE 用于指示查询优化器尝试进行简单参数化。 FORCED 用于指示查询优化器尝试进行强制参数化。 有关详细信息，请参阅[查询处理体系结构指南中的强制参数化](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)和[查询处理体系结构指南中的简单参数化](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)。  

 RECOMPILE  
 指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 为查询生成新的临时计划，并在查询完成执行后立即放弃该计划。 在未指定 RECOMPILE 的情况下执行同一查询时，生成的查询计划不会替换存储在缓存中的计划。 如果未指定 RECOMPILE，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将缓存查询计划并重新使用它们。 在编译查询计划时，RECOMPILE 查询提示将使用查询中任意本地变量的当前值，如果查询位于存储过程中，这些当前值将传递给任意参数。  
  
 在只须重新编译存储过程中的一部分查询，而不是重新编译整个存储过程时，RECOMPILE 是创建使用 WITH RECOMPILE 子句的存储过程的很有用的替代方法。 有关详细信息，请参阅[重新编译存储过程](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。 在创建计划指南时，RECOMPILE 也很有用。  
  
 ROBUST PLAN  
 强制查询优化器尝试一个计划，该计划可能以性能为代价获得最大可能的行大小。 处理查询时，中间表和运算符可能需要存储和处理比输入行宽的行。 在有些情况下，行可能很宽，以致某个运算符无法处理行。 如果发生这种情况，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在查询执行过程中生成错误。 通过使用 ROBUST PLAN，可以指示查询优化器不考虑可能会遇到该问题的所有查询计划。  
  
 如果不能使用这样的计划，查询优化器将返回错误而不是延迟对查询执行的错误检测。 行可以包含可变长度列；[!INCLUDE[ssDE](../../includes/ssde-md.md)]允许将行大小定义为超过[!INCLUDE[ssDE](../../includes/ssde-md.md)]处理能力的最大可能的大小。 通常，应用程序存储实际大小在[!INCLUDE[ssDE](../../includes/ssde-md.md)]处理能力范围内的行，而不管最大可能大小。 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]遇到过长的行，则返回执行错误。  
 
<a name="use_hint"></a> USE HINT ( 'hint\_name' )    
 适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 开始）和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。
 
 按照单引号内的提示名称的指定，向查询处理器提供一个或多个其他提示。   

 支持以下提示名称：    
 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS' <a name="use_hint_join_containment"></a>       
   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或更新版本的查询优化器[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型下，导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用联接的简单包含假设而非默认的基本包含假设来生成查询计划。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476 等效。 
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES' <a name="use_hint_correlation"></a>      
   会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在为了进行关联而对筛选的 AND 谓词进行估值时使用最小选择性来生成计划。 与 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更早版本的基数估计模式一起使用时，这等效于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137；与 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或更高版本的基数估计模式一起使用时，这等效于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471。
*  'DISABLE_BATCH_MODE_ADAPTIVE_JOINS'       
   禁用批处理模式自适应联接。 有关详细信息，请参阅[批处理模式自适应联接](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-adaptive-joins)。
*  'DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK'       
   禁用批处理模式内存授予反馈。 有关详细信息，请参阅[批处理模式内存授予反馈](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-memory-grant-feedback)。
*  'DISABLE_INTERLEAVED_EXECUTION_TVF'      
   禁用多语句表值函数的交错执行。 有关详细信息，请参阅[多语句表值函数的交错执行](../../relational-databases/performance/adaptive-query-processing.md#interleaved-execution-for-multi-statement-table-valued-functions)。
*  'DISABLE_OPTIMIZED_NESTED_LOOP'      
   指示查询处理器在生成查询计划时不对优化的嵌套循环联接使用排序操作（批处理排序）。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340 等效。
*  'DISABLE_OPTIMIZER_ROWGOAL' <a name="use_hint_rowgoal"></a>      
   导致 SQL Server 生成一个计划，该计划不对包含 TOP、OPTION (FAST N)、IN 或 EXISTS 关键字的查询使用行目标调整。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138 等效。
*  'DISABLE_PARAMETER_SNIFFING'      
   指示查询优化器使用平均数据分布，同时编译具有一个或多个参数的查询，使查询计划独立于编译查询时最先使用的参数值。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 或[数据库作用域配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 PARAMETER_SNIFFING=OFF 等效。
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'      
   针对需要对其执行基数估计的任何前导索引列，启用自动生成的快速统计信息（直方图修正）。 用于评估基数的直方图将在查询编译时针对此列的实际最大值或最小值进行调整。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139 等效。 
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'     
   启用查询优化器修补程序（SQL Server 累积更新和 Service Pack 中发布的更改）。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 或[数据库作用域配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 QUERY_OPTIMIZER_HOTFIXES=ON 等效。
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'      
   强制查询优化器使用与当前数据库兼容级别相对应的[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型。 使用此提示替代[数据库作用域域配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 LEGACY_CARDINALITY_ESTIMATION=ON 或[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481。
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION' <a name="use_hint_ce70"></a>      
   强制查询优化器使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更早版本的[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型。 这与[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 或[数据库作用域配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 LEGACY_CARDINALITY_ESTIMATION=ON 等效。
*  'QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n'          
 在查询级别强制执行查询优化器行为，就像使用数据库兼容性级别 n 来编译该查询（其中 n 是受支持的数据库兼容性级别）。 请参阅 [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)，以了解目前对 n 支持的值。 **适用范围**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（自 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU10 起）。    

   > [!NOTE]
   > QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n 提示不会重写默认或旧版基数估计设置（如果它是通过数据库范围的配置、跟踪标志或 QUERYTRACEON 等其他查询提示强制执行的）。   
   > 此提示仅影响查询优化器的行为。 它不会影响可能依赖于[数据库兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他功能（例如，某些数据库功能的可用性）。  
   > 若要了解有关此提示的详细信息，请参阅[开发人员选择：提示查询执行模型](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-hinting-query-execution-model)。
    
*  'QUERY_PLAN_PROFILE'      
 启用用于查询的轻型分析。 当包含此新提示的查询完成时，会触发一个新扩展事件：query_plan_profile。 此扩展事件公开执行统计信息和实际执行计划 XML，类似于 query_post_execution_showplan 扩展事件，但仅针对包含新提示的查询。 适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11 开始）。 

  > [!NOTE]
  > 如果启用收集 query_post_execution_showplan 扩展事件，会向在服务器上运行的每个查询添加标准分析基础结构，因此可能会影响服务器的总体性能。      
  > 如果启用 query_thread_profile 扩展事件集合以改为使用轻量分析基础结构，这将在很大程度上减少性能开销，但仍会影响服务器的总体性能。       
  > 如果启用 query_plan_profile 扩展事件，将只启用通过 QUERY_PLAN_PROFILE 执行的查询的轻量分析基础结构，因此不会影响服务器上的其他工作负载。 使用此提示来分析特定查询，而不会影响服务器工作负载的其他部分。
  > 若要了解有关轻量分析的详细信息，请参阅[开发人员选择：随时随地查询进度](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)。
 
可以使用动态管理视图 [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) 查询所有受支持的 USE HINT 名称的列表。    

> [!TIP]
> 提示名称不区分大小写。   
  
> [!IMPORTANT] 
> 某些 USE HINT 提示可能与在全局或会话级别启用的跟踪标志或与数据库作用域配置设置存在冲突。 在这种情况下，查询级别提示 (USE HINT) 将始终优先。 如果 USE HINT 与另一个查询提示或在查询级别启用（例如由 QUERYTRACEON 启用）的跟踪标志存在冲突，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在尝试执行查询时生成错误。 

 USE PLAN N'xml\_plan'     
 强制查询优化器对查询使用由 'xml\_plan' 指定的现有查询计划。 不能使用 INSERT、UPDATE、MERGE 或 DELETE 语句来指定 USE PLAN。  
  
TABLE HINT (exposed\_object\_name [ **,** \<table_hint> [ [, ]...n ] ] ) 将指定表提示应用于与 exposed_object_name 对应的表或视图。 我们建议仅在[计划指南](../../relational-databases/performance/plan-guides.md)的上下文中将表提示用作查询提示。  
  
 exposed_object_name 可以为以下引用之一：  
  
-   当对查询的 [FROM](../../t-sql/queries/from-transact-sql.md) 子句中的表或视图使用别名时，exposed_object_name 就是别名。  
  
-   如果不使用别名，exposed_object_name 与 FROM 子句中引用的表或视图完全匹配。 例如，如果使用由两部分组成的名称引用表或视图，则 exposed_object_name 就是这个由两部分组成的名称。  
  
 如果指定了 exposed_object_name 但未指定表提示，则将忽略在查询中指定为对象表提示的一部分的任何索引，并由查询优化器来决定索引的使用。 当您无法修改原始查询时，可以使用此方法来消除 INDEX 表提示的影响。 请参阅示例 J。  
  
\<table_hint> ::= { [ NOEXPAND ] { INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value ) | FORCESEEK [(index\_value(index\_column\_name [,... ] )) ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } 是作为查询提示应用于与 exposed_object_name 想对应的表或视图的表提示。 有关这些提示的说明，请参阅[表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 不允许将非 INDEX、FORCESCAN 和 FORCESEEK 的表提示用作查询提示，除非该查询已经具有一个指定该表提示的 WITH 子句。 有关详细信息，请参阅“备注”。  
  
> [!CAUTION] 
> 指定带参数的 FORCESEEK 限制优化器可以考虑的计划数大于指定不带参数的 FORCESEEK 时的计划数。 这可能导致在更多情况下出现“无法生成计划”错误。 在未来的版本中，对优化器进行内部修改后可允许考虑更多计划。  
  
## <a name="remarks"></a>Remarks  
 只有在 INSERT 语句中使用了 SELECT 子句时，才能在该语句中指定查询提示。  
  
 只能在顶级查询中指定查询提示，不能在子查询指定。 将表提示指定为查询提示时，可以在顶级查询或子查询中指定此提示；但是，为 TABLE HINT 子句中的 exposed_object_name 指定的值必须与该查询或子查询中公开的名称完全匹配。  
  
## <a name="specifying-table-hints-as-query-hints"></a>将表提示指定为查询提示  
 我们建议仅在[计划指南](../../relational-databases/performance/plan-guides.md)的上下文中将 INDEX、FORCESCAN 或 FORCESEEK 表提示用作查询提示。 当您无法修改原始查询时（例如，由于它是第三方应用程序），计划指南将很有用。 计划指南中指定的查询提示在查询编译和优化前添加到查询中。 对于即席查询，仅在测试计划指南语句时才应使用 TABLE HINT 子句。 对于所有其他即席查询，建议仅将这些提示指定为表提示。  
  
 如果将 INDEX、FORCESCAN 和 FORCESEEK 表提示指定为查询提示，它们会对以下对象有效：  
  
-   表  
-   视图  
-   索引视图  
-   公用表表达式（必须在其结果集填充公用表表达式的 SELECT 语句中指定提示）  
-   动态管理视图  
-   命名子查询  
  
可以为没有任何现有表提示的查询指定 INDEX、FORCESCAN 和 FORCESEEK 表提示作为查询提示，这些提示也可用于分别替换查询中的现有 INDEX、FORCESCAN 或 FORCESEEK 提示。 不允许将非 INDEX、FORCESCAN 和 FORCESEEK 的表提示用作查询提示，除非该查询已经具有一个指定该表提示的 WITH 子句。 这种情况下，还必须使用 OPTION 子句中的 TABLE HINT 来将匹配的提示指定为查询提示，以保留查询的语义。 例如，如果查询包含表提示 NOLOCK，则计划指南的 @hints 参数中的 OPTION 子句必须也包含 NOLOCK 提示。 请参阅示例 K。当通过使用 OPTION 子句中的 TABLE HINT 指定了非 INDEX、FORCESCAN 或 FORCESEEK 的表提示，而未指定匹配的查询提示，或指定了后者而未指定前者时，将会引发错误 8702（表示 OPTION 子句可能会导致查询的语义发生变化），该查询将失败。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-merge-join"></a>A. 使用 MERGE JOIN  
 下面的示例指定查询中的 JOIN 操作由 MERGE JOIN 执行。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. 使用 OPTIMIZE FOR  
 下面的示例指示查询优化器对局部变量 `@city_name` 使用值 `'Seattle'`，并在优化查询时使用统计数据来确定局部变量 `@postal_code` 的值。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>C. 使用 MAXRECURSION  
 可以使用 MAXRECURSION 来防止不合理的递归公用表表达式进入无限循环。 下面的示例特意创建了一个无限循环，然后使用 MAXRECURSION 提示将递归级别限制为两级。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 在更正代码错误之后，就不再需要 MAXRECURSION。  
  
### <a name="d-using-merge-union"></a>D. 使用 MERGE UNION  
 以下示例使用 MERGE UNION 查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. 使用 HASH GROUP 和 FAST  
 以下示例使用 HASH GROUP 和 FAST 查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. 使用 MAXDOP  
 以下示例使用 MAXDOP 查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. 使用 INDEX  
 以下示例使用 INDEX 提示。 第一个示例指定了一个索引。 第二个示例为单个表引用指定多个索引。 在这两个示例中，由于对使用别名的表应用了 INDEX 提示，因此 TABLE HINT 子句还必须将相同的别名指定为公开的对象名称。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>H. 使用 FORCESEEK  
 下面的示例使用 FORCESEEK 表提示。 由于对使用由两部分组成的名称的表应用了 INDEX 提示，因此 TABLE HINT 子句还必须将相同的由两部分组成的名称指定为公开的对象名称。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>I. 使用多个表提示  
 下面的示例将 INDEX 提示应用到一个表，将 FORCESEEK 提示应用到另一个表。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>J. 使用 TABLE HINT 覆盖现有的表提示  
 下面的示例演示如何在不指定提示的情况下使用 TABLE HINT 提示覆盖在查询的 FROM 子句中指定的 INDEX 表提示的行为。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>K. 指定语义影响的表提示  
 下面的示例在查询中包含两个表提示：NOLOCK 和 INDEX，其中前者为影响语义的提示，后者为不影响语义的提示。 若要保留查询的语义，应在计划指南的 OPTIONS 子句中指定 NOLOCK 提示。 除 NOLOCK 提示外，还指定了 INDEX 和 FORCESEEK 提示，它们在编译和优化语句时将替换查询中不影响语义的 INDEX 提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
 下面的示例演示另一种保留查询语义并使优化器能够选择并非在表提示中指定的索引的方法。 此方法是这样实现的：在 OPTIONS 子句中指定 NOLOCK 提示（因为它影响语义），并指定只有表引用而没有 INDEX 提示的 TABLE HINT 关键字。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>L. 使用 USE HINT  
 以下示例使用 RECOMPILE 和 USE HINT 查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
适用范围：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```sql  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>另请参阅  
 [提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)       
 [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)      
  
