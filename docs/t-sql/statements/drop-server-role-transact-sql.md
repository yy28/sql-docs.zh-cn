---
title: "删除服务器角色 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SERVER ROLE
- DROP_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, DROP
- DROP SERVER ROLE statement
ms.assetid: a2a1e6e6-e40c-4d6a-81be-d197b80bf226
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c493ed6556bde690f6b4a9ec6b46aeb3ceb59ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  删除用户定义的服务器角色。  
  
 用户定义的服务器角色是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中的新增角色。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>参数  
 *role_name*  
 指定要从服务器中删除的用户定义的服务器角色。  
  
## <a name="remarks"></a>注释  
 无法从服务器中删除拥有安全对象的用户定义服务器角色。 若要删除拥有安全对象的用户定义服务器角色，必须先转移这些安全对象的所有权或删除这些安全对象。  
  
 无法删除拥有成员的用户定义服务器角色。 若要删除具有成员的用户定义的服务器角色，你必须首先删除角色的成员使用[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 无法删除固定服务器角色。  
  
 你可以通过查询来查看有关角色成员身份的信息[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)目录视图。  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器角色的 CONTROL 权限或 ALTER ANY SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-to-drop-a-server-role"></a>A. 删除服务器角色  
 以下示例删除服务器角色 `purchasing`。  
  
```  
DROP SERVER ROLE purchasing;  
GO  
```  
  
### <a name="b-to-view-role-membership"></a>B. 查看角色成员身份  
 若要查看角色成员身份，使用**服务器角色 (成员**) 页中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或执行以下查询：  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
### <a name="c-to-view-role-membership"></a>C. 查看角色成员身份  
 若要确定服务器角色是否拥有其他服务器角色，请执行以下查询：  
  
```  
SELECT SP1.name AS RoleOwner, SP2.name AS Server_Role  
FROM sys.server_principals AS SP1  
JOIN sys.server_principals AS SP2  
    ON SP1.principal_id = SP2.owning_principal_id   
ORDER BY SP1.name ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 角色 &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [创建角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [删除角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  

