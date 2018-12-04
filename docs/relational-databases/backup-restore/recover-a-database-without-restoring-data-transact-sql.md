---
title: 恢复数据库但不还原数据 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14f0c0a28ca4ecd6b8a58576b46add9b4009bcb7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502494"
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>恢复数据库但不还原数据 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通常，恢复数据库之前，将还原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的所有数据。 但是，还原操作可以恢复数据库而不实际还原备份；例如，恢复那些与数据库一致的只读文件时。 这称为仅恢复还原。 当脱机数据已与数据库一致且只需变为可用时，仅恢复还原操作将完成恢复数据库并使数据联机。  
  
 仅恢复还原可以针对整个数据库或一个或多个文件或文件组进行。  
  
## <a name="recovery-only-database-restore"></a>仅恢复数据库还原  
 在以下情况下仅恢复数据库还原十分有用：  
  
-   您未在还原位于还原顺序中的最后备份时恢复数据库，现在希望恢复该数据库并使其联机。  
  
-   数据库处于备用模式，但您希望在不应用其他日志备份的情况下可以更新数据库。  
  
 仅恢复数据库还原的 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 语法是：  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  FROM =\<backup_device> 子句不用于仅恢复还原，因为不需要任何备份。  
  
 **示例**  
  
 以下示例在还原操作中恢复 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库而不还原数据。  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>仅恢复文件还原  
 在以下情况下仅恢复文件还原十分有用：  
  
 数据库按段落进行还原。 完成主文件组的还原之后，一个或多个未还原的文件变为与新数据库的状态一致，这也许是因为这些文件最近始终是只读的。 只需恢复这些文件即可；无需复制数据。  
  
 仅恢复还原操作将脱机文件组中的数据变为联机状态；不会有数据复制、重做或撤消这些阶段。 有关还原阶段的信息，请参阅[还原和恢复概述 (SQL Server) ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
 仅恢复文件还原的 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 语法是：  
  
 RESTORE DATABASE *database_name* { FILE **=**_logical_file_name_ | FILEGROUP **=**_logical_filegroup_name_ }[ **,**...*n* ] WITH RECOVERY  
  
 **示例**  
  
 以下示例显示了 `SalesGroup2`数据库中辅助文件组 `Sales` 中文件的仅恢复文件还原。 已在段落还原的初始步骤中还原了主文件组，并且 `SalesGroup2` 与还原的主文件组一致。 只需一条语句即可恢复此文件组并使其变为联机状态。  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>使用仅恢复还原完成段落还原方案的示例  
 **简单恢复模式**  
  
-   [示例：数据库的段落还原（简单恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（简单恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **完整恢复模式**  
  
-   [示例：数据库的段落还原（完整恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [示例：仅对某些文件组进行段落还原（完整恢复模式）](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>另请参阅  
 [联机还原 (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [文件还原（简单恢复模式）](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [文件还原（完整恢复模式）](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
