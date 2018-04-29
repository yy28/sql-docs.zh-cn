---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
caps.latest.revision: 75
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8a665ebed310f2ad80e8f73a03c429563a635884
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  重命名数据库用户或更改它的默认架构。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,… n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *userName*  
 指定在此数据库中用于识别该用户的名称。  
  
 LOGIN =loginName  
 通过将用户的安全标识符 (SID) 更改为另一个登录名的 SID，使用户重新映射到该登录名。  
  
 如果 ALTER USER 语句是 SQL 批处理中唯一的语句，则 Windows Azure SQL Database 将支持 WITH LOGIN 子句。 如果 ALTER USER 语句不是 SQL 批处理中唯一的语句或在动态 SQL 中执行，则不支持 WITH LOGIN 子句。  
  
 NAME =newUserName  
 指定此用户的新名称。 newUserName 不能已存在于当前数据库中。  
  
 DEFAULT_SCHEMA = { schemaName | NULL }  
 指定服务器在解析此用户的对象名时将搜索的第一个架构。 将默认架构设置为 NULL 将从 Windows 组中删除默认架构。   Windows 用户不能使用 NULL 选项。  
  
 PASSWORD = 'password'  
 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定正在更改的用户的密码。 密码是区分大小写的。  
  
> [!NOTE]  
>  此选项仅适用于包含的用户。 有关详细信息，请参阅[包含的数据库](../../relational-databases/databases/contained-databases.md)和 [sp_migrate_user_to_contained (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)。  
  
 OLD_PASSWORD ='oldpassword'  
 适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 将替换为“password”的当前用户密码。 密码是区分大小写的。 除非拥有 ALTER ANY USER 权限，否则需要具有 OLD_PASSWORD 才能更改密码。 需要 OLD_PASSWORD 可防止拥有 IMPERSONATION 权限的用户更改密码。  
  
> [!NOTE]  
>  此选项仅适用于包含的用户。  
  
 DEFAULT_LANGUAGE ={ NONE | \<lcid> | \<language name> | \<language alias> }  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将指派给用户的默认语言。 如果将此选项设置为 NONE，则默认语言将设置为数据库的当前默认语言。 如果之后更改数据库的默认语言，用户的默认语言将保持不变。 DEFAULT_LANGUAGE 可以为本地 ID (lcid)、语言的名称或语言别名。  
  
> [!NOTE]  
>  此选项只能在包含数据库中指定，且只能用于包含的用户。  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
 适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 取消在大容量复制操作期间对服务器进行加密元数据检查。 这使用户能够在表或数据库之间大容量复制加密数据，而无需对数据进行解密。 默认为 OFF。  
  
> [!WARNING]  
>  错误使用此选项可能导致数据损坏。 有关详细信息，请参阅[迁移通过 Always Encrypted 保护的敏感数据](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
## <a name="remarks"></a>Remarks  
 默认架构将是服务器为此数据库用户解析对象名时将搜索的第一个架构。 除非另外指定，否则默认架构将是此数据库用户创建的对象所属的架构。  
  
 如果用户具有默认架构，则将使用默认架构。 如果用户不具有默认架构，但该用户是具有默认架构的组的成员，则将使用该组的默认架构。 如果用户不具有默认架构而且是多个组的成员，则该用户的默认架构将是具有最低 principle_id 的 Windows 组的架构和一个显式设置的默认架构。 如果不能为用户确定默认架构，则将使用 dbo 架构。  
  
 可以将 DEFAULT_SCHEMA 设置为数据库中当前不存在的架构。 因此，可以在创建架构之前将 DEFAULT_SCHEMA 分配给用户。  
  
 不能为映射到证书或非对称密钥的用户指定 DEFAULT_SCHEMA。  
  
> [!IMPORTANT]  
>  如果用户是 sysadmin 固定服务器角色的成员，则忽略 DEFAULT_SCHEMA 的值。 sysadmin 固定服务器角色的所有成员都有默认架构 `dbo`。  
  
 仅当新用户名的 SID 与在数据库中记录的 SID 匹配时，才能更改映射到 Windows 登录名或组的用户的名称。 此检查将帮助防止数据库中的 Windows 登录名欺骗。  
  
 使用 WITH LOGIN 子句可以将用户重新映射到一个不同的登录名。 不能使用此子句重新映射以下用户：不具有登录名的用户、映射到证书的用户或映射到非对称密钥的用户。 只能重新映射 SQL 用户和 Windows 用户（或组）。 不能使用 WITH LOGIN 子句更改用户类型，例如将 Windows 帐户更改为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 如果满足以下条件，则用户的名称会自动重命名为登录名。  
  
-   用户是一个 Windows 用户。  
  
-   名称是一个 Windows 名称（包含反斜杠）。  
  
-   未指定新名称。  
  
-   当前名称不同于登录名。  
  
 如果不满足上述条件，则不会重命名用户，除非调用方另外调用了 NAME 子句。  
  
被映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名、证书或非对称密钥的用户名不能包含反斜杠字符 (\\)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Security  
  
> [!NOTE]  
>  拥有 ALTER ANY USER 权限的用户可以更改任何用户的默认架构。 更改了架构的用户可能会在不知情的情况下从错误表中选择数据，或者从错误架构中执行代码。  
  
### <a name="permissions"></a>权限  
 更改用户名需要具有 ALTER ANY USER 权限。  
  
 更改用户的目标登录名需要对数据库拥有 CONTROL 权限。  
  
 若要更改对数据库拥有 CONTROL 权限的用户名名称，则需要对数据库拥有 CONTROL 权限。  
  
 更改默认架构或语言需要对用户拥有 ALTER 权限。 用户可更改自己的默认架构或语言。  
  
## <a name="examples"></a>示例  

所有示例都在用户数据库中执行。  

### <a name="a-changing-the-name-of-a-database-user"></a>A. 更改数据库用户的名称  
 以下示例将数据库用户 `Mary5` 的名称更改为 `Mary51`。  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. 更改用户的默认架构  
 以下示例将用户 `Mary51` 的默认架构更改为 `Purchasing`。  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. 同时更改几个选项  
 以下示例可在一个语句中为一个包含数据库用户更改若干个选项。  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#’ OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER (Transact-SQL)](../../t-sql/statements/drop-user-transact-sql.md)   
 [包含的数据库](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_migrate_user_to_contained (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  


