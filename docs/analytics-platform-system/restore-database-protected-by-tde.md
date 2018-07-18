---
title: 还原受 TDE 的并行数据仓库数据库 |Microsoft 文档
description: 使用以下步骤来还原数据库加密分析平台系统并行数据仓库中使用透明数据加密。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538607"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>还原由并行数据仓库中的 TDE 保护的数据库
使用以下步骤以还原通过透明数据加密加密的数据库。  
  
[使用透明数据加密](transparent-data-encryption.md#using-tde)示例具有代码上启用 TDE`AdventureWorksPDW2012`数据库。 下面的代码继续执行该示例中，在原始分析平台系统 (AP) 设备上创建数据库的备份和还原证书和一个不同的设备上的数据库。  
  
第一步是创建源数据库的备份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
准备新的 SQL Server PDW TDE 通过创建一个主密钥、 启用加密，并创建网络凭据。  
  
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
  
最后两个步骤通过使用原始的 SQL Server PDW 的备份重新创建证书。 使用你在创建证书的备份时使用的密码。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>另请参阅  
[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[创建证书](../t-sql/statements/create-certificate-transact-sql.md)  
[还原数据库](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
