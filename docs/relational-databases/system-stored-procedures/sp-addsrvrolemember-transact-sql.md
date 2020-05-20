---
title: sp_addsrvrolemember （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab49a6572bfe8b2879b832642eeb1cf692177bb6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833641"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加登录名以作为固定服务器角色的成员。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>参数  
 [ @loginame **=** ] **"**_login_**"**  
 将添加到固定服务器角色中的登录名。 *login*的**sysname**为，无默认值。 *登录*名可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 Windows 登录名。 如果还没有为 Windows 登录名授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问权限，则会自动授予该访问权限。  
  
 [ @rolename **=** ] **"**_role_**"**  
 要添加登录名的固定服务器角色的名称。 *role*的数据值为**sysname**，默认值为 NULL，必须是下列值之一：  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 在将登录名添加到固定服务器角色时，该登录名将获得与该角色相关的权限。  
  
 不能更改 sa 登录和 public 的角色成员身份。  
  
 请使用 sp_addrolemember 将成员添加到固定数据库角色或用户定义的角色。  
  
 不能在用户定义的事务内执行 sp_addsrvrolemember。  
  
## <a name="permissions"></a>权限  
 需要具有要添加新成员的角色中的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例将 Windows 登录名添加 `Corporate\HelenS` 到 `sysadmin` 固定服务器角色。  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全功能 &#40;Transact-sql&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [&#40;Transact-sql&#41;创建服务器角色](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE (Transact-SQL)](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
