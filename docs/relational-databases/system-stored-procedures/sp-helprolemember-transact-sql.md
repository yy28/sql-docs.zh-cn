---
title: "sp_helprolemember (TRANSACT-SQL) |Microsoft 文档"
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
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d9b3b1a361b0e079d6c8d8fa844e86ed984fc66
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关当前数据库中某个角色的直接成员的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ]  *角色*   
 当前数据库中的角色的名称。 *角色*是**sysname**，默认值为 NULL。 *角色*必须存在于当前数据库。 如果*角色*未指定，则返回包含从当前数据库的至少一个成员的所有角色。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|当前数据库中角色的名称。|  
|**成员名称**|**sysname**|一个成员的名称**DbRole。**|  
|**MemberSID**|**varbinary(85)**|安全标识符**成员名称。**|  
  
## <a name="remarks"></a>注释  
 如果数据库包含嵌套的角色**MemberName**可能是角色的名称。 **sp_helprolemember**不显示通过嵌套角色的成员身份。 例如，如果 User1 是 Role1 的成员，而 Role1 是 Role2 的成员，则 `EXEC sp_helprolemember 'Role2'` 将返回 Role1，而不是 Role1 的成员（在这个示例中为 User1）。 若要返回嵌套的成员身份，则必须执行**sp_helprolemember**重复为每个嵌套的角色。  
  
 使用**sp_helpsrvrolemember**显示固定的服务器角色的成员。  
  
 使用[IS_ROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-rolemember-transact-sql.md)检查指定的用户角色成员身份。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例显示 `Sales` 角色的成员。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
