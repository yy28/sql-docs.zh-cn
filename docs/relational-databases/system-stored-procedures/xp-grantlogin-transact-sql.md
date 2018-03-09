---
title: "xp_grantlogin (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb35af7a2de8fae7d227ea146d2578a73e5c6c28
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授予 Windows 组或用户对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的访问权限。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame =** ] *登录*  
 要添加的 Windows 用户或用户组的名称。 Windows 用户或组必须用在窗体中的 Windows 域名称进行限定*域*\\*用户*。 *登录名*是**sysname**，无默认值。  
  
 [  **@logintype =** ] *logintype*  
 将授予其访问权限的登录名的安全级别。 *logintype*是**varchar(5)**，默认值为 NULL。 仅**管理员**可以指定。 如果**管理员**指定，则*登录*被授予访问权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并添加作为的成员**sysadmin**固定的服务器角色。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **xp_grantlogin**现在系统存储过程而不是扩展存储过程。 **xp_grantlogin**调用**sp_grantlogin**和**sp_addsrvrolemember**。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**securityadmin**固定的服务器角色。 更改时*logintype*，要求的成员身份**sysadmin**固定的服务器角色。  
  
## <a name="see-also"></a>另请参阅  
 [sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [常规扩展存储的过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
