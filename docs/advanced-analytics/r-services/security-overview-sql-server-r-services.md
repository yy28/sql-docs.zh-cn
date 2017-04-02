---
title: "安全性概述 (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# 安全性概述 (SQL Server R Services)

本主题介绍用于连接的整体安全体系结构 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎和相关的组件到 R 运行时。 为在企业环境中使用 R 的两个常见的情况提供了安全过程的示例︰

+ 执行在 RevoScaleR 函数 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 从数据科学客户端
+ 运行直接从 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用存储的过程

## 安全性概述

一个 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 登录名或 Windows 用户帐户运行所需使用的所有 R 作业 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 登录名或用户帐户标识 *安全主体*, ，用户必须具有运行 R 的数据库的访问权，以及从受保护的对象，如表、 读取数据或将新数据写入或添加新对象，如果 R 作业所需的权限。

因此，很严格的要求，每个运行的 R 代码人员针对 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 必须映射到在数据库中，无论该代码从一个远程数据科学客户端使用 RevoScaleR 函数发送还是使用 T-SQL 存储过程启动的登录名。 

例如，假设您创建了一些在您的便携式计算机运行的 R 代码，并且想要在上运行该代码 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 您必须确保满足以下条件︰

+ 数据库将允许远程连接。
+ SQL 登录名的名称和在 R 代码中使用的密码与已添加到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 在实例级别。 或者，如果使用 Windows 集成身份验证，必须为该实例上的用户添加的连接字符串中指定的 Windows 用户。
+ SQL 登录名或 Windows 用户必须授予执行外部脚本的权限。 通常情况下，只能由数据库管理员添加此权限。
+ 必须将 SQL 登录名或窗口用户添加为具有适当的权限，其中 R 作业将执行上述任何操作每个数据库中的用户︰
    + 检索数据
    + 写入或更新数据 
    + 创建新对象，如表或存储的过程

已设置并提供所需的权限的登录名或 Windows 用户帐户后，您可以在上运行的 R 代码 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 R 数据源对象或调用存储的过程。 每当在启动 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，数据库引擎安全性获取 R 作业的启动和管理的用户或登录名对安全对象的映射的用户的安全上下文。 

因此，从远程客户端启动的所有 R 作业必须都指定登录名或用户信息作为连接字符串的一部分。


## 之间的交互 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性和快速启动板安全性

R 脚本的上下文中执行时 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机， [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务从外部进程为建立辅助帐户的池获取可用的工作帐户 （本地用户帐户），并使用该辅助帐户来执行相关的任务。 

例如，如果在您的 Windows 域凭据下启动 R 作业，您的帐户可能会映射到快速启动板辅助帐户 *SQLRUser01*。

之后映射到辅助帐户， [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 创建用来启动进程的用户令牌。 

当所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作都已完成，用户工作帐户是标记为可用，并返回到池中。

有关详细信息 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], ，请参阅 [中支持的 R 集成到 SQL Server 的新组件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)。

## 工作人员帐户的安全性
为外部的 Windows 用户或工作帐户到有效的 SQL 登录名的此映射的有效期仅为运行 R 脚本的 SQL 查询的有效期限的生存期。 

并行查询相同的登录名映射到同一个用户工作帐户。

管理用于进程目录 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher，和目录进行访问限制。 工作帐户无法访问其自身的、 上述文件夹中的任何文件，但它可以读取、 写入或删除的 SQL 查询使用 R 脚本创建的会话工作文件夹下的子级。

有关如何更改辅助帐户、 帐户名或帐户密码的次数的详细信息，请参阅 [对 SQL Server R 服务，请修改用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。


## 多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 为特定语言运行时启动了附属进程，每个附属任务使用指定的辅助进程帐户 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]。 如果某个任务需要多个附属项，例如，在并行查询的情况下的单个辅助帐户用于所有相关的任务。

没有辅助帐户可以查看或操作的其他辅助帐户使用的文件。
 
如果您是计算机上的管理员，可以查看为每个进程创建的目录。 每个目录都由其会话 GUID 标识。

## 另请参阅
[体系结构概述](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)