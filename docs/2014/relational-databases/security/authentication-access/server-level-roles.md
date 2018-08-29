---
title: 服务器级别角色 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.Security.BUILTIN.administrators
- sql12.Security.NT_AUTHORITY.SYSTEM
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 87bbf94aa898d19a8f3a96d059644848ce95a298
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43035307"
---
# <a name="server-level-roles"></a>服务器级别角色
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供服务器级角色以帮助你管理服务器上的权限。 这些角色是可组合其他主体的安全主体。 服务器级角色的权限作用域为服务器范围。 （“角色”类似于 Windows 操作系统中的“组”。）  
  
 提供固定服务器角色是为了方便使用和向后兼容。 应尽可能分配更具体的权限。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了九种固定服务器角色。 无法更改授予固定服务器角色的权限。 从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]开始，您可以创建用户定义的服务器角色，并将服务器级权限添加到用户定义的服务器角色。  
  
 你可以将服务器级主体（[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名、Windows 帐户和 Windows 组）添加到服务器级角色。 固定服务器角色的每个成员都可以将其他登录名添加到该同一角色。 用户定义的服务器角色的成员则无法将其他服务器主体添加到角色。  
  
## <a name="fixed-server-level-roles"></a>服务器级的固定角色  
 下表显示了服务器级的固定角色及其权限。  
  
|服务器级的固定角色|Description|  
|------------------------------|-----------------|  
|sysadmin|sysadmin 固定服务器角色的成员可以在服务器上执行任何活动。|  
|serveradmin|serveradmin 固定服务器角色的成员可以更改服务器范围的配置选项和关闭服务器。|  
|securityadmin|securityadmin 固定服务器角色的成员可以管理登录名及其属性。 他们可以 GRANT、DENY 和 REVOKE 服务器级别的权限。 他们还可以 GRANT、DENY 和 REVOKE 数据库级权限（如果他们具有数据库的访问权限）。 此外，他们还可以重置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名的密码。<br /><br /> **\*\* 安全说明 \*\*** 能够授予 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的访问权限和配置用户权限的能力使得安全管理员可以分配大多数服务器权限。 `securityadmin`角色应视为等效于`sysadmin`角色。|  
|processadmin|processadmin 固定服务器角色的成员可以终止在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例中运行的进程。|  
|setupadmin|固定服务器角色的成员可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句添加和删除链接服务器。 （在使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]时需要 sysadmin 成员资格。）|  
|bulkadmin|bulkadmin 固定服务器角色的成员可以运行 BULK INSERT 语句。|  
|diskadmin|diskadmin 固定服务器角色用于管理磁盘文件。|  
|dbcreator|dbcreator 固定服务器角色的成员可以创建、更改、删除和还原任何数据库。|  
|public|每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名都属于 public 服务器角色。 如果未向某个服务器主体授予或拒绝对某个安全对象的特定权限，该用户将继承授予该对象的 public 角色的权限。 只有在希望所有用户都能使用对象时，才在对象上分配 Public 权限。 你无法更改具有 Public 角色的成员身份。<br /><br /> 注意：public 角色的实现方式与其他角色不同。 但是，可以从 public 授予、拒绝或撤销权限。|  
  
## <a name="permissions-of-fixed-server-roles"></a>固定服务器角色的权限  
 每个固定服务器角色都被分配了特定的权限。 有关分配给服务器角色的权限的图表，请参阅 [数据库引擎固定服务器和固定数据库角色](http://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx)。  
  
> [!IMPORTANT]  
>  `CONTROL SERVER`权限是类似但不是等同于`sysadmin`固定的服务器角色。 权限并不表示角色成员身份，并且角色成员身份不会授予权限。 （例如， `CONTROL SERVER` 不表示 `sysadmin` 固定服务器角色的成员身份。）但是，有时可在角色和相等的权限之间模拟。 大多数 `DBCC` 命令和许多系统过程要求 `sysadmin` 固定服务器角色的成员身份。 有关列表的 171 个系统存储过程的要求`sysadmin`成员身份，请参阅 Andreas Wolter 的以下博文[CONTROL SERVER 与 sysadmin/sa： 权限、 系统过程、 DBCC、 自动架构创建和特权升级-注意事项](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats)。  
  
## <a name="server-level-permissions"></a>服务器级权限  
 只能向用户定义的服务器角色中添加服务器级权限。 若要列出服务器级权限，请执行下面的语句。 服务器级权限如下：  
  
```tsql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 有关权限的详细信息，请参阅[权限（数据库引擎）](../permissions-database-engine.md) 和 [sys.fn_builtin_permissions (Tansact SQL)](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)。  
  
## <a name="working-with-server-level-roles"></a>使用服务器级角色  
 下表介绍了可以用于服务器级角色的命令、视图和功能。  
  
|功能|类型|Description|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql)|元数据|返回服务器级角色的列表。|  
|[sp_helpsrvrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql)|元数据|返回有关服务器级角色成员的信息。|  
|[sp_srvrolepermission (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql)|元数据|显示服务器级角色的权限。|  
|[IS_SRVROLEMEMBER (Transact-SQL)](/sql/t-sql/functions/is-srvrolemember-transact-sql)|元数据|指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名是否为指定服务器级角色的成员。|  
|[sys.server_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)|元数据|为每个服务器级角色的每个成员返回一行。|  
|[sp_addsrvrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql)|Command|将登录名添加为某个服务器级角色的成员。 不推荐使用。 应改用 [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) 。|  
|[sp_dropsrvrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql)|Command|从服务器级角色中删除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名或 Windows 用户或组。 不推荐使用。 应改用 [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) 。|  
|[CREATE SERVER ROLE (Transact-SQL)](/sql/t-sql/statements/create-server-role-transact-sql)|Command|创建用户定义的服务器角色。|  
|[ALTER SERVER ROLE (Transact-SQL)](/sql/t-sql/statements/alter-server-role-transact-sql)|Command|更改服务器角色的成员关系或更改用户定义的服务器角色的名称。|  
|[DROP SERVER ROLE (Transact-SQL)](/sql/t-sql/statements/drop-server-role-transact-sql)|Command|删除用户定义的服务器角色。|  
|[IS_SRVROLEMEMBER (Transact-SQL)](/sql/t-sql/functions/is-srvrolemember-transact-sql)|函数|确定服务器角色的成员关系。|  
  
## <a name="see-also"></a>请参阅  
 [数据库级别的角色](../authentication-access/database-level-roles.md)   
 [安全性目录视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)   
 [安全函数 (Transact-SQL)](/sql/t-sql/functions/security-functions-transact-sql)   
 [保护 SQL Server](../securing-sql-server.md)   
 [授予服务器主体权限 (Transact-SQL)](/sql/t-sql/statements/grant-server-principal-permissions-transact-sql)   
 [撤消服务器主体权限 (Transact-SQL)](/sql/t-sql/statements/revoke-server-principal-permissions-transact-sql)   
 [拒绝服务器主体权限 (Transact-SQL)](/sql/t-sql/statements/deny-server-principal-permissions-transact-sql)   
 [创建服务器角色](../authentication-access/create-a-server-role.md)  
  
  
