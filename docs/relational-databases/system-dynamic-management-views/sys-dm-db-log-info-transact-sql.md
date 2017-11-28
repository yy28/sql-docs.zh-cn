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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回`VLF`事务日志文件的信息。 （所有日志文件将都合并表输出中）。 在输出中的每一行都表示`VLF`事务日志中，并提供与该 VLF 在日志中相关的信息。

## <a name="syntax"></a>语法  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>参数  
 *database_id* |NULL |默认值  
 是数据库的 ID。 *database_id*是**int**。有效输入包括数据库、 NULL 或默认的 ID 号。 默认值为 NULL。 NULL 和 DEFAULT 是当前数据库的上下文中的等效值。
 
 指定 NULL 可返回`VLF`当前数据库的信息。

 内置函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 如果在不指定数据库名称的情况下使用 DB_ID，则当前数据库的兼容级别必须是 90 或更高。  

## <a name="table-returned"></a>返回的表  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|数据库 ID。|
|file_id|**int**|事务日志的文件 id。|  
|vlf_begin_offset|**bigint** |位置的偏移`VLF`从事务日志文件的开头。|
|vlf_size_mb |**float** |`VLF`以 mb 为单位的大小舍入为 2 个小数位数。|     
|vlf_sequence_number|**bigint** |`VLF`按创建顺序的序列号。 用于唯一标识`VLFs`日志文件中。|
|vlf_active|**bit** |指示 VLF 是否正在使用或不。 <br />0-vlf 不在使用中。<br />1-`VLF`处于活动状态。|
|vlf_status|**int** |状态`VLF`。 可能的值包括 <br />0-`VLF`处于非活动状态 <br />1-vlf 已初始化但未使用 <br /> 2-`VLF`处于活动状态。|
|vlf_parity|**tinyint** |奇偶校验的`VLF`。在内部用于确定在日志的结尾`VLF`。|
|vlf_first_lsn|**nvarchar(48)** |中的第一个日志记录的 LSN `VLF`。|
|vlf_create_lsn|**nvarchar(48)** |LSN 的日志记录创建`VLF`。|

## <a name="remarks"></a>注释
 `sys.dm_db_log_info`动态管理函数将替换`DBCC LOGINFO`语句。 
 
## <a name="permissions"></a>Permissions  
 需要`VIEW DATABASE STATE`数据库中的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 确定数据库中具有大量的 SQL Server 实例`VLFs`
以下查询确定了大于 100 的数据库`VLFs`在日志文件中，这可能会影响数据库启动、 还原和恢复时间。

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 最后一个状态正在判定`VLF`之前收缩日志文件的事务日志中

可以使用以下查询来确定上次状态`VLF`之前对事务日志以确定是否可以收缩事务日志运行 shrinkfile。

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



