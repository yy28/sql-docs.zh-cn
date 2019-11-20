---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 50c5edee93747c98060d664f1edd2d42036aa9b2
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982656"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>单击一个产品！

在下一行中，单击你感兴趣的产品名称。 单击时此网页上的此位置会显示适合你单击的任何产品的不同内容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[SQL 数据库<br />托管实例](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL 数据<br />数据仓库](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL 数据库托管实例

创建资源调控器工作负荷组并将工作负荷组与资源调控器资源池关联。 不是 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都提供资源调控器。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。

![“主题链接”图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>语法

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>参数

group_name      
是工作负荷组的用户定义名称。 group_name 由字母数字组成，最多可包含 128 个字符，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中必须是唯一的，并且必须符合[标识符](../../relational-databases/databases/database-identifiers.md)规则  。

IMPORTANCE = { LOW | MEDIUM | HIGH }      
指定工作负荷组中某个请求的相对重要性。 重要性为下列值之一，默认值为 MEDIUM：

- LOW
- MEDIUM（默认值）
- HIGH

> [!NOTE]
> 在内部，每个重要性设置都存储为用于计算的一个数字。

IMPORTANCE 对资源池而言是局部性的；同一资源池内重要性不同的工作负荷组会相互影响，但不会影响其他资源池中的工作负荷组。

REQUEST_MAX_MEMORY_GRANT_PERCENT = value      
指定单个请求可以从池中获取的最大内存量。 value 是相对于 MAX_MEMORY_PERCENT 指定的资源池大小的百分比  。 

value 是一个最大为 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 的整数，以及一个以 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开头的浮点数  。 默认值为 25。 value 的允许范围是 1 到 100  。

> [!NOTE]  
> 指定的量指的只是查询执行授予内存。  
  
> [!IMPORTANT]
> 将 value 设置为 0 可阻止在用户定义的工作负荷组中运行具有 SORT 和 HASH JOIN 操作的查询  。     
>
> 建议不要将 value 设置为大于 70，这是因为如果正在运行其他并发查询，则服务器可能无法保留足够的空闲内存  。 可能最终会导致查询超时错误 8645。      
  
> [!NOTE]  
> 如果查询内存要求超过了此参数指定的限制，服务器会执行以下操作：  
>   
> -  对于用户定义的工作负荷组，服务器会尝试降低查询的并行度，直到内存要求降到限制范围以内，或直到并行度等于 1。 如果查询内存要求仍然大于限制值，则会发生错误 8657。  
>   
> -  对于内部和默认工作负荷组，服务器会允许查询获取必需的内存。  
>   
> 请注意，如果服务器没有足够的物理内存，则这两种情况都会出现超时错误 8645。  

REQUEST_MAX_CPU_TIME_SEC = value      
指定请求可以使用的最长 CPU 时间，以秒为单位。 value 必须为 0 或一个正整数  。 value 的默认设置为 0，也就是说无限制  。

> [!NOTE]
> 默认情况下，如果超过最长时间，Resource Governor 并不会阻止继续发出请求。 但会生成一个事件。 有关详细信息，请参阅 [CPU Threshold Exceeded 事件类](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。     

> [!IMPORTANT]
> 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 开始以及使用[跟踪标志 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 时，Resource Governor 将在超出最大时间时终止请求。

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value      
指定查询等待内存授予（工作缓冲区内存）变为可用状态的最长时间（以秒为单位）。 value 必须为 0 或一个正整数  。 value 的默认设置为 0，表示使用基于查询开销的内部计算来确定最长时间  。

> [!NOTE]
> 查询并不总是在达到内存授予超时的时候失败。 仅当有太多并发查询运行时，查询才失败。 否则，查询只能获取最小内存授予，从而导致查询性能下降。

MAX_DOP = value      
指定并行查询执行的最大并行度 (MAXDOP)。  value 必须为 0 或一个正整数  。 value 的允许范围为 0 到 64  。 value 的默认设置为 0，表示使用全局设置  。 按如下方式处理 MAX_DOP：

> [!NOTE]
> 工作负荷组 MAX_DOP 会覆盖[最大并行度的服务器配置](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)和 MAXDOP [数据库范围的配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 

> [!TIP]
> 若要在查询级别完成此操作，请使用 MAXDOP [查询提示](../../t-sql/queries/hints-transact-sql-query.md)。  将最大并行度设置为查询提示时，在未超出工作负荷组 MAX_DOP 时保持有效。 如果 MAXDOP 查询提示值超出使用资源调控器配置的值，则 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 使用资源调控器 `MAX_DOP` 值。 MAXDOP [查询提示](../../t-sql/queries/hints-transact-sql-query.md)始终会覆盖[最大并行度的服务器配置](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。      
>   
> 若要在数据库级别完成此操作，请使用 MAXDOP [数据库范围的配置](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。       
>   
> 若要在服务器级别完成此操作，请使用最大并行度 (MAXDOP)  [服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。     

GROUP_MAX_REQUESTS = value      
指定在工作负荷组中允许执行的同时请求最大数。 value 必须为 0 或一个正整数  。 value 的默认设置为 0，表示允许的请求数不限  。 当达到最大并发请求数时，该组中的用户可以登录但置于等待状态，直至并发请求数降到指定值之下。

USING { pool_name | "default" }       
将工作负荷组与由 pool_name 标识的用户定义的资源池关联起来  。 这实际上是将工作负荷组放入资源池中。 如果没有提供 pool_name，或如果没有使用 USING 参数，将工作负荷组放入预定义的资源调控器默认池  。

"default" 是保留字，并且在与 USING 一起使用时，必须使用引号 ("") 引起来或用方括号 ([]) 括起来。

> [!NOTE]
> 预定义工作负荷组和资源池都使用小写名称，例如“default”。 对于使用区分大小写排序规则的服务器，应当注意这一点。 使用不区分大小写排序规则的服务器（例如 SQL_Latin1_General_CP1_CI_AS）会将“default”和“Default”视为相同。

EXTERNAL external_pool_name | “default“     
**适用于**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本）。

工作负荷组可以指定一个外部资源池。 可定义一个工作负荷组并关联两个池：

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作负荷和查询的资源池
- 外部进程的外部资源池。 有关详细信息，请参阅 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="remarks"></a>Remarks
使用 `REQUEST_MEMORY_GRANT_PERCENT` 时，允许索引创建操作使用比最初授予的工作区内存更多的工作区内存以提高性能。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的资源调控器支持这种特殊的处理方法。 然而，最初授予及任何其他内存授予都受资源池和工作负荷组设置的限制。

将按[任务](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)设置 `MAX_DOP` 限制。 它不是按[请求](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)限制或按查询限制。 这意味着，在并行查询期间，单个请求可以生成多个任务，然后将它们分配给[计划程序](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)。 有关详细信息，请参阅[线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md)。

如果使用 `MAX_DOP` 并在编译时将查询标记为串行，则在运行时无法更改回并行，不论工作负荷组或服务器配置如何设置。 配置 `MAX_DOP` 后，只能在内存不足时降低它。 工作负荷组重新配置在授予内存队列中等待时不可见。

### <a name="index-creation-on-a-partitioned-table"></a>对分区表创建索引

对非对齐的已分区表创建索引所占用的内存与涉及的分区数成正比。 如果所需的内存总量超过 Resource Governor 工作负荷组设置规定的每个查询的限制 `REQUEST_MAX_MEMORY_GRANT_PERCENT`，则可能无法执行此索引创建。 由于 "default" 工作负荷组允许查询超过每个查询的限制，并在开始时使用所需的最低内存，因此，如果 "default" 资源池配置了足够多的内存总量以运行此类查询，用户或许能够在 "default" 工作负荷组中运行相同的索引创建    。

## <a name="permissions"></a>权限
需要 `CONTROL SERVER` 权限。

## <a name="example"></a>示例

创建名称为 `newReports` 的工作负荷组，它使用资源调控器默认设置并位于资源调控器默认池中。 该示例指定了 `default` 池，但这并非必需的。

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>另请参阅

- [ALTER 工作负荷组 (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP 工作负荷组 (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [创建资源池 (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[SQL 数据库<br />托管实例](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||_\*SQL 数据<br />仓库\*_  &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse"></a>SQL 数据仓库 

CREATE WORKLOAD GROUP (Transact-SQL)（预览版）创建工作负荷组。  工作负荷组是一组请求的容器，是在系统上配置工作负荷管理的基础。  通过使用工作负荷组，能够为工作负荷隔离保留资源、包含资源、定义每个请求的资源并遵循执行规则。  语句完成后，设置生效。

 ![“主题链接”图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。 

```
CREATE WORKLOAD GROUP group_name  
 WITH  
 (        MIN_PERCENTAGE_RESOURCE = value  
      ,   CAP_PERCENTAGE_RESOURCE = value 
      ,   REQUEST_MIN_RESOURCE_GRANT_PERCENT = value   
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]  
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )  
  [ ; ]
```

group_name </br>
指定用于标识工作负荷组的名称。  group_name 为 sysname。  最长可为 128 个字符，并且在实例中必须是唯一的。

MIN_PERCENTAGE_RESOURCE = value </br>
指定为此工作负荷组保证的最小资源分配，这些资源不与其他工作负荷组共享。  取值为 0 到 100 之间的整数。  所有工作负荷组的 min_percentage_resource 的总和不能超过 100。  min_percentage_resource 的值不能大于 cap_percentage_resource。  有每个服务级别允许的最小有效值。  有关更多详细信息，请参阅有效值<link>。

CAP_PERCENTAGE_RESOURCE = value </br>
指定工作负荷组中所有请求的最大资源利用率。  取值范围为 1 到 100。  cap_percentage_resource 的值必须大于 min_percentage_resource。  如果在其他工作负荷组中将 min_percentage_resource 配置为大于零，则 cap_percentage_resource 的有效值会减少。

REQUEST_MIN_RESOURCE_GRANT_PERCENT = value </br>
设置每个请求分配到的最小资源量。  value 是一个必需参数，取值范围为 0.75 到 100.00（十进制）。  request_min_resource_grant_percent 的值必须是0.25 的倍数，必须是 min_percentage_resource 的因数，且小于 cap_percentage_resource。  有每个服务级别允许的最小有效值。  有关更多详细信息，请参阅有效值<link>。

例如：

```sql
CREATE WORKLOAD GROUP wgSample WITH  
( MIN_PERCENTAGE_RESOURCE = 26              -- integer value
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
 ,CAP_PERCENTAGE_RESOURCE = 100 )
```

将用于资源类的值视为 request_min_resource_grant_percent 的基准。  下表包含用于 Gen2 的资源分配。

|资源类|资源的百分比|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

REQUEST_MAX_RESOURCE_GRANT_PERCENT = value </br>
设置每个请求分配的最小资源量。  value 是一个可选参数，其默认值等于 request_min_resource_grant_percent。  value 不能低于 request_min_resource_grant_percent。  当 request_max_resource_grant_percent 的值大于 request_min_resource_grant_percent 并且系统资源可用时，会向请求分配其他资源。

IMPORTANCE = { LOW |  BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } </br>
指定工作负荷组中某个请求的默认重要性。  重要性为下列值之一，默认值为 NORMAL：
- LOW
- BELOW_NORMAL
- NORMAL（默认值）
- ABOVE_NORMAL
- HIGH  

在工作负荷组设置的重要性是工作负荷组中所有请求的默认重要性。  用户还可以在分类器级别设置重要性，这可能会覆盖工作负荷组的重要性设置。  这允许对工作负荷组内请求的重要性进行区分，以便更快地访问非保留资源。  当工作负荷组 min_percentage_resource 的总和小于 100 时，将根据重要性分配非保留资源。

QUERY_EXECUTION_TIMEOUT_SEC = value </br>
指定查询在取消之前可以执行的最长时间（以秒为单位）。  value 必须为 0 或一个正整数。  value 的默认设置为 0，也就是说无限制。  在请求队列中等待的时间不计入查询执行时间。

## <a name="remarks"></a>Remarks
自动创建对应于资源类的工作负荷组，以实现后向兼容性。  不能删除这些系统定义的工作负荷组。  可以创建额外的 8 个用户定义的工作负荷组。

## <a name="effective-values"></a>有效值

参数 min_percentage_resource、cap_percentage_resource、request_min_resource_grant_percent 和 request_max_resource_grant_percent 具备有效值，这些有效值会根据当前服务级别和其他工作负荷组的配置进行调整。

每个服务级别支持的并发与使用资源类定义每个查询授予的资源时保持一致，因此，request_min_resource_grant_percent 支持的值依赖于实例设置的服务级别。  最低服务级别 DW100c 支持 4 个并发。  配置的工作负荷组的有效 request_min_resource_grant_percent 可以为 25% 或更高。  有关详细信息，请参阅下表。

|服务级别|最大并行查询|REQUEST_MIN_RESOURCE_GRANT_PERCENT 和 MIN_PERCENTAGE_RESOURCE 支持的最小百分比|
|---|---|---|
|DW100c|4|25%|
|DW200c|8|12.5%|
|DW300c|12|8%|
|DW400c|16|6.25%|
|DW500c|20|5%|
|DW1000c|32|3%|
|DW1500c|32|3%|
|DW2000c|48|2%|
|DW2500c|48|2%|
|DW3000c|64|1.5%|
|DW5000c|64|1.5%|
|DW6000c|128|0.75%|
|DW7500c|128|0.75%|
|DW10000c|128|0.75%|
|DW15000c|128|0.75%|
|DW30000c|128|0.75%|
||||

同样，request_min_resource_grant_percent、min_percentage_resource 必须大于或等于有效 request_min_resource_grant_percent。  若工作负荷组的 min_percentage_resource 被配置为小于有效 min_percentage_resource，那么在运行时，该值会被调整为零。  发生这种情况时，为 min_percentage_resource 配置的资源可在所有工作负荷组中共享。  例如，工作负荷组 wgAdHoc 的 min_percentage_resource 为 10%，在 DW1000c 服务级别运行，其有效 min_percentage_resource 则为 10%（DW1000c 支持的最低值为 3.25%）。  DW100c 级别的 wgAdhoc 的有效 min_percentage_resource 为 0%。  为 wgAdhoc 配置的10% 将在所有工作负荷组之间共享。

Cap_percentage_resource 也具有有效值。  如果工作负荷组 wgAdhoc 配置 100% cap_percentage_resource，并且创建另一个 min_percentage_resource 为 25% 的工作负荷组 wgDashboards，则 wgAdhoc 的有效 cap_percentage_resource 将为 75%。

了解工作负荷组的运行时值的最简单方法是查询系统视图 [sys.dm_workload_management_workload_groups_stats] (../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md?view=azure-sqldw-latest)。

## <a name="permissions"></a>权限

需要 CONTROL DATABASE 权限

## <a name="see-also"></a>另请参阅
[DROP 工作负荷组 (Transact-SQL)](drop-workload-group-transact-sql.md)

::: moniker-end
