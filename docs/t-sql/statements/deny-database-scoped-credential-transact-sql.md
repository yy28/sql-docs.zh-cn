---
title: "拒绝数据库范围的凭据 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DENY DATABASE SCOPED CREDENTIAL
- DENY_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, database scoped credentials
- denying permissions [SQL Server], database scoped credential
ms.assetid: c508b1c9-169e-4e7a-9a49-7ddf2ca8f848
caps.latest.revision: 2
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dcb2ee7f32cea0c848850dc504a91067611b743e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-database-scoped-credential-transact-sql"></a>拒绝数据库范围的凭据 (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

  拒绝对数据库范围的凭据的权限。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DENY permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定在数据库范围的凭据可能遭到拒绝的权限。 如下所列。  
  
 在数据库作用域凭据**::***credential_name*  
 指定在其拒绝的权限的数据库范围的凭据。 需要使用作用域限定符“::”。  
  
 *database_principal*  
 指定要对其拒绝权限的主体。 可以是以下类型之一：  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
-   映射到 Windows 登录名的数据库用户  
  
-   映射到 Windows 组的数据库用户  
  
-   映射到证书的数据库用户  
  
-   映射到非对称密钥的数据库用户  
  
-   未映射到服务器主体的数据库用户。  
  
 CASCADE  
 指示要拒绝的权限也会被对此主体授予该权限的其他主体拒绝。  
  
 *denying_principal*  
 指定一个主体，执行该查询的主体从该主体获得拒绝授予该权限的权利。 可以是以下类型之一：  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
-   映射到 Windows 登录名的数据库用户  
  
-   映射到 Windows 组的数据库用户  
  
-   映射到证书的数据库用户  
  
-   映射到非对称密钥的数据库用户  
  
-   未映射到服务器主体的数据库用户。  
  
## <a name="remarks"></a>注释  
 数据库范围的凭据是数据库级安全对象是指其父权限层次结构中的该数据库包含的。 可以在数据库范围的凭据被拒绝的最特定和受限权限在下面列出，以及将其包含是通过默示的更多常规权限。  
  
|数据库范围凭据的权限|数据库范围凭据权限隐含|数据库权限隐含的权限|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 要求具有数据库范围凭据的 CONTROL 权限。 如果使用 AS 子句时，指定的主体必须拥有数据库范围的凭据。  
  
## <a name="see-also"></a>另请参阅  
 [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md)   
 [授予数据库范围的凭据 (TRANSACT-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [REVOKE 数据库范围的凭据 (TRANSACT-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

