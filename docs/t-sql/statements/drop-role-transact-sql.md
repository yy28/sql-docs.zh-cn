---
title: "删除角色 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ROLE
- DROP_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting roles
- database roles [SQL Server], removing
- removing roles
- DROP ROLE statement
- roles [SQL Server], removing
- dropping roles
ms.assetid: 1f6f13ae-56a2-4ef1-93f5-8e6151b83e1d
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: 86266835ec5d54ce08bdf7fe18d93dd9d4de1737
ms.contentlocale: zh-cn
ms.lasthandoff: 10/07/2017

---
# <a name="drop-role-transact-sql"></a>DROP ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  从数据库中删除角色。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
DROP ROLE [ IF EXISTS ] role_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP ROLE role_name  
```  
  
## <a name="arguments"></a>参数  
 *如果存在*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 仅当它已存在，则有条件地删除角色。  
  
 *role_name*  
 指定要从数据库删除的角色。  
  
## <a name="remarks"></a>注释  
 无法从数据库删除拥有安全对象的角色。 若要删除拥有安全对象的数据库角色，必须首先转移这些安全对象的所有权，或从数据库删除它们。 无法从数据库删除拥有成员的角色。 若要删除拥有成员的角色，必须首先删除角色的成员。  
  
 若要从数据库角色中删除成员，请使用[ALTER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md).  
  
 不能使用 DROP ROLE 删除固定数据库角色。  
  
 在 sys.database_role_members 目录视图中可以查看有关角色成员身份的信息。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 若要删除服务器角色，使用[DROP SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY ROLE**对数据库拥有权限或**控件**权限的角色，或中的成员身份**db_securityadmin**。  
  
## <a name="examples"></a>示例  
 下面的示例删除数据库角色`purchasing`从`AdventureWorks2012`数据库。  
  
```  
DROP ROLE purchasing;  
GO  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [创建角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER 角色 &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  



