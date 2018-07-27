---
title: sys.dm_db_log_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: cf12e737a798e671797880667b5fb75930a85847
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278948"
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (TRANSACT-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返回上的数据库的事务日志文件摘要级别特性和信息。 使用此信息来监视和诊断的事务日志运行状况。   
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>参数  

*database_id* |NULL |**默认**

是数据库的 ID。 `database_id` 为 `int`。 有效输入包括数据库的 ID 号`NULL`，或`DEFAULT`。 默认值为 `NULL`。 `NULL` 和`DEFAULT`是当前数据库上下文中的等效值。  
内置函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 当使用`DB_ID`而无需指定数据库名称，在当前数据库的兼容性级别必须为 90 或更高版本。

  
## <a name="tables-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |数据库 ID |  
|recovery_model |**nvarchar(60)**   |   数据库的恢复模式。 可能的值包括： <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   当前开始[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)事务日志中。|  
|log_end_lsn    |**nvarchar(24)**   |   [日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的事务日志中的最后一个日志记录。|  
|current_vlf_sequence_number    |**bigint** |   当前[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)时执行的序列号。|  
|current_vlf_size_mb    |**float**  |   当前[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小以 mb 为单位。|   
|total_vlf_count    |**bigint** |   总数[虚拟日志文件 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)事务日志中。 |  
|total_log_size_mb  |**float**  |   总事务日志大小 （mb）。 |  
|active_vlf_count   |**bigint** |   活动的总数[虚拟日志文件 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)事务日志中。|  
|active_log_size_mb |**float**  |   总活动事务日志大小 （mb）。|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   日志截断暂留的原因。 值是与相同`log_reuse_wait_desc`列的`sys.databases`。  (有关更多详细说明这些值，请参阅[事务日志](../../relational-databases/logs/the-transaction-log-sql-server.md))。 <br />可能的值包括： <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replication<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />其他暂时 |  
|log_backup_time    |**datetime**   |   最后一个事务日志备份时间。|   
|log_backup_lsn |**nvarchar(24)**   |   最后一个事务日志备份[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|   
|log_since_last_log_backup_mb   |**float**  |   自上次事务日志备份后日志以 mb 为单位的大小[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_checkpoint_lsn |**nvarchar(24)**   |   最后一个检查点[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_since_last_checkpoint_mb   |**float**  |   自上一个检查点后日志以 mb 为单位的大小[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_recovery_lsn   |**nvarchar(24)**   |   恢复[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的数据库。 如果`log_recovery_lsn`之前检查点 LSN，发生`log_recovery_lsn`是最早活动事务 LSN，否则`log_recovery_lsn`是检查点 LSN。|  
|log_recovery_size_mb   |**float**  |   自日志恢复日志以 mb 为单位的大小[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|recovery_vlf_count |**bigint** |   总数[虚拟日志文件 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)恢复，如果没有故障转移或服务器重新启动。 |  


## <a name="remarks"></a>Remarks
运行时`sys.dm_db_log_stats`针对参与可用性组作为次要副本的数据库，将返回上面所述的字段的一个子集。  目前，仅`database_id`， `recovery_model`，和`log_backup_time`对辅助数据库运行时，会返回。   

## <a name="permissions"></a>Permissions  
需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="examples"></a>示例  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. 确定数据库中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有大量的 Vlf 实例   
下面的查询返回了超过 100 个 Vlf 的数据库日志文件中。 大量的 Vlf 会影响数据库启动、 还原和恢复时间。

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. 确定数据库中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用超过 4 小时的事务日志备份的实例   
以下查询确定最后一个实例中数据库的日志备份的时间。

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>请参阅  
[动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
