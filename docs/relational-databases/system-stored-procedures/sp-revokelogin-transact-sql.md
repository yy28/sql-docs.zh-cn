---
title: sp_revokelogin (TRANSACT-SQL) |Microsoft 文档
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
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0d59e993563b340b7016887720fb8f3638dca247
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除相应的登录条目从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为 Windows 用户或组创建通过使用 CREATE LOGIN、 **sp_grantlogin**，或**sp_denylogin**。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame=**] *****登录*****  
 Windows 用户或用户组的名称。 *登录名*是**sysname**，无默认值。 *登录名*可以是任何现有的 Windows 用户名或组的形式*计算机名称*\\*用户或域*\\*用户*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_revokelogin**禁用使用指定的帐户的连接*登录*参数。 但通过 Windows 组中的成员身份被授权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 Windows 用户在其单独访问权限被撤消后仍可作为组来连接。 同样，如果*登录*参数指定 Windows 组的名称，该组的成员已单独授予访问权限的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]仍将能够连接。  
  
 例如，如果 Windows 用户**ADVWORKS\john**是 Windows 组的成员**ADVWORKS\Admins**，和**sp_revokelogin**撤消的访问权限`ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 用户**ADVWORKS\john**仍然可以连接，如果**ADVWORKS\Admins**已被授予访问权限的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 同样，如果 Windows 组**ADVWORKS\Admins**已吊销其访问权限但**ADVWORKS\john**授予访问权限， **ADVWORKS\john**仍然可以连接。  
  
 使用**sp_denylogin**要显式防止用户连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不管其 Windows 组成员身份。  
  
 **sp_revokelogin**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除的 Windows 用户的登录条目`Corporate\MollyA`。  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 或  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN & #40;Transact SQL & #41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
