---
title: SQL Server 机器学习和 R 的安全性 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2ca7b24b46c1d32fb12f050b31c74fef26769ca3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203569"
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>SQL Server 机器学习和 R 的安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了用于连接的总体安全体系结构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]数据库引擎和对 R 运行时的相关的组件。 有关在企业环境中使用 R 的这些常见方案提供的安全过程的示例：

+ 通过数据科学客户端在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中执行 RevoScaleR 函数
+ 使用存储过程通过 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 直接运行 R

## <a name="security-overview"></a>安全性概述

A[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]登录或 Windows 用户帐户才能运行 R 脚本使用 SQL Server 数据或通过 SQL Server 作为计算上下文验证运行。 此要求适用于[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]和 SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]。

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>交互[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]安全性和快速启动板安全性

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机的上下文中执行 R 脚本时，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务将从针对外部进程建立的辅助角色帐户池中获取可用的辅助角色帐户（本地用户帐户），并使用该辅助角色帐户来执行相关的任务。 

例如，如果你使用自己的 Windows 域凭据启动 R 作业，则你的帐户可能会映射到 Launchpad 辅助角色帐户 *SQLRUser01*。

映射到辅助角色帐户后，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将创建用于启动进程的用户令牌。 

完成所有 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 操作后，用户辅助角色帐户将标记为可用并返回到池中。

有关详细信息[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]，请参阅[中 SQL Server 以支持 R 集成的组件](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)。

### <a name="implied-authentication"></a>隐式身份验证

**默示身份验证**是术语在其下 SQL Server 获取用户的进程使用的凭据，然后执行代表用户，假定用户在数据库中具有正确的权限的所有外部脚本任务。 默示的身份验证是如果 R 脚本需要使 SQL Server 数据库之外的 ODBC 调用特别重要。 例如，代码可能会从电子表格或其他源中检索较短的因素列表。

若要成功执行此类环回调用，对于包含辅助帐户，SQLRUserGroup，组必须具有"允许本地登录"权限。 默认情况下，此权限提供给所有新的本地用户，但在某些组织可能会强制执行更严格的组策略。

![默示身份验证](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>工作人员帐户的安全性

外部的 Windows 用户或到辅助帐户的有效 SQL 登录名的映射的有效期仅为运行 R 脚本的 SQL 查询的生存期的生存期。

来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

用于进程的目录由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 使用 RLauncher 进行管理，并且这些目录的访问受限。 辅助角色帐户无法访问其上级文件夹中的任何文件，但可以使用 R 脚本读取、写入或删除针对 SQL 查询创建的会话工作文件夹下面的子级。

有关如何更改辅助帐户、 帐户名或帐户密码的数量的详细信息，请参阅[修改用户帐户池的 SQL Server 机器学习](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

## <a name="security-isolation-for-multiple-external-scripts"></a>多个外部脚本的安全隔离

隔离机制基于物理用户帐户。 由于附属进程是针对特定的语言运行时启动的，因此每个附属任务使用 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 指定的辅助角色帐户。 如果某个任务需要多个附属进程（例如，在并行查询中），将为所有相关任务使用单个辅助角色帐户。

任何辅助角色帐户都无法查看或操作其他辅助角色帐户使用的文件。
 
如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

## <a name="see-also"></a>另请参阅

[SQL Server 机器学习的体系结构概述](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
