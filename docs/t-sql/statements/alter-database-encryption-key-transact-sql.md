---
title: "ALTER DATABASE ENCRYPTION KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_ENCRYPTION_KEY_TSQL
- ALTER DATABASE ENCRYPTION
- ALTER_DATABASE_ENCRYPTION_TSQL
- ALTER DATABASE ENCRYPTION KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key, alter
- ALTER DATABASE ENCRYPTION KEY
ms.assetid: f88dac4b-efe0-47ed-9808-972a4381377e
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: c0ea8313662a84b71f665ac2402733aa15eaac7a
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="alter-database-encryption-key-transact-sql"></a>ALTER DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  改变用于以透明方式加密数据库的加密密钥和证书。 有关透明数据库加密的详细信息，请参阅[透明数据加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
ALTER DATABASE ENCRYPTION KEY  
      REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   |  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER DATABASE ENCRYPTION KEY  
    {  
      {  
        REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
        [ ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name ]  
      }  
      |  
      ENCRYPTION BY SERVER   CERTIFICATE Encryptor_Name    
    }  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
 指定用于加密密钥的加密算法。  
  
 服务器证书通过加密*Encryptor_Name*  
 指定用于加密数据库加密密钥的证书的名称。  
  
 通过服务器非对称密钥 Encryptor_Name 加密  
 指定用于加密数据库加密密钥的非对称密钥的名称。  
  
## <a name="remarks"></a>注释  
 用于加密数据库加密密钥的证书或非对称密钥必须位于 master 系统数据库中。  
  
 数据库所有者 (dbo) 发生更改时不必重新生成数据库加密密钥。  
  
 在数据库加密密钥修改过两次后，必须执行日志备份才能再次对数据库加密密钥进行修改。  
  
## <a name="permissions"></a>Permissions  
 需要数据库的 CONTROL 权限和用于加密数据库加密密钥的证书或非对称密钥的 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
 下面的示例将数据库加密密钥更改为使用 `AES_256` 算法。  
  
```  
-- Uses AdventureWorks  
  
ALTER DATABASE ENCRYPTION KEY  
REGENERATE WITH ALGORITHM = AES_256;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 和数据库加密密钥（数据库引擎）](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [创建数据库加密密钥 &#40;Transact SQL &#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
 [sys.dm_database_encryption_keys (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
  
  


