---
title: "拒绝程序集的权限 (Transact SQL) |Microsoft 文档"
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
- assemblies [CLR integration], permissions
- DENY statement, assemblies
- denying permissions [SQL Server], assemblies
ms.assetid: be0896b3-f793-44c9-9390-1c6e58f33b2b
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64a2f7f80cdcf654d295e49535bb61f8ada0b41b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-assembly-permissions-transact-sql"></a>DENY 程序集权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拒绝对程序集的权限。  
  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DENY { permission [ ,...n ] } ON ASSEMBLY :: assembly_name  
    TO database_principal [ ,...n ]   
        [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可拒绝授予程序集的权限。 如下所列。  
  
 程序集上**::***程序集 _ 名称*  
 指定拒绝将其权限授予他人的程序集。 需要使用作用域限定符“::”。  
  
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
 程序集是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下面列出了可拒绝授予程序集的最特定和最受限的权限，以及隐含这些权限的更常用权限。  
  
|程序集权限|程序集权限隐含的权限|数据库权限隐含的权限|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对程序集具有 CONTROL 权限。 如果使用 AS 选项，则指定的主体必须拥有程序集。  
  
## <a name="see-also"></a>另请参阅  
 [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [创建应用程序角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [创建程序集 &#40;Transact SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

