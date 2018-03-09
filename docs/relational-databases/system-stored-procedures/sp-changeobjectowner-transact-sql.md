---
title: "sp_changeobjectowner (Transact SQL) |Microsoft 文档"
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
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00d4fbb90a767294e3d529e6fa5706eecfd841f1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改当前数据库中对象的所有者。  
  
> [!IMPORTANT]  
>  此存储的过程仅适用于在提供的对象[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)或[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)相反。 **sp_changeobjectowner**更改架构和所有者。 若要保持与早期版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的兼容性，如果当前所有者和新所有者拥有的架构名称与它们的数据库用户名相同，则此存储过程将只更改对象所有者。  
  
> [!IMPORTANT]  
>  已经将新的权限要求添加到此存储过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>参数  
 [  **@objname =** ] *对象*  
 当前数据库中现有表、视图、用户定义函数或存储过程的名称。 *对象*是**nvarchar(776)**，无默认值。 *对象*可以限定与窗体中的现有对象的所有者*existing_owner***。***对象*如果的架构和其所有者具有相同的名称。  
  
 [  **@newowner=**] *所有者*   
 将成为对象的新所有者的安全帐户的名称。 *所有者*是**sysname**，无默认值。 *所有者*必须是有效的数据库用户、 服务器角色， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录名或有权访问当前数据库的 Windows 组。 如果新所有者是没有对应数据库级主体的 Windows 用户或 Windows 组，则将创建数据库用户。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_changeobjectowner**从对象中移除所有的现有权限。 你将需要重新应用任何你想要运行后保留的权限**sp_changeobjectowner**。 因此，我们建议你编写脚本之前运行的现有权限**sp_changeobjectowner**。 更改了对象的所有权之后，便可使用该脚本重新应用权限。 在运行该脚本之前必须在权限脚本中修改对象所有者。  
  
 若要更改安全对象的所有者，请使用 ALTER AUTHORIZATION. 若要更改架构，请使用 ALTER SCHEMA。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**在固定数据库角色或成员资格**db_ddladmin**固定的数据库角色和**db_securityadmin**固定数据库角色并且还控制对象的权限。  
  
## <a name="examples"></a>示例  
 下面的示例更改的所有者`authors`表`Corporate\GeorgeW`。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 架构 &#40;Transact SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
