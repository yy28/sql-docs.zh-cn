---
title: "sp_dropsrvrolemember (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc66cffd56d8eebf31f50ce784be407292261b89
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从固定服务器角色中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 Windows 用户或组。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>参数  
 [ @loginame  **=**  ] *登录*  
 要从固定服务器角色中删除的登录名。 *登录名*是**sysname**，无默认值。 *登录名*必须存在。  
  
 [ @rolename  **=**  ] *角色*  
 服务器角色的名称。 *角色*是**sysname**，默认值为 NULL。 *角色*必须是以下值之一：  
  
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
  
## <a name="remarks"></a>注释  
 仅 sp_dropsrvrolemember 可用来从固定的服务器角色中删除登录名。 Sp_droprolemember 用于从数据库角色中删除成员。  
  
 无法从任何固定的服务器角色中删除 sa 登录名。  
  
 sp_dropsrvrolemember 不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求上 sysadmin 固定服务器角色或这两个 ALTER ANY LOGIN 权限的服务器和角色正在从中删除成员的成员身份的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例从 `JackO` 固定服务器角色中删除登录 `sysadmin`。  
  
```  
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建服务器角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [删除服务器角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
