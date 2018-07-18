---
title: 在 SQL Server 机器学习中的 Python 的安全性概述 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d0e2e12dd40dd8a7f7a90beda5a06b751d70aed2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202129"
---
# <a name="security-overview-for-python-in-sql-server-machine-learning"></a>在 SQL Server 机器学习中的 Python 的安全性概述
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主题介绍用于连接的安全体系结构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]数据库引擎和 Python 组件。 所提供的两个常见方案的安全过程的示例： 在 SQL Server 使用存储的过程，并使用 SQL Server 作为远程计算上下文中运行 Python 中运行 Python。

## <a name="security-overview"></a>安全性概述

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登录名或 Windows 用户帐户需要在 SQL Server 中运行 Python 脚本。 这些*安全主体*和确定用户有权连接到数据库、 读取和写入数据，或创建数据库对象，如表或存储的过程来在实例级别和数据库级别进行管理。 此外，运行 Python 脚本的用户必须具有执行外部脚本数据库级别的权限。

如果用户需要运行 Python 代码中的数据库，或访问数据库对象和数据，即使在外部工具中使用 Python 的用户必须映射到登录名或数据库中的帐户。 Python 脚本从远程数据科学客户端发送还是使用 T-SQL 存储过程启动，则需要使用相同的权限。

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>交互[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性和快速启动板安全性

上下文中执行 Python 脚本时[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]计算机，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务从外部进程为建立的辅助帐户池获取可用的工作帐户 （本地用户帐户），并使用该工作帐户执行相关的任务。

例如，假定在您的 Windows 域凭据下启动的 Python 脚本。 SQL Server 获取你的凭据和的任务映射到可用的快速启动板辅助帐户，如*SQLRUser01*。

> [!NOTE]
> 无论你使用的 R 或 Python 相同工作人员帐户的组的名称。 但是，每个实例，您从中启用任何外部语言创建单独的组。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关详细信息[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，请参阅[中 SQL Server 以支持 Python 集成组件](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)。

### <a name="implied-authentication"></a>隐式身份验证

**默示身份验证**是术语在其下 SQL Server 获取用户的进程使用的凭据，然后执行代表用户，假定用户在数据库中具有正确的权限的所有外部脚本任务。 默示的身份验证是特别重要，如果需要使 SQL Server 数据库之外的 ODBC 调用 Python 脚本。 例如，代码可能会从电子表格或其他源中检索较短的因素列表。

若要成功执行此类环回调用，对于包含辅助帐户，SQLRUserGroup，组必须具有"允许本地登录"权限。 默认情况下，此权限提供给所有新的本地用户，但在某些组织可能会强制执行更严格的组策略。

![默示身份验证](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>工作人员帐户的安全性

外部的 Windows 用户或到辅助帐户的有效 SQL 登录名的映射无效，只能对 SQL 的生存期存储过程中执行 Python 脚本。

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

进程使用的目录由[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，和目录是访问限制。 对于 Python，PythonLauncher 执行此任务。 每个单个辅助帐户被限制到其自己的文件夹，且无法访问自己级别以上的文件夹中的文件。 但是，工作线程帐户可以读取、 写入或删除已创建的会话工作文件夹下的子级。

有关如何更改辅助帐户、 帐户名或帐户密码的数量的详细信息，请参阅[修改用户帐户池的 SQL Server 机器学习](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。


## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制取决于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。

如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>另请参阅

[体系结构概述](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
