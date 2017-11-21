---
title: "REVOKE 对象权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table permissions [SQL Server], revoking
- REVOKE statement, objects
- revoking permissions to access tables
- object permissions [SQL Server], revoking
ms.assetid: 99c7146e-d2e7-4f1a-80ff-21a05bc5e8bb
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8895f85a3484258ee68f40e8d2261206fd16d0a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-object-permissions-transact-sql"></a>REVOKE 对象权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤消表、视图、表值函数、存储过程、扩展存储过程、标量函数、聚合函数、服务队列或同义词的权限。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        { FROM | TO } <database_principal> [ ,...n ]   
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
 指定可对架构包含的对象撤消的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 ALL  
 撤消 ALL 不会撤消所有可能的权限。 撤消 ALL 等同于撤消适用于指定对象的所有 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 权限。 对于不同权限，ALL 的含义有所不同：  
  
 标量函数权限：EXECUTE、REFERENCES。  
  
 表值函数权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
 存储过程的权限： 执行。  
  
 表权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
 视图权限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
 PRIVILEGES  
 包含此参数以符合 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 标准。 请不要更改 ALL 的行为。  
  
 *列*  
 指定表、视图或表值函数中要对其撤消权限的列的名称。 括号 （） 是必需的。 仅可以拒绝对列的 SELECT、REFERENCES 和 UPDATE 权限。 *列*可以权限子句中或安全对象的名称后指定。  
  
 ON [对象::] [ *schema_name* ]。 *object_name*  
 指定要在其撤消权限的对象。 是可选的对象短语如果*schema_name*指定。 如果使用了 OBJECT 短语，则需要作用域限定符 (::)。 如果*schema_name*未指定，则使用默认架构。 如果*schema_name*指定，则是必需的架构范围限定符 （.）。  
  
 {从 |为} \<database_principal > 指定要从中撤消权限的主体。  
  
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
 可以在各种目录视图中查看对象的有关信息。 有关详细信息，请参阅[对象目录视图 & #40;Transact SQL & #41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 对象是一个架构级的安全对象，包含于权限层次结构中作为其父级的架构中。 下表列出了可撤消的对对象最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
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
  
 如果使用 AS 子句，则指定的主体必须拥有要对其撤消权限的对象。  
  
## <a name="examples"></a>示例  
  
### <a name="a-revoking-select-permission-on-a-table"></a>A. 撤消对表的 SELECT 权限  
 以下示例从用户 `SELECT` 中撤消对 `RosaQdM` 数据库中表 `Person.Address` 的 `AdventureWorks2012` 权限。  
  
```  
USE AdventureWorks2012;  
REVOKE SELECT ON OBJECT::Person.Address FROM RosaQdM;  
GO  
```  
  
### <a name="b-revoking-execute-permission-on-a-stored-procedure"></a>B. 撤消对存储过程的 EXECUTE 权限  
 以下示例从名为 `EXECUTE` 的应用程序角色中撤消对存储过程 `HumanResources.uspUpdateEmployeeHireInfo` 的 `Recruiting11` 权限。  
  
```  
USE AdventureWorks2012;  
REVOKE EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    FROM Recruiting11;  
GO   
```  
  
### <a name="c-revoking-references-permission-on-a-view-with-cascade"></a>C. 使用 CASCADE 撤消对视图的 REFERENCES 权限  
 以下示例使用 `REFERENCES`，从用户 `BusinessEntityID` 中撤消对视图 `HumanResources.vEmployee` 中列 `Wanida` 的 `CASCADE` 权限。  
  
```  
USE AdventureWorks2012;  
REVOKE REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    FROM Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [DENY 对象权限 (Transact-SQL)](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [对象目录视图 & #40;Transact SQL & #41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions & #40;Transact SQL & #41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  


