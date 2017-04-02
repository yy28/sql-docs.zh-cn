---
title: "凭据（数据库引擎） | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "主体 [SQL Server]，凭据"
  - "架构 [SQL Server]，凭据"
  - "权限 [SQL Server]，凭据"
  - "组 [SQL Server]，凭据"
  - "ALTER ANY CREDENTIAL 权限"
  - "安全性 [SQL Server]，凭据"
  - "身份验证 [SQL Server]，凭据"
  - "用户 [SQL Server]，凭据"
  - "凭据 [SQL Server]，关于凭据"
  - "凭据 [SQL Server]"
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 凭据（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  凭据是包含连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 外部资源所需的身份验证信息（凭据）的记录。 此信息由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在内部使用。 大多凭据都包含一个 Windows 用户名和密码。  
  
 利用凭据中存储的信息，通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证方式连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用户可以访问服务器实例外部的资源。 如果外部资源为 Windows，则此用户将作为在凭据中指定的 Windows 用户通过身份验证。 单个凭据可映射到多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。 但是，一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名只能映射到一个凭据。  
  
 有关存储在 master 数据库中且可在整个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中使用的凭据，请参阅 [CREATE CREDENTIAL (Transact-SQL)](../../../t-sql/statements/create-credential-transact-sql.md)。 有关特定数据库使用的且可提供该数据库移植的凭据，请参阅 [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。  
  
 系统凭据是自动创建的，并与特定端点关联， 系统凭据名以两个哈希符号 (##) 开头。  
  
 有关凭据的详细信息，请参阅 [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) 和 [sys.database_credentials (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md) 目录视图。  
  
## 相关内容  
 [创建凭据](../../../relational-databases/security/authentication-access/create-a-credential.md) [CREATE CREDENTIAL (Transact SQL)](../../../t-sql/statements/create-credential-transact-sql.md) [CREATE DATABASE SCOPED CREDENTIAL (Transact SQL)](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
  
 [保护 SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  