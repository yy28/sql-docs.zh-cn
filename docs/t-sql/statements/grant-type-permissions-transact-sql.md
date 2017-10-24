---
title: "GRANT 类型权限 (Transact SQL) |Microsoft 文档"
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
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e29ede5580418d1cbcb55d5a877196c3cabab92
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-type-permissions-transact-sql"></a>GRANT 类型权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  授予对类型的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
    TO <database_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 指定可以授予的类型权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 在类型上**::** [ *schema_name***。** ]*类型 _ 名称*  
 指定要授予其权限的类型。 作用域限定符 (**::**) 是必需的。 如果*schema_name*未指定，则将使用默认架构。 如果*schema_name*指定，则架构作用域限定符 (**。**) 是必需的。  
  
 到\<database_principal > 指定向其授予权限的主体。  
  
 WITH GRANT OPTION  
 指示该主体还可以向其他主体授予所指定的权限。  
  
 AS \<database_principal > 指定的主体执行此查询的主体从中派生其权限以授予的权限。  
  
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
 类型是架构级的安全对象，包含于权限层次结构中作为其父级的架构中。  
  
> [!IMPORTANT]  
>  **授予**， **DENY**和**撤消**权限不适用于系统类型。 可以为用户定义类型授予权限。 有关用户定义类型的详细信息，请参阅[使用 SQL Server 中的用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)。  
  
 下表列出了可授予的对类型最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|类型权限|类型权限隐含的权限|架构权限隐含的权限|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|在运行 CREATE 语句前执行|CONTROL|在运行 CREATE 语句前执行|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 授权者（或用 AS 选项指定的主体）必须具有带 GRANT OPTION 的相同权限，或具有隐含所授予权限的更高权限。  
  
 若要使用 AS 选项，还必须满足以下附加要求：  
  
|AS|所需的其他权限|  
|--------|------------------------------------|  
|数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到 Windows 登录名的数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到 Windows 组的数据库用户|中的 Windows 组中中的成员身份的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到证书的数据库用户|中的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到非对称密钥的数据库用户|中的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|未映射到任何服务器主体的数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|数据库角色|在角色中的成员身份的 ALTER 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|应用程序角色|在角色中的成员身份的 ALTER 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
  
## <a name="examples"></a>示例  
 以下示例使用 `VIEW DEFINITION` 授予用户 `GRANT OPTION` 对用户定义类型 `PhoneNumber` 的 `KhalidR` 权限。 `PhoneNumber`架构中位于`Telemarketing`。  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DENY 类型权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [REVOKE 类型权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


