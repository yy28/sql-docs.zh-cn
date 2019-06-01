---
title: SQL Server 2019-SQL Server 机器学习服务中的差异
description: 了解什么是 R 和 Python SQL Server 机器学习扩展 SQL Server 2019 预览版本中的新增功能。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 43d427129cae773fc17a0d73f57a26144b7cd09f
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454519"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>SQL Server 机器学习服务安装在 SQL Server 2019 之间的差异  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 Windows、 SQL Server 2019 安装程序更改外部进程隔离机制。 此更改将替换与本地辅助角色帐户[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)，一种用于在 Windows 上运行的客户端应用程序隔离技术。 

修改由于管理员没有特定的操作项。 新的或已升级服务器、 所有外部脚本和代码执行从上[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)自动遵循新的隔离模型。 

汇总，在此版本中的主要差异有：

+ 本地用户帐户下**SQL 受限制的用户组 (SQLRUserGroup)** 无法再创建或用于运行外部进程。 AppContainers 替换它们。
+ **SQLRUserGroup**成员身份已更改。 而不是多个本地用户帐户，成员资格包含，只需在 SQL Server 快速启动板服务帐户。 R 和 Python 进程现在在快速启动板服务标识，通过 AppContainers 隔离下执行。

尽管隔离模型已更改，安装向导和命令行参数将保持在 SQL Server 2019 相同。 有关安装帮助，请参阅[安装 SQL Server 机器学习服务](sql-machine-learning-services-windows-install.md)。

## <a name="about-appcontainer-isolation"></a>有关 AppContainer 隔离

在上一版本中， **SQLRUserGroup**包含的本地 Windows 用户帐户 (MSSQLSERVER00 MSSQLSERVER20) 用于隔离和运行外部进程池。 需要外部进程时，SQL Server Launchpad 服务将获取可用帐户，并使用它运行的进程。 

在 SQL Server 2019，安装程序无法再创建本地辅助角色帐户。 相反，通过实现隔离[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)。 在运行时，当嵌入式的脚本或代码中检测到的存储的过程或查询，SQL Server 快速启动板使用调用请求的特定于扩展的启动器。 快速启动板调用其标识下, 一个过程中的相应的运行时环境，并实例化 AppContainer 来包含它。 此更改是有益的因为不再需要本地帐户和密码管理。 此外，在安装中，禁止使用本地用户帐户，消除了本地用户帐户依赖项意味着现在可以使用此功能。

实现 SQL server 时，AppContainers 是内部机制。 虽然不会看到 AppContainers 在 Process Monitor 中的实际证据，您可以由安装程序以防止进程进行网络调用创建的出站防火墙规则中找到它们。

## <a name="firewall-rules-created-by-setup"></a>安装程序创建的防火墙规则

默认情况下，SQL Server 禁用出站连接，通过创建防火墙规则。 在过去，这些规则基于本地用户帐户，安装程序在其中创建一个出站规则**SQLRUserGroup** ，拒绝对其成员的网络访问 （每个辅助角色帐户被列为受 rule_ 本地原则。 

转到 AppContainers 的一部分，有新的防火墙规则根据 AppContainer Sid： 一个用于 20 AppContainers 的每个创建的 SQL Server 安装程序。 防火墙规则名称的命名约定是**阻止 AppContainer 00 的 SQL Server 实例 MSSQLSERVER 中的网络访问**，其中 00 是 AppContainer (00-20 默认情况下)，数量，MSSQLSERVER 是 SQL 的名称服务器实例。 

> [!Note]
> 如果网络调用是必需的则可以禁用 Windows 防火墙中的出站规则。

## <a name="program-file-permissions"></a>程序文件权限

与早期版本中，一样**SQLRUserGroup**将继续提供读取和执行 SQL Server 中的可执行文件的权限**Binn**， **R_SERVICES**，和**PYTHON_SERVICES**目录。 在此版本的唯一成员**SQLRUserGroup**是 SQL Server 快速启动板服务帐户。  快速启动板服务启动时 R 或 Python 执行环境，该过程作为快速启动板服务运行。

## <a name="implied-authentication"></a>隐式身份验证

因为在这之前，其他配置仍需要*隐式身份验证*脚本或代码具有要重新连接到 SQL Server 使用受信任的身份验证以检索数据或资源。 其他配置涉及到创建数据库登录名**SQLRUserGroup**，其唯一的成员现在是而不是多个辅助角色帐户的单个 SQL Server 快速启动板服务帐户。 有关此任务的详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md)。


## <a name="symbolic-link-created-by-setup"></a>安装程序创建的符号链接

为当前的默认值创建符号链接**R_SERVICES**并**PYTHON_SERVICES**作为 SQL Server 安装程序的一部分。 如果不想要创建此链接，一种替代方法是所有应用程序包读取的权限授予指向文件夹的层次结构。


## <a name="see-also"></a>另请参阅

+ [安装 SQL Server 机器学习在 Windows 上的服务](sql-machine-learning-services-windows-install.md)

+ [在 Linux 上安装 SQL Server 2019 机器学习服务](../../linux/sql-server-linux-setup-machine-learning.md)
