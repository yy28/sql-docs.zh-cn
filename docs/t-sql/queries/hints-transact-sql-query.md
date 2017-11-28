---
title: "查询提示 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
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
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
caps.latest.revision: "136"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 88d4de294e7fa31b7334b9b03cc127d479d6628a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="hints-transact-sql---query"></a>提示 (TRANSACT-SQL) 的查询
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  查询提示指定应在整个查询中使用指示的提示。 它们影响语句中的所有运算符。 如果主查询中涉及 UNION，则只有最后一个涉及 UNION 运算符的查询可以包含 OPTION 子句。 查询提示指定为的一部分[OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)。 如果一个或多个查询提示导致查询优化器不能生成有效计划，则引发 8622 错误。  
  
> [!CAUTION]  
>  由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器通常会为查询选择最佳执行计划，因此我们建议资深开发人员和数据库管理员只有在不得已时才可使用提示。  
  
 **适用范围：**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [Insert](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 如果在同一查询中的 FROM 子句中还为一对特定的表指定了联接提示，则尽管仍须遵守查询提示，但该联接提示将优先联接这两个表。 因此，这对表的联接提示可能只限制选择查询提示中允许的联接方法。 有关详细信息，请参阅[联接提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 指定展开索引视图，而且查询优化器不将任何索引视图看作是查询中任何部分的替代。 当视图名称由查询文本中的视图定义替换时，视图将展开。  
  
 实际上，该查询提示不允许在查询计划中直接使用索引视图和直接在索引视图上使用索引。  
  
 仅当在查询和与 (NOEXPAND) 或 WITH 的 SELECT 部分中直接引用该视图未展开该索引的视图 (NOEXPAND、 索引 ( *index_value* [ **，***...n*])) 指定。 有关查询提示与 (NOEXPAND) 的详细信息，请参阅[FROM](../../t-sql/queries/from-transact-sql.md)。  
  
 只有语句的 SELECT 部分中的视图（包括 INSERT、UPDATE、MERGE 和 DELETE 语句中的视图）才受提示影响。  
  
 快速*number_rows*  
 指定查询进行了优化的快速检索的第一个*number_rows。* 这是一个非负整数。 第一个之后*number_rows*返回，查询将继续执行，并生成其完整结果集。  
  
 FORCE ORDER  
 指定在查询优化过程中保持由查询语法指示的联接顺序。 使用 FORCE ORDER 不会影响查询优化器可能的角色逆转行为。  
  
> [!NOTE]  
>  在 MERGE 语句中，如果未指定 WHEN SOURCE NOT MATCHED 子句，则按照默认的联接次序，先访问源表再访问目标表。 如果指定 FORCE ORDER，则保留此默认行为。  
  
 {FORCE |禁用} EXTERNALPUSHDOWN  
 强制或禁用的符合条件的 Hadoop 中的表达式计算下推。 仅适用于使用 PolyBase 的查询。 将不向下传递到 Azure 存储空间。  
  
 KEEP PLAN  
 强制查询优化器对查询放宽估计的重新编译阈值。 当通过运行 UPDATE、DELETE、MERGE 或 INSERT 语句对表进行的索引列更改数目达到估计数目时，会自动重新编译查询，该估计数目即为估计的重新编译阈值。 指定 KEEP PLAN 可确保当表有多个更新时不会频繁地对查询进行重新编译。  
  
 KEEPFIXED PLAN  
 强制查询优化器不因统计信息的更改而重新编译查询。 指定 KEEPFIXED 计划可确保查询将重新编译，仅当基础表的架构已更改，或如果**sp_recompile**针对这些表执行。  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 使用非聚集内存优化的列存储索引会阻止查询。 如果查询包含避免使用 columnstore 索引的查询提示以及有关使用 columnstore 索引的索引提示，则这些提示将发生冲突，查询将返回错误。  
  
 MAX_GRANT_PERCENT =*百分比*  
 最大内存授予百分比的大小。 查询保证将不超过此限制。 实际限制可以是低于此设置的资源调控器是否较低。 有效的值可以介于 0.0 和 100.0。  
  
**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MIN_GRANT_PERCENT =*百分比*  
 最小内存授予百分比大小 = %的默认限制。 查询保证将获取最大值 （min 授予所需的内存），因为至少需要启动查询所需的内存。 有效的值可以介于 0.0 和 100.0。  
  
**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 MAXDOP*数*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 重写**最大并行度**配置选项的**sp_configure**和指定此选项以对查询的资源调控器。 MAXDOP 查询提示可以超出使用 sp_configure 配置的值。 如果 MAXDOP 超过配置到资源调控器中，值[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用中所述的资源调控器 MAXDOP 值[ALTER WORKLOAD GROUP &#40;Transact SQL &#41;](../../t-sql/statements/alter-workload-group-transact-sql.md). 与使用的所有语义规则**最大并行度**使用 MAXDOP 查询提示时，配置选项都适用。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
  
> [!WARNING]  
>  如果 MAXDOP 设置为零，服务器将选择最大并行度。  
  
 MAXRECURSION*数*  
 指定该查询允许的最大递归数。 *数*是 0 和 32767 之间的非负整数。 如果指定 0，则没有限制。 如果未指定此选项，则对服务器的默认限制为 100。  
  
 当在查询执行期间达到指定或默认的 MAXRECURSION 数量限制时，将结束查询并返回错误。  
  
 由于此错误，该语句的所有结果都被回滚。 如果该语句为 SELECT 语句，则可能会返回部分结果或不返回结果。 所返回的任何部分结果都可能无法包括超过指定最大递归级别的递归级别上的所有行。  
  
 有关详细信息，请参阅[使用 common_table_expression &#40;Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 NO_PERFORMANCE_SPOOL  
 **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 防止将后台打印运算符添加到 （除外假脱机需要保证有效的更新语义时的计划） 的查询计划。 在某些情况下，假脱机运算符可能会降低性能。 例如，假脱机使用 tempdb，并且如果存在在配合假脱机操作运行许多并发查询，则可能出现 tempdb 争用。  
  
 OPTIMIZE FOR (  *@variable_name*  {未知 | = *literal_constant}* [ **，** ...*n* ] )  
 在编译和优化查询时指示查询优化器对局部变量使用特定值。 仅在查询优化期间使用该值，在查询执行期间不使用该值。  
  
 *@variable_name*  
 在查询中使用的局部变量的名称，可以为其分配用于 OPTIMIZE FOR 查询提示的值。  
  
 *未知*  
 指定查询优化器在查询优化期间使用统计数据而不是初始值来确定局部变量的值。  
  
 *literal_constant*  
 是一个文字的常量值，以被指定 *@variable_name* 用于 OPTIMIZE FOR 查询提示。 *literal_constant*仅在查询优化期间，而不是值的使用 *@variable_name* 在查询执行过程。 *literal_constant*可以是任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以表示为文本常量的系统数据类型。 数据类型*literal_constant*必须是隐式转换为数据类型，  *@variable_name* 中查询的引用。  
  
 OPTIMIZE FOR 可以抵消优化器的默认参数检测行为，也可在创建计划指南时使用。 有关详细信息，请参阅[重新编译存储过程](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。  
  
 OPTIMIZE FOR UNKNOWN  
 指示查询优化器在编译和优化查询时使用所有局部变量的统计数据而不是初始值，包括使用强制参数化创建的参数。  
  
 如果 OPTIMIZE FOR @variable_name = *literal_constant*并且 OPTIMIZE FOR UNKNOWN 使用相同的查询提示中，查询优化器将使用*literal_constant*为特定值指定的和未知的剩余的变量值。 这些值仅用于查询优化期间，而不会用于查询执行期间。  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 指定在编译查询时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器应用于此查询的参数化规则。  
  
> [!IMPORTANT]  
>  PARAMETERIZATION 查询提示只能在计划指南中指定。 不能直接在查询中指定该查询提示。  
  
 SIMPLE 用于指示查询优化器尝试进行简单参数化。 FORCED 用于指示优化器尝试进行强制参数化。 PARAMETERIZATION 查询提示用于覆盖计划指南中 PARAMETERIZATION 数据库 SET 选项的当前设置。 有关详细信息，请参阅[通过使用计划指南指定查询参数化行为](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)。  
  
 RECOMPILE  
 指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]在执行为查询生成的计划后将其丢弃，从而在下次执行同一查询时强制查询优化器重新编译查询计划。 而无需指定重新编译，[!INCLUDE[ssDE](../../includes/ssde-md.md)]查询计划存入缓存并重用它们。 在编译查询计划时，RECOMPILE 查询提示将使用查询中任意本地变量的当前值，如果查询位于存储过程中，这些当前值将传递给任意参数。  
  
 在只须重新编译存储过程中的一部分查询，而不是重新编译整个存储过程时，RECOMPILE 是创建使用 WITH RECOMPILE 子句的存储过程的很有用的替代方法。 有关详细信息，请参阅[重新编译存储过程](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)。 在创建计划指南时，RECOMPILE 也很有用。  
  
 ROBUST PLAN  
 强制查询优化器尝试一个计划，该计划可能以性能为代价获得最大可能的行大小。 处理查询时，中间表和运算符可能需要存储和处理比输入行宽的行。 在有些情况下，行可能很宽，以致某个运算符无法处理行。 如果发生这种情况，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在查询执行过程中生成错误。 通过使用 ROBUST PLAN，可以指示查询优化器不考虑可能会遇到该问题的所有查询计划。  
  
 如果不能使用这样的计划，查询优化器将返回错误而不是延迟对查询执行的错误检测。 行可以包含可变长度列；[!INCLUDE[ssDE](../../includes/ssde-md.md)]允许将行大小定义为超过[!INCLUDE[ssDE](../../includes/ssde-md.md)]处理能力的最大可能的大小。 通常，应用程序存储实际大小在[!INCLUDE[ssDE](../../includes/ssde-md.md)]处理能力范围内的行，而不管最大可能大小。 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]遇到过长的行，则返回执行错误。  
 
 使用提示 ( *hint_name* )  
 **适用于**： 适用于 SQL Server （从 2016 SP1 开始） 和 Azure SQL 数据库。
 
 提供了一个或多个查询处理器的提示名称按指定的其他提示**在单引号内**。 
  **适用于**： 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。

 支持以下提示名称：
 
*  DISABLE_OPTIMIZED_NESTED_LOOP  
 指示查询处理器无法生成查询计划时使用优化的嵌套的循环联接的排序操作 （批处理排序）。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)2340年。
*  FORCE_LEGACY_CARDINALITY_ESTIMATION  
 强制查询优化器使用[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型的[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更早版本。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9481 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 LEGACY_CARDINALITY_ESTIMATION = ON。
*  ENABLE_QUERY_OPTIMIZER_HOTFIXES  
 启用查询优化器修补程序 （在 SQL Server 累积更新和 Service Pack 中发布的更改）。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4199 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 QUERY_OPTIMIZER_HOTFIXES = ON。
*  DISABLE_PARAMETER_SNIFFING  
 指示查询优化器使用时编译具有一个或多个参数，在第一次时使用已编译查询时的参数值上进行的查询计划独立的查询的平均数据分布。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4136 或[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 PARAMETER_SNIFFING = OFF。
*  ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES  
 会导致 SQL Server 以生成使用最小选择性估计 AND 筛选器谓词时帐户关联的计划。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4137 与的基数估算模型一起使用时[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和早期版本中，并且具有类似的效果时[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9471 用于基数估算模型的[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]或更高版本。
*  DISABLE_OPTIMIZER_ROWGOAL  
 导致 SQL Server 以生成不使用查询时，包含 TOP，选项 (FAST N)，使用行目标调整的计划，或存在关键字。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4138。
*  ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS  
 启用自动生成快速的统计信息 （直方图修正） 的基数估计所需的任何前导索引列。 用于估计基数直方图将调整在查询编译时，来应对此列的实际的最大或最小值。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)4139。 
*  ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS  
 SQL server 会生成查询计划对于联接，在查询优化器而不默认基包含假设使用简单的包含假设[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)模型的[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]或更高版本。 这相当于[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9476。 
*  FORCE_DEFAULT_CARDINALITY_ESTIMATION  
 强制查询优化器使用[基数估计](../../relational-databases/performance/cardinality-estimation-sql-server.md)对应于当前的数据库兼容性级别的模型。 使用此提示来覆盖[Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)设置 LEGACY_CARDINALITY_ESTIMATION = ON 或[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)9481。
 
> [!TIP]
> 提示名称不区分大小写。
  
  可以使用动态管理视图查询的所有受支持的使用提示名称的列表[sys.dm_exec_valid_use_hints ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)。
> [!IMPORTANT] 
> 一些使用提示提示可能会与在全局启用的跟踪标志冲突或会话级别或数据库作用域配置设置。 在这种情况下，查询级别提示 （使用提示） 始终将优先。 如果与另一个查询提示或在查询级别启用跟踪标志使用提示发生冲突 (例如通过 QUERYTRACEON)，在尝试执行查询时，SQL Server 将生成错误。 

 USE PLAN N*xml_plan*  
 强制查询优化器将查询指定的现有查询计划*xml_plan*。 不能使用 INSERT、UPDATE、MERGE 或 DELETE 语句来指定 USE PLAN。  
  
表提示**(***exposed_object_name* [ **，** \<table_hint > [[**，** ]... *n*  ]] **)**适用范围的表或视图的对应于指定的表提示*exposed_object_name*。 我们建议作为查询提示的上下文中仅使用表提示[计划指南](../../relational-databases/performance/plan-guides.md)。  
  
 *exposed_object_name*可以是以下引用之一：  
  
-   当为表或视图中的使用别名[FROM](../../t-sql/queries/from-transact-sql.md)子句的查询、 查询*exposed_object_name*是别名。  
  
-   如果不使用别名， *exposed_object_name*表或视图的 FROM 子句中引用的完全匹配项。 例如，如果使用两个部分构成的名称，引用表或视图*exposed_object_name*是相同的两部分名称。  
  
 当*exposed_object_name*指定如果没有指定表提示，将忽略表提示的对象的一部分以及索引的使用由查询优化器查询中指定任何索引。 当您无法修改原始查询时，可以使用此方法来消除 INDEX 表提示的影响。 请参阅示例 J。  
  
**\<table_hint >:: =** {[NOEXPAND] {索引 ( *index_value* [，...*n* ] ) |索引 = ( *index_value* ) |FORCESEEK [**(***index_value***(***index_column_name* [**，**...]**))** ]|FORCESCAN |HOLDLOCK |NOLOCK |NOWAIT |PAGLOCK |READCOMMITTED |READCOMMITTEDLOCK |READPAST |READUNCOMMITTED |REPEATABLEREAD |ROWLOCK |可序列化 |快照 |SPATIAL_WINDOW_MAX_CELLS |TABLOCK |TABLOCKX |UPDLOCK |XLOCK} 是要应用于表或视图的对应于表提示*exposed_object_name*作为查询提示。 有关这些提示的说明，请参阅[表提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 不允许将非 INDEX、FORCESCAN 和 FORCESEEK 的表提示用作查询提示，除非该查询已经具有一个指定该表提示的 WITH 子句。 有关详细信息，请参阅“备注”。  
  
> [!CAUTION] 
> 指定带参数的 FORCESEEK 限制优化器可以考虑的计划数大于指定不带参数的 FORCESEEK 时的计划数。 这可能导致在更多情况下出现“无法生成计划”错误。 在未来的版本中，对优化器进行内部修改后可允许考虑更多计划。  
  
## <a name="remarks"></a>注释  
 只有在 INSERT 语句中使用了 SELECT 子句时，才能在该语句中指定查询提示。  
  
 只能在顶级查询中指定查询提示，不能在子查询指定。 在顶级查询中或在子查询; 当表提示指定为查询提示时，可以指定提示但是，为指定的值*exposed_object_name*子句必须完全中查询或子查询的公开的名称匹配中表提示。  
  
## <a name="specifying-table-hints-as-query-hints"></a>将表提示指定为查询提示  
 我们建议作为查询提示的上下文中仅使用 INDEX、 FORCESCAN 或 FORCESEEK 表提示[计划指南](../../relational-databases/performance/plan-guides.md)。 当您无法修改原始查询时（例如，由于它是第三方应用程序），计划指南将很有用。 计划指南中指定的查询提示在查询编译和优化前添加到查询中。 对于即席查询，仅在测试计划指南语句时才应使用 TABLE HINT 子句。 对于所有其他即席查询，建议仅将这些提示指定为表提示。  
  
 如果将 INDEX、FORCESCAN 和 FORCESEEK 表提示指定为查询提示，它们会对以下对象有效：  
  
-   表  
  
-   视图  
  
-   索引视图  
  
-   公用表表达式（必须在其结果集填充公用表表达式的 SELECT 语句中指定提示）  
  
-   动态管理视图  
  
-   命名子查询  
  
 可以为没有任何现有表提示的查询指定 INDEX、FORCESCAN 和 FORCESEEK 表提示作为查询提示，这些提示也可用于分别替换查询中的现有 INDEX、FORCESCAN 或 FORCESEEK 提示。 不允许将非 INDEX、FORCESCAN 和 FORCESEEK 的表提示用作查询提示，除非该查询已经具有一个指定该表提示的 WITH 子句。 这种情况下，还必须使用 OPTION 子句中的 TABLE HINT 来将匹配的提示指定为查询提示，以保留查询的语义。 例如，如果查询包含表提示 NOLOCK 中的选项子句 **@hints** 计划指南的参数还必须包含 NOLOCK 提示。 请参阅示例 k。通过使用表提示，而无需匹配的查询提示的 OPTION 子句中指定表提示 INDEX、 FORCESCAN 或 FORCESEEK 以外时，反之亦然。错误 8702 引发 （指示 OPTION 子句可能会导致更改的查询语义），并查询失败。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-merge-join"></a>A. 使用 MERGE JOIN  
 下面的示例指定查询中的联接操作通过合并联接。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. 使用 OPTIMIZE FOR  
 下面的示例指示查询优化器使用值`'Seattle'`本地变量`@city_name`并使用统计数据来确定本地变量的值`@postal_code`优化查询时。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```  
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
 可以使用 MAXRECURSION 来防止不合理的递归公用表表达式进入无限循环。 下面的示例特意创建一个无限循环，并使用 MAXRECURSION 提示以限制为两个递归级别数。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```tsql  
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
 下面的示例使用合并联合查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. 使用 HASH GROUP 和 FAST  
 下面的示例使用的哈希组和快速的查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. 使用 MAXDOP  
 下面的示例使用 MAXDOP 查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
### <a name="l-using-use-hint"></a>L. 使用使用提示  
 下面的示例使用的重新编译和使用提示的查询提示。 该示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]， [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>另请参阅  
 [提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
