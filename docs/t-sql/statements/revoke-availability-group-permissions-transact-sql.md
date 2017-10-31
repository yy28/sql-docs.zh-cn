---
title: "REVOKE 可用性组的权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
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
- Availability Groups [SQL Server], permissions
- REVOKE statement, availability groups
- revoking permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 02c77378-a36d-4286-9235-d8867a2b92ad
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1573f866cec3105cde4eeab59c230ede46144ac3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-availability-group-permissions-transact-sql"></a>REVOKE 可用性组权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  撤消对 Always On 可用性组的权限。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON AVAILABILITY GROUP :: availability_group_name  
    { FROM | TO } < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可以撤消的对可用性组的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 可用性组上**::***availability_group_name*  
 指定要撤消权限的可用性组。 作用域限定符 (**::**) 是必需的。  
  
 {从 |为} \<server_principal > 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要向其撤消权限的登录名。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_Windows_login*  
 指定通过 Windows 登录帐户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_certificate*  
 指定映射到证书的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_AsymKey*  
 指定映射到非对称密钥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 GRANT OPTION  
 指示要撤消向其他主体授予指定权限的权限。 不会撤消该权限本身。  
  
> [!IMPORTANT]  
>  如果主体具有不带 GRANT 选项的指定权限，则将撤消该权限本身。  
  
 CASCADE  
 指示要撤消的权限也会从此主体授予或拒绝该权限的其他主体中撤消。  
  
> [!IMPORTANT]  
>  如果对授予了 WITH GRANT OPTION 权限的权限执行级联撤消，将同时撤消该权限的 GRANT 和 DENY 权限。  
  
 AS *SQL_Server_login*  
 指定执行此查询的主体从哪个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名派生其撤消该权限的权限。  
  
## <a name="remarks"></a>注释  
 仅当当前数据库时，可以吊销服务器范围的权限**master**。  
  
 有关可用性组的信息会显示在[sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。 有关服务器权限的信息会显示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目录视图，以及有关服务器主体的信息会显示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 可用性组为服务器级安全对象。 下表列出了可撤消的对可用性组最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|可用性组权限|可用性组权限隐含的权限|服务器权限隐含的权限|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要对可用性组的 CONTROL 权限或对服务器的 ALTER ANY AVAILABILTIY GROUP 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-revoking-view-definition-permission-on-an-availability-group"></a>A. 撤消对可用性组的 VIEW DEFINITION 权限  
 以下示例从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `VIEW DEFINITION` 撤消对可用性组 `MyAg` 的 `ZArifin` 权限。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade"></a>B. 使用 CASCADE 撤消 TAKE OWNERSHIP 权限  
 以下示例从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户 `TAKE OWNERSHIP` 以及 `MyAg` 授予对 MyAg 的 TAKE OWNERSHIP 权限的所有主体撤消对可用性组 `PKomosinski` 的 `PKomosinski` 权限。  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
### <a name="c-revoking-a-previously-granted-with-grant-option-clause"></a>C. 撤消以前授予的 WITH GRANT OPTION 子句  
 如果使用 WITH GRANT OPTION 授予了权限，用于撤消授予选项... 若要删除 WITH GRANT OPTION。 以下示例授予权限，然后删除权限的 WITH GRANT 部分。  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
REVOKE GRANT OPTION FOR CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski  
CASCADE  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [授予可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [拒绝可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


