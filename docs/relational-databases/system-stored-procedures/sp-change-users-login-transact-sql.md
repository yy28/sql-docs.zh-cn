---
title: sp_change_users_login (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 065126113e8914d1f22959bbfacc3e341d8855c8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spchangeuserslogin-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将现有数据库用户映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER USER](../../t-sql/statements/alter-user-transact-sql.md)相反。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ @Action=] '*操作*  
 描述过程要执行的操作。 *操作*是**varchar(10)**。 *操作*可以具有以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**Auto_Fix**|将当前数据库的 sys.database_principals 系统目录视图中的用户项链接到同名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果不存在同名的登录名，将会创建一个。 检查的结果**Auto_Fix**语句以确认事实上进行了正确的链接。 避免使用**Auto_Fix**在安全敏感的情况下。<br /><br /> 当你使用**Auto_Fix**，必须指定*用户*和*密码*如果不存在登录名，否则你必须指定*用户*但*密码*将被忽略。 *登录名*必须为 NULL。 *用户*必须是当前数据库中的有效用户。 不能将另一个用户映射到该登录名。|  
|**报告**|列出当前数据库中未链接到任何登录名的用户以及相应的安全标识符 (SID)。 *用户*，*登录*，和*密码*必须为 NULL 或未指定。<br /><br /> 若要将替换为一个查询使用的系统表报表选项，比较中的条目**sys.server_prinicpals**与中的条目**sys.database_principals**。|  
|**Update_One**|链接指定*用户*到一个现有当前数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*登录*。 *用户*和*登录*必须指定。 *密码*必须为 NULL 或未指定。|  
  
 [ @UserNamePattern=] '*用户*  
 当前数据库中的用户名。 *用户*是**sysname**，默认值为 NULL。  
  
 [ @LoginName=] '*登录*  
 是的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。 login 的数据类型为 sysname，默认值为 NULL。  
  
 [ @Password= ] '*password*'  
 是分配给一个新的密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过指定创建的登录名**Auto_Fix**。 如果已存在匹配的登录名，映射的用户和登录名和*密码*将被忽略。 如果不存在匹配的登录名，创建一个新 sp_change_users_login[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，并将分配*密码*为新登录名的密码。 *密码*是**sysname**，而且不能为 NULL。  
  
> **重要说明!!** 始终使用[强密码 ！](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|数据库用户名。|  
|UserSID|**varbinary(85)**|用户的安全标识符。|  
  
## <a name="remarks"></a>注释  
 使用 sp_change_users_login 将当前数据库中的数据库用户链接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果用户登录名已更改，则使用 sp_change_users_login 将用户链接到新的登录，而不会丢失用户的权限。 新*登录*不能为 sa，和*用户*不能为 dbo、 guest 或 INFORMATION_SCHEMA 用户。  
  
 sp_change_users_login 不能用于将数据库用户映射到 Windows 级主体、证书或非对称密钥。  
  
 sp_change_users_login 不能与通过 Windows 主体创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名一起使用，也不能与使用 CREATE USER WITHOUT LOGIN 创建的用户一起使用。  
  
 不能在用户定义的事务中执行 sp_change_users_login。  
  
## <a name="permissions"></a>权限  
 要求具有 db_owner 固定数据库角色中的成员资格。 只有 sysadmin 固定的服务器角色的成员可以指定**Auto_Fix**选项。  
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 显示当前用户与登录名的映射的报告  
 下例生成当前数据库中的用户及其安全标识符 (SID) 的报告。  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. 将数据库用户映射到新的 SQL Server 登录名  
 在以下示例中，数据库用户与新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名关联。 数据库用户 `MB-Sales` 首先映射到另一个登录名，然后重新映射到登录名 `MaryB`。  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. 自动将用户映射到登录名（必要时新建一个登录名）  
 以下示例显示如何使用 `Auto_Fix` 将现有用户映射到同名的登录名，以及如何在不存在登录名 `Mary` 的情况下，创建密码为 `B3r12-3x$098f6` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `Mary`。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
