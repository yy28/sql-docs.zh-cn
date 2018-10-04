---
title: 主体（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectroll.f1
- sql12.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6d91a6c21bc162ff1f6100e88101f34a0a275cd8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084547"
---
# <a name="principals-database-engine"></a>主体（数据库引擎）
  “主体” 是可以请求 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源的实体。 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 授权模型的其他组件一样，主体也可以按层次结构排列。 主体的影响范围取决于主体定义的范围（Windows、服务器或数据库）以及主体是否不可分或是一个集合。 例如，Windows 登录名就是一个不可分主体，而 Windows 组则是一个集合主体。 每个主体都具有一个安全标识符 (SID)。  
  
 **Windows 级主体**  
  
-   Windows 域登录名  
  
-   Windows 本地登录名  
  
 **SQL Server**- **主体**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名  
  
-   服务器角色  
  
 **数据库级的主体**  
  
-   数据库用户  
  
-   数据库角色  
  
-   应用程序角色  
  
## <a name="the-sql-server-sa-login"></a>SQL Server sa 登录名  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa 登录名是服务器级的主体。 默认情况下，该登录名是在安装实例时创建的。 从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]开始，sa 的默认数据库为“master”。 这是对早期版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的行为的更改。  
  
## <a name="public-database-role"></a>public 数据库角色  
 每个数据库用户都属于 public 数据库角色。 当尚未对某个用户授予或拒绝对安全对象的特定权限时，则该用户将继承授予该安全对象的 public 角色的权限。  
  
## <a name="informationschema-and-sys"></a>INFORMATION_SCHEMA 和 sys  
 每个数据库都包含两个实体：INFORMATION_SCHEMA 和 sys，它们都作为用户出现在目录视图中。 这两个实体是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所必需的。 它们不是主体，不能修改或删除它们。  
  
## <a name="certificate-based-sql-server-logins"></a>基于证书的 SQL Server 登录名  
 名称由双井号 (##) 括起来的服务器主体仅供内部系统使用。 下列主体是在安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时从证书创建的，不应删除。  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## <a name="the-guest-user"></a>guest 用户  
 每个数据库包括一个 **guest**。 授予 **guest** 用户的权限由对数据库具有访问权限，但在数据库中没有用户帐户的用户继承。 **来宾**不能删除用户，但可以通过撤消该禁用的`CONNECT`权限。 `CONNECT`可以通过执行撤消权限`REVOKE CONNECT FROM GUEST`master 或 tempdb 以外的任何数据库中。  
  
## <a name="client-and-database-server"></a>客户端和数据库服务器  
 根据定义，客户端和数据库服务器是安全主体，可以得到保护。 在建立安全的网络连接前，这些实体之间可以互相进行身份验证。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持[Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758)身份验证协议，定义客户端与网络身份验证服务的交互。  
  
## <a name="related-tasks"></a>Related Tasks  
 下列主题包括在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书的本节中：  
  
-   [管理登录名、用户和架构操作指南主题](managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [服务器级角色](server-level-roles.md)  
  
-   [数据库级别的角色](database-level-roles.md)  
  
-   [应用程序角色](application-roles.md)  
  
## <a name="see-also"></a>请参阅  
 [保护 SQL Server](../securing-sql-server.md)   
 [sys.database_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)   
 [sys.server_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)   
 [sys.sql_logins (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)   
 [sys.database_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)   
 [服务器级别角色](server-level-roles.md)   
 [数据库级别的角色](database-level-roles.md)  
  
  
