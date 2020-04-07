---
title: 系统master_key_passwords（转用-SQL） |微软文档
ms.custom: ''
ms.date: 04/06/2020
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
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752895"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  返回使用**sp_control_dbmasterkey_password**存储过程添加的每个数据库主密钥密码的行。 用于保护主密钥的密码存储在凭据存储区中。 凭据名称遵循此格式：##DBMKEY_<database_family_guid>_>_<random_password_guid>*。 该密码存储为凭据机密。 对于使用**sp_control_dbmasterkey_password**添加的每个密码 **，sys.凭据**中有一行。  
  
 此视图中的每一行都显示**一个credential_id**和数据库**的family_guid，** 主密钥受与该凭据关联的密码保护。 **credential_id**上具有**sys.凭据**的联接将返回有用的字段，如**create_date**和凭据名称。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**credential_id**|**Int**|密码所属的凭据的 ID。 该 ID 在服务器实例中是唯一的。|  
|**family_guid**|**uniqueidentifier**|创建时原始数据库的唯一 ID。 在还原或附加数据库后，即使更改了数据库名称，这个 GUID 也将始终保持不变。<br /><br /> 如果服务主密钥的自动解密失败，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]则使用**family_guid**标识可能包含用于保护数据库主密钥的密码的凭据。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]有关详细信息，请参阅[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;交易-SQL&#41;的目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password&#40;转算-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [安全目录视图&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [创建对称键&#40;转算-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
