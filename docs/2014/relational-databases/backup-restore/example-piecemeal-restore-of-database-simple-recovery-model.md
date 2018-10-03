---
title: 示例：数据库的段落还原（简单恢复模式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c2e44148d1cd250e575b46f83b7d801d40fc47b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229627"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>示例：数据库的段落还原（简单恢复模式）
  段落还原顺序将从主文件组和所有读写辅助文件组开始，按文件组级别分阶段还原和恢复数据库。  
  
 在此示例中，灾难发生后，数据库 `adb` 被还原到新计算机。 数据库使用的是简单恢复模式。 灾难发生之前，所有文件组均处于联机状态。 文件组 `A` 和 `C` 是可读/写的，文件组 `B` 是只读的。 文件组 `B` 在最新部分备份之前变为只读的，该文件组包含主文件组和读/写辅助文件组 `A` 和 `C`。 文件组 `B` 变为只读后，对文件组 `B` 进行了单独的文件备份。  
  
## <a name="restore-sequences"></a>还原顺序  
  
1.  主文件组以及文件组 `A` 和 `C`的部分还原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     此时，主文件组以及文件组 `A` 和 `C` 处于联机状态。 文件组 `B` 中的所有文件都处于恢复挂起状态，该文件组处于脱机状态。  
  
2.  对文件组 `B`进行联机还原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     所有文件组现在都处于联机状态。  
  
## <a name="additional-examples"></a>其他示例  
  
-   [示例：仅对某些文件组进行段落还原（简单恢复模式）](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [示例：只读文件的联机还原（简单恢复模式）](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [示例：数据库的段落还原（完整恢复模式）](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（完整恢复模式）](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [示例：读/写文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [示例：只读文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>请参阅  
 [联机还原 (SQL Server)](online-restore-sql-server.md)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [段落还原 (SQL Server)](piecemeal-restores-sql-server.md)  
  
  
