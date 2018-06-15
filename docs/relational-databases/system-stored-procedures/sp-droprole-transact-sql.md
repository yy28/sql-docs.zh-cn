---
title: sp_droprole (TRANSACT-SQL) |Microsoft 文档
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
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 39ef6031494b8e5bd4718c26d7635be4f916517e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263402"
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除数据库角色。  
  
> [!IMPORTANT]  
>  在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_droprole** DROP ROLE 语句替换为。 **sp_droprole**包含仅针对与早期版本的兼容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和可能不支持的未来版本中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] *****角色*****  
 要从当前数据库中删除的数据库角色的名称。 *角色*是**sysname**，无默认值。 *角色*必须已存在于当前数据库。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 可以使用删除仅数据库角色**sp_droprole**。  
  
 不能删除带有现有成员的数据库角色。 必须删除数据库角色的所有成员，然后才能删除该数据库角色。 若要从角色中删除用户，使用**sp_droprolemember**。 如果任何用户仍是角色的成员**sp_droprole**显示这些成员。  
  
 固定角色的成员和**公共**无法删除角色。  
  
 如果角色拥有任何安全对象，则不能将其删除。 在删除拥有安全对象的应用程序角色之前，必须首先移交安全对象的所有权或将其删除。 使用 ALTER AUTHORIZATION 更改必须删除的对象的所有者。  
  
 **sp_droprole**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>权限  
 需要对角色具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例删除应用程序角色 `Sales`。  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE (Transact-SQL)](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
