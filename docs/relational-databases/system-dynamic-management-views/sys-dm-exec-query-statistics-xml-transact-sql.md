---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 63e1d22670929448110083c31e9900e462d576bc
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58072301"
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

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|会话的 ID。 不可为 Null。|
|request_id|**int**|请求的 ID。 不可为 Null。|
|sql_handle|**varbinary(64)**|请求的 SQL 文本的哈希映射。 可以为 NULL。|
|plan_handle|**varbinary(64)**|查询计划哈希映射。 可以为 NULL。|
|query_plan|**xml**|使用部分统计信息的 Showplan XML。 可以为 NULL。|

## <a name="remarks"></a>备注
此系统函数是从开始提供[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。 请参阅知识库[3190871](https://support.microsoft.com/en-us/help/3190871)

此系统函数下都适用**标准**并**轻型**查询执行统计信息分析基础结构。 有关详细信息，请参阅[查询分析基础结构](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)。  

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

