---
title: R 和 Python 扩展-SQL Server 机器学习的安全概述
description: SQL Server 机器学习服务中的可扩展性框架的安全性概述。 登录名和用户帐户、 SQL Server 快速启动板服务、 辅助角色帐户，运行多个脚本和文件权限的安全性。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1f19e3322b8aee78fdb5a76a29a719148cc6a0c7
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454538"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server 机器学习服务中的可扩展性框架的安全性概述

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了用于将与可扩展性框架集成的 SQL Server 数据库引擎和相关的组件的总体安全体系结构。 它会检查安全对象、 服务、 进程标识和权限。 有关的关键概念和组件的 SQL Server 中的可扩展性的详细信息，请参阅[SQL Server 机器学习服务中的可扩展性体系结构](extensibility-framework.md)]。

## <a name="securables-for-external-script"></a>外部脚本的安全对象

外部 R 或 Python 编写的脚本提交的输入参数作为[系统存储过程](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)为此目的，创建或包装在您定义的存储过程。 或者，你可能会预先训练并存储在数据库表，可在 T-SQL 的调用中的二进制格式的模型[PREDICT](../../t-sql/queries/predict-transact-sql.md)函数。

通过现有数据库架构对象、 存储的过程和表提供的脚本，如有任何新[安全对象](../../relational-databases/security/securables.md)的 SQL Server 机器学习服务。

而不考虑如何使用脚本或它们的组成，将创建数据库对象，并将其可能保存，但用于存储脚本引入任何新的对象类型。 因此，无法使用，创建和保存数据库很大程度上已为你的用户定义的数据库权限将依赖对象。

<a name="permissions"></a>

## <a name="permissions"></a>权限

SQL Server 的数据的数据库登录名和角色的安全模式扩展到 R 和 Python 脚本。 SQL Server 登录名或 Windows 用户帐户需要运行外部脚本，使用 SQL Server 数据或使用 SQL Server 作为计算上下文的运行。 具有权限才能执行即席查询的数据库用户可以从 R 或 Python 脚本中访问相同的数据。

登录名或用户帐户标识*安全主体*，那些可能需要多个级别的访问权限，具体取决于外部脚本要求：

+ 若要访问启用了外部脚本的数据库的权限。
+ 若要从受保护的对象，如表中读取数据的权限。
+ 能够将新数据写入到一个表，如某一模型，或评分结果。
+ 能够创建新对象，如表、 存储过程使用外部脚本，或自定义函数，使用 R 或 Python 作业。
+ SQL Server 计算机上安装新包或使用包提供给一组用户权限。

每个人都在运行外部脚本使用 SQL Server 作为执行上下文必须映射到数据库中的用户。 而不是单独设置数据库用户权限，无法创建角色，以管理组的权限，并将用户分配到这些角色，而不是分别设置用户权限。

有关详细信息，请参阅[授予用户对 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)。

## <a name="permissions-when-using-an-external-client-tool"></a>权限时使用的外部客户端工具

使用 R 或 Python 中的外部客户端工具的用户必须具有其登录名或帐户映射到数据库中的用户，如果他们需要运行外部脚本中的数据库，或访问数据库对象和数据。 相同的权限所需的外部脚本是否来自远程数据科学客户端或运行使用 T-SQL 存储过程。

例如，假设您创建在本地计算机运行的外部脚本，并且你想要在 SQL Server 上运行该脚本。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ SQL 登录名或用于数据库访问权限的 Windows 帐户具有已添加到 SQL Server 实例级别。
+ SQL 登录名或 Windows 用户必须有权执行外部脚本。 通常，此权限只能由数据库管理员添加。
+ SQL 登录名或窗口用户必须添加为具有相应的权限，其中的外部脚本执行上述任何操作每个数据库中的用户：
  + 正在检索数据。
  + 写入或更新数据。
  + 创建新对象，如表或存储的过程。

已预配并提供所需的权限的登录名或 Windows 用户帐户后，你可以运行外部脚本在 SQL Server 上通过在 R 中使用数据源对象或**revoscalepy**在 Python 中，或通过调用存储库包含外部脚本的过程。

每次从 SQL Server 启动外部脚本时，数据库引擎安全获取启动作业，并管理用户或登录名对安全对象的映射的用户的安全上下文。

因此，从远程客户端发起的所有外部脚本必须作为连接字符串的一部分指定的登录名或用户的信息。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部处理 （快速启动板） 中使用的服务

可扩展性框架添加到一个新的 NT 服务[的服务列表](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)在 SQL Server 安装中：[**SQL Server 快速启动板 (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)。

数据库引擎使用 SQL Server Launchpad 服务来实例化的 R 或 Python 会话作为单独的进程。 低特权帐户; 下运行的进程不同于 SQL Server、 快速启动板本身，以及其下执行存储的过程或主机查询的用户标识。 在低特权帐户下的单独进程中运行脚本是对 R 和 Python 在 SQL Server 中的安全性和隔离模型的基础。

除了启动外部进程，快速启动板程序还负责跟踪调用用户的标识，并将该标识映射到用来启动进程的低权限辅助角色帐户。 在某些情况下，其中的脚本或代码调用返回到 SQL Server 数据和操作，快速启动板是通常能够无缝管理标识传输。 只有执行调用的用户有足够的权限时，脚本包含 SELECT 语句或调用函数和其他编程对象通常会成功。

> [!NOTE]
> 默认情况下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]配置为在运行**NT Service\MSSQLLaunchpad**，其中预配了所有必需的权限来运行外部脚本。 有关可配置选项的详细信息，请参阅[SQL Server 快速启动板服务配置](../security/sql-server-launchpad-service-account.md)。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>在处理过程 (SQLRUserGroup) 中使用的身份

**SQLRUserGroup** （SQL 受限制的用户组） 创建 SQL Server 安装程序，并且包含低特权本地 Windows 用户帐户的池。 当需要外部进程时，快速启动板采用一个可用的工作帐户，并使用它运行的进程。 更具体地说，快速启动板激活可用的工作帐户、 将其映射到调用用户的标识并运行辅助角色帐户下的脚本。

+ **SQLRUserGroup**链接到特定实例。 已在哪台计算机启用了学习每个实例需要一个单独的池的辅助角色帐户。 帐户不能在各个实例之间共享。

+ 用户帐户池的大小是静态的默认值为 20，它支持 20 个并发会话。 可以同时启动的外部运行时会话数受此用户帐户池的大小。 

+ 在池中的辅助角色帐户名属于 sqlinstancename*nn*。 例如，在默认实例， **SQLRUserGroup**包含帐户最多 MSSQLSERVER20 上命名 MSSQLSERVER01、 MSSQLSERVER02，等等。

并行的任务也不会占用更多的帐户。 例如，如果用户在运行使用并行处理的评分任务，同一个辅助角色帐户重复使用的所有线程。 如果想要的机器学习的频繁使用，则可以增加用于运行外部脚本的帐户数。 有关详细信息，请参阅[修改机器学习的用户帐户池](../../advanced-analytics/administration/modify-user-account-pool.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>在 SQL Server 2019 AppContainer 隔离

在 SQL Server 2019，安装程序无法再创建辅助角色帐户以执行**SQLRUserGroup**。 相反，通过实现隔离[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)。 在运行时，当存储的过程或查询中检测到的外部脚本，SQL Server 快速启动板使用调用请求的特定于扩展的启动器。 快速启动板调用其标识下, 一个过程中的相应的运行时环境，并实例化 AppContainer 来包含它。 此更改是有益的因为不再需要本地帐户和密码管理。 此外，在安装中，禁止使用本地用户帐户，消除了本地用户帐户依赖项意味着现在可以使用此功能。

实现 SQL server 时，AppContainers 是内部机制。 虽然不会看到 AppContainers 在 Process Monitor 中的实际证据，您可以由安装程序以防止进程进行网络调用创建的出站防火墙规则中找到它们。 有关详细信息，请参阅[SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)。

> [!Note]
> 在 SQL Server 2019 **SQLRUserGroup**仅有一个成员，它现在是而不是多个辅助角色帐户的单个 SQL Server 快速启动板服务帐户。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup 授予权限

默认情况下的成员**SQLRUserGroup**具有读取和执行 SQL Server 中的文件权限**Binn**， **R_SERVICES**，和**PYTHON_SERVICES**目录，有权访问的可执行文件、 库和 SQL Server 一起安装的 R 和 Python 分发版中的内置数据集。 

若要保护 SQL 服务器上的敏感资源，可以选择定义访问拒绝对访问控制列表 (ACL) **SQLRUserGroup**。 相反，您还可以授予对主机计算机，除了 SQL Server 本身存在的本地数据资源的权限。 

根据设计， **SQLRUserGroup**不具有数据库登录名或任何数据的权限。 在某些情况下，你可能想要创建一个登录名，以允许循环后的连接，尤其是在受信任的 Windows 标识调用用户时。 此功能称为[*隐式身份验证*](#implied-authentication)。 有关详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="identity-mapping"></a>标识映射

当启动会话时，快速启动板将调用用户的标识映射到辅助角色帐户。 外部 Windows 用户或到辅助角色帐户的有效 SQL 登录名的映射无效，仅对生存期的 SQL 存储过程用于执行外部脚本。 来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

在执行期间，快速启动板创建临时文件夹来存储会话数据，在会话结束时将其删除。 目录的访问受限。 对于 R，RLauncher 执行此任务。 对于 Python，PythonLauncher 执行此任务。 每个单独的辅助角色帐户限制到其自己的文件夹，并且无法访问其自身级别以上的文件夹中的文件。 但是，辅助角色帐户可以读取、 写入或删除已创建的会话工作文件夹下的子级。 如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>隐式身份验证 （循环后请求）

*隐式身份验证*描述在其下运行如低权限辅助角色帐户显示为受信任的用户标识到 SQL Server 上的外部进程循环后的数据或操作的请求的连接请求行为。 作为一个概念，隐式身份验证是唯一的 Windows 身份验证，在从外部进程，例如 R 或 Python 脚本发出的请求上指定可信的连接，SQL Server 连接字符串中。 它有时也称为*环回到*。

受信任的连接是从 R 和 Python 脚本，但仅限于与其他配置可正常工作。 在可扩展性体系结构中，R 和 Python 进程下运行辅助角色帐户，从父级继承权限**SQLRUserGroup**。 当连接字符串指定了`Trusted_Connection=True`，辅助角色帐户的标识显示在连接请求时，这是默认情况下，SQL Server 到未知。

若要建立受信任的连接成功，必须创建数据库登录名**SQLRUserGroup**。 这样做之后，任何受信任连接的任何成员**SQLRUserGroup**拥有到 SQL Server 登录权限。 有关分步说明，请参阅[添加到一个数据库登录名的 SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

受信任的连接不是连接请求的最常用的设计。 当 R 或 Python 脚本指定的连接时，它可以是更常见的是使用 SQL 登录名，或完全指定的用户名和密码，如果连接到 ODBC 数据源。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>如何隐式身份验证适用于 R 和 Python 的会话

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

作为下一步，请查看有关的说明[授予的权限](../../advanced-analytics/security/user-permission.md)。 对于使用 Windows 身份验证的服务器，则还应查看[添加到一个数据库登录名的 SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)若要了解何时需要额外的配置。