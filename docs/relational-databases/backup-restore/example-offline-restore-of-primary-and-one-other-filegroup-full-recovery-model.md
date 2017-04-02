---
title: "示例：主文件组和一个其他文件组的脱机还原（完整恢复模式） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "完整恢复模式 [SQL Server], RESTORE 示例"
  - "脱机还原 [SQL Server]"
  - "还原顺序 [SQL Server], 脱机"
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
caps.latest.revision: 32
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 32
---
# 示例：主文件组和一个其他文件组的脱机还原（完整恢复模式）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题仅与完整恢复模式下包含多个文件组的数据库有关。  
  
 在此示例中，名为 `adb` 的数据库包含三个文件组。 文件组 `A` 和 `C` 是可读/写的，文件组 `B` 是只读的。 主文件组和文件组 `B` 受损，但文件组 `A` 和 `C` 完好无损。 发生灾难性事件前所有文件组都处于联机状态。  
  
 数据库管理员决定还原和恢复主文件组及文件组 `B`。 该数据库使用完整恢复模式，因此，开始进行还原之前必须先获取数据库的结尾日志备份。 数据库变为联机后，文件组 `A` 和 `C` 将自动变为联机状态。  
  
> [!NOTE]  
>  只读文件的脱机还原顺序的步骤比联机还原要少。 有关示例，请参阅[示例：只读文件的联机还原（完整恢复模式）](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)。 但是，整个数据库在执行还原顺序期间处于脱机状态。  
  
## 结尾日志备份  
 在还原数据库之前，数据库管理员必须备份日志尾部。 由于数据库已损坏，因此创建结尾日志备份需要使用 NO_TRUNCATE 选项：  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 结尾日志备份是在以下还原顺序中应用的最后一个备份。  
  
## 还原顺序  
 若要还原主文件组和文件组 `B`，数据库管理员可使用不带 PARTIAL 选项的还原顺序，如下所示：  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 未还原的文件将自动变为联机状态。 此时，所有文件组都处于联机状态。  
  
## 另请参阅  
 [联机还原 (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [文件还原（完整恢复模式）](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  