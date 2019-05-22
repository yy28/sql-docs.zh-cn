---
title: sys.dm_exec_query_plan_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 92e5aaf103c1c8d08b8527bf859415686fd5f4f8
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993629"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

返回之前已缓存的查询计划的最后一个已知的实际执行计划的等效项。

## <a name="syntax"></a>语法

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>参数 
*plan_handle*  
是一个标记，用于唯一标识已执行的批次查询执行计划，其计划驻留在计划缓存中，或当前正在执行。 *plan_handle*是**varbinary(64)**。   

*Plan_handle*可以从以下动态管理对象中获得：  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>返回的表

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|在编译对应于此计划的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时有效的上下文数据库的 ID。 对于临时和预定义 SQL 语句，指编译这些语句时所在的数据库的 ID。<br /><br /> 此列可为空值。|  
|**objectid**|**int**|此查询计划的对象（如存储过程或用户定义函数）的 ID。 对于临时和预定义的批处理，则此列为**null**。<br /><br /> 此列可为空值。|  
|**number**|**smallint**|为存储过程编号的整数。 例如，一组的过程**订单**可能名为应用程序**orderproc; 1**， **orderproc; 2**，依次类推。 对于临时和预定义的批处理，则此列为**null**。<br /><br /> 此列可为空值。|  
|**encrypted**|**bit**|指示对应的存储过程是否已加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密<br /><br /> 此列不可为空值。|  
|**query_plan**|**xml**|包含最后一个已知的运行时使用指定的实际查询执行计划的显示计划表示形式*plan_handle*。 显示计划的格式为 XML。 为包含即席 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、存储过程调用以及用户定义函数调用等内容的每个批查询生成一个计划。<br /><br /> 此列可为空值。| 

## <a name="remarks"></a>备注
此系统函数是从开始提供[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]CTP 2.4。

这是一个选择加入功能，并且需要启用[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。 从开始[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]CTP 2.5 然后在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，若要在数据库级别完成此操作，请参阅中的 LAST_QUERY_PLAN_STATS 选项[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。

此系统函数工作原理**轻型**查询执行统计信息分析基础结构。 有关详细信息，请参阅[查询分析基础结构](../../relational-databases/performance/query-profiling-infrastructure.md)。  

在以下情况下的显示计划输出**等效于实际执行计划**中返回**query_plan**返回的表的列**sys.dm_exec_query_plan_统计信息**:  

-   可以在中找到计划[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **AND**    
-   正在执行的查询是复杂或消耗资源。

在以下情况下**简化<sup>1</sup>** 中返回显示计划输出**query_plan**返回的表的列**sys.dm_exec_query_plan_stats**:  

-   可以在中找到计划[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **AND**    
-   查询相当简单，通常属于 OLTP 工作负荷的一部分。

<sup>1</sup>开头[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]ctp 版本 2.5 时，这是指显示计划，其中仅包含根节点运算符 （选择）。 有关[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]这是指作为可通过缓存的计划的 CTP 2.4 `sys.dm_exec_cached_plans`。

在以下情况下**会返回任何输出**从**sys.dm_exec_query_plan_stats**:

-   使用指定的查询计划*plan_handle*已从计划缓存中逐出。     
    **OR**    
-   第一个位置中未缓存查询计划。 有关详细信息，请参阅[执行计划的缓存和重用](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)。
  
> [!NOTE] 
> 由于在允许的嵌套级别数的限制造成**xml**数据类型**sys.dm_exec_query_plan**不能返回达到或超过 128 级的嵌套元素的查询计划。 在早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这种情况导致无法返回查询计划，并生成[错误 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)。 在中[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Service Pack 2 和更高版本**query_plan**列返回 NULL。  

## <a name="permissions"></a>权限  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  

## <a name="examples"></a>示例  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 查找有关某个特定缓存的计划的最后已知的实际查询执行计划  
 下面的示例查询**sys.dm_exec_cached_plans**若要查找感兴趣的计划并复制其`plan_handle`输出中。  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
然后，若要获取的最后一个已知的实际查询执行计划，请使用复制`plan_handle`系统函数与**sys.dm_exec_query_plan_stats**。  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. 查找的所有缓存的计划的最后已知的实际查询执行计划
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 查找特定缓存的计划和查询文本的最后已知的实际查询执行计划

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. 查看缓存触发器的事件

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>请参阅
  [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

