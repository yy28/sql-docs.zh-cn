---
title: "吊销证书权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
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
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- REVOKE statement, certificates
ms.assetid: 2272324a-98f2-42c6-88b1-96a99020c9e9
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8b3c53547f1bf8091774d5eea566bd8108f41427
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-certificate-permissions-transact-sql"></a>REVOKE 证书权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  撤消对证书的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON CERTIFICATE :: certificate_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>参数  
 GRANT OPTION FOR  
 指示将撤消授予指定权限的能力。 不会撤消该权限本身。  
  
> [!IMPORTANT]  
>  如果主体具有不带 GRANT 选项的指定权限，则将撤消该权限本身。  
  
 *权限*  
 指定可以对证书撤消的权限。 如下所列。  
  
 ON 证书**::***certificate_name*  
 指定要撤消的权限所针对的证书。 需要使用作用域限定符“::”。  
  
 *database_principal*  
 指定要从中撤消权限的主体。 可以是以下类型之一：  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
-   映射到 Windows 登录名的数据库用户  
  
-   映射到 Windows 组的数据库用户  
  
-   映射到证书的数据库用户  
  
-   映射到非对称密钥的数据库用户  
  
-   未映射到服务器主体的数据库用户。  
  
 CASCADE  
 指示要撤消的权限也会从此主体授予该权限的其他主体中撤消。  
  
> [!CAUTION]  
>  如果对授予了 WITH GRANT OPTION 权限的权限执行级联撤消，将同时撤消该权限的 GRANT 和 DENY 权限。  
  
 AS *revoking_principal*  
 指定一个主体，执行该查询的主体从该主体获得撤消该权限的权利。 可以是以下类型之一：  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
-   映射到 Windows 登录名的数据库用户  
  
-   映射到 Windows 组的数据库用户  
  
-   映射到证书的数据库用户  
  
-   映射到非对称密钥的数据库用户  
  
-   未映射到服务器主体的数据库用户。  
  
## <a name="remarks"></a>注释  
 证书是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下面列出了可以撤消的最特定和最受限制的证书权限，同时列出了隐式包括它们的最常见权限。  
  
|证书权限|证书权限隐含的权限|数据库权限隐含的权限|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对证书具有 CONTROL 权限。  
  
## <a name="see-also"></a>另请参阅  
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [创建应用程序角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

