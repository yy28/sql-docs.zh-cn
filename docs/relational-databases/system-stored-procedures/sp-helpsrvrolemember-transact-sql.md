---
title: sp_helpsrvrolemember (TRANSACT-SQL) |Microsoft Docs
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
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4bbc6ed2343b9a659b30b737135c9f28cb2b401b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43035231"
---
# <a name="sphelpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定服务器角色成员的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@srvrolename =** ] **'***角色*****  
 是固定的服务器角色的名称。 *角色*是**sysname**，默认值为 NULL。 如果*角色*未指定，则结果集包含有关所有固定的服务器角色的信息。  
  
 *角色*可以是以下值之一。  
  
|固定的服务器角色|Description|  
|-----------------------|-----------------|  
|sysadmin|系统管理员|  
|securityadmin|安全管理员|  
|serveradmin|服务器管理员|  
|setupadmin|安装程序管理员|  
|processadmin|进程管理员|  
|diskadmin|磁盘管理员|  
|dbcreator|数据库创建者|  
|bulkadmin|可执行 BULK INSERT 语句|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|服务器角色的名称|  
|MemberName|**sysname**|服务器角色的成员的名称|  
|MemberSID|**varbinary(85)**|安全标识符的成员名称|  
  
## <a name="remarks"></a>Remarks  
 Sp_helprolemember 用于显示数据库角色的成员。  
  
 所有登录名都的公共成员。 sp_helpsrvrolemember 无法识别的公共角色，因为在内部，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不实现公共作为角色。  
  
 若要添加或删除的成员，从服务器角色，请参阅[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 sp_helpsrvrolemember 才会作为自变量的用户定义服务器角色。 若要确定用户定义的服务器角色的成员，请参阅中的示例[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将列出 `sysadmin` 固定服务器角色的成员。  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_helprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
