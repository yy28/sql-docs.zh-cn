---
title: "sys.dm_db_incremental_stats_properties (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server 2014
f1_keywords:
- sys.dm_db_incremental_stats_properties
- sys.dm_db_incremental_stats_properties_TSQL
- dm_db_incremental_stats_properties
- dm_db_incremental_stats_properties_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_incremental_stats_properties
ms.assetid: aa0db893-34d1-419c-b008-224852e71307
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7885e0ed338ad3691f821593b5ae8c74925297f4
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmdbincrementalstatsproperties-transact-sql"></a>sys.dm_db_incremental_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  返回当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中指定数据库对象（表）的增量统计信息属性。 使用 `sys.dm_db_incremental_stats_properties` （包含分区号）类似于 `sys.dm_db_stats_properties` （用于非增量统计信息）。 
  
  此函数在中引入[!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]Service Pack 2 和[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]Service Pack 1。
  
## <a name="syntax"></a>语法  
  
```  
sys.dm_db_incremental_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>参数  
 *object_id*  
 当前数据库中要请求其某个增量统计信息属性的对象的 ID。 *object_id* 是 **int**。  
  
 *stats_id*  
 指定 *object_id*的统计信息 ID。 可以从 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 动态管理视图获取该统计信息 ID。 *stats_id* 是 **int**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|要返回统计信息对象属性的对象（表）的 ID。|  
|stats_id|**int**|统计信息对象的 ID。 在表中是唯一的。 有关详细信息，请参阅 [sys.stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)。|
|partition_number|**int**|包含表的一部分的分区的编号。|  
|last_updated|**datetime2**|上次更新统计信息对象的日期和时间。 有关详细信息，请参阅[备注](#Remarks)在此页中的部分。|  
|rows|**bigint**|上次更新统计信息时表中的总行数。 如果筛选统计信息或者统计信息与筛选索引对应，该行数可能小于表中的行数。|  
|rows_sampled|**bigint**|用于统计信息计算的抽样总行数。|  
|步骤|**int**|直方图中的梯级数。 有关详细信息，请参阅 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。|  
|unfiltered_rows|**bigint**|应用筛选表达式（用于筛选的统计信息）之前表中的总行数。 如果未筛选统计信息，则 unfiltered_rows 等于行列中返回的值。|  
|modification_counter|**bigint**|自上次更新统计信息以来前导统计信息列（构建直方图的列）的总修改次数。<br /><br /> 此列不包含有关内存优化表的信息。|  
  
## <a name="Remarks"></a> 注释  
 `sys.dm_db_incremental_stats_properties` 在满足以下任一条件时将返回空的行集：  
  
-   `object_id` 或 `stats_id` 为 NULL。   
-   指定的对象未找到或不对应于具有增量统计信息的某个表。  
-   指定的统计信息 ID 不对应于指定对象 ID 的现有统计信息。  
-   当前用户没有权限查看统计信息对象。
 
 此行为在如 `sys.dm_db_incremental_stats_properties` 和 `sys.objects` 等视图中交叉应用于行时，允许安全使用 `sys.stats`。 此方法可返回对应于每个分区的统计信息的属性。 若要查看跨所有分区组合的合并统计信息的属性，请改为使用 sys.dm_db_stats_properties。 

统计信息更新日期存储在[统计信息 blob 对象](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)连同[直方图](../../relational-databases/statistics/statistics.md#histogram)和[密度向量](../../relational-databases/statistics/statistics.md#density)，而不是在元数据。 不读取任何数据以生成统计信息数据时, 未创建统计信息 blob，日期不可用，和*last_updated*列为 NULL。 这种情况的谓词不返回任何行，或为新的空表的筛选统计信息。

## <a name="permissions"></a>权限  
 要求用户对统计信息列拥有 select 权限，或用户拥有表，或用户是 `sysadmin` 固定服务器角色、`db_owner` 固定数据库角色或 `db_ddladmin` 固定数据库角色的成员。  
  
## <a name="examples"></a>示例  

### <a name="a-simple-example"></a>A. 简单示例
下面的示例将返回 `PartitionTable` 创建已分区表和已分区索引 [主题中所述的](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)表的统计信息。

```sql
SELECT * FROM sys.dm_db_incremental_stats_properties (object_id('PartitionTable'), 1);
``` 

有关其他使用建议，请参阅  [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)。
  
## <a name="see-also"></a>另请参阅  
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [与对象相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
