---
title: 为磁盘文件定义逻辑备份设备 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
ms.assetid: 86331d43-c738-4523-ae3d-7d6700348ed1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ae32391bd2f10525b89015272d11bcdb6468298
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537091"
---
# <a name="define-a-logical-backup-device-for-a-disk-file-sql-server"></a>为磁盘文件定义逻辑备份设备 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中为磁盘文件定义逻辑备份设备。 逻辑设备是指向特定物理备份设备（磁盘文件或磁带机）的用户定义名称。  将备份写入备份设备后，便会初始化物理设备。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要为磁盘文件定义逻辑备份设备，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   逻辑设备名称在服务器实例上的所有逻辑备份设备中必须是唯一的。 若要查看现有逻辑设备名称，请查询 [sys.backup_devices](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql) 目录视图。  
  
###  <a name="Recommendations"></a> 建议  
  
-   我们建议备份磁盘应不同于数据库数据和日志的磁盘。 这是数据或日志磁盘出现故障时访问备份数据必不可少的。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 **diskadmin** 固定服务器角色中的成员身份。  
  
 要求拥有写入磁盘的权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-disk-file"></a>为磁盘文件定义逻辑备份设备  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开“服务器对象”，然后右键单击“备份设备”。  
  
3.  单击 **“新建备份设备”**。 将打开 **“备份设备”** 对话框。  
  
4.  输入设备名称。  
  
5.  若要确定目标位置，请单击 **“文件”** 并指定该文件的完整路径。  
  
6.  若要定义新设备，请单击 **“确定”**。  
  
 若要备份至此新设备，请将该设备添加到“备份数据库”（“常规”）对话框中的“备份到：”字段。 有关详细信息，请参阅 [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)中创建差异数据库备份。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-define-a-logical-backup-for-a-disk-file"></a>为磁盘文件定义逻辑备份  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何使用 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) 为磁盘文件定义逻辑备份设备。 下面的示例以物理名称 `mydiskdump`添加名为 `c:\dump\dump1.bak`的磁盘备份设备。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [备份设备 (SQL Server)](backup-devices-sql-server.md)   
 [sys.backup_devices (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [为磁带驱动器定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [查看逻辑备份设备的属性和内容 (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
