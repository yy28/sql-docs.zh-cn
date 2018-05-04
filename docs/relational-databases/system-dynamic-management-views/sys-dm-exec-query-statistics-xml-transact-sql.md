---
title: sys.dm_exec_query_statistics_xml (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
caps.latest.revision: 6
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: f52c0a1a39d3c8ab56241644e4c8e4d42c9d0af7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

返回的查询正在进行的请求的执行计划。 使用此 DMV 来检索与临时统计信息的 showplan XML。 

## <a name="syntax"></a>语法

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>参数 
*session_id*  
 执行批处理要查找的会话 id。 *session_id*是**smallint**。 *session_id*可以从以下动态管理对象中获得：  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>返回的表
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|
|session_id|**int**|会话的 ID。 不可为 Null。|
|request_id|**int**|请求的 ID。 不可为 Null。|
|sql_handle|**varbinary(64)**|请求的 SQL 文本的哈希映射。 可以为 NULL。|
|plan_handle|**varbinary(64)**|查询计划哈希映射。 可以为 NULL。|
|query_plan|**xml**|使用部分的统计信息的 Showplan XML。 可以为 NULL。|

## <a name="remarks"></a>注释
此系统函数是从开始提供[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。

此系统函数可下都**标准**和**轻型**查询执行统计信息分析基础结构。  
  
**标准**可以通过启用分析基础结构的统计信息：
  -  [集上的统计信息 XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [集上的统计信息配置文件](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  `query_post_execution_showplan`扩展的事件。  
  
**轻型**分析基础结构的统计信息可用于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]并且可以启用：
  -  全局使用跟踪标志 7412。
  -  使用[ *query_thread_profile* ](http://support.microsoft.com/kb/3170113)扩展的事件。
  
> [!NOTE]
> 一旦启用了跟踪标志 7412，请将分析基础结构而不是标准分析，如 DMV 的查询执行统计信息的任何使用者到启用轻量分析[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)。
> 但是，标准分析仍适用于 SET STATISTICS XML，*包括实际的计划*中的操作[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]，和`query_post_execution_showplan`xEvent。

> [!IMPORTANT]
> 与工作负荷测试一样 TPC C，在启用轻量的统计信息分析基础结构中添加开销 1.5 到 2%。 与此相反，标准的统计信息分析基础结构可以添加多达 90%开销为相同的工作负荷方案。

## <a name="permissions"></a>权限  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  

## <a name="examples"></a>示例  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 查看实时查询计划和执行统计信息的正在运行的批处理  
 下面的示例查询**sys.dm_exec_requests**若要查找感兴趣的查询并复制其`session_id`从输出。  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 然后，若要获取的实时查询计划和执行统计信息，请使用复制`session_id`与系统函数**sys.dm_exec_query_statistics_xml**。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 或组合所有正在运行的请求。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>另请参阅
  [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

