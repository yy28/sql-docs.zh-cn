---
title: sp_revokelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 57c7ef9242b6c974c8043f8f6ab237b0fbe07941
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706647"
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除从相应登录名的条目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 用户或通过使用 CREATE LOGIN、 创建组**sp_grantlogin**，或**sp_denylogin**。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>参数  
 [  **@loginame=**] **'***登录*****  
 Windows 用户或用户组的名称。 *登录名*是**sysname**，无默认值。 *登录名*可以是任何现有 Windows 用户名或组的形式*计算机名*\\*用户或域*\\*用户*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_revokelogin**禁用使用指定的帐户的连接*登录名*参数。 但通过 Windows 组中的成员身份被授权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 Windows 用户在其单独访问权限被撤消后仍可作为组来连接。 同样，如果*登录名*参数指定 Windows 组的名称，已被分别该组的成员授予访问权限的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]仍将能够连接。  
  
 例如，如果 Windows 用户**ADVWORKS\john**是 Windows 组的成员**ADVWORKS\Admins**，并**sp_revokelogin**吊销的访问权限的`ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 用户**ADVWORKS\john**仍然可以连接如果**ADVWORKS\Admins**已被授予访问权限的一个实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 同样，如果 Windows 组**ADVWORKS\Admins**已撤消其访问权限，但**ADVWORKS\john**授予访问权限， **ADVWORKS\john**仍然可以连接。  
  
 使用**sp_denylogin**若要显式阻止用户连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而不考虑其 Windows 组成员身份。  
  
 **sp_revokelogin**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
 以下示例删除 Windows 用户的登录项`Corporate\MollyA`。  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 或  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN (Transact-SQL)](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
