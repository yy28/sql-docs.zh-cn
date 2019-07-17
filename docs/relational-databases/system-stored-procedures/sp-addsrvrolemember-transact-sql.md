---
title: sp_addsrvrolemember (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c927bdff462922d1846188366fbb92ce0d3663c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022426"
---
# <a name="spaddsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加登录名以作为固定服务器角色的成员。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>参数  
 [ @loginame **=** ] **'** _登录_   
 将添加到固定服务器角色中的登录名。 *登录名* 是 **sysname** ，无默认值。 *登录名*可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或 Windows 登录名。 如果还没有为 Windows 登录名授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问权限，则会自动授予该访问权限。  
  
 [ @rolename **=** ] **'** _角色_   
 要添加登录名的固定服务器角色的名称。 *角色*是**sysname**，默认值为 NULL，并且必须是下列值之一：  
  
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
  
 无法更改 sa 登录名和公共角色成员身份。  
  
 使用 sp_addrolemember 将成员添加到固定的数据库角色或用户定义的角色。  
  
 不能在用户定义的事务内执行 sp_addsrvrolemember。  
  
## <a name="permissions"></a>权限  
 需要具有要添加新成员的角色中的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例添加的 Windows 登录名`Corporate\HelenS`到`sysadmin`固定的服务器角色。  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE (Transact-SQL)](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE (Transact-SQL)](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
