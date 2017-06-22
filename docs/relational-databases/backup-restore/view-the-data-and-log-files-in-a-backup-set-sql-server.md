---
title: "查看备份集中的数据文件和日志文件 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database backups [SQL Server], viewing backup sets
- viewing backup set information
- backup sets [SQL Server], viewing files in
- displaying backup set information
- transaction log backups [SQL Server], viewing backup sets
- backing up [SQL Server], viewing backup sets
ms.assetid: abb6420c-f809-426e-aeb4-d0a74989cf39
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b315b0bc0d56cf0e618869f1eef69278fc0d6988
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="view-the-data-and-log-files-in-a-backup-set-sql-server"></a>查看备份集中的数据文件和日志文件 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看备份集中的数据文件和日志文件。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看备份集中的数据文件和日志文件，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关安全性的信息，请参阅 [RESTORE FILELISTONLY (Transact SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
####  <a name="Permissions"></a> 权限  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，获取有关备份集或备份设备的信息要求具有 CREATE DATABASE 权限。 有关详细信息，请参阅 [GRANT 数据库权限 (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-data-and-log-files-in-a-backup-set"></a>查看备份集中的数据文件和日志文件  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击该数据库，再单击“属性”，这将打开“数据库属性”对话框。  
  
4.  在 **“选择页”** 窗格中，单击 **“文件”**。  
  
5.  在 **“数据库文件”** 网格查找数据和日志文件及其属性的列表。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-data-and-log-files-in-a-backup-set"></a>查看备份集中的数据文件和日志文件  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  使用 [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md) 语句。 此示例返回有关`FILE=2`备份设备上的第二个备份集 ( `AdventureWorksBackups` ) 的信息。  
  
```tsql  
USE AdventureWorks2012 ;  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile (Transact-SQL)](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset (Transact-SQL)](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily (Transact-SQL)](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [备份设备 (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
