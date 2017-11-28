---
title: "sp_revokedbaccess (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs: TSQL
helpviewer_keywords: sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2802cbef18844b9b33b453db661d11c372d3654
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sprevokedbaccess-transact-sql"></a>sp_revokedbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除数据库用户。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md)相反。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>参数  
 [  **@name_in_db =** ] *名称*  
 要删除的数据库用户名称。 *名称*是**sysname**无默认值。 *名称*可以是 Windows 登录名或 Windows 组，服务器登录名的名称，必须存在于当前数据库。 当您指定 Windows 登录或 Windows 组时，请指定其在数据库中所使用的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 删除数据库用户时，依赖于该用户的权限和别名也会删除。  
  
 **sp_revokedbaccess**可以从当前数据库中删除仅数据库用户。 删除在当前数据库中拥有对象的数据库用户之前，您必须转移对象的所有权，或者将这些对象从数据库中删除。 有关详细信息，请参阅[ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 **sp_revokedbaccess**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库具有 ALTER ANY USER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除映射到的数据库用户`Edmonds\LolanSo`从当前数据库。  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [删除用户 &#40;Transact SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
