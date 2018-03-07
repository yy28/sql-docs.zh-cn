---
title: "创建角色 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cccfc9f6f9810d8f674ea32858e08683160b2ef1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在当前数据库中创建新的数据库角色。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
## <a name="arguments"></a>参数  
 *role_name*  
 待创建角色的名称。  
  
 授权*owner_name*  
 将拥有新角色的数据库用户或角色。 如果未指定用户，则执行 CREATE ROLE 的用户将拥有该角色。  
  
## <a name="remarks"></a>注释  
 角色是数据库级别的安全对象。 在创建角色后，可以使用 GRANT、DENY 和 REVOKE 来配置角色的数据库级权限。 若要将成员添加到数据库角色中，使用[ALTER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md). 有关详细信息，请参阅[数据库级角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
 在 sys.database_role_members 和 sys.database_principals 目录视图中可以查看数据库角色。  
  
 有关设计权限系统的信息，请参阅 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 需要**创建角色**权限中的成员身份的数据库**db_securityadmin**固定的数据库角色。 当你使用**授权**选项，都还需要以下权限：  
  
-   若要将角色的所有权分配给另一个用户，则需要对该用户具有 IMPERSONATE 权限。  
  
-   若要将角色的所有权分配给另一个角色，则需要具有被分配角色的成员身份或对该角色具有 ALTER 权限。  
  
-   若要将角色的所有权分配给应用程序角色，则需要对该应用程序角色具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
所有的以下示例使用 AdventureWorks 数据库。   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. 创建由数据库用户拥有的数据库角色  
 以下示例将创建用户 `buyers` 拥有的数据库角色 `BenMiller`。  
  
```  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. 创建由固定数据库角色拥有的数据库角色  
 以下示例将创建 `auditors` 固定数据库角色拥有的数据库角色 `db_securityadmin`。  
  
```  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER 角色 &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [删除角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


