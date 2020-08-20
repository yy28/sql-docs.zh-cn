---
description: 'sys. column_encryption_key_values (Transact-sql) '
title: sys. column_encryption_key_values (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: aee9c14d1b59055cc968e9b51fa2e07005ae94bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470004"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys. column_encryption_key_values (Transact-sql) 
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  返回 (Cek) 创建的列加密密钥的加密值的相关信息， [该加密](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 密钥 [&#40;transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 语句创建。 每一行都表示使用列主密钥加密的 CEK 的值 (CMK) 。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|数据库中 CEK 的 ID。|  
|**column_master_key_id**|**int**|用于对 CEK 值进行加密的列主密钥的 ID。|  
|**encrypted_value**|varbinary(8000)****|CEK 值用 column_master_key_id 中指定的 CMK 进行了加密。|  
|**encryption_algorithm_name**|**sysname**|用于对 CEK 值进行加密的算法的名称。<br /><br /> 用于对值进行加密的加密算法的名称。 系统提供程序的算法必须  **RSA_OAEP**。|  
  
## <a name="permissions"></a>权限  
 需要 **VIEW ANY COLUMN ENCRYPTION KEY** 权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql 中创建列加密密钥&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;更改列加密密钥 ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;删除列加密密钥 ](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [&#40;Transact-sql&#41;创建列主密钥 ](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys. column_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys. column_master_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted 安全 enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 的密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [管理具有安全 enclave 的 Always Encrypted 的密钥](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
