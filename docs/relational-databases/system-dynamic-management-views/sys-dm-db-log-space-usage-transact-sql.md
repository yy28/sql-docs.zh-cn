---
title: sys. dm_db_log_space_usage （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bfa102163012456e9b2660d26cb54dec3d58cfbb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264583"
---
# <a name="sysdm_db_log_space_usage-transact-sql"></a>sys. dm_db_log_space_usage （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回事务日志的空间使用情况信息。 
  
> [!NOTE]
> 所有事务日志文件都是组合的。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|数据库 ID。|  
|total_log_size_in_bytes |**bigint** |日志的大小  |
|used_log_space_in_bytes |**bigint** |日志的占用大小  |     
|used_log_space_in_percent |**实际上** |日志大小占总日志大小的百分比 |
|log_space_in_bytes_since_last_backup |**bigint** |自上次日志备份后使用的空间量 <br />**适用范围：** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)]到[!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。|
    
  
## <a name="permissions"></a>权限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要`VIEW DATABASE STATE`具有数据库中的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
  
## <a name="examples"></a>示例  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. 确定 tempdb 中的可用日志空间量   
下面的查询返回 tempdb 中可用的总可用日志空间（MB）。

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>另请参阅  
[动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys. dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[sys. dm_db_task_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys. dm_db_session_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys. dm_db_log_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys. dm_db_log_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



