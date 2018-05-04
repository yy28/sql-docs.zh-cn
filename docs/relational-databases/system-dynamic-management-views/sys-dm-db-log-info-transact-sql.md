---
title: sys.dm_db_log_info (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 04/24/2018
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
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: 4
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e791e9d48e6dad1ab3514caa1d1faa0fb3c259a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返回[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的事务日志的信息。 请注意所有事务日志文件都组合表输出中。 输出中的每一行表示事务日志中的 VLF，并提供与该 VLF 在日志中相关的信息。

## <a name="syntax"></a>语法  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>参数  
 *database_id* |NULL |默认值  
 是数据库的 ID。 database_id 的数据类型为 int。有效输入包括数据库、 NULL 或默认的 ID 号。 默认值为 NULL。 NULL 和 DEFAULT 是当前数据库的上下文中的等效值。
 
 指定 NULL 可返回当前数据库的 VLF 信息。

 内置函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 使用时`DB_ID`不指定数据库名称，当前数据库的兼容性级别必须是 90 或更高版本。  

## <a name="table-returned"></a>返回的表  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|数据库 ID。|
|file_id|**int**|事务日志的文件 id。|  
|vlf_begin_offset|**bigint** |位置的偏移[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)从事务日志文件的开头。|
|vlf_size_mb |**float** |[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小以 mb 为单位，舍入为 2 个小数位数。|     
|vlf_sequence_number|**bigint** |[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)序列号按创建顺序。 用于唯一标识 Vlf 日志文件中。|
|vlf_active|**bit** |指示是否[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)或未正在使用。 <br />0-VLF 不在使用中。<br />1-VLF 处于活动状态。|
|vlf_status|**int** |状态[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。 可能的值包括 <br />0-VLF 处于非活动状态 <br />1-VLF 已初始化但未使用 <br /> 2-VLF 处于活动状态。|
|vlf_parity|**tinyint** |奇偶校验的[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。在内部用于确定在 VLF 的日志的结尾。|
|vlf_first_lsn|**nvarchar(48)** |[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)中的第一个日志记录的[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_create_lsn|**nvarchar(48)** |[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的日志记录创建[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|

## <a name="remarks"></a>注释
`sys.dm_db_log_info`动态管理函数将替换`DBCC LOGINFO`语句。    
 
## <a name="permissions"></a>权限  
需要`VIEW DATABASE STATE`数据库中的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 确定数据库中具有大量 Vlf 的 SQL Server 实例
以下查询确定了 100 个以上 Vlf 的日志文件，这可能会影响数据库启动、 还原和恢复时间中的数据库。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 正在判定的最后一个位置`VLF`之前收缩日志文件的事务日志中

以下查询可以用于确定在对事务日志以确定是否可以收缩事务日志运行 shrinkfile 之前的最后一个活动 VLF 的位置。

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>另请参阅  
[动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

