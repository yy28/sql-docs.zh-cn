---
title: "sp_helpsrvrole (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
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
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs: TSQL
helpviewer_keywords: sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2761187daca8724b7674454cece7a6d0199973d9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定服务器角色的列表。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@srvrolename=** ] *角色*  
 固定服务器角色的名称。 *角色*是**sysname**，默认值为 NULL。 *角色*可以是以下值之一。  
  
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
|Description|**sysname**|服务器角色的说明|  
  
## <a name="remarks"></a>注释  
 固定服务器角色在服务器级上定义，这些角色具有执行特定服务器级管理活动的权限。 不能添加、删除或更改固定服务器角色。  
  
 若要添加或移除的成员的服务器角色，请参阅[ALTER SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 所有登录名是公共的成员。 sp_helpsrvrole 无法识别 public 角色，因为，在内部，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不实现公共作为角色。  
  
 sp_helpsrvrole 将不会作为自变量的用户定义的服务器角色。 若要列出的用户定义的服务器角色，请参阅中的示例[ALTER SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. 列出固定服务器角色  
 以下查询返回固定服务器角色的列表。  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. 列出固定和用户定义的服务器角色  
 以下查询返回固定和用户定义服务器角色的列表。  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. 返回固定服务器角色的说明  
 以下查询返回 `diskadmin` 固定服务器角色的名称和说明。  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [服务器级别角色](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
