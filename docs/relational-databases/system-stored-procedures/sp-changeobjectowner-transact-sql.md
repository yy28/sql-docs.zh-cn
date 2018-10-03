---
title: sp_changeobjectowner (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 30ae865060ff3d667de8f18c6d73f4b7087f0780
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707695"
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改当前数据库中对象的所有者。  
  
> [!IMPORTANT]  
>  此存储的过程仅适用于在提供的对象[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)或[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)相反。 **sp_changeobjectowner**更改架构和所有者。 若要保持与早期版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的兼容性，如果当前所有者和新所有者拥有的架构名称与它们的数据库用户名相同，则此存储过程将只更改对象所有者。  
  
> [!IMPORTANT]  
>  已经将新的权限要求添加到此存储过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>参数  
 [  **@objname =** ] **'***对象*****  
 当前数据库中现有表、视图、用户定义函数或存储过程的名称。 *对象*是**nvarchar(776)**，无默认值。 *对象*可使用的窗体中的现有对象所有者限定*existing_owner ***。*** 对象*如果架构及其所有者具有相同的名称。  
  
 [  **@newowner=**] **' * * * 所有者*   
 将成为对象的新所有者的安全帐户的名称。 *所有者*是**sysname**，无默认值。 *所有者*必须是有效的数据库用户、 服务器角色、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录名或 Windows 组有权访问当前数据库。 如果新所有者是没有对应数据库级主体的 Windows 用户或 Windows 组，则将创建数据库用户。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_changeobjectowner**从对象中移除所有现有权限。 必须重新应用任何你想要运行后保留的权限**sp_changeobjectowner**。 因此，我们建议你在运行之前的现有权限编写脚本**sp_changeobjectowner**。 更改了对象的所有权之后，便可使用该脚本重新应用权限。 在运行该脚本之前必须在权限脚本中修改对象所有者。  
  
 若要更改安全对象的所有者，请使用 ALTER AUTHORIZATION. 若要更改架构，请使用 ALTER SCHEMA。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**固定数据库角色或成员身份，在这种**db_ddladmin**固定的数据库角色并**db_securityadmin**固定数据库角色此外，还可以控制对象的权限。  
  
## <a name="examples"></a>示例  
 下面的示例更改的所有者`authors`表到`Corporate\GeorgeW`。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [ALTER SCHEMA (Transact-SQL)](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
