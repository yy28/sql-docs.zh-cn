---
title: "DENY 非对称密钥权限 (Transact SQL) |Microsoft 文档"
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
- denying permissions [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- DENY statement, asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: dd7d8cd5-536b-460c-ab5b-cb4752bbdfaa
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 386db84b88813109e10d951689868a5c3931cff9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-asymmetric-key-permissions-transact-sql"></a>DENY 非对称密钥权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拒绝对非对称密钥的权限。  
   
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DENY { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
        TO database_principal [ ,...n ]  
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可拒绝授予非对称密钥的权限。 如下所列。  
  
 非对称密钥**::***asymmetric_key_name*  
 指定拒绝将其权限授予他人的非对称密钥。 需要使用作用域限定符“::”。  
  
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
 非对称密钥是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下面列出了可授予非对称密钥的最特定和最受限的权限，以及隐含这些权限的更常用权限。  
  
|非对称密钥权限|非对称密钥权限隐含的权限|数据库权限隐含的权限|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对非对称密钥具有 CONTROL 权限。 如果使用 AS 子句，则指定的主体必须拥有非对称密钥。  
  
## <a name="see-also"></a>另请参阅  
 [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

