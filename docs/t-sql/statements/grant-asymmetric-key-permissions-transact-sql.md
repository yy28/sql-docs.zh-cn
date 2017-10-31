---
title: "授予非对称密钥权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/12/2017
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
- granting permissions [SQL Server], asymmetric keys
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- GRANT statement, asymmetric keys
ms.assetid: a70e2ee6-59b0-4543-b883-e9cbae6199be
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c7234246958d82b8c90df9e5ad54d042248cc2d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-asymmetric-key-permissions-transact-sql"></a>GRANT 非对称密钥权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  授予对非对称密钥的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
GRANT { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
       TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可对非对称密钥授予的权限。 如下所列。  
  
 非对称密钥**::***asymmetric_key_name*  
 指定对其授予权限的非对称密钥。 需要使用作用域限定符“::”。  
  
 *database_principal*  
 指定要向其授予权限的主体。 可以是以下类型之一：  
  
-   数据库用户  
-   数据库角色  
-   应用程序角色  
-   映射到 Windows 登录名的数据库用户  
-   映射到 Windows 组的数据库用户  
-   映射到证书的数据库用户  
-   映射到非对称密钥的数据库用户  
-   未映射到服务器主体的数据库用户。  
  
GRANT OPTION  
 指示该主体还可以向其他主体授予所指定的权限。  
  
AS *granting_principal*  
 指定一个主体，执行该查询的主体从该主体获得授予该权限的权利。 可以是以下类型之一：  
  
-   数据库用户  
-   数据库角色  
-   应用程序角色  
-   映射到 Windows 登录名的数据库用户  
-   映射到 Windows 组的数据库用户  
-   映射到证书的数据库用户  
-   映射到非对称密钥的数据库用户  
-   未映射到服务器主体的数据库用户。  
  
## <a name="remarks"></a>注释  
 非对称密钥是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下面列出了可授予非对称密钥的最特定和最受限的权限，以及隐含这些权限的更常用权限。  
  
|非对称密钥权限|非对称密钥权限隐含的权限|数据库权限隐含的权限|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 授权者（或用 AS 选项指定的主体）必须具有带 GRANT OPTION 的相同权限，或具有隐含所授予权限的更高权限。  
  
 如果使用 AS 选项，还必须满足以下附加要求：  
  
|AS *granting_principal*|所需的其他权限|  
|------------------------------|------------------------------------|  
|数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到 Windows 登录名的数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到 Windows 组的数据库用户|中的 Windows 组中中的成员身份的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到证书的数据库用户|中的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|映射到非对称密钥的数据库用户|中的成员身份**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|未映射到任何服务器主体的数据库用户|针对用户、 中的成员身份的 IMPERSONATE 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|数据库角色|在角色中的成员身份的 ALTER 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
|应用程序角色|在角色中的成员身份的 ALTER 权限**db_securityadmin**固定的数据库角色、 中的成员身份**db_owner**固定数据库角色或中的成员身份**sysadmin**固定的服务器角色。|  
  
 对象所有者可以授予对其所拥有的对象的权限。 对某安全对象具有 CONTROL 权限的主体可以授予对该安全对象的权限。  
  
 被授权者的 CONTROL SERVER 权限，例如成员**sysadmin**固定的服务器角色，可以授予任何权限上任何服务器中安全对象。 数据库，如的成员拥有 CONTROL 权限的被授权者**db_owner**固定的数据库角色，可以授予任何权限对任何数据库中安全对象。 被授权 CONTROL 权限的用户可以授予对相应架构中任一个对象的任意权限。  
  
## <a name="see-also"></a>另请参阅  
 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [创建应用程序角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  

