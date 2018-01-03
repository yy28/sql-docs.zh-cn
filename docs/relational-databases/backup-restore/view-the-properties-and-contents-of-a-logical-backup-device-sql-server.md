---
title: "查看逻辑备份设备的属性和内容 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32583e8e6b2cf06f9437ee00821cdf1b62f3b938
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>查看逻辑备份设备的属性和内容 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查看 [!INCLUDE[tsql](../../includes/tsql-md.md)]中逻辑备份设备的属性和内容。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看逻辑备份设备的属性和内容，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关安全性的信息，请参阅 [RESTORE LABELONLY (Transact SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)。  
  
####  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，获取有关备份集或备份设备的信息要求具有 CREATE DATABASE 权限。 有关详细信息，请参阅 [GRANT 数据库权限 (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>查看逻辑备份设备的属性和内容  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“服务器对象”**，然后展开 **“备份设备”**。  
  
3.  单击设备并右键单击“属性”，将打开“备份设备”对话框。  
  
4.  **“常规”** 页将显示设备名称和目标，目标为磁带设备或者文件路径。  
  
5.  在 **“选择页”** 窗格中，单击 **“介质内容”**。  
  
6.  以下属性面板中将显示右侧窗格：  
  
    -   **介质**  
  
         介质顺序信息（介质序列号、簇序列号和镜像标识符（如果存在））以及介质的创建日期和时间。  
  
    -   **介质集**  
  
         介质集信息：介质集名称和说明（如果有）以及介质集中的簇数。  
  
7.  **“备份集”** 网格显示了有关介质集内容的信息。  
  
> [!NOTE]  
>  有关详细信息，请参阅 [媒体内容页](../../relational-databases/backup-restore/backup-device-media-contents-page.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>查看逻辑备份设备的属性和内容  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  使用 [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 语句。 此示例返回有关 `AdvWrks2008R2Backup` 逻辑备份设备的信息。  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile (Transact-SQL)](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset (Transact-SQL)](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily (Transact-SQL)](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [备份设备 (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
