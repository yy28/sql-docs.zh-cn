---
title: 安全对象 | Microsoft Docs
ms.custom: ''
ms.date: 10/14/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7c4a82cfa4d8a82db1e01c49899c3c49c2e01ee9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745716"
---
# <a name="securables"></a>安全对象
  安全对象是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 授权系统控制对其进行访问的资源。 例如，表是安全对象。 通过创建可以为自己设置安全性的名为“范围”的嵌套层次结构，可以将某些安全对象包含在其他安全对象中。 安全对象范围有 **服务器**、 **数据库**和 **架构**。  
  
## <a name="securable-scope-server"></a>安全对象范围：“服务器”  
 **服务器** 安全对象范围包含以下安全对象：  
  
-   可用性组 (availability group)  
  
-   端点  
  
-   登录  
  
-   服务器角色  
  
-   “数据库”  
  
## <a name="securable-scope-database"></a>安全对象范围：“数据库”  
 **数据库** 安全对象范围包含以下安全对象：  
  
-   应用程序角色  
  
-   Assembly  
  
-   非对称密钥  
  
-   证书  
  
-   约定  
  
-   全文目录  
  
-   全文非索引字表  
  
-   消息类型  
  
-   远程服务绑定  
  
-   （数据库）角色  
  
-   路由  
  
-   架构  
  
-   搜索属性列表  
  
-   服务  
  
-   对称密钥  
  
-   “用户”  
  
## <a name="securable-scope-schema"></a>安全对象范围：架构  
 **架构** 安全对象范围包含以下安全对象：  
  
-   类型  
  
-   XML 架构集合  
  
-   对象 - 对象类包含以下成员：  
  
    -   Aggregate  
  
    -   函数  
  
    -   过程  
  
    -   队列  
  
    -   同义词  
  
    -   表  
  
    -   “查看”  
  
## <a name="controlling-access-to-a-securable"></a>控制对安全对象的访问  
 接收对安全对象的权限的实体称为主体。 最常见的主体是登录名和数据库用户。 对安全对象的访问通过授予或拒绝权限进行控制，或者通过将登录名和用户添加到有权访问的角色进行控制。 有关控制权限的信息，请参阅 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)、[REVOKE (Transact-SQL)](/sql/t-sql/statements/revoke-transact-sql)、[DENY (Transact-SQL)](/sql/t-sql/statements/deny-transact-sql)、[sp_addrolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) 和 [sp_droprolemember (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)。  
  
> [!CAUTION]  
>  安装期间授予系统对象的默认权限已针对可能的威胁进行了仔细评估，并且作为强化 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装的一部分，无需进行更改。 对系统对象权限的任何更改都可能限制或破坏功能，并且可能让你的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装处于不受支持的状态。  
  
## <a name="related-content"></a>相关内容  
 [保护 SQL Server](securing-sql-server.md)  
  
 [sys.database_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)  
  
 [sys.database_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)  
  
 [sys.server_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)  
  
 [sys.server_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)  
  
 [sys.sql_logins (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)  
  
  
