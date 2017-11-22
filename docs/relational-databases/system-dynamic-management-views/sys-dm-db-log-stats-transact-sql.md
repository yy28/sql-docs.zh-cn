---
title: "sys.dm_db_log_stats (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_stats dynamic management function
ms.assetid: 
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba933bad47beead99ea5f645a910b1783caa280e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (TRANSACT-SQL)   
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回上的数据库的事务日志文件的摘要级别的特性和信息。 此信息用于监视和诊断的事务日志运行状况。   
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>参数  

*database_id* |NULL |**默认**

是数据库的 ID。 `database_id` 为 `int`。 有效输入包括数据库的 ID 号`NULL`，或`DEFAULT`。 默认值为 `NULL`。 `NULL`和`DEFAULT`是当前数据库的上下文中的等效值。  
内置函数`DB_ID`可以指定。 使用时`DB_ID`不指定数据库名称，当前数据库的兼容性级别必须是 90 或更高版本。

  
## <a name="tables-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |数据库 ID |  
|recovery_model |**nvarchar(60)**   |   数据库恢复模式。 可能的值包括： <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   事务日志中的当前开始 LSN。 |  
|log_end_lsn    |**nvarchar(24)**   |   事务日志中的最后一个日志记录的 LSN。 |  
|current_vlf_sequence_number    |**bigint** |   当前 VLF 序列号时执行。 |  
|current_vlf_size_mb    |**float**  |   以 mb 为单位的当前 VLF 大小。 |   
|total_vlf_count    |**bigint** |   Vlf 的事务日志中的总数。 |  
|total_log_size_mb  |**float**  |   以 mb 为单位的总事务日志大小。 |  
|active_vlf_count   |**bigint** |   事务日志中的活动 Vlf 的总数。 |  
|active_log_size_mb |**float**  |   以 mb 为单位的总活动事务日志大小。 |  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   日志截断暂留原因。 值是与相同`log_reuse_wait_desc`列`sys.databases`。  (有关更多详细介绍这些值，请参阅[事务日志](../../relational-databases/logs/the-transaction-log-sql-server.md))。 <br />可能的值包括： <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />Replication<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />其他暂时性 |  
|log_backup_time    |**datetime**   |   最后一个事务日志备份时间。 |   
|log_backup_lsn |**nvarchar(24)**   |   最后一个事务日志备份 LSN。 |   
|log_since_last_log_backup_mb   |**float**  |   自上次事务日志备份 LSN 日志大小 （mb）。 |  
|log_checkpoint_lsn |**nvarchar(24)**   |   最后一个检查点 LSN。 |  
|log_since_last_checkpoint_mb   |**float**  |   由于最后一个检查点 LSN 日志大小 （mb）。 |  
|log_recovery_lsn   |**nvarchar(24)**   |   恢复 LSN 的数据库。 如果`log_recovery_lsn`发生之前检查点 LSN，`log_recovery_lsn`是最早的活动事务 LSN，否则`log_recovery_lsn`是检查点 LSN。 |  
|log_recovery_size_mb   |**float**  |   由于日志恢复 LSN 日志大小 （mb）。 |  
|recovery_vlf_count |**bigint** |   Vlf 要恢复，如果没有故障转移或服务器重新启动的总数。 |  


## <a name="permissions"></a>Permissions  
需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="examples"></a>示例  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. 确定数据库中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有大量 vlf 实例   
下面的查询返回了超过 100 个 vlf 的数据库日志文件中。 大量 Vlf 可能会影响数据库启动、 还原和恢复时间。

``` t-sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. 确定数据库中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与超过 4 小时的事务日志备份的实例   
以下查询确定实例中数据库的最后一个日志备份时间。

``` t-sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>另请参阅  
[动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  

  
