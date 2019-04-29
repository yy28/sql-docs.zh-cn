---
title: 指定是备份或还原操作将继续还是停止后遇到错误 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], backups
- backing up databases [SQL Server], errors
- backups [SQL Server], errors
- database backups [SQL Server], errors
ms.assetid: 042be17a-b9b0-4629-b6bb-b87a8bc6c316
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 79ab28861fb4ad1eb3fb166e0cccb6b30ff89f86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877033"
---
# <a name="specify-whether-a-backup-or-restore-operation-continues-or-stops-after-encountering-an-error-sql-server"></a>指定备份或还原操作在遇到错误后是继续还是停止 (SQL Server)
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中遇到错误后备份或还原操作是继续还是停止。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要指定备份或还原操作在遇到错误后是停止还是继续，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP  
 默认情况下，为 **sysadmin** 固定服务器角色以及 **db_owner** 和 **db_backupoperator** 固定数据库角色的成员授予 BACKUP DATABASE 和 BACKUP LOG 权限。  
  
 备份设备的物理文件的所有权和权限问题可能会妨碍备份操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须能够读取和写入设备；运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户必须具有写入权限。 但是，用于在系统表中为备份设备添加项目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)不检查文件访问权限。 备份设备物理文件的这些问题可能直到为备份或还原而访问物理资源时才会出现。  
  
 RESTORE  
 如果不存在要还原的数据库，则用户必须有 CREATE DATABASE 权限才能执行 RESTORE。 如果数据库存在，则 RESTORE 权限默认授予 **sysadmin** 和 **dbcreator** 固定服务器角色成员以及数据库的所有者 (**dbo**)（对于 FROM DATABASE_SNAPSHOT 选项，数据库始终存在）。  
  
 RESTORE 权限被授予那些成员身份信息始终可由服务器使用的角色。 因为只有在固定数据库可以访问且没有损坏时（在执行 RESTORE 时并不会总是这样）才能检查固定数据库角色成员身份，所以 **db_owner** 固定数据库角色成员没有 RESTORE 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-specify-whether-backup-continues-or-stops-after-an-error-is-encountered"></a>指定备份操作在遇到错误后是继续还是停止  
  
1.  执行以下步骤以便 [创建数据库备份](create-a-full-database-backup-sql-server.md)。  
  
2.  在 **“选项”** 页的 **“可靠性”** 部分中，单击 **“写入介质前检查校验和”** 和 **“出错时继续”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-whether-a-backup-operation-continues-or-stops-after-encountering-an-error"></a>指定备份操作在遇到错误后是继续还是停止  
  
1.  连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  在 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 语句中，指定 CONTINUE_AFTER ERROR 选项可继续操作，指定 STOP_ON_ERROR 选项可停止操作。 默认行为是遇到错误后停止。 下面的示例指示备份操作在遇到错误时仍继续。  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
#### <a name="to-specify-whether-a-restore-operation-continues-or-stops-after-encountering-an-error"></a>指定还原操作在遇到错误后是继续还是停止  
  
1.  连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  在 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语句中，指定 CONTINUE_AFTER ERROR 选项可继续操作，指定 STOP_ON_ERROR 选项可停止操作。 默认行为是遇到错误后停止。 下面的示例指示还原操作在遇到错误时仍继续。  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'   
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [RESTORE FILELISTONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE HEADERONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)   
 [RESTORE LABELONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [RESTORE VERIFYONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [backupset (Transact-SQL)](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [RESTORE 参数 (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql)   
 [备份和还原期间可能出现的媒体错误 (SQL Server)](possible-media-errors-during-backup-and-restore-sql-server.md)   
 [在备份或还原期间启用或禁用备份校验和 (SQL Server)](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
  
