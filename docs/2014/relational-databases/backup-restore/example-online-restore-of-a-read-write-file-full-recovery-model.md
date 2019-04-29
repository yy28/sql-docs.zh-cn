---
title: 例如：联机还原读写文件 （完整恢复模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 0dbeda81-1464-44ba-9011-914900096368
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45056586be543894c714f4005ba84826aa856674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876064"
---
# <a name="example-online-restore-of-a-read-write-file-full-recovery-model"></a>例如：读/写文件的联机还原（完整恢复模式）
  本主题与完整恢复模式下包含多个文件或文件组的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库相关。  
  
 在此示例中，名为 `adb`的数据库（使用完整恢复模式）包含三个文件组。 文件组 `A` 为读/写文件组，文件组 `B` 和文件组 `C` 为只读文件组。 最初，所有文件组都处于联机状态。  
  
 文件组 `a1` 中的文件 `A` 似乎已损坏，数据库管理员决定在数据库处于联机状态时还原该文件。  
  
> [!NOTE]  
>  在简单恢复模式下，不允许联机还原读/写数据。  
  
## <a name="restore-sequences"></a>还原顺序  
  
> [!NOTE]  
>  联机还原顺序的语法与脱机还原顺序的语法完全相同。  
  
1.  联机还原文件 `a1`。  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     此时，文件 a1 处于 RESTORING 状态，文件组 A 处于脱机状态。  
  
2.  完成文件还原之后，数据库管理员进行新的日志备份以确保捕获到该文件脱机时的点。  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  联机还原日志备份。  
  
     管理员还原自从还原了文件备份后一直到获得最新日志备份（在步骤 2 中创建的*log_backup3*）所进行的所有日志备份。 还原最后一个备份之后，应当恢复数据库。  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE LOG adb WITH RECOVERY;  
    ```  
  
     文件 `a1` 现处于联机状态。  
  
## <a name="additional-examples"></a>其他示例  
  
-   [示例：数据库的段落还原（简单恢复模式）](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（简单恢复模式）](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [示例：只读文件的联机还原（简单恢复模式）](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [示例：数据库的段落还原（完整恢复模式）](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（完整恢复模式）](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [示例：只读文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>请参阅  
 [联机还原 (SQL Server)](online-restore-sql-server.md)   
 [段落还原 (SQL Server)](piecemeal-restores-sql-server.md)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [还原和恢复概述 (SQL Server)](restore-and-recovery-overview-sql-server.md)   
 [应用事务日志备份 (SQL Server)](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
