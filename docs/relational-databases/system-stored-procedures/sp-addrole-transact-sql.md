---
title: "sp_addrole (TRANSACT-SQL) |Microsoft 文档"
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
- sp_addrole
- sp_addrole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 070e1d0e71b49689e547dc29300bf5a5476d17ec
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在当前数据库中创建新的数据库角色。  
  
> [!IMPORTANT]  
>  **sp_addrole**包含是为了与早期版本的兼容性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和可能不支持的未来版本中。 使用[创建角色](../../t-sql/statements/create-role-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] *角色*  
 新数据库角色的名称。 *角色*是**sysname**，无默认值。 *角色*必须是有效的标识符 (ID) 和当前数据库中不必须已存在。  
  
 [  **@ownername =**] *所有者*  
 新数据库角色的所有者。 *所有者*是**sysname**，默认值为当前正在执行的用户。 *所有者*必须是数据库用户或当前数据库中的数据库角色。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库角色的名称可以包含 1 到 128 个字符，包括字母、符号和数字。 数据库角色的名称不能： 包含反斜杠字符 (\\)、 为 NULL，或空字符串 (**'**)。  
  
 添加数据库角色后，使用[sp_addrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)将主体添加到角色。 当使用 GRANT、DENY 或 REVOKE 语句将权限应用于数据库角色时，数据库角色的成员将继承这些权限，就好像将权限直接应用于其帐户一样。  
  
> [!NOTE]  
>  不能创建新服务器角色。 只能在数据库级别上创建角色。  
  
 **sp_addrole**不在用户定义的事务内使用。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库具有 CREATE ROLE 权限。 如果创建架构，则需要对数据库的 CREATE SCHEMA 权限。 如果*所有者*指定为用户或组，该用户或组将需要模拟。 如果*所有者*指定作为角色，需要在该角色或在该角色的成员上拥有 ALTER 权限。 如果将所有者指定为应用程序角色，则需要对此应用程序角色的 ALTER 权限。  
  
## <a name="examples"></a>示例  
 以下示例向当前数据库中添加名为 `Managers` 的新角色。  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE (Transact-SQL)](../../t-sql/statements/create-role-transact-sql.md)  
  
  
