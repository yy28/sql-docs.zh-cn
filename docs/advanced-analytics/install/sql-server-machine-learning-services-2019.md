---
title: Windows 的隔离更改
description: 本文介绍 Windows 上 SQL Server 2019 中机器学习服务隔离机制的变化。 这些更改会影响 SQLRUserGroup、防火墙规则、文件权限和隐含身份验证。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fae460e78682263c604d8e1e86ca40b7b62df97
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531041"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>Windows 上的 SQL Server 2019:机器学习服务的隔离更改
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍 Windows 上 SQL Server 2019 中机器学习服务隔离机制的变化。 这些更改会影响**SQLRUserGroup**、防火墙规则、文件权限和隐含身份验证。

有关详细信息, 请参阅如何[在 Windows 上安装 SQL Server 机器学习服务](sql-machine-learning-services-windows-install.md)。

## <a name="changes-to-isolation-mechanism"></a>隔离机制的更改

在 Windows 上, SQL Server 2019 安装程序将更改外部进程的隔离机制。 此更改会将本地辅助角色帐户替换为[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), 这是 Windows 上运行的客户端应用程序的隔离技术。 

由于此修改, 管理员没有特定的操作项。 在新的或升级的服务器上, 从[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)执行的所有外部脚本和代码都将自动遵循新的隔离模型。 

概括而言, 此版本中的主要区别是:

+ 不会再创建或使用**SQL 受限用户组 (SQLRUserGroup)** 下的本地用户帐户来运行外部进程。 AppContainers 替换它们。
+ **SQLRUserGroup**成员身份已更改。 成员身份只包含 SQL Server Launchpad 服务帐户, 而不是多个本地用户帐户。 现在 R 和 Python 进程在启动板服务标识下执行, 并通过 AppContainers 隔离。

虽然隔离模型发生了更改, 但安装向导和命令行参数在 SQL Server 2019 中保持不变。 有关安装的帮助, 请参阅[Install SQL Server 机器学习服务](sql-machine-learning-services-windows-install.md)。

## <a name="about-appcontainer-isolation"></a>关于 AppContainer 隔离

在以前的版本中, **SQLRUserGroup**包含用于隔离和运行外部进程的本地 Windows 用户帐户 (MSSQLSERVER00-MSSQLSERVER20) 池。 需要外部进程时, SQL Server Launchpad 服务将采用可用帐户, 并使用该帐户运行进程。 

在 SQL Server 2019 中, 安装程序不再创建本地辅助角色帐户。 相反, 隔离是通过[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)实现的。 在运行时, 如果在存储过程或查询中检测到嵌入的脚本或代码, SQL Server 会调用快速启动板, 请求提供特定于扩展程序的启动程序。 快速启动板在进程的标识下调用适当的运行时环境, 并实例化 AppContainer 以包含它。 此更改很有用, 因为不再需要本地帐户和密码管理。 此外, 在禁止本地用户帐户的安装上, 消除本地用户帐户依赖关系意味着你现在可以使用此功能。

SQL Server 实现, AppContainers 是一种内部机制。 尽管你不会在进程监视器中看到 AppContainers 的物理证据, 但你可以在由安装程序创建的出站防火墙规则中找到它们, 以防止进程发出网络调用。

## <a name="firewall-rules-created-by-setup"></a>安装程序创建的防火墙规则

默认情况下, 通过创建防火墙规则 SQL Server 禁用出站连接。 过去, 这些规则基于本地用户帐户, 其中, 安装程序为拒绝对其成员的网络访问的**SQLRUserGroup**创建了一个出站规则 (每个辅助角色帐户作为 rule_ 的本地原则列出。 

在移动到 AppContainers 的过程中, 有基于 AppContainer Sid 的新防火墙规则: SQL Server 安装程序创建的20个 AppContainers 中的一个。 防火墙规则名称的命名约定会**阻止 SQL Server 实例 MSSQLSERVER 中的 appcontainer-00 的网络访问**, 其中00是 appcontainer 的编号 (默认值为 00-20), 而 MSSQLSERVER 是 SQL Server 实例的名称。 

> [!Note]
> 如果需要网络调用, 你可以在 Windows 防火墙中禁用出站规则。

## <a name="program-file-permissions"></a>程序文件权限

与以前的版本一样, **SQLRUserGroup**继续提供对 SQL Server **Binn**、 **R_SERVICES**和**PYTHON_SERVICES**目录中的可执行文件的读取和执行权限。 在此版本中, **SQLRUserGroup**的唯一成员是 SQL Server Launchpad 服务帐户。  当启动板服务启动 R 或 Python 执行环境时, 该进程将作为启动板服务运行。

## <a name="implied-authentication"></a>隐式身份验证

与之前一样, 在脚本或代码必须使用可信身份验证连接回 SQL Server 以检索数据或资源的情况下, 仍需要进行*隐式身份验证*。 其他配置涉及创建**SQLRUserGroup**的数据库登录名, 其唯一成员现在是单一 SQL Server Launchpad 服务帐户, 而不是多个辅助角色帐户。 有关此任务的详细信息, 请参阅[将 SQLRUserGroup 添加为数据库用户](../security/create-a-login-for-sqlrusergroup.md)。


## <a name="symbolic-link-created-by-setup"></a>安装程序创建的符号链接

在 SQL Server 安装程序的过程中, 将为当前默认的**R_SERVICES**和**PYTHON_SERVICES**创建一个符号链接。 如果你不想创建此链接, 一种替代方法是向指向文件夹的层次结构授予 "所有应用程序包" 读取权限。


## <a name="see-also"></a>请参阅

+ [在 Windows 上安装 SQL Server 机器学习服务](sql-machine-learning-services-windows-install.md)
+ [在 Linux 上安装 SQL Server 机器学习服务](../../linux/sql-server-linux-setup-machine-learning.md)
