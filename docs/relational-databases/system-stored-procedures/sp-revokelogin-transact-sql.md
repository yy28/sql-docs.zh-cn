---
title: sp_revokelogin （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 95598885a80b1f697f5e1287e22c1048e737ba6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944725"
---
# <a name="sp_revokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]删除使用 CREATE login、 **sp_grantlogin**或**sp_denylogin**创建的 Windows 用户或组的登录项。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>参数  
`[ @loginame = ] 'login'`Windows 用户或组的名称。 *login*的**sysname**为，无默认值。 *登录*名可以是任何现有 Windows 用户名或*计算机名为计算机名*\\*用户或域*\\*用户*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_revokelogin**使用*login*参数指定的帐户禁用连接。 但通过 Windows 组中的成员身份被授权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 Windows 用户在其单独访问权限被撤消后仍可作为组来连接。 同样，如果*login*参数指定了 Windows 组的名称，则该组的成员被单独授予对实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问权限仍然能够连接。  
  
 例如，如果 Windows 用户**ADVWORKS\john**是 windows 组**ADVWORKS\Admins**的成员，并且**sp_revokelogin**吊销`ADVWORKS\john`以下内容的访问权限：  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 如果**ADVWORKS\Admins**已被授予对实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]访问权限，则用户**ADVWORKS\john**仍可以连接。 同样，如果 Windows 组**ADVWORKS\Admins**已撤消其访问权限，但授予**ADVWORKS\john**访问权限，则**ADVWORKS\john**仍可连接。  
  
 使用**sp_denylogin**显式阻止用户连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而不考虑其 Windows 组成员身份。  
  
 不能在用户定义的事务中执行**sp_revokelogin** 。  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除 Windows 用户`Corporate\MollyA`的登录项。  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 或  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
