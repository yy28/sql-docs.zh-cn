---
title: "拒绝 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 78bf8698ac1b567abdf4ec0d340d972e2e33002f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  拒绝为主体授予权限。 防止该主体通过组或角色成员身份继承权限。 DENY 的优先于所有权限，但拒绝不适用于对象所有者或 sysadmin 固定的服务器角色的成员。
  **安全说明**Sysadmin 固定服务器角色和对象所有者不能拒绝权限。"
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 该选项不拒绝所有可能权限。 拒绝 ALL 相当于拒绝下列权限。  
  
-   如果安全对象是数据库，则 ALL 对应 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
-   如果安全对象是标量函数，则 ALL 对应 EXECUTE 和 REFERENCES。  
  
-   如果安全对象是表值函数，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全对象是存储过程，则 ALL 表示 EXECUTE。  
  
-   如果安全对象是表，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全对象是视图，则 ALL 对应 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
> [!NOTE]  
>  不推荐使用 DENY ALL 语法。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]应改为拒绝特定权限。  
  
 PRIVILEGES  
 包含此参数是为了符合 ISO 标准。 请不要更改 ALL 的行为。  
  
 *权限*  
 权限的名称。 下面列出的子主题介绍了不同权限与安全对象之间的有效映射。  
  
 *列*  
 指定表中拒绝授予其权限的列名。 需要使用圆括号 ()。  
  
 *类*  
 指定拒绝授予其权限的安全对象的类。 作用域限定符**::**是必需的。  
  
 *安全对象*  
 指定拒绝授予其权限的安全对象。  
  
 到*主体*  
 是主体的名称。 可以对其拒绝安全对象权限的主体随安全对象而异。 有关有效的组合，请参阅下面列出的特定于安全对象的主题。  
  
 CASCADE  
 指示拒绝授予指定主体该权限，同时，对该主体授予了该权限的所有其他主体，也拒绝授予该权限。 当主体具有带 GRANT OPTION 的权限时，为必选项。  
  
 AS*主体*  
  使用 AS 主体子句以指示主体记录的权限 denier 都应当以外的其他人执行语句主体。 例如，假设用户 Mary 是 principal_id 12，并且用户 Raul 为主体 15。 Mary 执行`DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`现在 sys.database_permissions 表将指示的 deny 语句 grantor_prinicpal_id 已 15 (Raul)，即使该语句实际执行了用户 13 (Mary)。
  
使用此语句不意味着能够模拟其他用户。  
  
## <a name="remarks"></a>注释  
 DENY 语句的完整语法很复杂。 上面的语法关系图进行了简化以突出其结构。 下列主题说明了用于拒绝授予特定安全对象的权限的完整语法。  
  
 如果在拒绝为主体授予某种权限时未指定 CASCADE，而之前为该主体授予此权限时指定了 GRANT OPTION，则 DENY 将失败。  
  
 sp_helprotect 系统存储过程可报告对数据库级安全对象的权限。  
  
> [!CAUTION]  
>  表级 DENY 并不优先于列级 GRANT。 保留了权限层次结构中这种不一致性以保持向后兼容。 未来的版本会将其删除。  
  
> [!CAUTION]  
>  拒绝授予数据库 CONTROL 权限将隐式拒绝授予该数据库 CONNECT 权限。 如果拒绝授予某一主体对某一数据库的 CONTROL 权限，该主体将无法连接到该数据库。  
  
> [!CAUTION]  
>  拒绝授予 CONTROL SERVER 权限将隐式拒绝授予对服务器的 CONNECT SQL 权限。 如果拒绝授予某一主体对某一服务器的 CONTROL SERVER 权限，该主体将无法连接到该服务器。  
  
## <a name="permissions"></a>Permissions  
 调用方（或使用 AS 选项指定的主体）必须对安全对象具有 CONTROL 权限，或对该安全对象具有隐含 CONTROL 权限的更高权限。 如果使用 AS 选项，那么指定主体必须拥有其权限被拒绝授予的安全对象。  
  
 被授予 CONTROL SERVER 权限的用户（如 sysadmin 固定服务器角色的成员）可以拒绝对服务器中任何安全对象授予权限。 被授予数据库 CONTROL 权限的用户（如 db_owner 固定数据库角色的成员）可以拒绝对数据库中任何安全对象授予权限。 被授予架构 CONTROL 权限的用户可以拒绝对架构中任何对象授予权限。 如果使用 AS 子句，那么指定主体必须拥有其权限被拒绝授予的安全对象。  
  
## <a name="examples"></a>示例  
 下表列出的安全对象以及描述特定安全对象的语法的主题。  
  
|||  
|-|-|  
|应用程序角色|[DENY 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Assembly|[拒绝程序集权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|非对称密钥|[拒绝非对称密钥权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|可用性组|[拒绝可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|证书|[拒绝证书权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|约定|[拒绝 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|数据库|[DENY 数据库权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|数据库范围的凭据|[拒绝数据库范围的凭据 (Transact SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|端点|[拒绝终结点权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|全文目录|[拒绝的全文权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|全文非索引字表|[拒绝的全文权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|函数|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|登录|[拒绝服务器主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|消息类型|[拒绝 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|对象|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|队列|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|远程服务绑定|[拒绝 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|角色|[DENY 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|路由|[拒绝 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|架构|[DENY 架构权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|搜索属性列表|[拒绝搜索属性列表权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Server|[拒绝服务器权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|服务|[拒绝 Service Broker 权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|存储过程|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|对称密钥|[拒绝非对称密钥权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|同义词|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|系统对象|[拒绝系统对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|表|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|类型|[DENY 类型权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|用户|[DENY 数据库主体权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|视图|[DENY 对象权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|XML 架构集合|[拒绝 XML 架构集合权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>另请参阅  
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
