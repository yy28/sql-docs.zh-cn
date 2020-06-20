---
title: 第 9 课。 从 Azure 存储还原数据库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 37d8344323add8b9b6f520d59862cdd978823e4f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049774"
---
# <a name="lesson-9-restore-a-database-from-azure-storage"></a>第 9 课。 从 Azure 存储还原数据库
  在本课中，您将学习如何将数据库备份文件从 Azure 存储还原到数据库（驻留在本地或 Azure 中的虚拟机上）。 不需要学完第 4、5、6、7 和 8 课即可听懂本课。  
  
 本课假定您已完成以下步骤：  
  
-   已在源计算机中创建了数据库。  
  
-   已通过使用[SQL Server 备份和还原与 Azure Blob 存储服务](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)功能在 azure 存储中创建数据库的备份。 注意，需要在此步骤中创建另一个 SQL Server 凭据。 此凭据使用存储帐户密钥。  
  
-   你有 Azure 存储帐户。  
  
-   在 Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在计算机上为 Azure 存储集成功能创建了 SQL Server 凭据。 注意，此凭据需要共享访问签名 (SAS) 密钥。  
  
 若要从 Azure 存储还原数据库，可以执行以下步骤：  
  
1.  启动 SQL Server Management Studio。 连接到默认实例。  
  
2.  单击 "标准" 工具栏上的 "**新建查询**"。  
  
3.  复制以下完整脚本并将其粘贴到查询窗口。 根据需要修改脚本。  
  
     **注意：** 运行 `RESTORE` 语句，将 Azure 存储中的数据库备份（.bak）还原到其他计算机中的数据库实例。  
  
    ```sql  
  
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
    -- Create a credential to be used by SQL Server Backup and Restore with Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Azure Storage.   
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
  
 **教程结束：在 Azure 存储服务中 SQL Server 数据文件**  
  
  
