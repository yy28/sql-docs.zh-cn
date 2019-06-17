---
title: sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50549b10793346331d2e5cb8668243db615a443b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719506"
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返回[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)事务日志的信息。 请注意在表输出中合并所有事务日志文件。 输出中的每一行表示 VLF 中的事务日志，并提供与该 VLF 日志中相关的信息。

## <a name="syntax"></a>语法  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>参数  
 *database_id* |NULL |默认值  
 是数据库的 ID。 database_id 的数据类型为 int   。有效输入包括数据库、 NULL 或默认的 ID 号。 默认值为 NULL。 NULL 和 DEFAULT 是当前数据库的上下文中的等效值。
 
 指定 NULL 可返回当前数据库的 VLF 信息。

 内置函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 当使用`DB_ID`而无需指定数据库名称，在当前数据库的兼容性级别必须为 90 或更高版本。  

## <a name="table-returned"></a>返回的表  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|数据库 ID。|
|file_id|**smallint**|事务日志的文件 id。|  
|vlf_begin_offset|**bigint** |位置的偏移[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)从事务日志文件的开头。|
|vlf_size_mb |**float** |[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小以 mb 为单位，舍入为 2 个小数位。|     
|vlf_sequence_number|**bigint** |[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)序列中创建的订单号。 用于唯一标识日志文件中的 Vlf。|
|vlf_active|**bit** |指示是否[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)或未正在使用。 <br />0-VLF 不是在使用中。<br />1-VLF 处于活动状态。|
|vlf_status|**int** |状态[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。 可能的值包括 <br />0-VLF 处于非活动状态 <br />1-VLF 是已初始化但未使用 <br /> 2-VLF 处于活动状态。|
|vlf_parity|**tinyint** |奇偶校验[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。在内部用于确定在 VLF 日志的结尾。|
|vlf_first_lsn|**nvarchar(48)** |[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)中的第一个日志记录[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_create_lsn|**nvarchar(48)** |[日志序列号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)创建的日志记录[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_encryptor_thumbprint|**varbinary(20)**| 适用范围：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]  <br><br> 显示 VLF 的加密程序的指纹使用加密 VLF[透明数据加密](../../relational-databases/security/encryption/transparent-data-encryption.md)，否则为 NULL。 |

## <a name="remarks"></a>备注
`sys.dm_db_log_info`动态管理函数将替换`DBCC LOGINFO`语句。    
 
## <a name="permissions"></a>权限  
需要`VIEW DATABASE STATE`数据库中的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 确定数据库中具有大量的 Vlf 的 SQL Server 实例
以下查询确定了超过 100 个 Vlf 的日志文件，这可能会影响数据库启动、 还原和恢复时间中的数据库。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 确定的最后一个位置`VLF`之前日志文件收缩事务日志中

下面的查询可以用于对事务日志以确定是否可以收缩事务日志运行 shrinkfile 之前确定最后一个活动的 VLF 的位置。

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

## <a name="see-also"></a>请参阅  
[动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

