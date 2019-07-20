---
title: R 和 Python 扩展的安全性概述
description: SQL Server 机器学习服务中扩展性框架的安全性概述。 登录名和用户帐户、SQL Server Launchpad 服务、辅助角色帐户、运行多个脚本的安全性以及文件权限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 51587878d4a16145ff53eaa397da69130c04d7d5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343369"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server 机器学习服务中扩展性框架的安全性概述

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了用于将 SQL Server 数据库引擎与相关组件与扩展性框架集成的总体安全体系结构。 它检查安全对象、服务、进程标识和权限。 有关 SQL Server 中的扩展性的主要概念和组件的详细信息, 请参阅[SQL Server 机器学习服务中的扩展性体系结构](extensibility-framework.md))。

## <a name="securables-for-external-script"></a>外部脚本的安全对象

使用 R 或 Python 编写的外部脚本将作为输入参数提交给为此目的而创建的[系统存储过程](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 或者包装在您定义的存储过程中。 另外, 还可以在数据库表中使用二进制格式预先训练和存储的模型, 该模型可在 T-sql[预测](../../t-sql/queries/predict-transact-sql.md)函数中调用。

由于脚本是通过现有的数据库架构对象、存储过程和表提供的, 因此没有针对 SQL Server 机器学习服务的新[安全对象](../../relational-databases/security/securables.md)。

无论你使用脚本的方式如何, 或者它们所包含的内容如何, 都将创建并保存数据库对象, 但不会引入新的对象类型来存储脚本。 因此, 使用、创建和保存数据库对象的功能很大程度上取决于已为用户定义的数据库权限。

<a name="permissions"></a>

## <a name="permissions"></a>权限

SQL Server 的数据库登录名和角色的数据安全模型将扩展到 R 和 Python 脚本。 需要 SQL Server 登录名或 Windows 用户帐户才能运行使用 SQL Server 数据的外部脚本或以 SQL Server 作为计算上下文运行的外部脚本。 具有执行即席查询权限的数据库用户可以从 R 或 Python 脚本访问相同的数据。

登录名或用户帐户标识的*安全主体*可能需要多个级别的访问权限, 具体取决于外部脚本要求:

+ 访问启用了外部脚本的数据库的权限。
+ 从安全对象 (如表) 读取数据的权限。
+ 将新数据写入表的功能, 如模型或评分结果。
+ 能够创建新对象 (如表)、使用外部脚本的存储过程或使用 R 或 Python 作业的自定义函数。
+ 在 SQL Server 计算机上安装新包或使用提供给一组用户的包的权限。

使用 SQL Server 作为执行上下文的每个用户都必须映射到数据库中的用户。 您可以创建角色来管理权限集, 并将用户分配到这些角色, 而不是单独设置用户权限, 而不是单独设置数据库用户权限。

有关详细信息, 请参阅[向用户授予 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)。

## <a name="permissions-when-using-an-external-client-tool"></a>使用外部客户端工具时的权限

如果用户需要在数据库中运行外部脚本或访问数据库对象和数据, 则在外部客户端工具中使用 R 或 Python 的用户必须将其登录名或帐户映射到数据库中的用户。 无论是从远程数据科学客户端发送外部脚本还是使用 T-sql 存储过程运行外部脚本, 都需要相同的权限。

例如, 假设你创建了一个在本地计算机上运行的外部脚本, 并且想要在 SQL Server 上运行该脚本。 必须确保符合以下条件：

+ 数据库允许远程连接。
+ 用于数据库访问的 SQL 登录名或 Windows 帐户已添加到实例级别的 SQL Server。
+ SQL 登录名或 Windows 用户必须有权执行外部脚本。 通常，此权限只能由数据库管理员添加。
+ 必须在每个数据库中的外部脚本执行以下任一操作的数据库中, 以具有相应权限的用户身份添加 SQL 登录名或窗口用户:
  + 正在检索数据。
  + 写入或更新数据。
  + 创建新对象, 例如表或存储过程。

设置登录名或 Windows 用户帐户并为其提供必要的权限后, 可以通过使用 R 中的数据源对象或 Python 中的**revoscalepy**库, 或通过调用存储过程来在 SQL Server 上运行外部脚本,包含外部脚本。

每当从 SQL Server 启动外部脚本时, 数据库引擎安全将获取启动该作业的用户的安全上下文, 并管理用户的映射或登录到安全对象的登录。

因此, 从远程客户端启动的所有外部脚本都必须指定登录名或用户信息作为连接字符串的一部分。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部处理中使用的服务 (快速启动板)

扩展性框架将一个新的 NT 服务添加到 SQL Server 安装中的[服务列表](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details):[**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)。

数据库引擎使用 SQL Server Launchpad 服务将 R 或 Python 会话实例化为单独的进程。 该进程在低特权帐户下运行;与 SQL Server 不同, 快速启动板本身, 以及用于执行存储过程或主机查询的用户标识。 在较低特权帐户下, 在单独的进程中运行脚本是 SQL Server 中的 R 和 Python 的安全和隔离模型的基础。

除了启动外部进程外, 快速启动板还负责跟踪调用用户的标识, 并将该标识映射到用于启动进程的低特权辅助角色帐户。 在某些情况下, 脚本或代码回调到 SQL Server 进行数据和操作时, 快速启动板通常能够无缝地管理标识传输。 如果调用用户具有足够的权限, 则包含 SELECT 语句或调用函数以及其他编程对象的脚本通常会成功。

> [!NOTE]
> 默认情况下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] , 配置为在**NT Service\MSSQLLaunchpad**下运行, 该设置具有运行外部脚本所需的所有权限。 有关可配置选项的详细信息, 请参阅[SQL Server Launchpad 服务配置](../security/sql-server-launchpad-service-account.md)。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>处理中使用的标识 (SQLRUserGroup)

**SQLRUserGroup**(SQL 受限用户组) 由 SQL Server 安装程序创建, 并且包含低权限本地 Windows 用户帐户的池。 需要外部进程时, 快速启动板将使用可用的辅助角色帐户, 并使用该帐户来运行进程。 更具体地说, 快速启动板将激活可用的辅助角色帐户, 将其映射到调用用户的标识, 并在辅助角色帐户下运行该脚本。

+ **SQLRUserGroup**链接到特定的实例。 启用了机器学习的每个实例都需要一个单独的辅助角色帐户池。 帐户不能在各个实例之间共享。

+ 用户帐户池的大小是静态的, 默认值为 20, 这支持20个并发会话。 可以同时启动的外部运行时会话数受此用户帐户池的大小限制。 

+ 池中的辅助角色帐户名称的格式为 SQLInstanceName*nn*。 例如, 在默认实例上, **SQLRUserGroup**包含名为 MSSQLSERVER01、mssqlserver02 等用户名的帐户, 依此类推, 最多 MSSQLSERVER20。

并行化任务不会使用其他帐户。 例如, 如果用户运行的计分任务使用并行处理, 则将对所有线程重复使用同一辅助角色帐户。 如果要大量使用机器学习, 可以增加用于运行外部脚本的帐户数。 有关详细信息, 请参阅[为机器学习修改用户帐户池](../../advanced-analytics/administration/modify-user-account-pool.md)。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019 中的 AppContainer 隔离

在 SQL Server 2019 中, 安装程序不再为**SQLRUserGroup**创建辅助角色帐户。 相反, 隔离是通过[AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation)实现的。 在运行时, 在存储过程或查询中检测到外部脚本时, SQL Server 会调用快速启动板, 请求提供特定于扩展的启动程序。 快速启动板在进程的标识下调用适当的运行时环境, 并实例化 AppContainer 以包含它。 此更改很有用, 因为不再需要本地帐户和密码管理。 此外, 在禁止本地用户帐户的安装上, 消除本地用户帐户依赖关系意味着你现在可以使用此功能。

SQL Server 实现, AppContainers 是一种内部机制。 尽管你不会在进程监视器中看到 AppContainers 的物理证据, 但你可以在由安装程序创建的出站防火墙规则中找到它们, 以防止进程发出网络调用。 有关详细信息, 请参阅[SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)。

> [!Note]
> 在 SQL Server 2019 中, **SQLRUserGroup**只具有一个现在为单一 SQL Server Launchpad 服务帐户而不是多个辅助角色帐户的成员。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>向 SQLRUserGroup 授予的权限

默认情况下, **SQLRUserGroup**的成员对 SQL Server **Binn**、 **R_SERVICES**和**PYTHON_SERVICES**目录中的文件具有读取和执行权限, 可以访问 R 中的可执行文件、库和内置数据集和 Python 分发版随 SQL Server 一起安装。 

若要保护 SQL Server 上的敏感资源, 可以选择定义拒绝访问**SQLRUserGroup**的访问控制列表 (ACL)。 相反, 你还可以授予对主计算机上的本地数据资源的权限, 而不是 SQL Server 本身。 

按照设计, **SQLRUserGroup**没有数据库登录名或任何数据的权限。 在某些情况下, 你可能想要创建一个登录名以允许环回连接, 特别是当受信任的 Windows 标识是调用用户时。 此功能称为[*隐含身份验证*](#implied-authentication)。 有关详细信息, 请参阅[Add SQLRUserGroup as a database user](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="identity-mapping"></a>标识映射

会话启动时, 启动板将调用用户的标识映射到辅助角色帐户。 外部 Windows 用户或有效 SQL 登录名的映射仅在执行外部脚本的 SQL 存储过程的生存期内有效。 来自同一登录名的并行查询将映射到同一用户辅助角色帐户。

在执行期间, 快速启动板将创建用于存储会话数据的临时文件夹, 并在会话结束时删除它们。 目录受访问限制。 对于 R, RLauncher 执行此任务。 对于 Python, PythonLauncher 执行此任务。 每个单独的辅助角色帐户仅限于其自己的文件夹, 并且不能访问其自身级别以上的文件夹中的文件。 不过, 辅助角色帐户可以读取、写入或删除已创建的会话工作文件夹下的子文件夹。 如果你是计算机的管理员，可以查看针对每个进程创建的目录。 每个目录按其会话 GUID 标识。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>默示身份验证 (循环发送请求)

*默示身份验证*描述了连接请求行为, 在这种情况下, 以低特权辅助角色帐户运行的外部进程作为受信任的用户标识显示, 以 SQL Server 对数据或操作的循环后请求。 作为一种概念, 隐含身份验证对于 Windows 身份验证是唯一的, 在 SQL Server 连接字符串中指定可信连接, 这是来自外部进程 (如 R 或 Python 脚本) 的请求。 有时也称为 "*循环*"。

可信连接可从 R 和 Python 脚本中进行, 但仅适用于其他配置。 在扩展性体系结构中, R 和 Python 进程在辅助角色帐户下运行, 从父**SQLRUserGroup**继承权限。 当连接字符串指定`Trusted_Connection=True`时, 将在连接请求中显示辅助角色帐户的标识, 默认情况下, 该标识为 SQL Server。

若要成功进行可信连接, 必须创建**SQLRUserGroup**的数据库登录名。 完成此操作后, 来自**SQLRUserGroup**的任何成员的任何受信任连接都具有对 SQL Server 的登录权限。 有关分步说明, 请参阅[将 SQLRUserGroup 添加到数据库登录名](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

可信连接不是连接请求的最广泛使用的表述。 当 R 或 Python 脚本指定连接时, 如果连接到 ODBC 数据源, 则使用 SQL 登录名或完全指定的用户名和密码可能更常见。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>默示身份验证如何适用于 R 和 Python 会话

下图显示了与 R 运行时的 SQL Server 组件之间的交互, 以及如何对 R 执行隐含身份验证。

![R 的隐含身份验证](../security/media/implied-auth-rsql.png)

下图显示了 SQL Server 组件与 Python 运行时之间的交互, 以及如何对 Python 进行隐含身份验证。

![适用于 Python 的隐式身份验证](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>不支持静态透明数据加密

对于发送到外部脚本运行时或从中接收的数据, 不支持[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) 。 原因是外部进程 (R 或 Python) 在 SQL Server 进程之外运行。 因此, 外部运行时使用的数据不受数据库引擎的加密功能保护。 此行为与在 SQL Server 计算机上运行的任何其他客户端 (从数据库读取数据并进行复制) 没有什么不同。

因此, TDE 不会应用于 R 或 Python 脚本中使用的任何数据, 也**不会**应用到保存到磁盘的任何数据或任何持久的中间结果。 但是, 其他类型的加密, 如在文件或文件夹级别应用的 Windows BitLocker 加密或第三方加密仍适用。

在[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)的情况下, 外部运行时不具有对加密密钥的访问权限。 因此, 无法将数据发送到脚本。

## <a name="next-steps"></a>后续步骤

本文介绍可[扩展性框架](../../advanced-analytics/concepts/extensibility-framework.md)中内置的安全体系结构的组件和交互模型。 本文中所述的要点包括快速启动板、SQLRUserGroup 和辅助角色帐户的用途、R 和 Python 的进程隔离, 以及如何将用户标识映射到辅助角色帐户。 

下一步, 请查看有关[授予权限](../../advanced-analytics/security/user-permission.md)的说明。 对于使用 Windows 身份验证的服务器, 还应查看 "[将 SQLRUserGroup 添加到数据库登录名](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)" 以了解何时需要其他配置。