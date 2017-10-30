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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>安全性概述

本主题介绍用于连接的安全体系结构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]数据库引擎和 Python 组件。 所提供的两个常见方案的安全过程的示例： 在 SQL Server 使用存储的过程，并使用 SQL Server 作为远程计算上下文中运行 Python 中运行 Python。

## <a name="security-overview"></a>安全性概述

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登录名或 Windows 用户帐户需要在 SQL Server 中运行 Python 脚本。 登录名或用户帐户标识*安全主体*，用户必须有权访问的数据库从中检索数据。 具体取决于是否 Python 脚本创建的新对象，或将新数据写入，用户可能需要创建表、 写入数据，或创建自定义函数或存储的过程的权限。

因此，很严格的要求，每个用户都运行 Python 代码中[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]必须映射到登录名或数据库中的帐户。 此限制适用而不考虑从远程数据科学客户端是否发送了脚本，或开始使用 T-SQL 存储过程。

例如，假设你创建你的笔记本电脑运行的 Python 脚本，并且你想要在运行该代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ 用于数据库访问权限的 Windows 帐户或 SQL 登录名添加到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]在实例级别。
+ 必须向 SQL 登录名或 Windows 用户授予执行外部脚本的权限。 通常，此权限只能由数据库管理员添加。
+ 必须将 SQL 登录名或窗口用户添加为具有 Python 脚本中执行任何一种操作的每个数据库中的适当权限的用户：
    + 检索数据
    + 写入或更新数据
    + 创建新对象，例如表或存储过程

已设置并提供所需的权限的登录名或 Windows 用户帐户后，你可以在运行 Python 代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通过使用提供的数据源对象**revoscalepy**库，或通过调用的已存储包含 Python 脚本的过程。

每当的 Python 脚本启动从[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，数据库引擎安全获取启动了作业，并管理的用户或对安全对象的登录名的映射的用户的安全上下文。

因此，从远程客户端启动的所有 Python 脚本必须作为连接字符串的一部分都指定的登录名或用户的信息。


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安全性与 LaunchPad 安全性之间的交互

上下文中执行 Python 脚本时[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]计算机，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务从外部进程为建立的辅助帐户池获取可用的工作帐户 （本地用户帐户），并使用该工作帐户执行相关的任务。

例如，假定在您的 Windows 域凭据下启动的 Python 脚本。 SQL Server 将获取你的凭据并将其映射到可用的快速启动板辅助帐户，如*SQLRUser01*。

> [!NOTE]
> 无论你使用的 R 或 Python 相同工作人员帐户的组的名称。 但是，每个实例，您从中启用任何外部语言创建单独的组。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关详细信息[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，请参阅[支持 Python 集成到 SQL Server 中的新组件](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)。

> [!NOTE]
> 有关快速启动板以管理辅助进程帐户和执行 Python 作业，包含辅助帐户中，组*SQLRUserGroup*，必须具有"允许本地登录"权限; 否则 Python 运行时可能不会启动。 默认情况下，此权限提供给所有新的本地用户，但在某些组织更严格的组策略可能会强制，这阻止辅助帐户连接到 SQL Server 到 Python 作业。

## <a name="security-of-worker-accounts"></a>辅助角色帐户的安全性

外部的 Windows 用户或到辅助帐户的有效 SQL 登录名的映射无效，只能对 SQL 的生存期存储过程中执行 Python 脚本。

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

进程使用的目录由[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，和目录是访问限制。 对于 Python，PythonLauncher 执行此任务。 每个单个辅助帐户被限制到其自己的文件夹，且无法访问自己级别以上的文件夹中的文件。 但是，工作线程帐户可以读取、 写入或删除已创建的会话工作文件夹下的子级。

有关如何更改辅助角色帐户数目、帐户名或帐户密码的详细信息，请参阅[修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。

如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>另请参阅

[体系结构概述](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

