---
title: "授予可用性组的权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/12/2017
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
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 154c99ddfb9f3a69a4a9eeae35f20c5e9720100d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-availability-group-permissions-transact-sql"></a>GRANT 可用性组权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  授予对 Always On 可用性组的权限。  
  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可以授予的对可用性组的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 可用性组上**::***availability_group_name*  
 指定要授予权限的可用性组。 作用域限定符 (**::**) 是必需的。  
  
 到\<server_principal >  
 指定要对其授予权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_Windows_login*  
 指定通过 Windows 登录帐户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_certificate*  
 指定映射到证书的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_AsymKey*  
 指定映射到非对称密钥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 WITH GRANT OPTION  
 指示该主体还可以向其他主体授予所指定的权限。  
  
 AS *SQL_Server_login*  
 指定执行此查询的主体要从哪个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名派生其授予该权限的权限。  
  
## <a name="remarks"></a>注释  
 仅当当前数据库时，可以授予服务器范围的权限**master**。  
  
 有关可用性组的信息会显示在[sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。 有关服务器权限的信息会显示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目录视图，以及有关服务器主体的信息会显示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 可用性组为服务器级安全对象。 下表列出了可授予的对可用性组最为具体的限定权限，以及隐含这些权限的更为通用的权限。  
  
|可用性组权限|可用性组权限隐含的权限|服务器权限隐含的权限|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 有关所有活动的图表[!INCLUDE[ssDE](../../includes/ssde-md.md)]权限，请参阅[数据库引擎权限海报](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="permissions"></a>Permissions  
 需要对可用性组的 CONTROL 权限或对服务器的 ALTER ANY AVAILABILTIY GROUP 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. 授予对可用性组的 VIEW DEFINITION 权限  
 以下示例将对可用性组 `VIEW DEFINITION` 的 `MyAg` 权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `ZArifin`。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. 使用 GRANT OPTION 授予 TAKE OWNERSHIP 权限  
 以下示例使用 `TAKE OWNERSHIP`，将对可用性组 `MyAg` 的 `PKomosinski` 权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户 `GRANT OPTION`。  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. 授予对可用性组的 CONTROL 权限  
 以下示例将对可用性组 `CONTROL` 的 `MyAg` 权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户 `PKomosinski`。 CONTROL 允许登录名完全控制可用性组，即使它们不是可用性组的所有者。 若要更改的所有权，请参阅[ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [REVOKE 可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [拒绝可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [权限 &#40; 数据库引擎 &#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

