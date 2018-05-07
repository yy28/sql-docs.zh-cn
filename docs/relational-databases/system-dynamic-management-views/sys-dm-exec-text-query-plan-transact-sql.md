---
title: sys.dm_exec_text_query_plan (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f5ed66bb58d986647df1f678553245eab2be8571
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexectextqueryplan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理或批处理中的特定语句返回文本格式的显示计划。 查询计划指定的计划句柄可以处于缓存或当前正在执行。 此表值函数是类似于[sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)，但有以下不同：  
  
-   查询计划的输出以文本格式返回。  
  
-   查询计划的输出无大小限制。  
  
-   可以指定批处理内的单个语句。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>参数  
*plan_handle*  
为已缓存或当前正在执行的批查询唯一标识查询计划。 *plan_handle*是**varbinary(64)**。  
  
可以从下列动态管理对象中获得计划句柄：  
  
-  [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_start_offset* | 0 | DEFAULT  
指示行所说明的查询在其批处理或持久性对象文本中的起始位置（字节）。 *statement_start_offset*是**int**。值 0 指示批处理的起始处。 默认值为 0。  
  
可以从下列动态管理对象中获得语句起始偏移量：  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | DEFAULT  
指示行所说明的查询在其批处理或持久性对象文本中的结束位置（字节）。  
  
*statement_start_offset*是**int**。  
  
值 -1 指示批查询的结尾处。 默认值为-1。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|在编译对应于此计划的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时有效的上下文数据库的 ID。 对于临时和预定义 SQL 语句，指编译这些语句时所在的数据库的 ID。<br /><br /> 此列可为空值。|  
|**objectid**|**int**|此查询计划的对象（如存储过程或用户定义函数）的 ID。 对于即席和已准备好的批处理，此列为**null**。<br /><br /> 此列可为空值。|  
|**number**|**int**|为存储过程编号的整数。 例如，一组过程**订单**应用程序可能名为**orderproc; 1**， **orderproc; 2**，依次类推。 对于即席和已准备好的批处理，此列为**null**。<br /><br /> 此列可为空值。|  
|**加密**|**bit**|指示对应的存储过程是否已加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密<br /><br /> 此列不可为空值。|  
|**query_plan**|**nvarchar(max)**|包含与指定的查询执行计划的编译时显示计划表示*plan_handle*。 显示计划采用文本格式。 为包含即席 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、存储过程调用以及用户定义函数调用等内容的每个批查询生成一个计划。<br /><br /> 此列可为空值。|  
  
## <a name="remarks"></a>注释  
 在以下情况下不显示计划输出中返回**计划**返回的表的列**sys.dm_exec_text_query_plan**:  
  
-   通过使用指定的查询计划，如果*plan_handle*已从计划缓存中逐出**query_plan**列返回的表为 null。 例如，可能发生此问题，如果没有时捕获计划句柄并将其用于使用之间的时间延迟**sys.dm_exec_text_query_plan**。  
  
-   有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句未放入缓存，如大容量操作语句或包含大于 8 KB 的字符串文字的语句。 不能通过使用来检索这些语句的显示计划**sys.dm_exec_text_query_plan**因为它们在缓存中不存在。  
  
-   如果[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理或存储的过程包含对用户定义函数的调用或动态 SQL，例如使用 EXEC 的调用 (*字符串*)，则该用户定义函数不会包含表中已编译 XML 显示计划返回**sys.dm_exec_text_query_plan**为批处理或存储的过程。 相反，必须进行单独调用**sys.dm_exec_text_query_plan**为*plan_handle*相对应的用户定义函数。  
  
当即席查询使用[简单](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)或[强制参数化](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)、 **query_plan**列将包含仅语句文本，而不是实际查询计划。 若要返回查询计划，请调用**sys.dm_exec_text_query_plan**的已准备的参数化查询的计划句柄。 你可以确定查询是否已通过引用参数化**sql**列[sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)视图或文本列[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)动态管理视图。  
  
## <a name="permissions"></a>权限  
 若要执行**sys.dm_exec_text_query_plan**，用户必须是属于**sysadmin**固定服务器角色或服务器上具有 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 检索运行速度缓慢的 Transact-SQL 查询或批处理的缓存查询计划  
 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询或批查询在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定连接上运行的时间很长，请检索该查询或批查询的执行计划，以查找导致延迟的原因。 以下示例显示的是如何检索运行速度缓慢的查询或批处理的显示计划。  
  
> [!NOTE]  
> 若要运行此示例中，值替换为*session_id*和*plan_handle*使用特定于你的服务器的值。  
  
 首先，使用 `sp_who` 存储过程检索正在执行查询或批查询的进程的服务器进程 ID (SPID)。  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 由 `sp_who` 返回的结果集指示 SPID 为 `54`。 可以在 `sys.dm_exec_requests` 动态管理视图中使用该 SPID，以便使用以下查询来检索计划句柄：  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 通过返回的表**sys.dm_exec_requests**指示运行速度缓慢的查询或批处理的计划句柄是`0x06000100A27E7C1FA821B10600`。 以下示例返回指定计划句柄的查询计划，并使用默认值 0 和 -1 返回查询或批处理中的所有语句。  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. 从计划缓存中检索每个查询计划  
 若要检索驻留在计划缓存中的所有查询计划的快照，请通过查询 `sys.dm_exec_cached_plans` 动态管理视图来检索缓存中所有查询计划的计划句柄。 计划句柄存储在 `plan_handle` 的 `sys.dm_exec_cached_plans` 列中。 然后，使用 CROSS APPLY 运算符将计划句柄传递给 `sys.dm_exec_text_query_plan`，如下所示。 显示计划输出中的每个计划缓存中的当前计划个`query_plan`返回的表的列。  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 检索服务器从计划缓存中收集了查询统计信息的每个查询计划  
 若要检索服务器已收集了其当前驻留在计划缓存中的统计信息的所有查询计划的快照，请通过查询 `sys.dm_exec_query_stats` 动态管理视图来检索缓存中这些计划的计划句柄。 计划句柄存储在 `plan_handle` 的 `sys.dm_exec_query_stats` 列中。 然后，使用 CROSS APPLY 运算符将计划句柄传递给 `sys.dm_exec_text_query_plan`，如下所示。 每个计划的显示计划输出位于返回的表的 `query_plan` 列中。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 检索有关前五个查询按平均 CPU 时间的信息  
 以下示例返回前五个查询的查询计划和平均 CPU 时间。 **Sys.dm_exec_text_query_plan**函数指定的默认值 0 和-1 以返回批处理中的所有语句，查询计划中。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
