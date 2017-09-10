---
title: "ALTER 角色 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3eaee2d346eda964545caa60cd7168b531f47ad9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  添加或移除成员到或从数据库角色，或更改用户定义的数据库角色的名称。  
  
> [!NOTE]  
>  若要更改中的角色[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_addrolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)和[sp_droprolemember &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *role_name*  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2008年开始，）  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要更改的数据库角色。  
  
 添加成员*database_principal*l  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2012年开始，）  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定将数据库主体添加到数据库角色的成员身份。  
  
-   *database_principal*是数据库用户定义的数据库角色。  
  
-   *database_principal*不能为固定的数据库角色或服务器主体。  
  
删除成员*database_principal*  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2012年开始，）  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要从数据库角色的成员身份中删除数据库主体。  
  
-   *database_principal*是数据库用户定义的数据库角色。  
  
-   *database_principal*不能为固定的数据库角色或服务器主体。  
  
NAME = *new_name*  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2008年开始，）  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要更改用户定义的数据库角色的名称。 新名称必须已存在数据库中。  
  
 更改数据库角色的名称不会更改角色的 ID 号、所有者或权限。  
  
## <a name="permissions"></a>Permissions  
 若要运行此命令需要一个或多个这些权限或成员身份：  
  
-   **ALTER**在角色上的权限  
-   **ALTER ANY ROLE**对数据库拥有权限  
-   中的成员身份**db_securityadmin**固定的数据库角色  
  
此外，若要更改在固定的数据库角色的成员身份你需要：  
  
-   中的成员身份**db_owner**固定的数据库角色  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 无法更改固定的数据库角色的名称。  
  
## <a name="metadata"></a>元数据  
 这些系统视图包含有关数据库角色和数据库主体的信息。  
  
-   [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>示例  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. 更改数据库角色的名称  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2008年开始，）  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 以下示例将角色 `buyers` 的名称更改为 `purchasing`。 [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. 添加或删除角色成员  
 **适用于：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （从 2012年开始，）  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 此示例创建名为的数据库角色`Sales`。 它将添加名 Barry 为成员资格的数据库用户，然后显示如何删除成员 Barry。 [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [删除角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  

