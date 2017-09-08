---
title: "REVOKE 数据库主体权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- REVOKE statement, roles
- database user permissions [SQL Server]
- REVOKE statement, users
- application roles [SQL Server], permissions
ms.assetid: c45e1086-c25b-48bb-a764-4a893e983db2
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eee64655f9ac49775692d88ff6bcd95fd7ff28f4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-database-principal-permissions-transact-sql"></a>REVOKE 数据库主体权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  撤消授予或拒绝的对数据库用户、数据库角色或应用程序角色的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
       | [ ROLE :: database_role ]  
       | [ APPLICATION ROLE :: application_role ]  
    }  
    { FROM | TO } <database_principal> [ ,...n ]  
        [ CASCADE ]  
    [ AS <database_principal> ]  
  
<database_principal> ::=  
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可以撤消的对数据库主体的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 用户::*database_user*  
 指定要撤消对其权限的用户的类和名称。 作用域限定符 (**::**) 是必需的。  
  
 角色::*database_role*  
 指定要撤消对其权限的角色的类和名称。 作用域限定符 (**::**) 是必需的。  
  
 应用程序角色::*application_role*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 指定要撤消对其权限的应用程序角色的类和名称。 作用域限定符 (**::**) 是必需的。  
  
 GRANT OPTION  
 指示要撤消向其他主体授予指定权限的权限。 不会撤消该权限本身。  
  
> [!IMPORTANT]  
>  如果主体具有不带 GRANT 选项的指定权限，则将撤消该权限本身。  
  
 CASCADE  
 指示要撤消的权限也会从此主体授予或拒绝该权限的其他主体中撤消。  
  
> [!CAUTION]  
>  如果对授予了 WITH GRANT OPTION 权限的权限执行级联撤消，将同时撤消该权限的 GRANT 和 DENY 权限。  
  
 AS \<database_principal > 指定的主体执行此查询的主体从中派生其权限以撤消的权限。  
  
 *Database_user*  
 指定数据库用户。  
  
 *Database_role*  
 指定数据库角色。  
  
 *Application_role*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 指定应用程序角色。  
  
 *Database_user_mapped_to_Windows_User*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定映射到 Windows 用户的数据库用户。  
  
 *Database_user_mapped_to_Windows_Group*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定映射到 Windows 组的数据库用户。  
  
 *Database_user_mapped_to_certificate*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定映射到证书的数据库用户。  
  
 *Database_user_mapped_to_asymmetric_key*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定映射到非对称密钥的数据库用户。  
  
 *Database_user_with_no_login*  
 指定无相应服务器级主体的数据库用户。  
  
## <a name="remarks"></a>注释  
  
## <a name="database-user-permissions"></a>数据库用户权限  
 数据库用户是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下表列出了可撤消的对数据库用户最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|数据库用户权限|数据库用户权限隐含的权限|数据库权限隐含的权限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>数据库角色权限  
 数据库角色是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下表列出了可撤消的对数据库角色最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|数据库角色权限|数据库角色权限隐含的权限|数据库权限隐含的权限|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>应用程序角色权限  
 应用程序角色是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下表列出了可以撤消的对应用程序角色的最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|应用程序角色权限|应用程序角色权限隐含的权限|数据库权限隐含的权限|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对指定主体的 CONTROL 权限或隐含 CONTROL 权限的更高权限。  
  
 数据库，如的成员拥有 CONTROL 权限的被授权者**db_owner**固定的数据库角色，可以授予任何权限对任何数据库中安全对象。  
  
## <a name="examples"></a>示例  
  
### <a name="a-revoking-control-permission-on-a-user-from-another-user"></a>A. 撤消一个用户对另一个用户的 CONTROL 权限  
 以下示例撤消用户 `CONTROL` 对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 用户 `Wanida` 的 `RolandX` 权限。  
  
```  
USE AdventureWorks2012;  
REVOKE CONTROL ON USER::Wanida FROM RolandX;  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-on-a-role-from-a-user-to-which-it-was-granted-with-grant-option"></a>B. 撤消被通过 GRANT OPTION 授予了 VIEW DEFINITION 权限的用户对角色的该权限  
 以下示例撤消数据库用户 `VIEW DEFINITION` 对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 角色 `SammamishParking` 的 `JinghaoLiu` 权限。 指定了 `CASCADE` 选项，因为用户 `JinghaoLiu` 被通过 `VIEW DEFINITION` 授予了 `WITH GRANT OPTION` 权限。  
  
```  
USE AdventureWorks2012;  
REVOKE VIEW DEFINITION ON ROLE::SammamishParking   
    FROM JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-revoking-impersonate-permission-on-a-user-from-an-application-role"></a>C. 撤消应用程序角色对用户的 IMPERSONATE 权限  
 下面的示例撤消 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 应用程序角色 `IMPERSONATE` 对用户 `HamithaL` 的 `AccountsPayable17` 权限。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
```  
USE AdventureWorks2012;  
REVOKE IMPERSONATE ON USER::HamithaL FROM AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>另请参阅  
 [GRANT 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [DENY 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)   
 [创建应用程序角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [创建角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


