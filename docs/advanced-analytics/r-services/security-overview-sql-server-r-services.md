---
title: "安全概述 (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c3dc18f0943c3731a1fae1f9591a63ae70181356
ms.lasthandoff: 04/11/2017

---
# <a name="security-overview-sql-server-r-services"></a>安全概述 (SQL Server R Services)

本主题介绍用于将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎和相关组件连接到 R 运行时的总体安全体系结构。 本文提供了安全流程的示例，演示在企业环境中使用 R 的两种常见方案：

+ 通过数据科学客户端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中执行 RevoScaleR 函数
+ 使用存储过程通过 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 直接运行 R

## <a name="security-overview"></a>安全性概述

若要运行利用 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 的所有 R 作业，需要一个 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 登录名或 Windows 用户帐户。 登录名或用户帐户标识有权访问运行 R 的数据库，以及有权从受保护对象（例如表）中读取数据，或者写入新数据或添加新对象（如果 R 作业有此所需）的*安全主体*。

因此，一项严格的要求是，针对 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 运行 R 代码的每个用户必须映射到数据库中的登录名，不管该代码是使用 RevoScaleR 函数从远程数据科学客户端发送的，还是使用 T-SQL 存储过程启动的。 

例如，假设你已创建一些在笔记本电脑上运行的 R 代码，并希望在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上运行该代码。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ 具有你在 R 代码中使用的名称和密码的 SQL 登录名已在实例级别添加到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 或者，如果你使用 Windows 集成身份验证，则必须将连接字符串中指定的 Windows 用户添加为实例上的用户。
+ 必须向 SQL 登录名或 Windows 用户授予执行外部脚本的权限。 通常，此权限只能由数据库管理员添加。
+ 在 R 作业执行以下任一操作的每个数据库中，必须将 SQL 登录名或 Windows 用户添加为拥有相应权限的用户：
    + 检索数据
    + 写入或更新数据 
    + 创建新对象，例如表或存储过程

预配登录名或 Windows 用户帐户并向其授予所需的权限后，可以使用 R 数据源对象或者通过调用存储过程在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 上运行 R 代码。 每当从 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 启动 R 时，数据库引擎就会获取启动 R 作业的用户的安全上下文，并管理该用户或登录名到安全对象的映射。 

因此，从远程客户端启动的所有 R 作业必须指定登录名或用户信息作为连接字符串的一部分。


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性与 LaunchPad 安全性之间的交互

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机的上下文中执行 R 脚本时，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务将从针对外部进程建立的辅助角色帐户池中获取可用的辅助角色帐户（本地用户帐户），并使用该辅助角色帐户来执行相关的任务。 

例如，如果你使用自己的 Windows 域凭据启动 R 作业，则你的帐户可能会映射到 Launchpad 辅助角色帐户 *SQLRUser01*。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 的详细信息，请参阅 [New Components in SQL Server to Support R Integration](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)（SQL Server 中用于支持 R 集成的新组件）。

> [!NOTE]
要让 Launchpad 管理辅助角色帐户和执行 R 作业，包含辅助角色帐户的组 SQLRUserGroup 必须拥有“允许本地登录”权限；否则 R Services 可能无法正常工作。 默认情况下，此权限已授予所有新的本地用户，但某些组织可能实施了更严格的组策略，阻止辅助角色帐户连接到 SQL Server 来执行 R 作业。  

## <a name="security-of-worker-accounts"></a>辅助角色帐户的安全性
这种从外部 Windows 用户或有效 SQL 登录名到辅助角色帐户的映射仅在运行 R 脚本的 SQL 查询的生存期内有效。 

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

用于进程的目录由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher 进行管理，并且这些目录的访问受限。 辅助角色帐户无法访问其上级文件夹中的任何文件，但可以使用 R 脚本读取、写入或删除针对 SQL 查询创建的会话工作文件夹下面的子级。

有关如何更改辅助角色帐户数目、帐户名或帐户密码的详细信息，请参阅[修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。
 
如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>另请参阅
[体系结构概述](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

