---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: fe8d7ae38915a335276e661e3ce5f28c61b9a40e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710995"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

提供所有数据库的事务日志空间使用情况统计信息。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中还可用于重置等待和闩锁统计信息。
  
适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]（[在某些区域以预览版提供](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)）
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
LOGSPACE  
返回事务日志的当前大小和用于每个数据库的日志空间的百分比。 使用此信息来监视事务日志中使用的空间量。

> [!IMPORTANT]
> 有关从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始的事务日志的空间使用情况的详细信息，请参阅本主题的[备注](#Remarks)部分。
  
**"sys.dm_os_latch_stats"**, CLEAR  
重置闩锁统计信息。 有关详细信息，请参阅 [sys.dm_os_latch_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)。 此选项在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中不可用。  
  
**"sys.dm_os_wait_stats"**, CLEAR  
重置等待统计信息。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 此选项在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中不可用。  
  
WITH NO_INFOMSGS  
取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
 下表对结果集中的列进行了说明。  
  
|列名|定义|  
|---|---|
|**Database Name**|数据库名称，为该数据库显示日志统计信息。|  
|**日志大小 (MB)**|分配给日志的当前大小。 该值始终小于最初为日志空间分配的量，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]会保留一小部分磁盘空间，用以存放内部标头信息。|  
|**已用日志空间 (%)**|当前用于存储事务日志信息的日志文件的百分比。|  
|**“状态”**|日志文件的状态。 始终为 0。|  
  
## <a name="Remarks"></a> 注释  
从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，使用 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV 而不是 `DBCC SQLPERF(LOGSPACE)` 来返回每个数据库事务日志的空间使用情况信息。    
 
事务日志记录数据库中执行的每个事务。 有关详细信息，请参阅[事务日志 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 和 [SQL Server 事务日志体系结构和管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)。
  
## <a name="permissions"></a>Permissions  
对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，运行 `DBCC SQLPERF(LOGSPACE)` 需要对服务器的 `VIEW SERVER STATE` 权限。 重置等待和闩锁统计信息需要对服务器的 `ALTER SERVER STATE` 权限。
  
对于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 高级层和业务关键层，需要数据库的 `VIEW DATABASE STATE` 权限。 对于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 标准层、基本层和常规用途层，需要 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 管理员帐户。 不支持重置等待和闩锁统计信息。
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. 显示所有数据库的日志空间信息  
下面的示例显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中包含的所有数据库的 `LOGSPACE` 信息。
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. 重置等待统计信息  
以下示例为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重置等待统计信息。
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

