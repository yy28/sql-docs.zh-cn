---
title: sys. master_key_passwords （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7d4bdd76786d4c70b0c27bf60c1a51f08828d1b2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825079"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  为使用**sp_control_dbmasterkey_password**存储过程添加的每个数据库主密钥密码返回一行。 用于保护主密钥的密码存储在凭据存储区中。 凭据名称采用以下格式： # #DBMKEY_<database_family_guid>_<random_password_guid # #。 该密码存储为凭据机密。 对于使用**sp_control_dbmasterkey_password**添加的每个密码，都有**一行。**  
  
 此视图中的每一行都显示了一个**credential_id** **family_guid** ，以及数据库的主密钥，该密钥受与该凭据关联的密码保护。 在**credential_id**上，与**sys.** credential 的联接将返回有用的字段，例如**create_date**和凭据名称。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|密码所属的凭据的 ID。 该 ID 在服务器实例中是唯一的。|  
|**family_guid**|**uniqueidentifier**|创建时原始数据库的唯一 ID。 在还原或附加数据库后，即使更改了数据库名称，这个 GUID 也将始终保持不变。<br /><br /> 如果服务主密钥的自动解密失败， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则使用**family_guid**来识别可能包含用于保护数据库主密钥的密码的凭据。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Transact-sql&#41;&#40;安全目录视图](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;创建对称密钥](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
