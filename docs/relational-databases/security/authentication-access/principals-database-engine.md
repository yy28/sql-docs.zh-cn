---
title: "主体（数据库引擎） | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "证书 [SQL Server], 主体"
  - "角色 [SQL Server], 主体"
  - "权限 [SQL Server], 主体"
  - "##MS_SQLAuthenticatorCertificate##"
  - "主体 [SQL Server]"
  - "##MS_SQLResourceSigningCertificate##"
  - "组 [SQL Server], 主体"
  - "##MS_AgentSigningCertificate##"
  - "身份验证 [SQL Server], 主体"
  - "架构 [SQL Server], 主体"
  - "主体 [SQL Server], 关于主体"
  - "安全性 [SQL Server], 主体"
  - "用户 [SQL Server], 主体"
  - "##MS_SQLReplicationSigningCertificate##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 主体（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  “主体” 是可以请求 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源的实体。 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 授权模型的其他组件一样，主体也可以按层次结构排列。 主体的影响范围取决于主体定义的范围（Windows、服务器或数据库）以及主体是否不可分或是一个集合。 例如，Windows 登录名就是一个不可分主体，而 Windows 组则是一个集合主体。 每个主体都具有一个安全标识符 (SID)。  
  
 **Windows 级别的主体**  
  
-   Windows 域登录名  
  
-   Windows 本地登录名  
  
 **SQL Server**- **级的****主体**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名  
  
-   服务器角色  
  
 **数据库级的主体**  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
## SQL Server sa 登录名  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa 登录名是服务器级的主体。 默认情况下，该登录名是在安装实例时创建的。 从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，sa 的默认数据库为“master”。 这是对早期版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的行为的更改。  
  
## public 数据库角色  
 每个数据库用户都属于 public 数据库角色。 当尚未对某个用户授予或拒绝对安全对象的特定权限时，则该用户将继承授予该安全对象的 public 角色的权限。  
  
## INFORMATION_SCHEMA 和 sys  
 每个数据库都包含两个实体：INFORMATION_SCHEMA 和 sys，它们都作为用户出现在目录视图中。 这两个实体是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所必需的。 它们不是主体，不能修改或删除它们。  
  
## 基于证书的 SQL Server 登录名  
 名称由双井号 (##) 括起来的服务器主体仅供内部系统使用。 下列主体是在安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时从证书创建的，不应删除。  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## guest 用户  
 每个数据库包括一个 **guest**。 授予 **guest** 用户的权限由对数据库具有访问权限，但在数据库中没有用户帐户的用户继承。 不能删除 **guest** 用户，但可通过撤消该用户的 **CONNECT** 权限将其禁用。 可以通过在 master 或 tempdb 以外的任何数据库中执行 `REVOKE CONNECT FROM GUEST` 来撤消 **CONNECT** 权限。  
  
## 客户端和数据库服务器  
 根据定义，客户端和数据库服务器是安全主体，可以得到保护。 在建立安全的网络连接前，这些实体之间可以互相进行身份验证。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持 [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758) 身份验证协议，该协议定义客户端与网络身份验证服务交互的方式。  
  
## 相关任务  
 有关设计权限系统的信息，请参阅 [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
 下列主题包括在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书的本节中：  
  
-   [管理登录名、用户和架构操作指南主题](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [服务器级别角色](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [数据库级别的角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [应用程序角色](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## 另请参阅  
 [保护 SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [服务器级别角色](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [数据库级别的角色](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  