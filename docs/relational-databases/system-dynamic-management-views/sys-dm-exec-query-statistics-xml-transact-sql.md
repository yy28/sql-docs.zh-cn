---
title: sys.dm_exec_query_statistics_xml (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 06091ffc26ea036a4a0bd7e30196545bcaca60d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936948"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

返回查询执行计划正在进行的请求。 使用此 DMV 来检索 showplan XML 使用临时统计信息。 

## <a name="syntax"></a>语法

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>参数 
*session_id*  
 执行要查找的批处理的会话 id。 *session_id*是**smallint**。 *session_id*可以从以下动态管理对象中获得：  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>返回的表

|列名|数据类型|描述|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|会话的 ID。 不可为 Null。|
|request_id|**int**|请求的 ID。 不可为 Null。|
|sql_handle|**varbinary(64)**|是一个令牌，用于唯一标识批处理或存储的过程的查询。 可以为 NULL。|
|plan_handle|**varbinary(64)**|是唯一标识当前正在执行的批次查询执行计划的令牌。 可以为 NULL。|
|query_plan|**xml**|包含运行时使用指定的查询执行计划的显示计划表示形式*plan_handle*包含部分统计信息。 显示计划的格式为 XML。 为包含即席 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、存储过程调用以及用户定义函数调用等内容的每个批查询生成一个计划。 可以为 NULL。|

## <a name="remarks"></a>备注
此系统函数是从开始提供[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。 请参阅知识库[3190871](https://support.microsoft.com/en-us/help/3190871)

此系统函数下都适用**标准**并**轻型**查询执行统计信息分析基础结构。 有关详细信息，请参阅[查询分析基础结构](../../relational-databases/performance/query-profiling-infrastructure.md)。  

在以下情况下不显示计划输出中返回**query_plan**返回的表的列**sys.dm_exec_query_statistics_xml**:  
  
-   对应于指定的查询计划，如果*session_id*不再执行**query_plan**列返回的表为 null。 例如，可能会发生此问题，如果没有捕获计划句柄的和已使用与时间之间的时间延迟**sys.dm_exec_query_statistics_xml**。  
    
由于在允许的嵌套级别数的限制造成**xml**数据类型**sys.dm_exec_query_statistics_xml**不能返回达到或超过 128 级的嵌套元素的查询计划。 在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这种情况将导致无法返回查询计划，并生成错误 6335。 在中[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Service Pack 2 和更高版本**query_plan**列返回 NULL。   

## <a name="permissions"></a>权限  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  

## <a name="examples"></a>示例  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 查看实时查询计划和执行统计信息用于运行批处理  
 下面的示例查询**sys.dm_exec_requests**若要查找感兴趣的查询并复制其`session_id`输出中。  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 然后，若要获取实时查询计划和执行统计信息，请使用复制`session_id`系统函数与**sys.dm_exec_query_statistics_xml**。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 或组合的所有正在运行的请求。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>请参阅
  [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

