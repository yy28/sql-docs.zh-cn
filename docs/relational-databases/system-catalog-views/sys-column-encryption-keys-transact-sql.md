---
title: sys. column_encryption_keys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_encryption_keys
- column_encryption_keys_TSQL
- sys.column_encryption_keys_TSQL
- column_encryption_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_keys catalog view
ms.assetid: 43980dd8-b9b1-4869-a304-2c183ae8977d
author: jaszymas
ms.author: jaszymas
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4cd6b4a4cb8eeed0dd0a2a78adc2d39c6a2e895d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593721"
---
# <a name="syscolumn_encryption_keys--transact-sql"></a>sys. column_encryption_keys （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]

  返回有关用[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)语句创建的列加密密钥（cek）的信息。 每行表示一个 CEK。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|CMK 的名称。|  
|**column_encryption_key_id**|**int**|CEK 的 ID。|  
|**create_date**|**datetime**|CEK 的创建日期。|  
|**modify_date**|**datetime**|上次修改 CEK 的日期。|  
  
## <a name="permissions"></a>权限  
 需要**VIEW ANY COLUMN ENCRYPTION KEY**权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted 安全 enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted  的密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)  
 [管理具有安全 enclaves 的 Always Encrypted 的密钥](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)    

  
  
