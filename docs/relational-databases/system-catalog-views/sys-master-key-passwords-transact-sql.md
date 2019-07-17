---
title: sys.master_key_passwords (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87bb4a97db318330f253d068febb1309e4eda12a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102405"
---
# <a name="sysmasterkeypasswords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为使用添加的每个数据库主密钥密码返回一行**sp_control_dbmasterkey_password**存储过程。 用于保护主密钥的密码存储在凭据存储区中。 凭据名称遵循以下格式: # # DBMKEY_ < database_family_guid > _ < random_password_guid > # #。 该密码存储为凭据机密。 对于使用添加的每个密码**sp_control_dbmasterkey_password**，没有中的一行**sys.credentials**。  
  
 此视图中的每一行显示**credential_id**并**family_guid**的由与该凭据关联的密码保护主密钥的数据库。 使用联接**sys.credentials**上**credential_id**将返回一些有用的字段，如**create_date**和凭据名称。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|密码所属的凭据的 ID。 该 ID 在服务器实例中是唯一的。|  
|**family_guid**|**uniqueidentifier**|创建时原始数据库的唯一 ID。 在还原或附加数据库后，即使更改了数据库名称，这个 GUID 也将始终保持不变。<br /><br /> 如果通过服务主密钥自动解密失败，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**family_guid**来标识可能包含用于保护数据库主密钥的密码的凭据。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
