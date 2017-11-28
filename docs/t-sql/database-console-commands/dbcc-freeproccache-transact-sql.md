---
title: "DBCC FREEPROCCACHE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs: TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: "61"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ae416ab23f27a7f71951ac05a6c69d0abb00a90d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

删除计划高速缓存中的所有元素，通过指定计划句柄或 SQL 句柄从计划高速缓存中删除特定计划，或者删除与指定资源池相关联的所有高速缓存条目。

>[!NOTE]
>DBCC FREEPROCCACHE 不清除本机编译的存储过程的执行统计信息。 过程高速缓存不包含有关本机编译的存储过程的信息。 从过程执行收集任何执行统计信息将出现在 Dmv 的执行统计信息： [sys.dm_exec_procedure_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)和[sys.dm_exec_query_plan &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
SQL Server 的语法：

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

对于 Azure SQL 数据仓库和并行数据仓库的语法：
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>参数  
 ({ *plan_handle* | *sql_handle* | *pool_name* })  
*plan_handle*唯一标识一批，已执行，并且其计划位于计划缓存中的查询计划。 *plan_handle*是**varbinary(64)**并且可以从下列动态管理对象中获取该值：  
 -   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

*sql 句柄*批处理要清除的 SQL 句柄。 *sql 句柄*是**varbinary(64)**并且可以从下列动态管理对象中获取该值：  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

*pool_name*是资源调控器资源池的名称。 *pool_name*是**sysname** ，并且可以通过查询获取[sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)动态管理视图。  
 若要将资源调控器工作负荷组关联的资源池，请查询[sys.dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)动态管理视图。 有关适用于会话的工作负荷组，查询[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)动态管理视图。  

  
 WITH NO_INFOMSGS  
 取消显示所有信息性消息。  
  
 COMPUTE  
 清除查询计划缓存中每个计算节点。 这是默认值。  
  
 ALL  
 从每个计算节点和管理节点，请清除查询计划缓存。  

> [!NOTE]
> 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]、`ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE`以清除作用域中的数据库的过程 （计划） 缓存。

## <a name="remarks"></a>注释  
小心使用 DBCC FREEPROCCACHE 清除计划高速缓存。 清除过程 （计划） 缓存导致的所有计划被逐出和传入的查询执行将编译新的计划，而不重用任何以前缓存的计划。 

这会导致为新编译增加数的查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的高速缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志将包含以下信息性消息：“由于 'DBCC FREEPROCCACHE' 或 'DBCC FREESYSTEMCACHE' 操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 高速缓存存储区(计划缓存的一部分)的 %d 次刷新。” 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。

以下重新配置操作也将清除过程缓存：
-   访问检查缓存存储桶计数  
-   访问检查缓存配额  
-   clr enabled  
-   并行的开销阈值  
-   cross db ownership chaining  
-   索引创建内存  
-   最大并行度  
-   max server memory  
-   max text repl size  
-   最大工作线程数  
-   min memory per query  
-   min server memory  
-   查询调控器开销限制  
-   查询等待  
-   remote query timeout  
-   user options  
  
## <a name="result-sets"></a>结果集  
如果未指定 WITH NO_INFOMSGS 子句，DBCC FREEPROCCACHE 返回:"DBCC 执行完毕。 如果 DBCC 输出了错误消息，请与系统管理员联系。”
  
## <a name="permissions"></a>Permissions  
适用于： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- 需要对服务器的 ALTER SERVER STATE 权限。  

适用于：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- 要求具有 DB_OWNER 固定的服务器角色的成员身份。  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>常规备注[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
可以同时运行多个 DBCC FREEPROCCACHE 命令。
在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、 清除计划缓存可能导致临时降低查询性能，如传入的查询编译新的计划，而不是重用任何先前缓存计划。 

DBCC FREEPROCCACHE （计算） 仅会导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新编译查询，在运行时计算节点上。 它不会导致[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]重新编译控制节点上的并行查询计划的生成。
可以在执行期间取消 DBCC FREEPROCCACHE。
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>限制和局限为[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
无法在事务中运行 DBCC FREEPROCCACHE。
在解释语句中不支持 DBCC FREEPROCCAHCE。
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>元数据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
运行 DBCC FREEPROCCACHE 时，会 sys.pdw_exec_requests 系统视图中添加新的一行。

## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>示例：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>A. 从计划高速缓存中清除查询计划  
以下示例通过指定查询计划句柄从计划高速缓存中清除查询计划。 为了确保示例查询在计划高速缓存中，首先执行该查询。 `sys.dm_exec_cached_plans`和`sys.dm_exec_sql_text`动态管理视图查询以返回查询的计划句柄。 

然后，将结果集中的计划句柄值插入 `DBCC FREEPROCACHE` 语句，以从计划高速缓存中仅删除该计划。
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
plan_handle                                         text  
--------------------------------------------------  -----------------------------  
0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;  
  
(1 row(s) affected)
 ```
 
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>B. 清除计划高速缓存中的所有计划  
以下示例清除计划高速缓存中的所有元素。 WITH`NO_INFOMSGS`子句指定以防止信息消息显示。
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. 清除与资源池相关联的所有高速缓存条目  
以下示例清除与指定资源池相关联的所有高速缓存条目。 `sys.dm_resource_governor_resource_pools`视图首先查询以获取的值*pool_name*。
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. DBCC FREEPROCCACHE 基本语法示例  
下面的示例从计算节点中删除所有现有的查询计划缓存。 虽然上下文设置为 UserDbSales，所有数据库的计算节点查询计划缓存将会被删除。 WITH NO_INFOMSGS 子句可防止在结果中显示信息性消息。  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 下面的示例具有相同的结果与前面的示例中，只是信息性消息将显示在结果中。  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
当请求信息性消息，并执行是成功时，查询结果将具有一个行，每个计算节点。
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. 运行 DBCC FREEPROCCACHE 授予权限  
下面的示例提供的登录名 David 权运行 DBCC FREEPROCCACHE。  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  
