---
title: "事务日志备份 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b7bad833291d3ad6b61cb4fac99334284404b97f
ms.lasthandoff: 04/11/2017

---
# <a name="transaction-log-backups-sql-server"></a>事务日志备份 (SQL Server)
  本主题仅与使用完整恢复模式或大容量日志恢复模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库相关。 本主题讨论备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的事务日志。  
  
 在创建任何日志备份之前，您必须至少创建一个完整备份。 然后，可以随时备份事务日志，除非已备份此日志。 
 
建议经常执行日志备份，这样既可尽量减少丢失工作的风险，也可以截断事务日志。 
 
数据库管理员通常偶尔（如每周）会创建完整数据库备份，还可以选择以较短间隔（如每天）创建一系列差异备份。 与数据库备份无关，数据库管理员可以比较频繁地（例如每隔 10 分钟）创建事务日志备份。 对于给定的备份类型，最恰当的备份间隔取决于一系列因素，如数据的重要性、数据库的大小和服务器的工作负荷。  
   
##  <a name="LogBackupSequence"></a> 日志备份顺序的工作方式  
 事务日志备份“日志链”  的序列与数据备份无关。 例如，假设有下列事件顺序。  
  
|Time|事件|  
|----------|-----------|  
|上午 8:00|备份数据库。|  
|中午|备份事务日志。|  
|下午 4:00|备份事务日志。|  
|下午 6:00|备份数据库。|  
|晚上 8:00|备份事务日志。|  
  
 在下午 8:00 创建的事务日志备份 包含从下午 4:00 到下午 8:00 的事务日志记录， 跨越创建完整数据库备份的时间点（下午 6:00）。 事务日志备份序列是连续的，从创建初始完整数据库备份的时间（上午 8:00） 到创建最后事务日志备份的时间（下午 8:00）。 有关如何应用这些日志备份的信息，请参阅 [应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).中的示例。  
  
##  <a name="Recommendations"></a> 建议  
  
-   如果事务日志损坏，则最新有效备份以后执行的工作将丢失。 因此，我们强烈建议您将日志文件存储在容错的存储设备中。  
  
-   如果数据库已损坏，或者你要还原数据库，建议你创建一个 [结尾日志备份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) ，使你可以将数据库还原到当前时间点。  
  
-   默认情况下，每个成功的备份操作都会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和系统事件日志中添加一个条目。 如果非常频繁地备份日志，这些成功消息会迅速累积，从而产生一个巨大的错误日志，这样会使查找其他消息变得非常困难。 在这些情况下，如果任何脚本均不依赖于这些日志条目，则可以使用跟踪标志 3226 取消这些条目。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **创建事务日志备份**  
  
-   [备份事务日志 (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 若要计划备份作业，请参阅 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  

## <a name="see-also"></a>另请参阅  
 [事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [结尾日志备份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  

