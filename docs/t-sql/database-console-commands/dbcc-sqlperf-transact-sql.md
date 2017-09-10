---
title: "DBCC SQLPERF (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f854ce5ff1261829df621931d3a736426f32c8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

提供所有数据库的事务日志空间使用情况统计信息。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]还可以用于重置等待和闩锁统计信息。
  
**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([在某些区域以预览版提供](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     |  
          [ "sys.dm_os_latch_stats" , CLEAR ]  
     |  
     [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
LOGSPACE  
返回事务日志的当前大小和用于每个数据库的日志空间的百分比。 可以使用此信息来监视事务日志中使用的空间量。  
  
**"** **sys.dm_os_latch_stats"，**清除  
重置闩锁统计信息。 有关详细信息，请参阅[sys.dm_os_latch_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). 此选项在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中不可用。  
  
**"sys.dm_os_wait_stats"**清除  
重置等待统计信息。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 此选项在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中不可用。  
  
WITH NO_INFOMSGS  
取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
 下表对结果集中的列进行了说明。  
  
|列名|定义|  
|---|---|
|**数据库名称**|数据库名称，为该数据库显示日志统计信息。|  
|**日志大小 (MB)**|分配给日志的当前大小。 该值始终小于最初为日志空间分配的量，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]会保留一小部分磁盘空间，用以存放内部标头信息。|  
|**使用日志空间 （%）**|当前正在使用，以存储事务日志信息的日志文件的百分比。|  
|**状态**|日志文件的状态。 始终为 0。|  
  
## <a name="remarks"></a>注释  
事务日志记录数据库中执行的每个事务。 有关详细信息请参阅[事务日志 &#40;SQL server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要运行 DBCC SQLPERF(LOGSPACE) 需要服务器上的 VIEW SERVER STATE 权限。 若要重置等待和闩锁统计信息，需要在服务器上拥有 ALTER SERVER STATE 权限。
  
上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要 VIEW DATABASE STATE 权限的数据库中。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。 不支持重置等待和闩锁统计信息。
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. 显示所有数据库的日志空间信息  
下面的示例显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中包含的所有数据库的 `LOGSPACE` 信息。
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
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
[sp_spaceused &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
  
  


