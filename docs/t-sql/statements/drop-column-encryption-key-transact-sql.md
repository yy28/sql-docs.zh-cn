---
title: DROP COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP COLUMN ENCRYPTION
- DROP COLUMN ENCRYPTION KEY
- DROP_COLUMN_ENCRYPTION_TSQL
- DROP_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP COLUMN ENCRYPTION KEY statement
- column encryption key, drop
ms.assetid: 86415302-1383-4d36-9fc7-f780831a2d37
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 8e480940623388e64c965d385c383d144d8738c3
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635380"
---
# <a name="drop-column-encryption-key-transact-sql"></a>DROP COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  删除数据库中的列加密密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```syntaxsql
  
DROP COLUMN ENCRYPTION KEY key_name [;]  
```  
  
## <a name="arguments"></a>参数  
 key_name   
 从数据库中删除列加密密钥所依据的名称。  
  
## <a name="remarks"></a>备注  
 如果列加密密钥用于对数据库中的任何列进行加密，则无法将其删除。 必须首先删除所有使用列加密密钥的列。  
  
## <a name="permissions"></a>权限  
 需要对数据库具有 ALTER ANY COLUMN ENCRYPTION KEY 权限  。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-a-column-encryption-key"></a>A. 删除列加密密钥  
 以下示例删除名为 `MyCEK` 的列加密密钥。  
  
```  
DROP COLUMN ENCRYPTION KEY MyCEK;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [创建列主密钥 (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [具有安全 enclave 的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [管理具有安全 enclave 的 Always Encrypted 的密钥](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
  
