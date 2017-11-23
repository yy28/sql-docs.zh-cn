---
title: "sys.dm_db_stats_properties (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_stats_properties_TSQL
- sys.dm_db_stats_properties
- dm_db_stats_properties_TSQL
- dm_db_stats_properties
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_stats_properties
ms.assetid: 8a54889d-e263-4881-9fcb-b1db410a9453
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2a1ebc3301372b490de9ec631c3cdb0743f264b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbstatsproperties-transact-sql"></a>sys.dm_db_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中指定数据库对象（表或索引视图）的统计信息属性。 用于已分区表，请参阅类似[sys.dm_db_incremental_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)。 
 
## <a name="syntax"></a>语法  
  
```  
sys.dm_db_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>参数  
 *object_id*  
 当前数据库中您要请求其某个统计信息属性的对象的 ID。 *object_id* 是 **int**。  
  
 *stats_id*  
 指定 *object_id*的统计信息 ID。 可以从 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 动态管理视图获取该统计信息 ID。 *stats_id* 是 **int**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|要返回统计信息对象属性的对象（表或索引视图）的 ID。|  
|stats_id|**int**|统计信息对象的 ID。 在表或索引视图中是唯一的。 有关详细信息，请参阅 [sys.stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)。|  
|last_updated|**datetime2**|上次更新统计信息对象的日期和时间。|  
|rows|**bigint**|上次更新统计信息时表或索引视图中的总行数。 如果筛选统计信息或者统计信息与筛选索引对应，该行数可能小于表中的行数。|  
|rows_sampled|**bigint**|用于统计信息计算的抽样总行数。|  
|步骤|**int**|直方图中的梯级数。 有关详细信息，请参阅 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。|  
|unfiltered_rows|**bigint**|应用筛选表达式（用于筛选的统计信息）之前表中的总行数。 如果未筛选统计信息，则 unfiltered_rows 等于行列中返回的值。|  
|modification_counter|**bigint**|自上次更新统计信息以来前导统计信息列（构建直方图的列）的总修改次数。<br /><br /> 内存优化表： 正在启动[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]并在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]此列包含： 对表的最后一个时间统计信息已更新或重启了数据库后修改的总数。|  
|persisted_sample_percent|**float**|保留用于未显式指定抽样百分比的统计信息更新的示例百分比。 如果值为零，则无持久化的示例百分比设置为此统计信息。<br /><br /> **适用于：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4|  
  
## <a name="remarks"></a>注释  
 **sys.dm_db_stats_properties**返回行集在任何以下情况下的为空：  
  
-   **object_id**或**stats_id**为 NULL。  
  
-   指定的对象未找到或不对应于某个表或索引视图。  
  
-   指定的统计信息 ID 不对应于指定对象 ID 的现有统计信息。  
  
-   当前用户没有权限查看统计信息对象。  
  
 此行为允许的安全用法**sys.dm_db_stats_properties**跨应用时视图中的行如**sys.objects**和**sys.stats**。  
  
## <a name="permissions"></a>Permissions  
 要求用户对统计信息列拥有 select 权限，或用户拥有表，或用户是 `sysadmin` 固定服务器角色、`db_owner` 固定数据库角色或 `db_ddladmin` 固定数据库角色的成员。  
  
## <a name="examples"></a>示例  

### <a name="a-simple-example"></a>A. 简单示例
下面的示例返回的统计信息`Person.Person`AdventureWorks 数据库中的表。

```
SELECT * FROM sys.dm_db_stats_properties (object_id('Person.Person'), 1);
``` 
  
### <a name="b-returning-all-statistics-properties-for-a-table"></a>B. 返回表的所有统计信息属性  
 以下示例返回表 TEST 的所有统计信息属性。  
  
```  
SELECT sp.stats_id, name, filter_definition, last_updated, rows, rows_sampled, steps, unfiltered_rows, modification_counter   
FROM sys.stats AS stat   
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE stat.object_id = object_id('TEST');  
```  
  
### <a name="c-returning-statistics-properties-for-frequently-modified-objects"></a>C. 返回频繁修改的对象的统计信息属性  
 以下示例返回自上次更新统计信息以来当前数据库中前导列修改次数超过 1000 的所有表、索引视图和统计信息。  
  
```  
SELECT obj.name, obj.object_id, stat.name, stat.stats_id, last_updated, modification_counter  
FROM sys.objects AS obj   
INNER JOIN sys.stats AS stat ON stat.object_id = obj.object_id  
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE modification_counter > 1000;  
```  
  
## <a name="see-also"></a>另请参阅  
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [与对象相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_incremental_stats_properties (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)  
 [sys.dm_db_stats_histogram (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  

