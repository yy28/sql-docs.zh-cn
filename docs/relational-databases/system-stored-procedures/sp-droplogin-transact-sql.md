---
title: sp_droplogin （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplogin
- sp_droplogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplogin
ms.assetid: e58684d1-c394-48de-906e-da6ee91100c3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 07a91b923ffedb2c76cc1140ae3b5a4ee33a8553
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830111"
---
# <a name="sp_droplogin-transact-sql"></a>sp_droplogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 这将阻止使用该登录名对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行访问。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droplogin [ @loginame = ] 'login'  
```  
  
## <a name="arguments"></a>参数  
`[ @loginame = ] 'login'`要删除的登录名。 *login*的**sysname**为，无默认值。 *登录名*必须已存在于中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_droplogin**调用删除登录名。  
  
 不能在用户定义的事务中执行**sp_droplogin** 。  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
 以下示例使用 `DROP LOGIN` 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中删除登录名 `Victoria`。 这是首选方法。  
  
```  
DROP LOGIN Victoria;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
