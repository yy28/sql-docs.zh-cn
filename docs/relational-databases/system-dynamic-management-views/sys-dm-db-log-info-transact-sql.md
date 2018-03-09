---
title: "sys.dm_db_log_info (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 661647715d2fcff3a4821250dfaa65e0fea07d6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回[虚拟日志文件 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的事务日志的信息。 请注意所有事务日志文件都组合表输出中。 输出中的每一行表示事务日志中的 VLF，并提供与该 VLF 在日志中相关的信息。

## <a name="syntax"></a>语法  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>参数  
 *database_id* |NULL |默认值  
 是数据库的 ID。 *database_id*是**int**。有效输入包括数据库、 NULL 或默认的 ID 号。 默认值为 NULL。 NULL 和 DEFAULT 是当前数据库的上下文中的等效值。
 
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

## <a name="remarks"></a>Remarks
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

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 最后一个状态正在判定`VLF`之前收缩日志文件的事务日志中

以下查询可以用于确定在对事务日志以确定是否可以收缩事务日志运行 shrinkfile 之前的最后一个 VLF 的状态。

```sql
USE AdventureWorks2016
GO

SELECT TOP 1 DB_NAME(database_id) AS "Database Name", file_id, vlf_size_mb, vlf_sequence_number, vlf_active, vlf_status
FROM sys.dm_db_log_info(DEFAULT)
ORDER BY vlf_sequence_number DESC
```


## <a name="see-also"></a>另请参阅  
[动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

