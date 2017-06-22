---
title: "示例：数据库的段落还原（完整恢复模式）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5a939ad4e9e5313961f681c06f896a9f53a906e8
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>示例：数据库的段落还原（完整恢复模式）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  段落还原顺序将从主文件组及所有具有读写权限的辅助文件组开始，在文件组级别分阶段还原和恢复数据库。  
  
 在此示例中，灾难发生后，数据库 `adb` 被还原到新计算机。 该数据库使用完整恢复模式，因此，开始进行还原之前必须先获取数据库的结尾日志备份。 灾难发生之前，所有文件组均处于联机状态。 文件组 `B` 是只读的。 必须还原所有辅助文件组，但这些辅助文件组将按重要性顺序进行还原： `A` （最高）， `C`其次，最后为 `B`。 在此示例中，存在四个日志备份，其中包括结尾日志备份。  
  
## <a name="tail-log-backup"></a>结尾日志备份  
 在还原数据库之前，数据库管理员必须备份日志尾部。 由于数据库已损坏，因此创建结尾日志备份需要使用 NO_TRUNCATE 选项：  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 结尾日志备份是在以下还原顺序中应用的最后一个备份。  
  
## <a name="restore-sequences"></a>还原顺序  
  
> [!NOTE]  
>  联机还原顺序的语法与脱机还原顺序的语法完全相同。  
  
1.  部分还原主文件组和辅助文件组 `A`。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  对文件组 `C`进行联机还原。  
  
     此时，主文件组和辅助文件组 `A` 处于联机状态。 文件组 `B` 和 `C` 中的所有文件都处于恢复挂起状态，这两个文件组处于脱机状态。  
  
     来自步骤 1 中的最后一条 `RESTORE LOG` 语句的消息指出：由于文件组 `C` 不可用，因此涉及此文件组的事务回滚已延迟。 可继续执行常规操作，但这些事务将持有锁并且在完成回滚前不会截断日志。  
  
     在第二个还原顺序中，数据库管理员将还原文件组 `C`：  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     此时，主文件组和文件组 `A` 以及 `C` 处于联机状态。 文件组 `B` 中的文件仍保持恢复挂起状态，而该文件组处于脱机状态。 解析延迟的事务后，日志被截断。  
  
3.  对文件组 `B`进行联机还原。  
  
     在第三个还原顺序中，数据库管理员将还原文件组 `B`。 文件组 `B` 的备份是在该文件组变为只读状态之后进行的，因此，在恢复过程中无需将其前滚。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
    ```  
  
     所有文件组现在都处于联机状态。  
  
## <a name="additional-examples"></a>其他示例  
  
-   [示例：数据库的段落还原（简单恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（简单恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [示例：只读文件的联机还原（简单恢复模式）](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（完整恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [示例：读/写文件的联机还原（完整恢复模式）](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [示例：只读文件的联机还原（完整恢复模式）](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [联机还原 (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)   
 [段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
