---
title: 解决事务日志已满的问题（SQL Server 错误 9002）| Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f809f65be52e77e84e1391df0151cc183013624
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656505"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>解决事务日志已满的问题（SQL Server 错误 9002）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题讨论对已满事务日志可以采取的几种应对措施，并就以后如何避免出现已满事务日志给出建议。 
  
  如果事务日志已满，则 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会发出 **9002 错误**。 当数据库联机或恢复时，日志可能会满。 如果数据库联机时日志已满，则数据库保持联机状态，但是只能进行读取而不能更新。 如果恢复过程中日志已满，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将数据库标记为 RESOURCE PENDING。 不管哪种情况，都需要用户执行操作才能使日志空间可用。  
  
## <a name="responding-to-a-full-transaction-log"></a>对已满事务日志的响应  
 正确响应已满事务日志在某种程度上取决于导致日志已满的情况。 
 
 若要在给定情况下查找阻止日志截断的原因，请使用 **sys.database** 目录视图的 **log_reuse_wait** 列和 **log_reuse_wait_desc** 列。 有关详细信息，请参阅 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。 有关延迟日志截断的因素的说明，请参阅[事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
> **重要说明!!**  
>  如果数据库在恢复过程中出现 9002 错误，则在解决此问题后，可使用 [ALTER DATABASE *database_name* SET ONLINE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 恢复数据库。  
  
 响应已满事务日志的备选方法包括：  
  
-   备份日志。  
  
-   释放磁盘空间以便日志可以自动增长。  
  
-   将日志文件移到具有足够空间的磁盘驱动器。  
  
-   增加日志文件的大小。  
  
-   在其他磁盘上添加日志文件。  
  
-   完成或取消长时间运行的事务。  
  
 下列部分介绍了这些备选方法。 请选择最适用于您情况的响应。  
  
## <a name="back-up-the-log"></a>备份日志  
 在完整恢复模式或大容量日志恢复模式下，如果最近尚未备份事务日志，则请立即进行备份以免发生日志截断。 如果从未备份日志，则 **必须创建两个日志备份** ，以允许 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将日志截断到上次的备份点。 截断日志可释放空间以供新的日志记录使用。 若要防止日志再次填满，请经常执行日志备份。  
  
 **创建事务日志备份**  
  
> **重要事项**  
>  如果数据库已损坏，请参阅[结尾日志备份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
-   [备份事务日志 (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>释放磁盘空间  
 您可以通过删除或移动其他文件的方法来释放包含数据库事务日志文件的磁盘驱动器上的磁盘空间。 释放磁盘空间后，恢复系统将自动扩大日志文件。  
  
### <a name="move-the-log-file-to-a-different-disk"></a>将日志文件移至其他磁盘  
 如果在当前包含日志文件的驱动器上无法释放足够的磁盘空间，请考虑将该文件移至空间充足的其他驱动器上。  
  
> **重要说明!!** 日志文件决不要放在压缩文件系统中。  
  
 **移动日志文件**  
  
-   [移动数据库文件](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>增加日志文件大小。  
 如果日志磁盘上具有可用空间，则可以增加日志文件的大小。 日志文件的最大大小是每个日志文件 2 TB。  
  
 **增加文件大小**  
  
 如果禁用自动增长，数据库处于联机状态，并且磁盘上有足够的可用空间，则可采用以下方法之一：  
  
-   手动增加文件大小以生成单个增量。  
  
-   使用 ALTER DATABASE 语句启用自动增长以针对 FILEGROWTH 选项设置非零增量。  
  
> **请注意** 不管哪种情况，如果已达到当前大小限制，则应增加 MAXSIZE 值。  
  
### <a name="add-a-log-file-on-a-different-disk"></a>在其他磁盘上添加日志文件  
 使用 ALTER DATABASE <database_name> ADD LOG FILE，向具有足够空间的其他磁盘上的数据库中添加新日志文件。  
  
 **添加日志文件**  
  
-   [向数据库中添加数据文件或日志文件](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>完成或终止长时间运行的事务
### <a name="discovering-long-running-transactions"></a>发现长时间运行的事务
很长时间运行的事务会导致事务日志填满。 若要查看长时间运行的事务，请使用下列方法之一：
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。**
此动态管理视图返回有关数据库级事务的信息。 对于长时间运行的事务，最需要注意的列包括：第一条日志记录的时间 [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)、事务的当前状态 [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)和事务日志中开始记录的 [日志序列号 (LSN)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)。**
通过此语句，您可以标识该事务所有者的用户 ID，因此可以隐性地跟踪该事务的源以得到更加有序的终止（将其提交而非回滚）。

### <a name="kill-a-transaction"></a>终止一个事务
有时只是需要结束进程；此时可能需要使用 [KILL](../../t-sql/language-elements/kill-transact-sql.md) 语句。 请谨慎使用此语句，特别是在运行不想终止的重要进程时。 有关详细信息，请参阅 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)

## <a name="see-also"></a>另请参阅  
[KB 支持文章 - A transaction log grows unexpectedly or becomes full in SQL Server](https://support.microsoft.com/en-us/kb/317375)（SQL Server 中的事务日志意外增大或已满）[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [管理事务日志文件的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [事务日志备份 (SQL Server)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
