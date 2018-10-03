---
title: 设置备份的到期日期 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], expiration dates
- expiration [SQL Server]
- database backups [SQL Server], expiration dates
ms.assetid: 76e814df-6487-4893-9f09-7759f1863a5c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3c5811676a3a25df4ad7668c4172f1803c5b2adf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856125"
---
# <a name="set-the-expiration-date-on-a-backup-sql-server"></a>设置备份的过期日期 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中设置备份的过期日期。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要设置备份的过期日期，请使用**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 默认情况下，为 **sysadmin** 固定服务器角色以及 **db_owner** 和 **db_backupoperator** 固定数据库角色的成员授予 BACKUP DATABASE 和 BACKUP LOG 权限。  
  
 备份设备的物理文件的所有权和权限问题可能会妨碍备份操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须能够读取和写入设备；运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户必须具有写入权限。 但是，用于在系统表中为备份设备添加项目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)不检查文件访问权限。 备份设备物理文件的这些问题可能直到为备份或还原而访问物理资源时才会出现。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>设置备份的过期日期  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击数据库，指向“任务”，再单击“备份”。 将出现 **“备份数据库”** 对话框。  
  
4.  在 **“常规”** 页上，为 **“备份集过期时间”** 指定一个过期日期以指明其他备份可以覆盖该备份集的时间：  
  
    -   若要使备份集在特定天数后过期，请单击“之后”（默认选项），并输入备份集从创建到过期所需的天数。 此值范围为 0 到 99999 天；0 天表示备份集将永不过期。  
  
         默认值在 **“服务器属性”** 对话框（位于 **“数据库设置”** 页上）的 **“默认备份媒体保持期(天)”** 选项中设置。 若要访问它，请在对象资源管理器中右键单击服务器名称，选择属性，再选择“数据库设置”页。  
  
    -   若要使备份集在特定日期过期，请单击 **“在”**，并输入备份集的过期日期。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>设置备份的过期日期  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 语句中，指定 EXPIREDATE 或 RETAINDAYS 选项以便确定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 何时可以覆盖备份。 如果这两个选项均未指定，则过期日期由 [介质保持期](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) 服务器配置设置确定。 下面的示例使用 `EXPIREDATE` 选项指定过期日期为 2015 年 6 月 30 日 (`6/30/2015`)。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH EXPIREDATE = '6/30/2015' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [备份文件和文件组 (SQL Server)](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [备份事务日志 (SQL Server)](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [创建差异数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
  
