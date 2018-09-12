---
title: SQL Server 机器学习中适用于 Python 的安全概述 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a33701283635327fcaac4a9629cb02044b30dda8
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890053"
---
# <a name="security-overview-for-python-in-sql-server-machine-learning"></a>SQL Server 机器学习中适用于 Python 的安全性概述
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主题介绍用于连接的安全体系结构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]数据库引擎和 Python 组件。 两种常见方案提供的安全过程的示例： 在 SQL Server 使用存储的过程和 SQL 服务器作为远程计算上下文中运行 Python 中运行 Python。

## <a name="security-overview"></a>安全概述

一个[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]需要登录名或 Windows 用户帐户在 SQL Server 中运行 Python 脚本。 这些*安全主体*托管实例和数据库级别，并确定用户有权连接到数据库、 读取和写入数据，或创建数据库对象，如表或存储的过程。 此外，运行 Python 脚本的用户必须具有执行外部脚本在数据库级别的权限。

如果用户需要运行 Python 代码中的数据库，或访问数据库对象和数据，即使用户在外部工具中使用 Python 必须映射到登录名或数据库中的帐户。 Python 脚本从远程数据科学客户端发送还是使用 T-SQL 存储过程启动，则需要使用相同的权限。

例如，假设您创建用于在笔记本电脑上运行的 Python 脚本，并且你想要在上运行该代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ SQL 登录名或用于数据库访问权限的 Windows 帐户添加到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]在实例级别。
+ 必须向 SQL 登录名或 Windows 用户授予执行外部脚本的权限。 通常，此权限只能由数据库管理员添加。
+ SQL 登录名或窗口用户必须添加为具有 Python 脚本中执行上述任何操作的每个数据库中的适当权限的用户：
    + 检索数据
    + 写入或更新数据
    + 创建新对象，例如表或存储过程

已预配并提供所需的权限的登录名或 Windows 用户帐户后，可以在上运行 Python 代码[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通过使用提供的数据源对象**revoscalepy**库，或通过调用存储包含 Python 脚本的过程。

每当从启动 Python 脚本[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，数据库引擎安全获取启动作业，并管理用户或登录名对安全对象的映射的用户的安全上下文。

因此，所有从远程客户端启动的 Python 脚本必须作为连接字符串的一部分指定的登录名或用户的信息。

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>之间的交互[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性与 Launchpad 安全性

上下文中执行 Python 脚本时[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]计算机，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务从外部进程建立的辅助角色帐户池中获取可用的工作帐户 （本地用户帐户），并使用到该辅助角色帐户执行相关的任务。

例如，假设您的 Windows 域凭据下启动的 Python 脚本。 SQL Server 获取你的凭据和任务映射到可用的快速启动板辅助角色帐户，如*SQLRUser01*。

> [!NOTE]
> 无论你使用 R 或 Python 相同的辅助角色帐户组的名称。 但是，每个实例，您从中启用任何外部语言创建一个单独的组。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关服务的详细信息，请参阅[可扩展性框架](../concepts/extensibility-framework.md)。

### <a name="implied-authentication"></a>隐式身份验证

**隐式身份验证**是一词用的 SQL Server 获取的用户的进程使用的凭据，然后执行可代表用户，假设用户已在数据库中的正确权限的所有外部脚本任务。 隐式身份验证是特别重要，如果需要进行外部 SQL Server 数据库的 ODBC 调用的 Python 脚本。 例如，代码可能会从电子表格或其他源中检索较短的因素列表。

对于此类环回调用成功执行，包含辅助角色帐户，SQLRUserGroup 的组必须具有"允许本地登录"权限。 默认情况下，此权限已授予给所有新的本地用户，但在某些组织可能会强制实施更严格的组策略。

![适用于 R 的隐式身份验证](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>辅助角色帐户的安全性

外部 Windows 用户或到辅助角色帐户的有效 SQL 登录名的映射无效，仅对生存期的 SQL 存储过程用于执行 Python 脚本。

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

管理用于进程目录[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，并且这些目录的访问限制。 对于 Python，PythonLauncher 执行此任务。 每个单独的辅助角色帐户限制到其自己的文件夹，并且无法访问其自身级别以上的文件夹中的文件。 但是，辅助角色帐户可以读取、 写入或删除已创建的会话工作文件夹下的子级。

有关如何更改辅助角色帐户、 帐户名或帐户密码的数量的详细信息，请参阅[修改 SQL Server 机器学习的用户帐户池](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。

如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>请参阅

[体系结构概述](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
