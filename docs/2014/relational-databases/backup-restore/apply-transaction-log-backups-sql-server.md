---
title: 应用事务日志备份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7532f2a6f2c50f53e5af01c2cec979170b493147
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922929"
---
# <a name="apply-transaction-log-backups-sql-server"></a>应用事务日志备份 (SQL Server)
  本主题只与完整恢复模式或大容量日志恢复模式相关。  
  
 本主题介绍在还原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库过程中应用事务日志备份。  
  
 **本主题内容：**  
  
-   [还原事务日志备份的要求](#Requirements)  
  
-   [恢复和事务日志](#RecoveryAndTlogs)  
  
-   [使用日志备份还原到故障点](#PITrestore)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="Requirements"></a> 还原事务日志备份的要求  
 若要应用事务日志备份，必须满足下列要求：  
  
-   **为还原顺序准备足够的日志备份：** 必须备份足够的日志记录，才能完成还原顺序。 必要的日志备份（需要时包含 [结尾日志备份](tail-log-backups-sql-server.md) ）必须在还原顺序开始之前可用。  
  
-   **正确的还原顺序：** 必须先还原上一个完整数据库备份或差异数据库备份。 然后，在完整数据库备份或差异数据库备份后创建的所有事务日志必须按时间顺序还原。 如果此事务日志链中的事务日志备份丢失或损坏，则您只能还原丢失的事务日志之前的事务日志。  
  
-   **数据库尚未恢复：** 除非已应用最后的事务日志，否则无法恢复数据库。 如果要在还原其中一个中间事务日志备份之后恢复数据库，则在日志链结束之前，除非从完整数据库备份开始重新启动整个还原顺序，否则，将无法还原该点之前的数据库。  
  
    > [!TIP]  
    >  最佳方法是还原所有日志备份 (RESTORE LOG *database_name* WITH NORECOVERY)。 还原上一次日志备份后，用单独的操作恢复数据库 (RESTORE DATABASE *database_name* WITH RECOVERY)。  
  
##  <a name="RecoveryAndTlogs"></a> 恢复和事务日志  
 当您完成还原操作并恢复数据库后，恢复将回滚所有未完成的事务。 此步骤称为“撤消阶段” 。 回滚对还原数据库的完整性是必需的。 回滚后，数据库将进入联机状态，不能再将其他事务日志备份应用到数据库。  
  
 例如，一系列事务日志备份包含一个运行时间长的事务。 该事务的起点记录在第一个事务日志备份中，终点记录在第二个事务日志备份中。 第一个事务日志备份中没有任何关于提交或回滚操作的记录。 如果在应用第一个事务日志备份后运行恢复操作，则运行时间长的事务被视为未完成，并且将回滚事务的第一个事务日志备份中记录的数据修改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许在此点后应用第二个事务日志备份。  
  
> [!NOTE]  
>  某些情况下可以在日志还原期间显式添加文件。  
  
##  <a name="PITrestore"></a> 使用日志备份还原到故障点  
 假设有下列事件顺序。  
  
|Time|Event|  
|----------|-----------|  
|上午 8:00|备份数据库以创建完整数据库备份。|  
|中午|备份事务日志。|  
|下午 4:00|备份事务日志。|  
|下午 6:00|备份数据库以创建完整数据库备份。|  
|晚上 8:00|备份事务日志。|  
|晚上 9:45|出现故障。|  
  
> [!NOTE]  
>  有关此示例备份顺序的说明，请参阅[事务日志备份 (SQL Server)](transaction-log-backups-sql-server.md)。  
  
 若要将数据库还原到晚上 9:45（故障点）时的状态， 可以使用以下两种备选过程：  
  
 **替换选项 1：使用最新的完整数据库备份还原数据库**  
  
1.  失败时创建当前活动事务日志的结尾日志备份。  
  
2.  不要还原上午 8:00 的 所需的时间长。 相反，应还原下午 6:00 的 这一时间更近的完整数据库备份，然后应用晚上 8:00 的 日志备份和结尾日志备份。  
  
 **替换选项 2：使用较早的完整数据库备份还原数据库**  
  
> [!NOTE]  
>  如果出现问题，使您无法使用下午 6:00 的完整数据库备份， 所需的时间长。 此过程比从下午 6:00 的完整数据库备份还原 所需的时间长。  
  
1.  失败时创建当前活动事务日志的结尾日志备份。  
  
2.  还原上午 8:00 的 完整数据库备份，然后按顺序还原所有四个事务日志备份。 所有完成的事务都将前滚到晚上 9:45。  
  
     此备选过程指出了冗余安全性，该安全性通过维护一系列完整数据库备份中的事务日志链备份来获得。  
  
> [!NOTE]  
>  某些情况下，您还可以使用事务日志将数据库还原到特定的时间点。 有关详细信息，请参阅 [将 SQL Server 数据库还原到某个时间点（完整恢复模式）](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **应用事务日志备份**  
  
-   [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
 **还原到恢复点**  
  
-   [在完整恢复模式下将数据库还原到故障点 (Transact-SQL)](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [将 SQL Server 数据库还原到某个时间点（完整恢复模式）](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [包含标记的事务的相关数据库的恢复](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [恢复到日志序列号 (SQL Server)](recover-to-a-log-sequence-number-sql-server.md)  
  
 **使用 WITH NORECOVERY 在还原备份后恢复数据库**  
  
-   [恢复数据库但不还原数据 (Transact-SQL)](recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>请参阅  
 [事务日志 (SQL Server)](../logs/the-transaction-log-sql-server.md)  
  
  
