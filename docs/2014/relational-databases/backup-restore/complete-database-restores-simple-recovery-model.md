---
title: 完整数据库还原（简单恢复模式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- complete database restores
- database restores [SQL Server], complete database
- restoring databases [SQL Server], complete database
- simple recovery model [SQL Server]
- restoring [SQL Server], database
ms.assetid: 49828927-1727-4d1d-9ef5-3de43f68c026
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e64bf4d4642d8091cd0892283a996e7dccc56e26
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877116"
---
# <a name="complete-database-restores-simple-recovery-model"></a>完整数据库还原（简单恢复模式）
  数据库完整还原的目的是还原整个数据库。 整个数据库在还原期间处于脱机状态。 在数据库的任何部分变为联机之前，必须将所有数据恢复到同一点，即数据库的所有部分都处于同一时间点并且不存在未提交的事务。  
  
 在简单恢复模式下，数据库不能还原到特定备份中的特定时间点。  
  
> [!IMPORTANT]  
>  建议您不要附加或还原来自未知或不可信源的数据库。 这些数据库可能包含执行非预期 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 代码的恶意代码，或通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。  
  

  
> [!NOTE]  
>  有关支持从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的早期版本进行备份的信息，请参阅 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)中的“兼容性支持”部分。  
  
##  <a name="Overview"></a> 在简单恢复模式下还原数据库的概述  
 简单恢复模式下的完整数据库还原只涉及一个或两个 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语句，具体取决于是否需要还原差异数据库备份。 如果只使用完整数据库备份，则只需还原最近的备份，如下图所示。  
  
 ![仅还原完整数据库备份](../../database-engine/media/bnrr-rmsimple1-fulldbbu.gif "仅还原完整数据库备份")  
  
 如果还使用差异数据库备份，则应还原最近的完整数据库备份而不恢复数据库，然后还原最近的差异数据库备份并恢复数据库。 下图显示了这一过程。  
  
 ![还原完整数据库备份和差异数据库备份](../../database-engine/media/bnrr-rmsimple2-diffdbbu.gif "还原完整数据库备份和差异数据库备份")  
  
> [!NOTE]  
>  如果你计划将数据库备份还原到其它服务器实例，请参阅 [通过备份和还原来复制数据库](../databases/copy-databases-with-backup-and-restore.md)。  
  
###  <a name="TsqlSyntax"></a> 基本 TRANSACT-SQL RESTORE 语法  
 用于还原完整数据库备份的基本 [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语法是：  
  
 RESTORE DATABASE *database_name* FROM *backup_device* [ WITH NORECOVERY ]  
  
> [!NOTE]  
>  如果还打算还原差异数据库备份，则应使用 WITH NORECOVERY。  
  
 用于还原数据库备份的 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语句的基本语法是：  
  
 RESTORE DATABASE *database_name* FROM *backup_device* WITH RECOVERY  
  
###  <a name="Example"></a> 示例 (Transact-SQL)  
 以下示例首先显示如何使用 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 语句来创建 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的完整数据库备份和差异数据库备份。 然后按顺序还原这些备份。 将数据库还原到完成差异数据库备份时的状态。  
  
 该示例说明数据库完整还原方案的还原序列中的关键选项。 *还原顺序* 由通过一个或多个还原阶段来移动数据的一个或多个还原操作组成。 将省略与此目的不相关的语法和详细信息。 在恢复数据库时，尽管 RECOVERY 选项是默认值，但为清楚起见，仍建议显式指定该选项。  
  
> [!NOTE]  
>  此示例以 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 语句开头，该语句将恢复模式设置为 `SIMPLE`。  
  
```  
USE master;  
--Make sure the database is using the simple recovery model.  
ALTER DATABASE AdventureWorks2012 SET RECOVERY SIMPLE;  
GO  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
  WITH FORMAT;  
GO  
--Create a differential database backup.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH DIFFERENTIAL;  
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=1, NORECOVERY;  
--Restore the differential backup (from backup set 2).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=2, RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **还原完整数据库备份**  
  
-   [在简单恢复模式下还原数据库备份 (Transact-SQL)](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [还原数据库备份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [将数据库还原到新位置 (SQL Server)](restore-a-database-to-a-new-location-sql-server.md)  
  
 **还原差异数据库备份**  
  
-   [还原差异数据库备份 (SQL Server)](restore-a-differential-database-backup-sql-server.md)  
  
 **使用 SQL Server 管理对象 (SMO) 还原备份**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  

  
## <a name="see-also"></a>请参阅  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [sp_addumpdevice (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [完整数据库备份 (SQL Server)](full-database-backups-sql-server.md)   
 [差异备份 (SQL Server)](differential-backups-sql-server.md)   
 [备份概述 (SQL Server)](backup-overview-sql-server.md)   
 [还原和恢复概述 (SQL Server)](restore-and-recovery-overview-sql-server.md)  
  
  
