---
title: "拒绝可用性组的权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/15/2017
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
- permissions [SQL Server], availability group
- DENY statement, availability groups
- denying permissions, [SQL Server], availability groups
ms.assetid: bda60b36-a0b9-4c20-80c1-6a5cb1d638a5
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d2e96c60c2811f0a0a87de3d50e3567cd8655cf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-availability-group-permissions-transact-sql"></a>DENY 可用性组权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  拒绝对中的 Always On 可用性组的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DENY permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
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
 指定可以拒绝的对可用性组的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 可用性组上**::***availability_group_name*  
 指定所拒绝权限的可用性组。 作用域限定符 (**::**) 是必需的。  
  
 到\<server_principal >  
 指定要拒绝权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_Windows_login*  
 指定通过 Windows 登录帐户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_certificate*  
 指定映射到证书的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_AsymKey*  
 指定映射到非对称密钥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 CASCADE  
 指示要拒绝的权限也会被对此主体授予该权限的其他主体拒绝。  
  
 AS *SQL_Server_login*  
 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行此查询的主体从中派生其权限以拒绝的权限的登录名。  
  
## <a name="remarks"></a>注释  
 仅当当前数据库时，服务器范围的权限可能会遭到拒绝**master**。  
  
 有关可用性组的信息会显示在[sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。 有关服务器权限的信息会显示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目录视图，以及有关服务器主体的信息会显示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 可用性组为服务器级安全对象。 下表列出了可拒绝的对可用性组最为具体和有限的权限，以及隐含这些权限的更为通用的权限。  
  
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
  
### <a name="a-denying-view-definition-permission-on-an-availability-group"></a>A. 拒绝可用性组的 VIEW DEFINITION 权限  
 以下示例拒绝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `VIEW DEFINITION` 对可用性组 `MyAg` 的 `ZArifin` 权限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-the-cascade-option"></a>B. 拒绝使用 CASCADE 选项的 TAKE OWNERSHIP 权限  
 以下示例使用 `TAKE OWNERSHIP` 选项来拒绝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户 `MyAg` 对可用性组 `PKomosinski` 的 `CASCADE` 权限。  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [REVOKE 可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [授予可用性组权限 &#40;Transact SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性组目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

