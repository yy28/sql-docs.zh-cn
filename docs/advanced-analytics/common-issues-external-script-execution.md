---
title: "SQL Server 中的外部脚本执行的常见问题 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 10/11/2017
ms.prod: sql-non-specified
ms.prod_service: r-services
ms.service: 
ms.component: advanced-analytics
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1dfc244fbe77d7938853cf6c1109e190c464436
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="common-issues-with-external-script-execution-in-sql-server"></a>SQL Server 中的外部脚本执行的常见问题

本文包含已知的问题和常见问题的 SQL Server 中运行 R 或 Python 代码的列表。

在开始之前，我们建议你有关你的系统收集一些信息。 若要了解如何操作，请参阅[数据收集以进行故障排除](data-collection-ml-troubleshooting-process.md)。

此外，请查看特定于初始设置或配置的常见问题的列表：[安装和升级常见问题](r/upgrade-and-installation-faq-sql-server-r-services.md)。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="launchpad-issues"></a>快速启动板问题

SQL Server 受信任的快速启动板服务管理外部脚本和通信与 R、 Python 或其他外部运行时的执行。 多个问题会阻止从开始，包括配置问题或更改，或缺少网络协议的快速启动板。

故障排除过程的一部分，首先通过回答以下问题：

- 未快速启动板始终无法运行，或它未停止工作？
- 快速启动板下运行的服务帐户？
- 快速启动板服务帐户有哪些用户权限？

### <a name="determine-whether-launchpad-is-running"></a>确定是否正在运行快速启动板

1. 打开**服务**面板 (Services.msc)。 或者，从命令行中，键入**SQLServerManager13.msc**或**SQLServerManager14.msc**以打开[SQL Server 配置管理器](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 记下运行快速启动板服务帐户。 启用了 R 或 Python 每个实例应具有自己的快速启动板服务实例。 例如，对于命名实例的服务可能类似于_MSSQLLaunchpad$ InstanceName_。

3. 如果该服务已停止，重新启动它。 在重新启动，如果没有配置任何问题，在系统事件日志中，发布消息，并再次停止服务。 检查系统事件日志中有关服务停止原因的详细信息。

4. 查看 RSetup.log 中的内容，并确保在设置中没有任何错误。 例如，消息*退出代码 0*指示服务启动失败。

5. 若要查找其他错误，请查看 rlauncher.log 的内容。

### <a name="check-the-launchpad-service-account"></a>检查快速启动板服务帐户

默认服务帐户可能是"NT 服务\$SQL2016"或"NT 服务\$SQL2017"。 最后部分可能有所不同，具体取决于你的 SQL 实例名称。

快速启动板服务 (Launchpad.exe) 通过使用低特权服务帐户运行。 但是，若要启动 R 和 Python 和与数据库实例通信，快速启动板服务帐户需要以下用户权限：

- 以服务身份登录 (SeServiceLogonRight)
- 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)
- 跳过遍历检查 (SeChangeNotifyPrivilege)
- 调整进程 (SeIncreaseQuotaSizePrivilege) 的内存配额

有关这些用户权限的信息，请参阅中的"Windows 特权和权限"部分[配置 Windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

> [!TIP]
> 如果你熟悉支持诊断平台 (SDP) 工具用于 SQL Server 诊断，你可以使用 SDP 来查看 MachineName_UserRights.txt 同名输出文件。

### <a name="review-launchpad-requirements"></a>查看快速启动板要求

任何几个问题可以阻止启动快速启动板。 快速启动板服务可能会启动，然后停止或崩溃或该服务可能会停止出现连接超时。 在这些情况下，系统通常已被更改或配置，从而快速启动板无法运行。

#### <a name="determine-whether-8dot3-notation-is-enabled"></a>确定是否已启用 8.3 文件名表示法

为了与 R 兼容，SQL Server 2016 R Services （数据库） 所需功能安装以使用支持的短文件名创建的驱动器*8.3 文件名表示法*。 8.3 文件名也被称为*的短文件名*，并且它适用于使用早期版本的 Microsoft Windows 或作为长文件名的替代方法的兼容性。

如果你安装 R 的卷不支持短文件名，启动 R 从 SQL Server 的进程可能无法找到正确的可执行文件，并快速启动板将不会启动。

一种解决方法，你可以启用卷上的 8.3 文件名表示法，其中安装 SQL Server 和 R Services 的安装位置。 然后，必须提供 R Services 配置文件中工作目录的短名称。

1. 若要启用 8.3 文件名表示法，运行 fsutil 实用程序用于*8dot3name*参数如下所述： [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 8.3 文件名表示法启用后，打开 RLauncher.config 文件并记下的属性`WORKING_DIRECTORY`。 有关如何查找此文件的信息，请参阅[用于机器学习故障排除数据收集](data-collection-ml-troubleshooting-process.md)。

3. 将 fsutil 实用程序用于*文件*参数来指定 WORKING_DIRECTORY 中指定的文件夹的短文件名路径。

4. 编辑配置文件以指定在 WORKING_DIRECTORY 属性中输入相同的工作目录。 或者，可以指定不同的工作目录，并选择已 8.3 文件名表示法与兼容的路径。

> [!NOTE] 
> 以后版本将消除此限制。 如果你遇到此问题，安装以下项之一：
> * SQL Server 2016 SP1 和 CU1: [for SQL Server 的累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、 累积更新 3 和这[修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)，即可以根据需要使用。

#### <a name="the-user-group-for-launchpad-cannot-log-on-locally"></a>快速启动板的用户组不能在本地登录

安装过程中的机器学习服务，SQL Server 创建 Windows 用户组**SQLRUserGroup** ，然后将其设置使用快速启动板来连接到 SQL Server 和运行外部脚本作业所需的所有权限。 如果启用了此用户组，它还用于执行 Python 脚本。

但是，在组织中限制性更强的安全策略实施的情况，此组所需的权限可能已被手动删除，或者它们可能会自动吊销的策略。 如果删除了权限，快速启动板可以不再连接到 SQL Server，并且 SQL Server 不能调用外部运行时。

若要解决此问题，请确保组 **SQLRUserGroup** 拥有系统权限“允许本地登录”。

有关详细信息，请参阅[配置 Windows 服务帐户和权限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。

#### <a name="improper-setup-leading-to-mismatched-dlls"></a>从而导致不匹配的 Dll 不正确的安装程序

如果你使用其他功能，修补程序服务器上，安装数据库引擎，然后通过使用原始媒体更高版本添加机器学习功能，可能安装了错误版本的机器学习组件。 当快速启动板检测到版本不匹配时，则它将关闭并创建转储文件。

若要避免此问题，请务必与服务器实例安装在相同的修补程序级别的任何新功能。

**升级的错误方法：**

1. 安装不 R Services 的 SQL Server 2016。
2. 升级 SQL Server 2016 累积更新 2。
3. 通过使用 RTM 媒体中安装 R Services （数据库）。

**升级的正确方法：**

1. 安装不 R Services 的 SQL Server 2016。
2. 升级到所需的修补程序级别的 SQL Server 2016。 例如，安装 Service Pack 1 和累积更新 2。
3. 若要在正确的修补程序级别添加功能，请运行 SP1 和 CU2 重新，安装程序，然后选择 R Services （数据库）。 

#### <a name="check-whether-a-user-has-rights-to-run-external-scripts"></a>检查用户是否有权运行外部脚本

即使快速启动板已正确配置，它将返回错误，如果用户没有权限来运行 R 或 Python 脚本。

如果您安装 SQL Server 作为数据库管理员或数据库所有者，你会自动将授予此权限。 但是，其他用户通常具有更受限制的权限。 如果用户尝试运行 R 脚本时，它们会获得快速启动板错误。

若要解决此问题，在 SQL Server Management Studio，安全管理员可以修改的 SQL 登录名或 Windows 用户帐户通过运行以下脚本：

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

有关详细信息，请参阅[GRANT (Transact SQL](../t-sql/statements/grant-transact-sql.md)。

### <a name="common-launchpad-errors"></a>常见的快速启动板错误

本部分列出的快速启动板返回的最常见的错误消息。

#### <a name="error-unable-to-launch-runtime-for-r-script"></a>错误：*无法启动 R 脚本的运行时*

如果 Windows 组 （也用于 Python） 的 R 用户无法登录到运行 R Services 的实例，你可能会看到以下错误：

- 当你尝试运行 R 脚本时生成的错误：

    * *无法启动“R”脚本的运行时。请检查“R”运行时的配置。

    * *发生外部脚本错误。无法启动运行时。

- 生成的错误[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服务：

    * 无法初始化启动器 RLauncher.dll

    * 未注册任何启动器 dll！

    * *安全日志指示 NT 服务的帐户无法登录*

有关如何授予必要的权限的此用户组的信息，请参阅[设置 SQL Server R Services](r/set-up-sql-server-r-services-in-database.md)。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制。

#### <a name="error-logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>错误：*登录失败： 尚未授予用户请求的登录类型*

默认情况下，[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]在启动时使用以下帐户： `NT Service\MSSQLLaunchpad`。 帐户由配置[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安装程序以具有所有必需的权限。

如果将不同的帐户分配给快速启动板，或右删除的 SQL Server 计算机上的策略，该帐户可能没有必要的权限，并且你可能会看到此错误：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登录失败: 未授予用户在此计算机上的请求登录类型。*

若要授予必要的权限来的新的服务帐户，使用本地安全策略应用程序，并更新该帐户的权限，以便包括以下权限：

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

#### <a name="error-unable-to-communicate-with-the-launchpad-service"></a>错误：*无法与快速启动板服务通信*

如果你事先安装并随后启用机器学习中，但当你尝试运行 R 或 Python 脚本时出现此错误，针对该实例快速启动板服务可能已停止运行。

1. 通过 Windows 命令提示符打开 SQL Server 配置管理器。 有关详细信息，请参阅 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 对于实例，右键单击 SQL Server 快速启动板，然后选择**属性**。

3. 选择**服务**选项卡上，然后验证该服务正在运行。 如果未运行，更改**启动模式**到**自动**，然后选择**应用**。

4. 重新启动服务通常可以解决问题，以便计算机学习脚本可以运行。 如果在重新启动操作未修复问题，请注意的路径和中的自变量**二进制路径**属性，并执行以下：

    a. 查看启动器的.config 文件，并确保工作目录无效。

    b. 确保使用快速启动板的 Windows 组可以连接到 SQL Server 实例中所述[上一节](#bkmk_LaunchpadTS)。

    c. 如果你更改任何服务属性，请重新启动快速启动板服务。

#### <a name="error-fatal-error-creation-of-tmpfile-failed"></a>错误： *tmpFile 错误创建失败*

在此方案中，你已成功安装机器学习功能，并快速启动板正在运行。 您尝试运行一些简单的 R 或 Python 代码，但快速启动板失败并出现错误如下所示： 

>*无法与 R 脚本的运行时进行通信。请检查 R 运行时的要求。*

同时，外部脚本运行时作为 STDERR 消息的一部分编写以下消息： 

>*错误： 创建 tmpfile 失败。*

此错误指示快速启动板尝试要使用的帐户不具有登录到数据库的权限。 当实现严格的安全策略时，会发生此情况。 若要确定这是否是这种情况，请查看 SQL Server 日志中，并检查以查看是否 MSSQLSERVER01 帐户被拒绝在登录。 在日志中特定于 R 提供的相同信息\_服务或 PYTHON\_服务。 查找 ExtLaunchError.log。

默认情况下，20 帐户设置和与 Launchpad.exe 过程中，与通过 MSSQLSERVER20 名称 MSSQLSERVER01 关联。 如果你进行大量使用 R 或 Python，则可以增加的帐户的数量。

若要解决此问题，请确保组具有*允许本地登录*到机器学习功能已安装并启用其中的本地实例的权限。 在某些环境中，此权限级别可能需要从网络管理员 GPO 异常。

## <a name="r-script-issues"></a>R 脚本问题

本部分包含特定于执行 R 脚本和 R 脚本错误的一些常见的问题。 该列表不是全面，因为存在许多 R 程序包，并且错误可能会与不同版本之间的相同的 R 包。 我们建议你在上发布 R 脚本错误[Microsoft R Server 论坛](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)，它支持机器学习中 R Services （数据库中），机学习 Python、 Microsoft R 客户端，与 Microsoft R 服务使用的组件服务器。

### <a name="multiple-r-instances-on-the-same-computer"></a>同一台计算机上的多个 R 实例

它可以轻松地在不同版本中发现自己与在同一计算机上的 R 的多种发行版本，以及相同的 R 包的多个副本。 例如，如果你安装机器学习 Server （独立） 和机器学习服务 （数据库），安装程序将创建单独的 R 库版本。 

当您尝试从命令行运行脚本，并且你不确定你使用的库，实现这种复制将成为问题。 或者，可能会将程序包安装到错误的库，然后稍后想要知道为什么无法找到包从 SQL Server。

+ 避免直接使用的 R 库和安装的 SQL Server 实例，用于除在有限情况下，例如故障排除的工具或安装新包。 
+ 如果你需要使用 R 命令行工具，则可以安装[Microsoft R 客户端](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)。 
+ SQL Server 提供 R 包的数据库中的管理。 这是创建可以在用户之间共享的 R 包库的最简单方法。 有关详细信息，请参阅[for SQL Server 的 R 包管理](r/r-package-management-for-sql-server-r-services.md)。

### <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免当在 SQL 计算上下文中运行 R 时清除工作区

尽管在 R 控制台工作时，清除工作区中均相同，但它可以有 SQL 中的意外的后果计算上下文。

`revoScriptConnection`是包含有关从 SQL Server 调用 R 会话的信息的 R 工作区中的对象。 但是，如果 R 代码中包含的命令以清除工作区 (如`rm(list=ls())`)，以及清除有关会话和 R 工作区中的其他对象的所有信息。

一种解决方法，避免不加选择地清除的变量和其他对象，当 SQL Server 中运行 R 时。 你可以通过使用删除特定变量**删除**函数：

```R
remove('name1', 'name2', ...)
```

如果有多个要删除的变量，我们建议你将临时变量的名称保存到列表，然后执行列表上的定期垃圾回收。

### <a name="implied-authentication-for-remote-execution-via-odbc"></a>通过 ODBC 远程执行的的默示身份验证

如果你连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算机，以便运行 R 命令通过使用**RevoScaleR**函数时可能会出现错误使用将数据写入到服务器的 ODBC 调用。 仅在你使用 Windows 身份验证时，将发生此错误。

原因是为 R Services 创建的工作帐户没有权限来连接到服务器。 因此，不能代表你执行 ODBC 调用。 因为具有 SQL 登录名的凭据通过显式从 R 客户端到 SQL Server 实例，然后执行到 ODBC 具有 SQL 登录名未出现该问题。 但是，使用 SQL 登录名也是比使用 Windows 身份验证的安全级别较低的。

若要启用您的 Windows 凭据启动了远程的 SQL Server 脚本从安全地传递必须模拟你的凭据。 此过程称为_默示身份验证_。 若要完成此操作，请在 SQL Server 计算机运行 R 或 Python 脚本辅助帐户必须具有正确的权限。

1. 打开[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]为你想要运行 R 代码的实例上的管理员。

2. 运行以下脚本。 请务必编辑该用户组名称，如果更改了默认值和的计算机和实例名称。

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

### <a name="the-r-script-works-outside-of-t-sql-but-not-in-a-stored-procedure"></a>R 脚本适用 T-SQL 的外部，但不是能在存储过程

将 R 代码包装在存储过程中之前, 它是一个外部 IDE，或如 RTerm 或 RGui R 工具之一中运行 R 代码的好办法。 通过使用这些方法，你可以测试和调试的代码通过使用由。 详细的错误消息

但是，有时可正常运行在外部 IDE 或实用程序中的代码可能无法运行存储过程中或在 SQL Server 计算上下文。 如果发生这种情况，有各种问题，若要寻找之前可以假定包无法在 SQL Server 中工作。

1. 检查是否正在运行快速启动板。

2. 查看消息的输入的数据或输出数据是否包含具有不兼容或不受支持的数据类型的列。 例如，在 SQL 数据库上的查询通常返回 Guid 或 Rowguid，二者都是不受支持。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

3. 查看各个 R 函数，以确定所有参数是否都支持 SQL Server 计算上下文的帮助页。 ScaleR 的帮助，请使用内联 R 帮助命令，或请参阅[程序包引用](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

### <a name="you-get-different-results-from-the-same-script-when-running-in-sql-compared-to-other-environments"></a>从同一个脚本中获取不同的结果，在 SQL 相比其他环境中运行时

R 脚本可以在 SQL Server 环境中，返回不同的值，原因有多种：

- 当 SQL Server 和。 之间传递数据自动上某些数据类型，执行隐式类型转换有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

- 确定位数是一个因素。 例如，通常有 32 位和 64 位浮点点库的数学运算的结果中的差异。

- 确定是否在任何操作生成 Nan。 这可能会使结果无效。

- 当你拍摄接近于零的数字的倒数时，可以放大细微差异。

- 累积的舍入误差可能会导致小于零时而不是零的值之类的内容。

### <a name="error-not-enough-quota-to-process-this-command"></a>错误：*配额不足，无法处理此命令*

此错误可能意味着几种方法之一：

- 快速启动板可能会有足够的外部用户来运行外部查询。 例如，如果与此同时，你正在使用 20 个以上的外部查询，并且仅有 20 个的默认用户，则一个或多个查询可能会失败。

- 内存不足，便可处理 R 任务。 在默认环境中，其中 SQL Server 可能会使用为达 70%的计算机的资源通常发生此错误。 有关如何修改服务器配置，以支持更好地利用的资源的信息，请参阅[实现 R 代码](r/operationalizing-your-r-code.md)。

### <a name="error-cant-find-package"></a>错误：*找不到程序包*

如果你在 SQL Server 中运行 R 代码和收到此消息，但未获取消息，这是运行 SQL Server 外部相同的代码时，它表示到 SQL Server 使用的默认库位置未安装的包。

在许多方面会发生该错误：

- 在服务器上，安装新包，但访问被拒绝，因此，R 安装到用户库包。

- 你安装 R Services 安装 R 的另一个工具或的库，包括 Microsoft R Server （独立），Microsoft R 客户端，RStudio、 设置和等等。

若要确定实例所使用的 R 包库的位置，打开 SQL Server Management Studio （或任何其他数据库查询工具），连接到的实例，然后运行以下存储的过程：

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>示例结果

*STDOUT message(s) from external script:*

*[1]"c:\\程序文件\\Microsoft SQL Server\\MSSQL13。SQL2016\\R_SERVICES"*

*[1]"c: / Program 文件/Microsoft SQL Server/MSSQL13。SQL2016/R_SERVICES/库"*

若要解决此问题，你必须重新安装 SQL Server 实例库的程序包。

>[!NOTE]
>如果你已升级的 SQL Server 2016，以便使用最新版本的 Microsoft R 实例，则默认库位置会不同。 有关详细信息，请参阅[使用 SqlBindR 升级 R Services 的实例](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知的问题](machine-learning-troubleshooting-faq.md)

[进行故障排除机器学习的数据收集](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接进行故障排除](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
