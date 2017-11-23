---
title: "sp_helprole (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helprole_TSQL
- sp_helprole
dev_langs: TSQL
helpviewer_keywords: sp_helprole
ms.assetid: b023103f-ccf3-44e2-b418-4be9bdd49f4a
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a912cb79346ea35e7da110ed336138231e28ee1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelprole-transact-sql"></a>sp_helprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回当前数据库中有关角色的信息。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helprole [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] *角色*  
 当前数据库中的角色的名称。 *角色*是**sysname**，默认值为 NULL。 *角色*必须存在于当前数据库。 如果*角色*是未指定，返回有关当前数据库中的所有角色的信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**RoleName**|**sysname**|当前数据库中角色的名称。|  
|**RoleId**|**int**|ID **RoleName**。|  
|**IsAppRole**|**int**|0 = **RoleName**不是应用程序角色。<br /><br /> 1 = **RoleName**是应用程序角色。|  
  
## <a name="remarks"></a>注释  
 若要查看与角色关联的权限，请使用**sp_helprotect**。 若要查看数据库角色的成员，请使用**sp_helprolemember**。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下查询将返回当前数据库中的所有角色。  
  
```  
EXEC sp_helprole  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [服务器级别角色](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [sp_addapprole &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_addrole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [sp_droprole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
