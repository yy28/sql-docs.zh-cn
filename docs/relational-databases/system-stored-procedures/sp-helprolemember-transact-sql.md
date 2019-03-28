---
title: sp_helprolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 547ac1bce010e1f25eb2fce178844ff2b3f77bd1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526939"
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
`[ @rolename = ] ' role '` 是当前数据库中的名称。 *角色* 是 **sysname** ，默认值为 NULL。 *角色*必须存在于当前数据库。 如果*角色*中未指定，则返回包含从当前数据库的至少一个成员的所有角色。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|当前数据库中角色的名称。|  
|**MemberName**|**sysname**|成员的名称**数据库角色。**|  
|**MemberSID**|**varbinary(85)**|安全标识符**成员名称。**|  
  
## <a name="remarks"></a>备注  
 如果数据库包含嵌套的角色， **MemberName**可能是角色的名称。 **sp_helprolemember**不显示通过嵌套角色获取的成员身份。 例如，如果 User1 是 Role1 的成员，而 Role1 是 Role2 的成员，则 `EXEC sp_helprolemember 'Role2'` 将返回 Role1，而不是 Role1 的成员（在这个示例中为 User1）。 若要返回嵌套的成员身份，必须执行**sp_helprolemember**重复的每个嵌套角色。  
  
 使用**sp_helpsrvrolemember**显示固定的服务器角色的成员。  
  
 使用[IS_ROLEMEMBER &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md)若要检查的指定用户角色成员身份。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例显示 `Sales` 角色的成员。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
