---
title: 第 5 课。 （可选）加密数据库使用 TDE |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7e78a787a67c430ec82bea4788fd1c92c4c72c4a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090677"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>第 5 课。 （可选）使用 TDE 加密数据库
  作为一个可选步骤，可加密新创建的数据库。 “透明数据加密”(TDE) 可对数据和日志文件执行实时 I/O 加密和解密。 这种加密使用数据库加密密钥 (DEK)，该密钥存储在数据库引导记录中以供恢复时使用。 有关详细信息，请参阅[透明数据加密&#40;TDE&#41; ](security/encryption/transparent-data-encryption.md)并[将受 TDE 保护的数据库移动到另一个 SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md)。  
  
 本课假定您已完成以下步骤：  
  
-   具有 Windows Azure 存储帐户。  
  
-   已在 Windows Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在源计算机上创建了 SQL Server 凭据。  
  
-   已按第 4 课中所述的步骤创建了数据库。  
  
 如果要加密数据库，请执行以下步骤：  
  
1.  在源计算机上，在查询窗口中修改并运行以下语句：  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  然后，通过执行以下步骤，在源计算机中加密新数据库：  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 如果要了解数据库的加密状态及其关联的数据库加密密钥，请运行以下语句：  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 有关本课程中使用的详细的信息 Transact SQL 语句，请参阅[CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)， [ALTER DATABASE &#40;-&#41; ](/sql/t-sql/statements/alter-database-transact-sql)， [CREATE MASTER KEY &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)， [CREATE CERTIFICATE &#40;-&#41;](/sql/t-sql/statements/create-certificate-transact-sql)，并[sys.dm_database_encryption_keys &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)。  
  
 **下一课：**  
  
 [第 6 课：将数据库从一个源计算机的本地到 Windows Azure 中的目标计算机](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
