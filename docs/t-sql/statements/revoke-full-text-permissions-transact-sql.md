---
title: "撤消全文权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- REVOKE statement, full-text permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
ms.assetid: ef617436-1e86-4573-900a-702e27a202b9
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66e9cfe5b6a7b9c191dd82262a4751c966b09949
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="revoke-full-text-permissions-transact-sql"></a>REVOKE 全文权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  撤消全文目录或全文非索引字表权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>参数  
 GRANT OPTION FOR  
 指示要撤消向其他主体授予指定权限的权限。 不会撤消该权限本身。  
  
> [!IMPORTANT]  
>  如果主体具有不带 GRANT 选项的指定权限，则将撤消该权限本身。  
  
 *权限*  
 权限的名称。 本主题后面的“备注”部分中介绍了不同权限与安全对象之间的有效映射。  
  
 对全文目录**::***完整 text_catalog_name*  
 指定对其撤消权限的全文目录。 作用域限定符**::**是必需的。  
  
 全文非索引字表上**::***完整 text_stoplist_name*  
 指定要对其撤消权限的全文非索引字表。 作用域限定符**::**是必需的。  
  
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
  
## <a name="fulltext-catalog-permissions"></a>FULLTEXT CATALOG 权限  
 全文目录是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下表列出了可撤消的对全文目录最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|全文目录权限|全文目录权限隐含的权限|数据库权限隐含的权限|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>FULLTEXT STOPLIST 权限  
 全文非索引字表是一个数据库级的安全对象，包含于权限层次结构中作为其父级的数据库中。 下表列出了可撤消的对全文非索引字表最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|全文非索引字表权限|全文非索引字表权限隐含的权限|数据库权限隐含的权限|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对全文目录的 CONTROL 权限。  
  
## <a name="see-also"></a>另请参阅  
 [创建应用程序角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [创建 FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [创建全文非索引字表 &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT Full-text 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fulltext_catalogs &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
