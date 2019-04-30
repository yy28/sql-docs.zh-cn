---
title: 还原受 TDE-并行数据仓库数据库 |Microsoft Docs
description: 使用以下步骤来还原的数据库，在分析平台系统并行数据仓库中使用透明数据加密进行加密。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157013"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>还原由并行数据仓库中的 TDE 保护的数据库
使用以下步骤来还原的数据库，使用透明数据加密进行加密。  
  
[使用透明数据加密](transparent-data-encryption.md#using-tde)示例具有代码上启用 TDE`AdventureWorksPDW2012`数据库。 下面的代码继续该示例中，通过在原始的 Analytics Platform System (APS) 设备上创建数据库的备份，然后将证书和不同的设备上的数据库还原。  
  
第一步是创建源数据库的备份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
准备新的 SQL Server PDW 用于 TDE 通过创建一个主密钥、 启用加密，并创建网络凭据。  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
最后两个步骤通过使用来自原始 SQL Server PDW 备份重新创建该证书。 使用在创建证书的备份时使用的密码。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>请参阅  
[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[创建证书](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
