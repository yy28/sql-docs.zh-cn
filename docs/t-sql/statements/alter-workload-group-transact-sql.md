---
title: "ALTER WORKLOAD GROUP (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs: TSQL
helpviewer_keywords: ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
caps.latest.revision: "56"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d48a892ef00610cc0d69ff8d2a36e0fce4be7704
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改现有的资源调控器工作负荷组配置，并且可以选择将其分配给资源调控器资源池。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *group_name* | "**default**"  
 是现有用户定义工作负荷组或资源调控器默认工作负荷组的名称。  
  
> [!NOTE]  
> 在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时资源调控器创建“默认”和内部组。  
  
 与 ALTER WORKLOAD GROUP 一起使用时，选项 "default" 必须用引号 ("") 引起来或用方括号 ([]) 括起来，以免与系统保留字 DEFAULT 冲突。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
> [!NOTE]  
> 预定义的工作负荷组和资源池全部使用小写字母的名称，例如"默认"。 对于使用区分大小写排序规则的服务器，应当注意这一点。 使用不区分大小写排序规则的服务器（例如 SQL_Latin1_General_CP1_CI_AS）会将“default”和“Default”视为相同。  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 指定工作负荷组中某个请求的相对重要性。 重要性为以下值之一：  
  
-   LOW  
-   MEDIUM（默认值）  
-   HIGH  
  
> [!NOTE]  
> 在内部，每个重要性设置都存储为用于计算的一个数字。  
  
 IMPORTANCE 对资源池而言是局部性的；同一资源池内重要性不同的工作负荷组会相互影响，但不会影响其他资源池中的工作负荷组。  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*value*  
 指定单个请求可以从池中获取的最大内存量。 此百分比是相对于 MAX_MEMORY_PERCENT 指定的资源池大小而言的。  
  
> [!NOTE]  
> 指定的量指的只是查询执行授予内存。  
  
 *值*必须为 0 或一个正整数。 所允许的范围*值*是从 0 到 100 之间。 默认设置*值*为 25。  
  
 请注意以下事项：  
  
-   设置*值*为 0 会阻止包含用户定义的工作负荷组中的排序和哈希联接运算的查询运行。  
  
-   我们不建议设置*值*大于 70 因为服务器可能无法留出足够的可用内存，如果其他并发查询正在运行。 可能最终会导致查询超时错误 8645。  
  
> [!NOTE]  
>  如果查询内存要求超过了此参数指定的限制，服务器会执行以下操作：  
>   
>  对于用户定义的工作负荷组，服务器会尝试降低查询的并行度，直到内存要求降到限制范围以内，或直到并行度等于 1。 如果查询内存要求仍然大于限制值，则会发生错误 8657。  
>   
>  对于内部和默认工作负荷组，服务器会允许查询获取必需的内存。  
>   
>  请注意，如果服务器没有足够的物理内存，则这两种情况都会出现超时错误 8645。  
  
 REQUEST_MAX_CPU_TIME_SEC =*value*  
 指定请求可以使用的最长 CPU 时间，以秒为单位。 *值*必须为 0 或一个正整数。 默认设置*值*为 0，这意味着无限制。  
  
> [!NOTE]  
> 默认情况下，资源调控器不会阻止请求继续如果超出最大时间。 但会生成一个事件。 有关详细信息，请参阅[CPU 阈值超出 Event Class](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。 

> [!IMPORTANT]
> 从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3，并使用[跟踪标志 2422年](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，资源调控器将中止请求时超出最大时间。
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*值*  
 指定查询等待内存授予（工作缓冲区内存）变为可用的最长时间（以秒为单位）。  
  
> [!NOTE]  
>  查询并不总是在达到内存授予超时的时候失败。 仅当有太多并发查询运行时，查询才失败。 否则，查询只能获取最小内存授予，从而导致查询性能下降。  
  
 *值*必须是正整数。 默认设置*值*，0，使用基于查询开销的内部计算来确定的最长时间。  
  
 MAX_DOP =*value*  
 指定最大并行度 (DOP 并行请求)。 *值*必须是 0 或正整数，1 到 255。 当*值*为 0，则服务器会选择最大并行度。 这是默认设置，还是推荐设置。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]为 MAX_DOP 设置的实际值可能小于指定值。 最终值由的公式的最小值 (255，*的 Cpu 数)*。  
  
> [!CAUTION]  
>  更改 MAX_DOP 可能会对服务器的性能产生不利影响。 如果必须更改 MAX_DOP，我们建议将其设置为小于或等于在单个 NUMA 节点中存在的硬件计划程序的最大数目。 我们建议您不要将 MAX_DOP 设置为大于 8 的值。  
  
 按如下方式处理 MAX_DOP：  
  
-   只要作为查询提示的 MAX_DOP 不超过工作负荷组 MAX_DOP，便遵守作为查询提示的 MAX_DOP。  
  
-   作为查询提示的 MAX_DOP 始终会覆盖 sp_configure 'max degree of parallelism'。  
  
-   工作负荷组 MAX_DOP 覆盖 sp_configure 'max degree of parallelism'。  
  
-   如果查询在编译时标记为串行 (MAX_DOP = 1)，则无论工作负荷组或 sp_configure 的设置如何，在运行时该查询都无法改回并行。  
  
 配置 DOP 后，只能在授予内存不足时降低它。 工作负荷组重新配置在授予内存队列中等待时不可见。  
  
 GROUP_MAX_REQUESTS =*value*  
 指定在工作负荷组中允许执行的同时请求最大数。 *值*必须为 0 或一个正整数。 默认设置*值*，0，允许无限的请求。 当达到最大并发请求数时，该组中的用户可以登录但置于等待状态，直至并发请求数降到指定值之下。  
  
 使用 { *pool_name* |"**默认**"}  
 将与由标识的用户定义的资源池关联的工作负荷组*pool_name*，这实际上将放置在资源池的工作负荷组。 如果*pool_name*未提供或使用自变量未使用，如果工作负荷组放在预定义的资源调控器默认池。  
  
 与 ALTER WORKLOAD GROUP 一起使用时，选项 "default" 必须用引号 ("") 引起来或用方括号 ([]) 括起来，以免与系统保留字 DEFAULT 冲突。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
> [!NOTE]  
>  选项 "default" 区分大小写。  
  
## <a name="remarks"></a>注释  
 允许对默认组使用 ALTER WORKLOAD GROUP。  
  
 对工作负荷组配置的更改直到执行 ALTER RESOURCE GOVERNOR RECONFIGURE 后才会生效。 在执行 DBCC FREEPROCCACHE 后新设置时更改影响设置的计划，只会在以前缓存的计划生效 (*pool_name*)，其中*pool_name*是资源的名称在其工作负荷组都与关联的调控器资源池。  
  
-   如果您要更改 MAX_DOP 为 1，执行 DBCC FREEPROCCACHE 不需要，因为并行计划可以在串行模式下运行。 但是，它可能不是编译为串行计划的计划与一样有效。  
  
-   如果您要 MAX_DOP 从 1 更改为 0 或大于 1，执行 DBCC FREEPROCCACHE 的值不是必需。 但是，串行计划不能并行运行，以便清除相应的缓存将可能允许到新计划进行编译，并行度。  
  
> [!CAUTION]  
>  清除缓存的计划，从与多个工作负荷组关联的资源池将影响所有工作负荷组与用户定义的资源池由标识*pool_name*。  
  
 建议您在熟悉资源调控器状态之后再执行 DDL 语句。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。  
  
 REQUEST_MEMORY_GRANT_PERCENT：在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，允许索引创建操作使用比最初授予的工作区内存多的工作区内存，以便提高性能。 这个特别处理在更高版本中由资源调控器支持，然而，最初授予及任何其他内存授予都受资源池和工作负荷组设置的限制。  
  
 **已分区表创建索引**  
  
 针对非对齐已分区表创建索引占用的内存是涉及的分区数成正比。  如果所需的内存总量超过资源调控器工作负荷组设置为每个查询设定的限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，则可能无法执行这种索引创建。 由于“默认”工作负荷组允许查询超过每个查询的限制，并在开始时使用所需的最低内存以便与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 保持兼容，因此，如果“默认”资源池配置了足够多的内存总量以运行此类查询，则用户或许能够在“默认”工作负荷组中运行相同的索引创建。  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例说明了如何将默认组中请求的重要性从 `MEDIUM` 更改为 `LOW`。  
  
```  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 下面的示例说明了如何将一个工作负荷组从它所在的池中移到默认池中。  
  
```  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
