---
title: SQL Server 机器学习的安全 |Microsoft Docs
description: SQL Server 机器学习服务中的可扩展性框架的安全性概述。 登录名和用户帐户、 SQL Server 快速启动板服务、 辅助角色帐户，运行多个脚本和文件权限的安全性。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bee8e2162c56ac1b26273873943d848c2167dbda
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100398"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server 机器学习服务中的可扩展性框架的安全性概述

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍用于连接到可扩展性框架的 SQL Server 数据库引擎和相关的组件的总体安全体系结构。 它描述组件的各部分和交互。 

<a name="launchpad"></a>

## <a name="sql-server-launchpad-service"></a>SQL Server 快速启动板服务

若要实例化外部进程，数据库引擎提供要创建的 R 或 Python 的会话的 SQL Server Launchpad 服务。 单独[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]为 SQL Server 机器学习 （R 或 Python） 集成，每个实例的一个服务已添加的数据库引擎实例创建服务。

默认情况下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]配置为在运行**NT Service\MSSQLLaunchpad**，其中预配了所有必需的权限来运行外部脚本。 最小化此帐户的权限可能会导致[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]未能启动或访问应在何处运行外部脚本的 SQL Server 实例。 快速启动板服务通常用作-，但可配置选项的详细信息，请参阅[SQL Server 快速启动板服务配置](../security/sql-server-launchpad-service-account.md)。

<a name="sqlrusergroup"></a>

## <a name="sqlrusergroup-and-worker-accounts"></a>SQLRUserGroup 和辅助角色帐户

在外部进程，最小特权的本地辅助角色帐户，受访问控制列表 (ACL) 的父级的标识下运行外部脚本**SQLRUserGroup** （SQL 受限制的用户组）。 

**SQLRUserGroup**创建 SQL Server 安装程序，并且包含本地 Windows 用户帐户的池。 当需要外部进程时，快速启动板采用一个可用的工作帐户，并使用它运行的进程。 更具体地说，快速启动板激活可用的工作帐户、 将其映射到调用用户的标识并运行辅助角色帐户下的脚本。 

+ **SQLRUserGroup**链接到特定实例。 已在哪台计算机启用了学习每个实例需要一个单独的池的辅助角色帐户。 帐户不能在各个实例之间共享。

+ 用户帐户池的大小是静态的默认值为 20，它支持 20 个并发会话。 可以同时启动的外部运行时会话数受此用户帐户池的大小。 

+ 在池中的辅助角色帐户名属于 sqlinstancename*nn*。 例如，在默认实例， **SQLRUserGroup**包含帐户最多 MSSQLSERVER20 上命名 MSSQLSERVER01、 MSSQLSERVER02，等等。

并行的任务也不会占用更多的帐户。 例如，如果用户在运行使用并行处理的评分任务，同一个辅助角色帐户重复使用的所有线程。 如果想要的机器学习的频繁使用，则可以增加用于运行外部脚本的帐户数。 有关详细信息，请参阅[修改机器学习的用户帐户池](../../advanced-analytics/administration/modify-user-account-pool.md)。

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup 授予权限

默认情况下的成员**SQLRUserGroup**具有读取和执行 SQL Server 中的文件权限**Binn**， **R_SERVICES**，和**PYTHON_SERVICES**目录，有权访问的可执行文件、 库和 SQL Server 一起安装的 R 和 Python 分发版中的内置数据集。 

若要保护 SQL 服务器上的敏感资源，可以选择定义访问拒绝对访问控制列表 (ACL) **SQLRUserGroup**。 相反，您还可以授予对主机计算机，除了 SQL Server 本身存在的本地数据资源的权限。 

根据设计， **SQLRUserGroup**不具有数据库登录名或任何数据的权限。 在某些情况下，你可能想要创建一个登录名，以允许循环后的连接，尤其是在受信任的 Windows 标识调用用户时。 此功能称为[*隐式身份验证*](#implied-authentication)。 有关详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>在 SQL Server 2019 AppContainer 隔离

在 SQL Server 2019，安装程序无法再创建辅助角色帐户以执行**SQLRUserGroup**。 相反，通过实现隔离[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)。 在运行时，当嵌入式的脚本或代码中检测到的存储的过程或查询，SQL Server 快速启动板使用调用请求的特定于扩展的启动器。 快速启动板调用其标识下, 一个过程中的相应的运行时环境，并实例化 AppContainer 来包含它。 此更改是有益的因为不再需要本地帐户和密码管理。 此外，在安装中，禁止使用本地用户帐户，消除了本地用户帐户依赖项意味着现在可以使用此功能。

实现 SQL server 时，AppContainers 是内部机制。 虽然不会看到 AppContainers 在 Process Monitor 中的实际证据，您可以由安装程序以防止进程进行网络调用创建的出站防火墙规则中找到它们。

> [!Note]
> 在 SQL Server 2019 **SQLRUserGroup**仅有一个成员，它现在是而不是多个辅助角色帐户的单个 SQL Server 快速启动板服务帐户。
::: moniker-end

## <a name="user-security"></a>用户安全性

SQL Server 的数据的数据库登录名和角色的安全模式扩展到 R 和 Python 脚本。 数据库登录名可以基于 Windows 标识或 SQL Server 数据库用户。 

作为数据库用户时，如果您有权执行特定查询，SQL Server 运行任何 R 或 Python 脚本还会提供检索相同的数据的权限。 无法使用，创建和保存数据库对象依赖于数据库的权限。 有关详细信息，请参阅[授予用户对 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)。

### <a name="mapping-user-identities-to-worker-accounts"></a>将用户标识映射到辅助角色帐户

当启动会话时，快速启动板将调用用户的标识映射到辅助角色帐户。 外部 Windows 用户或到辅助角色帐户的有效 SQL 登录名的映射无效，仅对生存期的 SQL 存储过程用于执行外部脚本。 来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

在执行期间，快速启动板创建临时文件夹来存储会话数据，在会话结束时将其删除。 目录的访问受限。 对于 R，RLauncher 执行此任务。 对于 Python，PythonLauncher 执行此任务。 每个单独的辅助角色帐户限制到其自己的文件夹，并且无法访问其自身级别以上的文件夹中的文件。 但是，辅助角色帐户可以读取、 写入或删除已创建的会话工作文件夹下的子级。 如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

<a name="implied-authentication"></a>

### <a name="implied-authentication"></a>隐式身份验证

*隐式身份验证*描述在其下运行如低权限辅助角色帐户显示为受信任的用户标识到 SQL Server 上的外部进程循环后的数据或操作的请求的连接请求行为。 作为一个概念，隐式身份验证是唯一的 Windows 身份验证，在从外部进程，例如 R 或 Python 脚本发出的请求上指定可信的连接，SQL Server 连接字符串中。 它有时也称为*环回到*。

受信任的连接是从 R 和 Python 脚本，但仅限于与其他配置可正常工作。 在可扩展性体系结构中，R 和 Python 进程下运行辅助角色帐户，从父级继承权限**SQLRUserGroup**。 当指定了连接字符串"Trusted_Connection = True"，在连接请求时，它是未知到 SQL Server 的默认情况下显示的辅助角色帐户的标识。 

若要建立受信任的连接成功，必须创建数据库登录名**SQLRUserGroup**。 这样做之后，任何受信任连接的任何成员**SQLRUserGroup**拥有到 SQL Server 登录权限。 有关分步说明，请参阅[添加到一个数据库登录名的 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

受信任的连接不是连接请求的最常用的设计。 当 R 或 Python 脚本指定的连接时，它可以是更常见的是使用 SQL 登录名，或完全指定的用户名和密码，如果连接到 ODBC 数据源。

#### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>如何隐式身份验证适用于 R 和 Python 的会话

下图显示了与 R 运行时，它是如何实现为 R 的隐式身份验证的 SQL Server 组件交互

![适用于 R 的隐式身份验证](../security/media/implied-auth-rsql.png)

下图显示了与 Python 运行时，它是如何实现用于 Python 的隐式身份验证的 SQL Server 组件交互。

![用于 Python 的隐式身份验证](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>不支持透明数据加密的静态

[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)的数据发送到或从外部脚本运行时收到不支持。 原因是，在 SQL Server 进程之外运行外部进程 （R 或 Python）。 因此，外部运行时使用的数据不受数据库引擎的加密功能。 此行为是在从数据库读取数据，并将副本的 SQL Server 计算机上运行的任何其他客户端没有什么不同。

因此，TDE**不是**应用于在 R 或 Python 脚本中使用的任何数据或保存到磁盘，或任何持久的中间结果的任何数据。 但是，其他类型的加密，如 Windows BitLocker 加密或第三方加密应用于文件或文件夹级别，仍然适用。

情况下[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)，外部运行时不能对加密密钥的访问。 因此，数据不能发送到脚本。


## <a name="next-steps"></a>后续步骤

在本文中，你学习了组件和交互模型的安全体系结构中内置[可扩展性框架](../../advanced-analytics/concepts/extensibility-framework.md)。 本文中所述的关键点包括 R 和 Python，以及如何将用户标识映射到辅助角色帐户的进程隔离的快速启动板、 SQLRUserGroup 和辅助角色帐户的目的。 

作为下一步，请查看有关的说明[授予的权限](../../advanced-analytics/security/user-permission.md)。 对于使用 Windows 身份验证的服务器，则还应查看[添加到一个数据库登录名的 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)若要了解何时需要额外的配置。