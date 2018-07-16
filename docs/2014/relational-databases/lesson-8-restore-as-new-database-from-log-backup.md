---
title: 第 9 课。 从 Windows Azure 存储还原数据库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 380ceeabb5a91dffafe0624e073856a837a99f14
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37175910"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>第 9 课。 从 Windows Azure 存储还原数据库
  在本课中，您将学习如何将 Windows Azure 存储中的数据库备份文件还原到数据库，该数据库位于本地或 Windows Azure 的虚拟机中。 不需要学完第 4、5、6、7 和 8 课即可听懂本课。  
  
 本课假定您已完成以下步骤：  
  
-   已在源计算机中创建了数据库。  
  
-   通过使用 Windows Azure 存储中创建的数据库 (.bak) 备份[Windows Azure Blob 存储服务使用 SQL Server 备份和还原](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)功能。 注意，需要在此步骤中创建另一个 SQL Server 凭据。 此凭据使用存储帐户密钥。  
  
-   具有 Windows Azure 存储帐户。  
  
-   已在 Windows Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在计算机上创建了 SQL Server 凭据用于 Windows Azure 存储集成功能。 注意，此凭据需要共享访问签名 (SAS) 密钥。  
  
 若要还原 Windows Azure 存储中的数据库，可执行以下步骤：  
  
1.  启动 SQL Server Management Studio。 连接到默认实例。  
  
2.  单击**新查询**标准工具栏上。  
  
3.  复制以下完整脚本并将其粘贴到查询窗口。 根据需要修改脚本。  
  
     **注意：** 运行`RESTORE`语句以在 Windows Azure 存储中的数据库备份 (.bak) 还原到另一台计算机中的数据库实例。  
  
    ```tsql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **教程结束时： 在 Windows Azure 存储服务的 SQL Server 数据文件**  
  
  
