---
title: 解决事务日志已满的问题（SQL Server 错误 9002）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 54
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b3fa89db4f8fb95ca1f2e912c6ee1d131808f42
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254029"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>解决事务日志已满的问题（SQL Server 错误 9002）
  本主题讨论对已满事务日志可以采取的几种应对措施，并就以后如何避免出现已满事务日志给出建议。 如果事务日志已满，则 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]会发出 9002 错误。 当数据库联机或恢复时，日志可能会满。 如果数据库联机时日志已满，则数据库保持联机状态，但是只能进行读取而不能更新。 如果恢复过程中日志已满，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将数据库标记为 RESOURCE PENDING。 不管哪种情况，都需要用户执行操作才能使日志空间可用。  
  
## <a name="responding-to-a-full-transaction-log"></a>应对已满事务日志  
 正确响应已满事务日志在某种程度上取决于导致日志已满的情况。 若要在给定情况下查找阻止日志截断的原因，请使用 **sys.database** 目录视图的 **log_reuse_wait** 列和 **log_reuse_wait_desc** 列。 有关详细信息，请参阅 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)。 有关延迟日志截断的因素的说明，请参阅[事务日志 (SQL Server)](the-transaction-log-sql-server.md)。  
  
> [!IMPORTANT]  
>  如果数据库在恢复过程中出现 9002 错误，在解决问题后恢复数据库使用 ALTER DATABASE *database_name*将设置为联机。  
  
 响应已满事务日志的备选方法包括：  
  
-   备份日志。  
  
-   释放磁盘空间以便日志可以自动增长。  
  
-   将日志文件移到具有足够空间的磁盘驱动器。  
  
-   增加日志文件的大小。  
  
-   在其他磁盘上添加日志文件。  
  
-   完成或取消长时间运行的事务。  
  
 下列部分介绍了这些备选方法。 请选择最适用于您情况的响应。  
  
### <a name="backing-up-the-log"></a>备份日志  
 在完整恢复模式或大容量日志恢复模式下，如果最近尚未备份事务日志，则请立即进行备份以免发生日志截断。 如果从未备份日志，则必须创建两个日志备份，以允许[!INCLUDE[ssDE](../../includes/ssde-md.md)]将日志截断到上次的备份点。 截断日志可释放空间以供新的日志记录使用。 若要防止日志再次填满，请经常执行日志备份。  
  
 **创建事务日志备份**  
  
> [!IMPORTANT]  
>  如果数据库已损坏，请参阅[结尾日志备份 (SQL Server)](../backup-restore/tail-log-backups-sql-server.md)。  
  
-   [备份事务日志 (SQL Server)](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>释放磁盘空间  
 您可以通过删除或移动其他文件的方法来释放包含数据库事务日志文件的磁盘驱动器上的磁盘空间。 释放磁盘空间后，恢复系统将自动扩大日志文件。  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>将日志文件移至其他磁盘  
 如果在当前包含日志文件的驱动器上无法释放足够的磁盘空间，请考虑将该文件移至空间充足的其他驱动器上。  
  
> [!IMPORTANT]  
>  日志文件决不要放在压缩文件系统中。  
  
 **若要移动日志文件**  
  
-   [移动数据库文件](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>增加日志文件的大小  
 如果日志磁盘上具有可用空间，则可以增加日志文件的大小。 日志文件的最大大小是每个日志文件 2 TB。  
  
 **若要增加文件大小**  
  
 如果禁用自动增长，数据库处于联机状态，并且磁盘上有足够的可用空间，则可采用以下方法之一：  
  
-   手动增加文件大小以生成单个增量。  
  
-   使用 ALTER DATABASE 语句启用自动增长以针对 FILEGROWTH 选项设置非零增量。  
  
> [!NOTE]  
>  不管哪种情况，如果已达到当前大小限制，则应增加 MAXSIZE 值。  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>在其他磁盘上添加日志文件  
 使用 ALTER DATABASE <database_name> ADD LOG FILE，向具有足够空间的其他磁盘上的数据库中添加新日志文件。  
  
 **添加日志文件**  
  
-   [向数据库中添加数据文件或日志文件](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [管理事务日志文件的大小](manage-the-size-of-the-transaction-log-file.md)   
 [事务日志备份 (SQL Server)](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
