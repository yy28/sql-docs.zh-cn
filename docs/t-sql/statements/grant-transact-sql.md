---
title: "GRANT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bb9bf548f042a4a6f41322fb789a2cd7e5b6bec9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为主体授予安全对象的权限。  常规的概念是授予\<某些权限 > ON\<某个对象 > 收件人\<某些用户、 登录名或组 >。 有关权限的一般讨论，请参阅[权限 &#40; 数据库引擎 &#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>参数  
 ALL  
 不推荐使用此选项，保留此选项仅用于向后兼容。 它不会授予所有可能的权限。 授予 ALL 参数相当于授予以下权限。  
  
-   如果安全对象是数据库，则 ALL 对应 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
-   如果安全对象是标量函数，则 ALL 对应 EXECUTE 和 REFERENCES。  
  
-   如果安全对象是表值函数，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全对象是存储过程，则 ALL 表示 EXECUTE。  
  
-   如果安全对象是表，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全对象是视图，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
PRIVILEGES  
 包含此参数是为了符合 ISO 标准。 请不要更改 ALL 的行为。  
  
*权限*  
 权限的名称。 下面列出的子主题介绍了不同权限与安全对象之间的有效映射。  
  
*列*  
 指定表中将授予权限的列的名称。 需要使用圆括号 ()。  
  
*类*  
 指定将授予权限的安全对象的类。 作用域限定符**::**是必需的。  
  
*安全对象*  
 指定将授予权限的安全对象。  
  
到*主体*  
 是主体的名称。 可为其授予安全对象权限的主体随安全对象而异。 有关有效的组合，请参阅下面列出的子主题。  
  
GRANT OPTION  
 指示被授权者在获得指定权限的同时还可以将指定权限授予其他主体。  
  
AS*主体*  
 使用 AS 主体子句以指示主体记录因为权限的授权者应该是以外的其他人执行语句主体。 例如，假设用户 Mary 是 principal_id 12，并且用户 Raul 为主体 15。 Mary 执行`GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`现在 sys.database_permissions 表将指示 grantor_prinicpal_id 已 15 (Raul)，即使该语句实际执行了用户 13 (Mary)。

通常不建议使用 AS 子句的除非您需要显式定义权限链。 有关详细信息，请参阅**的权限检查算法摘要**部分[权限 （数据库引擎）](../../relational-databases/security/permissions-database-engine.md)。

使用此语句不意味着能够模拟其他用户。 
  
## <a name="remarks"></a>注释  
 GRANT 语句的完整语法非常复杂。 上面的语法关系图进行了简化以突出其结构。 下面列出的主题介绍了在授予特定安全对象权限时使用的完整语法。  
  
 REVOKE 语句可用于删除已授予的权限，DENY 语句可用于防止主体通过 GRANT 获得特定权限。  
  
 授予权限将删除对所指定安全对象的相应权限的 DENY 或 REVOKE 权限。 如果在包含该安全对象的更高级别拒绝了相同的权限，则 DENY 优先。 但是，在更高级别撤消已授予权限的操作并不优先。  
  
 数据库级权限在指定的数据库范围内授予。 如果用户需要另一个数据库中的对象的权限，请在该数据库中创建用户帐户，或者授权用户帐户访问该数据库以及当前数据库。  
  
> [!CAUTION]  
>  表级 DENY 并不优先于列级 GRANT。 保留了权限层次结构中这种不一致性以保持向后兼容。 未来的版本会将其删除。  
  
 sp_helprotect 系统存储过程可报告对数据库级安全对象的权限。  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 **授予**... **使用 GRANT OPTION**指定接收权限的安全主体给定授予对其他安全帐户的指定的权限的能力。 当接收权限的主体是角色还是 Windows 组， **AS**对象权限的用户不是组或角色的成员授予可以进一步在需要时，必须使用子句。 由于只有的用户，而不是组或角色，可以执行**授予**语句、 组或角色的特定成员必须使用**AS**子句显式时要调用的角色或组成员身份授予权限。 下面的示例演示如何**WITH GRANT OPTION**时授予角色或 Windows 组使用。  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 权限图表  
 有关 pdf 格式的所有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 权限的海报大小的图表，请参阅 [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="permissions"></a>Permissions  
 授权者（或用 AS 选项指定的主体）必须具有带 GRANT OPTION 的相同权限，或具有隐含所授予权限的更高权限。 如果使用 AS 选项，则还应满足其他要求。 有关详细信息，请参阅特定于安全对象的主题。  
  
 对象所有者可以授予对其所拥有的对象的权限。 对某安全对象具有 CONTROL 权限的主体可以授予对该安全对象的权限。  
  
 被授予 CONTROL SERVER 权限的用户（例如，sysadmin 固定服务器角色的成员）可以授予对相应服务器中任一个安全对象的任意权限。 将某一数据库的 CONTROL 权限授予用户（例如，db_owner 固定数据库角色的成员）后，该用户就可授予对该数据库中任何一个安全对象的任意权限。 被授权 CONTROL 权限的用户可以授予对相应架构中任一个对象的任意权限。  
  
## <a name="examples"></a>示例  
 下表列出的安全对象以及描述特定安全对象的语法的主题。  
  
|||  
|-|-|  
|应用程序角色|[GRANT 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Assembly|[程序集授予权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|非对称密钥|[授予非对称密钥权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|可用性组|[授予可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|证书|[授予证书权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|约定|[授予 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|数据库|[GRANT 数据库权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|数据库范围的凭据|[授予数据库范围的凭据 (Transact SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|端点|[GRANT 终结点权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|全文目录|[GRANT Full-text 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|全文非索引字表|[GRANT Full-text 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|函数|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|登录|[授予服务器主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|消息类型|[授予 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|对象|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|队列|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|远程服务绑定|[授予 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|角色|[GRANT 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|路由|[授予 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|架构|[GRANT 架构权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|搜索属性列表|[授予搜索属性列表权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Server|[GRANT 服务器权限 (Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|服务|[授予 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|存储过程|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|对称密钥|[授予非对称密钥权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|同义词|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|系统对象|[GRANT 系统对象权限 (Transact-SQL)](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|表|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|类型|[GRANT 类型权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|用户|[GRANT 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|视图|[GRANT 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML 架构集合|[授予 XML 架构集合权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

