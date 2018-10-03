---
title: sp_droprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77c642d6b1574006122af74f0538cdb7ef607535
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620805"
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除数据库角色。  
  
> [!IMPORTANT]  
>  在中[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_droprole**由 DROP ROLE 语句取代。 **sp_droprole**只是为了与早期版本的兼容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在将来的版本中可能不支持。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] **'***角色*****  
 要从当前数据库中删除的数据库角色的名称。 *角色*是**sysname**，无默认值。 *角色*必须已存在于当前数据库。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 只有数据库角色可以通过使用移除**sp_droprole**。  
  
 不能删除带有现有成员的数据库角色。 必须删除数据库角色的所有成员，然后才能删除该数据库角色。 若要从角色中删除用户，请使用**sp_droprolemember**。 如果任何用户仍是该角色的成员**sp_droprole**显示这些成员。  
  
 固定角色的成员以及**公共**不能删除角色。  
  
 如果角色拥有任何安全对象，则不能将其删除。 在删除拥有安全对象的应用程序角色之前，必须首先移交安全对象的所有权或将其删除。 使用 ALTER AUTHORIZATION 更改必须删除的对象的所有者。  
  
 **sp_droprole**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 需要对角色具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例删除应用程序角色 `Sales`。  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE (Transact-SQL)](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
