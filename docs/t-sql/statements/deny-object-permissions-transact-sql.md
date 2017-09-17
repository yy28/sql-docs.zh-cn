---
title: "DENY 对象权限 (Transact SQL) |Microsoft 文档"
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
- DENY statement, objects
- table permissions [SQL Server]
ms.assetid: 0b8d3ddc-38c0-4241-b7bb-ee654a5081aa
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2655a796d6d097cb635576313664ea6bfa7162db
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-object-permissions-transact-sql"></a>DENY 对象权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拒绝对安全对象的 OBJECT 类成员授予的权限。 OBJECT 类的成员包括：表、视图、表值函数、存储过程、扩展存储过程、标量函数、聚合函数、服务队列以及同义词。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DENY <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        TO <database_principal> [ ,...n ]   
    [ CASCADE ]  
        [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
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
 指定可对架构包含的对象拒绝的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 ALL  
 拒绝 ALL 不会拒绝所有可能的权限。 拒绝 ALL 等同于拒绝适用于指定对象的所有 ANSI-92 权限。 对于不同权限，ALL 的含义有所不同：  
  
 - 标量函数权限：EXECUTE、REFERENCES。  
 - 表值函数权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
 - 存储过程的权限： 执行。  
 - 表权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
 - 视图权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
PRIVILEGES  
 包含此参数以符合 ANSI-92 标准。 请不要更改 ALL 的行为。  
  
*列*  
 指定表、视图或表值函数中要对其拒绝权限的列的名称。 括号**（)**所需。 仅可以拒绝对列的 SELECT、REFERENCES 和 UPDATE 权限。 *列*可以权限子句中或安全对象的名称后指定。  
  
> [!CAUTION]  
>  表级 DENY 并不优先于列级 GRANT。 保留了权限层次结构中的这种不一致性以保持向后兼容。  
  
 ON [对象**::** ] [ *schema_name* ] **。** *object_name*  
 指定在其拒绝的权限的对象。 是可选的对象短语如果*schema_name*指定。 如果使用对象短语，则作用域限定符 (**::**) 是必需的。 如果*schema_name*未指定，则使用默认架构。 如果*schema_name*指定，则架构作用域限定符 (**。**) 是必需的。  
  
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
 可以在各种目录视图中查看对象的有关信息。 有关详细信息，请参阅[对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 对象是一个架构级的安全对象，包含于权限层次结构中作为其父级的架构中。 下表列出了可拒绝的对对象最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|对象权限|对象权限隐含的权限|架构权限隐含的权限|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|DELETE|CONTROL|DELETE|  
|在运行 CREATE 语句前执行|CONTROL|在运行 CREATE 语句前执行|  
|Insert|CONTROL|Insert|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对对象的 CONTROL 权限。  
  
 如果使用 AS 子句，则指定的主体必须拥有要对其拒绝权限的对象。  
  
## <a name="examples"></a>示例  
下面的示例使用 AdventureWorks 数据库。
  
### <a name="a-denying-select-permission-on-a-table"></a>A. 拒绝对表的 SELECT 权限  
 下面的示例拒绝`SELECT`对用户权限`RosaQdM`表`Person.Address`。  
  
```  
DENY SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-denying-execute-permission-on-a-stored-procedure"></a>B. 拒绝对存储过程的 EXECUTE 权限  
 以下示例拒绝名为 `EXECUTE` 的应用程序角色对存储过程 `HumanResources.uspUpdateEmployeeHireInfo` 的 `Recruiting11` 权限。  
  
```  
DENY EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-denying-references-permission-on-a-view-with-cascade"></a>C. 使用 CASCADE 拒绝对视图的 REFERENCES 权限  
 以下示例使用 `REFERENCES`，拒绝用户 `BusinessEntityID` 对视图 `HumanResources.vEmployee` 中列 `Wanida` 的 `CASCADE` 权限。  
  
```  
DENY REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [REVOKE 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

