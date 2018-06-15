---
title: sp_denylogin (TRANSACT-SQL) |Microsoft 文档
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
- sp_denylogin_TSQL
- sp_denylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_denylogin
ms.assetid: db80f152-e8af-4303-95b6-3a3a7b664374
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ef296a57b8fec029695654e5e519b723b455b59f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33241835"
---
# <a name="spdenylogin-transact-sql"></a>sp_denylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  防止 Windows 用户或 Windows 组连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_denylogin [ @loginame = ] 'login'   
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame =** ] *** * * 登录*   
 是 Windows 用户或组的名称。 *登录名*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_denylogin**拒绝对映射到指定的 Windows 用户或 Windows 组的服务器级别主体 CONNECT SQL 权限。 如果服务器主体不存在，将创建它。 新的主体就会出现在[sys.server_principals &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 **sp_denylogin**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何使用**sp_denylogin**以防 Windows 用户`CORPORATE\GeorgeV`从连接到服务器。  
  
```  
EXEC sp_denylogin 'CORPORATE\GeorgeV';  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
