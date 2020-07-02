---
title: sys. column_encryption_key_values （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9c17ef0384d1b4ef1bc5534ffeffa8b2ba3d598
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718884"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys. column_encryption_key_values （Transact-sql）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  返回有关列加密密钥（Cek）的加密值的信息，创建的列加密密钥（）是通过[创建列加密密钥](../../t-sql/statements/create-column-encryption-key-transact-sql.md)或[ALTER column Encryption key &#40;transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)语句创建的。 每行都表示使用列主密钥（CMK）加密的 CEK 值。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|数据库中 CEK 的 ID。|  
|**column_master_key_id**|**int**|用于对 CEK 值进行加密的列主密钥的 ID。|  
|**encrypted_value**|varbinary(8000)****|CEK 值用 column_master_key_id 中指定的 CMK 进行了加密。|  
|**encryption_algorithm_name**|**sysname**|用于对 CEK 值进行加密的算法的名称。<br /><br /> 用于对值进行加密的加密算法的名称。 系统提供程序的算法必须**RSA_OAEP**。|  
  
## <a name="permissions"></a>权限  
 需要**VIEW ANY COLUMN ENCRYPTION KEY**权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql 中创建列加密密钥&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;更改列加密密钥](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;删除列加密密钥](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;创建列主密钥](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Transact-sql&#41;&#40;安全目录视图](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys. column_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys. column_master_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted 安全 enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 的密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [管理具有安全 enclave 的 Always Encrypted 的密钥](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
