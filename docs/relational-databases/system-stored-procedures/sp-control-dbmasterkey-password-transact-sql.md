---
title: sp_control_dbmasterkey_password（转算-SQL） |微软文档
ms.custom: ''
ms.date: 04/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 620a174f50d133c4a1dd34ed54c74abb7ee06a71
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012438"
---
# <a name="sp_control_dbmasterkey_password-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  添加或删除包含打开数据库主密钥所需的密码的凭据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>参数  
 @db_name[N'*database_name*'  
 指定与此凭据关联的数据库的名称。 不能为系统数据库。 *database_name*是**恩瓦尔查尔**。  
  
 @password*N'*密码*'  
 指定主密钥的密码。 *密码*是**nvarchar。**  
  
 @action[N'add'  
 指定已指定数据库的凭据将添加到凭据存储区中。 凭据将包含数据库主密钥的密码。 传递给@action的值是**nvarchar**。  
  
 @action[N'下降'  
 指定将从凭据存储区中删除已指定数据库的凭据。 传递给@action的值是**nvarchar**。  
  
## <a name="remarks"></a>备注  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要数据库主密钥对密钥进行解密或加密时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会尝试使用实例的服务主密钥对数据库主密钥进行解密。 如果解密失败，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]搜索凭据存储，以搜索与需要主密钥的数据库具有相同的父密钥凭据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试使用每个匹配的凭据对数据库主密钥进行解密，直到成功解密或者没有更多的凭据为止。  
  
> [!CAUTION]  
>  对于 sa 和其他特权级别高的服务器主体无法访问的数据库，不要为其创建主密钥凭据。 可以对数据库进行配置，以便服务主密钥无法对其密钥层次结构进行解密。 该选项可作为数据库（包含 sa 或其他特权级别高的服务器主体不可访问的加密信息）的深度防御。 为此类数据库创建主密钥凭据将会删除这种深度防御功能，从而使 sa 和其他特权级别高的服务器主体能够对数据库进行解密。  
  
 使用sp_control_dbmasterkey_password创建的凭据在[sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md)目录视图中可见。 为数据库主密钥创建的凭据的名称具有如下格式：`##DBMKEY_<database_family_guid>_<random_password_guid>##`。 该密码存储为凭据机密。 对于每个添加到凭据存储区中的密码，都在 sys.credentials 中占一行。  
  
 不能使用 sp_control_dbmasterkey_password 为下列系统数据库创建凭据：master、model、msdb 或 tempdb。  
  
 sp_control_dbmasterkey_password 不会验证密码是否可以打开已指定数据库的主密钥。  
  
 如果为已指定数据库指定一个已存储在凭据中的密码，则 sp_control_dbmasterkey_password 将会失败。  
  
> [!NOTE]  
>  来自不同服务器实例的两个数据库可以共享相同的系列 GUID。 如果出现这种情况，则这两个数据库将会共享凭据存储区中的相同主密钥记录。  
  
 传递给 sp_control_dbmasterkey_password 的参数不会出现在跟踪中。  
  
> [!NOTE]  
>  在您使用通过 sp_control_dbmasterkey_password 添加的凭据打开数据库主密钥时，服务主密钥重新对数据库主密钥加密。 如果数据库为只读模式，则加密操作将会失败，数据库主密钥将会保留为未加密状态。 随后访问数据库主密钥时，必须使用 OPEN MASTER KEY 语句和密码。 为避免使用密码，请在将数据库迁移到只读模式前创建凭据。  
  
 **潜在的向后兼容性问题：** 目前，存储过程不检查主密钥是否存在。 这是为了向后兼容，但会显示警告。 不推荐使用此行为。 在将来的版本中，主密钥必须存在，并且存储过程中使用的密码**sp_control_dbmasterkey_password**必须与用于加密数据库主密钥的密码之一的密码相同。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. 为 AdventureWorks2012 主密钥创建凭据  
 以下示例为 `AdventureWorks2012` 数据库主密钥创建凭据，并将主密钥密码作为机密内容存储在凭据中。 由于传递给的所有参数`sp_control_dbmasterkey_password`必须为数据类型**nvarchar，** 因此文本字符串将随强制转换运算符`N`。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. 删除数据库主密钥的凭据  
 以下示例删除在示例 A 中创建的凭据。请注意，需要所有的参数，包括密码。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [设置加密镜像数据库](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [安全存储过程&#40;处理-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系统存储过程&#40;处理-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [系统凭据&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
