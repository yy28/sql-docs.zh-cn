---
title: 示例：仅对某些文件组进行段落还原（完整恢复模式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b3cb1a5ea33a5016c99fdf1f5a7f4e892c045b59
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958140"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>示例：仅对某些文件组进行段落还原（完整恢复模式）
  本主题与完整恢复模式下包含多个文件或文件组的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库相关。  
  
 段落还原顺序将从主文件组和所有读写辅助文件组开始，按文件组级别分阶段还原和恢复数据库。  
  
 在此示例中，名为 `adb`的数据库（使用完整恢复模式）包含三个文件组。 文件组 `A` 为读/写文件组，文件组 `B` 和文件组 `C` 为只读文件组。 最初，所有文件组都处于联机状态。  
  
 数据库 `B` 的主文件组和文件组 `adb` 显示为已损坏。 主文件组很小，可以快速还原。 数据库管理员决定使用段落还原顺序还原这些文件组。 首先，还原主文件组和后续事务日志，并恢复数据库。  
  
 完好的文件组 `A` 和 `C` 包含关键数据。 因此，接着对它们进行还原，以尽快使它们处于联机状态。 最后，还原和恢复损坏的辅助文件组 `B`。  
  
## <a name="restore-sequences"></a>还原顺序：  
  
> [!NOTE]  
>  联机还原顺序的语法与脱机还原顺序的语法完全相同。  
  
1.  创建数据库 `adb`的结尾日志备份。 此步骤对于使完好文件组 `A` 和 `C` 与数据库恢复点保持同步至关重要。  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  对主文件组进行部分还原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     此时主文件组处于联机状态。 文件组 `A`、 `B`和 `C` 中的文件处于恢复挂起状态，这几个文件组则处于脱机状态。  
  
3.  对文件组 `A` 和 `C`进行联机还原。  
  
     由于这些文件组中的数据并没有损坏，因此不需要从备份中还原这些文件组，但需要恢复以使它们联机。  
  
     数据库管理员立即恢复 `A` 和 `C` 。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     此时，主文件组和文件组 `A` 以及 `C` 处于联机状态。 文件组 `B` 中的文件仍保持恢复挂起状态，而该文件组处于脱机状态。  
  
4.  对文件组 `B`进行联机还原。  
  
     在随后的任意时间还原文件组 `B` 中的文件。  
  
    > [!NOTE]  
    >  文件组 `B` 的备份是在该文件组成为只读以后进行的；因此，不需要前滚这些文件。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
    ```  
  
     所有文件组现在都处于联机状态。  
  
## <a name="additional-examples"></a>其他示例  
  
-   [示例：数据库的段落还原（简单恢复模式）](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（简单恢复模式）](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [示例：只读文件的联机还原（简单恢复模式）](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [示例：数据库的段落还原（完整恢复模式）](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [示例：读/写文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [示例：只读文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [联机还原 (SQL Server)](online-restore-sql-server.md)   
 [应用事务日志备份 (SQL Server)](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [段落还原 (SQL Server)](piecemeal-restores-sql-server.md)  
  
  
