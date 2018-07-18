---
title: sp_adduser (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4f7afe6646fd22ff24aa6aee4e5dcde416420e9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036095"
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向当前数据库中添加新的用户。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE USER](../../t-sql/statements/create-user-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@loginame =** ] **'***login***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录或 Windows 登录的名称。 *登录名*是**sysname**，无默认值。 *登录名*必须是现有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或 Windows 登录名。  
  
 [  **@name_in_db =** ] **'***用户*****  
 新数据库用户的名称。 *用户*是**sysname**，默认值为 NULL。 如果*用户*未指定，则新的数据库用户的名称默认为*登录名*名称。 指定*用户*为新用户提供不同的服务器级别登录名从数据库中的名称。  
  
 [  **@grpname =** ] **'***角色*****  
 新用户成为其成员的数据库角色。 *角色*是**sysname**，默认值为 NULL。 *角色*必须是当前数据库中的有效的数据库角色。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_adduser**还将创建一个架构具有的用户的名称。  
  
 在添加完用户之后，可以使用 GRANT、DENY 和 REVOKE 等语句来定义控制用户所执行的活动的权限。  
  
 使用**sys.server_principals**以显示有效登录名的列表。  
  
 使用**sp_helprole**显示有效的角色名称的列表。 当指定一个角色时，用户会自动地获得那些为该角色定义的权限。 如果不指定角色，用户将获得默认授予的权限**公共**角色。 若要将用户添加到角色，为值*用户名*必须提供。 (*用户名*可以是与相同*login_id*。)  
  
 用户**来宾**每个数据库中已存在。 添加用户**来宾**将启用此用户，如果之前处于禁用状态。 默认情况下，用户**来宾**在新数据库中禁用。  
  
 **sp_adduser**不能在用户定义的事务内执行。  
  
 无法添加**来宾**用户由于**来宾**每个数据库中已存在的用户。 若要启用**来宾**用户，授予**来宾**CONNECT 权限所示：  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>权限  
 要求具有数据库的所有权。  
  
## <a name="examples"></a>示例  
  
### <a name="a-adding-a-database-user"></a>A. 添加数据库用户  
 以下示例使用现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `Vidur`，将数据库用户 `Recruiting` 添加到当前数据库中的现有 `Vidur` 角色。  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. 添加数据库用户（使用相同的登录 ID）  
 以下示例将用户 `Arvind` 添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `Arvind` 的当前数据库。 此用户归属的默认值**公共**角色。  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. 添加数据库用户（使用不同于其服务器级别登录名的名称）  
 以下示例将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `BjornR` 添加到具有用户名 `Bjorn` 的当前数据库，并将数据库用户 `Bjorn` 添加到 `Production` 数据库角色。  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
