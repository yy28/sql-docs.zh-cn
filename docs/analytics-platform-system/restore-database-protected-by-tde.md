---
title: "还原由并行数据仓库中的 TDE 保护的数据库"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "使用以下步骤以还原通过透明数据加密加密的数据库。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: ffb681ca-8598-4614-b06c-660376333fc3
caps.latest.revision: "4"
ms.openlocfilehash: 31f81447bd4fdaf5a2528f5828cc3d70618240c6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restore-a-database-protected-by-tde"></a>还原由 TDE 保护的数据库
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
  
