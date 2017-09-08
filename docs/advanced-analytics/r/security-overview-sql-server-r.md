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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>安全概述 (SQL Server R Services)

本主题介绍用于将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎和相关组件连接到 R 运行时的总体安全体系结构。 本文提供了安全流程的示例，演示在企业环境中使用 R 的两种常见方案：

+ 通过数据科学客户端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中执行 RevoScaleR 函数
+ 使用存储过程通过 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 直接运行 R

## <a name="security-overview"></a>安全性概述

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登录或 Windows 用户帐户才能运行 R 脚本使用 SQL Server 数据或通过 SQL Server 作为计算上下文验证运行。 此要求适用于[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]和 SQL Server 自 2017 年 1 机器学习 Services。 

登录名或用户帐户标识*安全主体*，他们可能需要多个级别的访问权限，具体取决于 R 脚本要求：
+ R 在何处启用数据库的访问权
+ 从受保护的对象，如表读取数据的权限
+ 能够将新数据写入到的表，例如模型，或评分结果
+ 能够创建新对象，如表、 存储过程使用 R 脚本或自定义函数该使用 R 作业
+ 使用 R 包提供给一组用户在 SQL Server 计算机上安装新包中的权限。 

因此，每个用户都运行 R 代码使用[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]与执行上下文必须映射到数据库中具有登录名。 在 SQL Server 安全机制，最好是通常最简单的方法创建角色，以管理组的权限，并将用户分配到这些角色，而不是单独设置用户权限。 

例如，假定你创建了你的笔记本电脑运行一些 R 代码，并且你想要在运行该代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 仅当满足这些条件时，可以执行此操作：

+ 数据库允许远程连接。
+ 具有你在 R 代码中使用的名称和密码的 SQL 登录名已在实例级别添加到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 或者，如果你使用 Windows 集成身份验证，则必须将连接字符串中指定的 Windows 用户添加为实例上的用户。
+ SQL 登录名或 Windows 用户必须有权执行外部脚本。 通常，此权限只能由数据库管理员添加。
+ 在 R 作业执行以下任一操作的每个数据库中，必须将 SQL 登录名或 Windows 用户添加为拥有相应权限的用户：
    + 检索数据
    + 写入或更新数据 
    + 创建新对象，例如表或存储过程

已设置并提供所需的权限的登录名或 Windows 用户帐户后，你可以在运行 R 代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通过使用 R 数据源对象或通过调用存储的过程。 每当从启动 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，数据库引擎安全获取 R 作业的启动或运行存储的过程，并管理的用户或对安全对象的登录名的映射的用户的安全上下文。 

因此，从远程客户端启动的所有 R 作业必须作为连接字符串的一部分都指定的登录名或用户的信息。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性与 LaunchPad 安全性之间的交互

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机的上下文中执行 R 脚本时，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务将从针对外部进程建立的辅助角色帐户池中获取可用的辅助角色帐户（本地用户帐户），并使用该辅助角色帐户来执行相关的任务。 

例如，如果你使用自己的 Windows 域凭据启动 R 作业，则你的帐户可能会映射到 Launchpad 辅助角色帐户 *SQLRUser01*。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 的详细信息，请参阅 [New Components in SQL Server to Support R Integration](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)（SQL Server 中用于支持 R 集成的新组件）。

> [!NOTE]
要让 Launchpad 管理辅助角色帐户和执行 R 作业，包含辅助角色帐户的组 SQLRUserGroup 必须拥有“允许本地登录”权限；否则 R Services 可能无法正常工作。 默认情况下，此权限已授予所有新的本地用户，但某些组织可能实施了更严格的组策略，阻止辅助角色帐户连接到 SQL Server 来执行 R 作业。  

## <a name="security-of-worker-accounts"></a>辅助角色帐户的安全性

外部的 Windows 用户或到辅助帐户的有效 SQL 登录名的映射的有效期仅为运行 R 脚本的 SQL 查询的生存期的生存期。 

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

用于进程的目录由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher 进行管理，并且这些目录的访问受限。 辅助角色帐户无法访问其上级文件夹中的任何文件，但可以使用 R 脚本读取、写入或删除针对 SQL 查询创建的会话工作文件夹下面的子级。

有关如何更改辅助角色帐户数目、帐户名或帐户密码的详细信息，请参阅[修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。
 
如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>另请参阅
[体系结构概述](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)

