---
title: "创建服务器角色 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 445c44ad009ff9bd6509d077f5f579d0f7f42855
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  创建新的用户定义的服务器角色。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
## <a name="arguments"></a>参数  
 *role_name*  
 待创建的服务器角色的名称。  
  
 授权*server_principal*  
 将拥有新服务器角色的登录名。 如果未指定登录名，则执行 CREATE SERVER ROLE 的登录名将拥有该服务器角色。  
  
## <a name="remarks"></a>注释  
 服务器角色是服务器级别的安全对象。 创建服务器角色后，使用 GRANT、DENY 和 REVOKE 配置角色的服务器级别权限。 若要添加到的登录名或从服务器角色中删除登录名，请使用[ALTER SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md). 若要删除服务器角色，使用[DROP SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md). 有关详细信息，请参阅 [ys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
 你可以通过查询查看服务器角色[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)和[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目录视图。  
  
 不能向服务器角色授予对数据库级安全对象的权限。 若要创建数据库角色，请参阅 [CREATE ROLE (Transact-SQL)](../../t-sql/statements/create-role-transact-sql.md)。  
  
 有关设计权限系统的信息，请参阅 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
## <a name="permissions"></a>Permissions  
 要求具有 CREATE SERVER ROLE 权限，或者 sysadmin 固定服务器角色中的成员身份。  
  
 还需要针对登录名的 *server_principal* 的 IMPERSONATE 权限、针对用作 *server_principal*的服务器角色的 ALTER 权限或用作 server_principal 的 Windows 组的成员身份。  
  
 这将触发 Audit Server Principal Management 事件与要添加的对象类型设置为服务器角色和事件类型。  
  
 使用 AUTHORIZATION 选项分配服务器角色所有权时，还需要具有下列权限：  
  
-   若要将服务器角色的所有权分配给另一个登录名，则需要对该登录名具有 IMPERSONATE 权限。  
  
-   若要将服务器角色的所有权分配给另一个服务器角色，则需要具有被分配服务器角色的成员身份或对该服务器角色具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>A. 创建由登录名拥有的服务器角色  
 以下示例将创建一个由登录名 `buyers` 拥有的服务器角色 `BenMiller`。  
  
```  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>B. 创建由固定服务器角色拥有的服务器角色  
 以下示例将创建一个由 `auditors` 固定服务器角色拥有的服务器角色 `securityadmin`。  
  
```  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [删除服务器角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  

