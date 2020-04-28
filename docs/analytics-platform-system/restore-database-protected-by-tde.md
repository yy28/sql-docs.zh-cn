---
title: 还原 TDE 保护的数据库
description: 使用以下步骤来还原使用分析平台系统并行数据仓库中的透明数据加密进行加密的数据库。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 53707c62e018b9923f2bb923a4df46f6917d2902
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400440"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>还原由并行数据仓库中的 TDE 保护的数据库
使用以下步骤还原通过使用透明数据加密进行加密的数据库。  
  
[使用透明数据加密](transparent-data-encryption.md#using-tde)示例包含用于在`AdventureWorksPDW2012`数据库上启用 TDE 的代码。 以下代码继续该示例，方法是在原始分析平台系统（AP）设备上创建数据库的备份，然后在不同的设备上还原证书和数据库。  
  
第一步是创建源数据库的备份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
通过创建主密钥、启用加密以及创建网络凭据为 TDE 准备新的 SQL Server PDW。  
  
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
  
最后两个步骤使用原始 SQL Server PDW 中的备份重新创建证书。 使用创建证书备份时使用的密码。  
  
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
[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[创建主密钥](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
