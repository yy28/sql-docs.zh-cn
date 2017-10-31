---
title: "拒绝服务器主体权限 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/09/2017
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
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15be2bfb51e6cdd9d111f052c62838c3326c61b5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deny-server-principal-permissions-transact-sql"></a>拒绝服务器主体权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  拒绝为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名授予的权限。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>参数  
 *权限*  
 指定可对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名拒绝的权限。 有关权限的列表，请参阅本主题后面的“备注”部分。  
  
 登录名**::** *SQL_Server_login*  
 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在其拒绝的权限的登录名。 作用域限定符 (**::**) 是必需的。  
  
 服务器角色**::** *server_role*  
 指定要拒绝权限的服务器角色。 作用域限定符 (**::**) 是必需的。  
  
 到\<server_principal >  
 指定要授予权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或服务器角色。  
  
 到*SQL_Server_login*  
 指定要拒绝权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_Windows_login*  
 指定通过 Windows 登录帐户创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_certificate*  
 指定映射到证书的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *SQL_Server_login_from_AsymKey*  
 指定映射到非对称密钥的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的名称。  
  
 *server_role*  
 指定服务器角色的名称。  
  
 CASCADE  
 指示要拒绝的权限也会被对此主体授予该权限的其他主体拒绝。  
  
 AS *SQL_Server_login*  
 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行此查询的主体从中派生其权限以拒绝的权限的登录名。  
  
## <a name="remarks"></a>注释  
 只有在当前数据库为 master 时，才可拒绝其服务器范围内的权限。  
  
 中提供了有关服务器权限的信息[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目录视图。 中提供了有关服务器主体的信息[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 如果你将向主体授予该权限使用 GRANT OPTION 拒绝权限时未指定 CASCADE，DENY 语句将失败。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和服务器角色是服务器级安全对象。 下表列出了可为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或服务器角色拒绝的最具体的限定权限，以及隐含这些权限的更一般的权限。  
  
|SQL Server 登录名或服务器角色权限|SQL Server 登录名或服务器角色权限隐含的权限|服务器权限隐含的权限|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissions  
 对于登录名，要求具有登录名的 CONTROL 权限或服务器上的 ALTER ANY LOGIN 权限。  
  
 对于服务器角色，要求具有服务器角色的 CONTROL 权限或服务器上的 ALTER ANY SERVER ROLE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. 拒绝登录名的 IMPERSONATE 权限  
 下面的示例拒绝`IMPERSONATE`权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录`WanidaBenshoof`到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名从 Windows 用户创建`AdvWorks\YoonM`。  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. 使用 CASCADE 拒绝 VIEW DEFINITION 权限  
 以下示例拒绝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `VIEW DEFINITION` 对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `EricKurjan` 的 `RMeyyappan` 权限。 `CASCADE` 选项指示还会拒绝 `VIEW DEFINITION` 授予 `EricKurjan` 权限的主体对 `RMeyyappan` 的该权限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. 拒绝服务器角色的 VIEW DEFINITION 权限  
 以下示例拒绝 `VIEW DEFINITION` 和 `Sales` 服务器角色的  `Auditors` 权限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [授予服务器主体权限 (Transact-SQL)](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [撤消服务器主体权限 (Transact-SQL)](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

