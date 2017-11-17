---
title: "拒绝 XML 架构集合权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], XML schema collections
- XML schema collections [SQL Server], permissions
- DENY statement, XML schema collections
- schema collections [SQL Server], permissions
ms.assetid: 159969a7-8313-41bc-bb19-c55af76597e6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d50f055c6dbc419c8a979160f45a884f46f795d6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-xml-schema-collection-permissions-transact-sql"></a>DENY XML 架构集合权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拒绝对 XML 架构集合的权限。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DENY permission  [ ,...n ] ON   
    XML SCHEMA COLLECTION :: [ schema_name . ]  
    XML_schema_collection_name  
    TO <database_principal> [ ,...n ]  
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
 指定可对 XML 架构集合拒绝的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 ON XML 架构集合:: [ *schema_name***。** ] *XML_schema_collection_name*  
 指定要对其拒绝权限的 XML 架构集合。 需要作用域限定符 ::。 如果*schema_name*未指定，则使用默认架构。 如果*schema_name*指定，则是必需的架构范围限定符 （.）。  
  
 到\<database_principal >  
 指定要对其拒绝权限的主体。  
  
 CASCADE  
 指示要拒绝的权限也会被对此主体授予该权限的其他主体拒绝。  
  
 AS \<database_principal >  
 指定一个主体，执行该查询的主体从该主体获得拒绝授予该权限的权利。  
  
 *Database_user*  
 指定数据库用户。  
  
 *Database_role*  
 指定数据库角色。  
  
 *Application_role*  
 指定应用程序角色。  
  
 *Database_user_mapped_to_Windows_User*  
 指定映射到 Windows 用户的数据库用户。  
  
 *Database_user_mapped_to_Windows_Group*  
 指定映射到 Windows 组的数据库用户。  
  
 *Database_user_mapped_to_certificate*  
 指定映射到证书的数据库用户。  
  
 *Database_user_mapped_to_asymmetric_key*  
 指定映射到非对称密钥的数据库用户。  
  
 *Database_user_with_no_login*  
 指定无相应服务器级主体的数据库用户。  
  
## <a name="remarks"></a>注释  
 有关 XML 架构集合的信息会显示在[sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)目录视图。  
  
 XML 架构集合是架构级的安全对象，包含于权限层次结构中作为其父级的架构中。 下表列出了可拒绝的对 XML 架构集合最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|XML 架构集合权限|XML 架构集合权限隐含的权限|架构权限隐含的权限|  
|--------------------------------------|-------------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|在运行 CREATE 语句前执行|CONTROL|在运行 CREATE 语句前执行|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 要求对 XML 架构集合具有 CONTROL 权限。 若要使用 AS 选项，则指定的主体必须拥有 XML 架构集合。  
  
## <a name="examples"></a>示例  
 以下示例拒绝用户 `EXECUTE` 对 XML 架构集合 `Invoices4` 的 `Wanida` 权限。 XML 架构集合 `Invoices4` 位于 `Sales` 数据库的 `AdventureWorks2012` 架构中。  
  
```  
USE AdventureWorks2012;  
DENY EXECUTE ON XML SCHEMA COLLECTION::Sales.Invoices4 TO Wanida;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [授予 XML 架构集合权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)   
 [撤消 XML 架构集合权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)   
 [sys.xml_schema_collections &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)   
 [创建 XML 架构集合 &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

