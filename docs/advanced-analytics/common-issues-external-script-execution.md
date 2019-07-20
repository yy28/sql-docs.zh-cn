---
title: 启动板服务和外部脚本执行的常见问题
ms.prod: sql
ms.technology: ''
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3786ab3ee17bbbc0b54e439e3466236af098ffd3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345167"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>SQL Server 中的快速启动板服务和外部脚本执行的常见问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server 受信任的快速启动板服务支持 R 和 Python 的外部脚本执行。 在 SQL Server 2016 R Services 中, SP1 提供服务。 SQL Server 2017 在初始安装过程中包括启动板服务。

多个问题可能会阻止启动板启动, 包括配置问题或更改或缺少网络协议。 本文提供了许多问题的疑难解答指南。 对于缺少的任何内容, 你可以将问题发布到[Machine Learning Server 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)。

## <a name="determine-whether-launchpad-is-running"></a>确定启动板是否正在运行

1. 打开 "**服务**" 面板 (services.msc)。 或者, 在命令行中键入 " **sqlservermanager13.msc** " 或 " **SQLServerManager14** " 以打开[SQL Server 配置管理器](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 记下启动板正在其下运行的服务帐户。 启用 R 或 Python 的每个实例都应具有其自己的启动板服务的实例。 例如, 命名实例的服务可能类似于_MSSQLLaunchpad $ InstanceName_。

3. 如果服务已停止, 请重新启动该服务。 重新启动时, 如果存在任何配置问题, 会在系统事件日志中发布一条消息, 并再次停止该服务。 有关服务停止的原因的详细信息, 请查看系统事件日志。

4. 查看 RSetup 的内容, 并确保安装程序中没有任何错误。 例如,*以代码0退出*的消息表示服务启动失败。

5. 若要查找其他错误, 请查看 rlauncher 的内容。

## <a name="check-the-launchpad-service-account"></a>检查快速启动板服务帐户

默认的服务帐户可能是 "nt service\$SQL2016" 或 "nt service\$SQL2017"。 最终部分可能会有所不同, 具体取决于你的 SQL 实例名称。

启动板服务 (启动板) 使用低特权服务帐户运行。 但是, 若要启动 R 和 Python 并与数据库实例通信, 启动板服务帐户需要以下用户权限:

- 以服务身份登录 (SeServiceLogonRight)
- 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)
- 跳过遍历检查 (SeChangeNotifyPrivilege)
- 调整进程的内存配额 (SeIncreaseQuotaSizePrivilege)

有关这些用户权限的信息, 请参阅[配置 windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)中的 "windows 特权和权限" 一节。

> [!TIP]
> 如果你熟悉如何使用支持诊断平台 (SDP) 工具进行 SQL Server 诊断, 则可以使用 SDP 检查名为 MachineName_UserRights 的输出文件。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>快速启动板的用户组无法在本地登录

在机器学习服务的设置过程中, SQL Server 创建 Windows 用户组**SQLRUserGroup** , 然后对其进行设置, 使其具有启动面板连接到 SQL Server 和运行外部脚本作业所需的所有权限。 如果启用此用户组, 则它还用于执行 Python 脚本。

但是, 在实施了更严格的安全策略的组织中, 此组所需的权限可能已被手动删除, 或者策略会自动吊销。 如果已删除权限, 则启动板将无法再连接到 SQL Server, SQL Server 无法调用外部运行时。

若要解决此问题，请确保组 **SQLRUserGroup** 拥有系统权限“允许本地登录”。 

有关详细信息，请参阅[配置 Windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

## <a name="permissions-to-run-external-scripts"></a>运行外部脚本的权限

即使快速启动板已正确配置, 如果用户无权运行 R 或 Python 脚本, 它也会返回错误。

如果作为数据库管理员安装了 SQL Server, 或者您是数据库所有者, 则会自动向您授予此权限。 但是, 其他用户通常具有更有限的权限。 如果他们尝试运行 R 脚本, 则会出现快速启动板错误。

若要解决此问题, 请在 SQL Server Management Studio 中, 安全管理员可以通过运行以下脚本来修改 SQL 登录名或 Windows 用户帐户:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

有关详细信息, 请参阅[GRANT (transact-sql)](../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>常见快速启动板错误

此部分列出了快速启动板返回的最常见错误消息。

## <a name="unable-to-launch-runtime-for-r-script"></a>"无法启动 R 脚本的运行时"

如果 R 用户的 Windows 组 (也用于 Python) 无法登录到运行 R Services 的实例, 你可能会看到以下错误:

- 尝试运行 R 脚本时生成的错误:

    * *无法启动“R”脚本的运行时。请检查“R”运行时的配置。*

    * *发生外部脚本错误。无法启动运行时。*

- [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服务生成的错误:

    * 无法初始化启动器 RLauncher.dll 

    * 未注册任何启动器 dll！ 

    * *安全日志指示帐户 NT 服务无法登录*

有关如何授予此用户组所需权限的信息, 请参阅[Install SQL Server 2016 R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制。

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"登录失败: 未向用户授予请求的登录类型"

默认情况下[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] , 在启动时使用以下帐户`NT Service\MSSQLLaunchpad`:。 此帐户由[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安装程序配置为具有所有必需的权限。

如果你将其他帐户分配到快速启动板, 或者 SQL Server 计算机上的某个策略删除了权限, 则该帐户可能没有必要的权限, 并且你可能会看到此错误:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登录失败: 未授予用户在此计算机上的请求登录类型。*

若要向新服务帐户授予必要的权限, 请使用本地安全策略应用程序, 并更新帐户的权限, 使其包含以下权限:

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"无法与启动板服务通信"

如果已安装了, 然后又启用了机器学习, 但当你尝试运行 R 或 Python 脚本时收到此错误, 则实例的启动板服务可能已停止运行。

1. 通过 Windows 命令提示符打开 SQL Server 配置管理器。 有关详细信息，请参阅 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 右键单击该实例的 SQL Server Launchpad, 然后选择 "**属性**"。

3. 选择 "**服务**" 选项卡, 然后验证该服务是否正在运行。 如果未运行, 请将**启动模式**更改为 "**自动**", 然后选择 "**应用**"。

4. 重新启动服务通常会解决此问题, 以便机器学习脚本能够运行。 如果重新启动不能解决问题, 请记下**二进制路径**属性中的路径和参数, 并执行以下操作:

    a. 查看启动器的 .config 文件, 并确保工作目录有效。

    b. 确保快速启动板使用的 Windows 组可以连接到 SQL Server 的实例。

    c. 如果更改任何服务属性, 请重新启动启动板服务。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"TmpFile 的错误创建失败"

在此方案中, 您已成功安装了机器学习功能, 并且启动了快速启动板。 尝试运行一些简单的 R 或 Python 代码, 但快速启动板失败, 并出现如下错误: 

>*无法与 R 脚本的运行时通信。请检查 R 运行时的要求。*

同时, 外部脚本运行时将以下消息作为 STDERR 消息的一部分写入: 

>*错误: 创建 tmpfile 失败。*

此错误表示快速启动板尝试使用的帐户没有登录数据库的权限。 实施严格的安全策略时可能会发生这种情况。 若要确定是否为这种情况, 请查看 SQL Server 日志, 并查看登录时是否拒绝了 MSSQLSERVER01 帐户。 特定于 R\_SERVICES 或 PYTHON\_服务的日志中提供了相同的信息。 查找 ExtLaunchError。

默认情况下, 将设置20个帐户并将其与 MSSQLSERVER01 到 MSSQLSERVER20 的名称关联。 如果使用 R 或 Python, 则可以增加帐户数。

若要解决此问题, 请确保组已安装并启用机器学习功能的本地实例的 "*允许本地登录*" 权限。 在某些环境中, 此权限级别可能需要来自网络管理员的 GPO 例外。

## <a name="not-enough-quota-to-process-this-command"></a>"配额不足, 无法处理此命令"

此错误可能意味着:

- 快速启动板可能没有足够的外部用户运行外部查询。 例如, 如果同时运行的外部查询超过20个, 并且只有20个默认用户, 则一个或多个查询可能会失败。

- 内存不足, 无法处理 R 任务。 此错误通常发生在默认环境中, 其中 SQL Server 可能使用最多 70% 的计算机资源。 有关如何修改服务器配置以支持通过 R 更好地使用资源的信息, 请参阅[实现 r 代码](r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>"找不到包"

如果在 SQL Server 中运行 R 代码, 并收到此消息, 但在 SQL Server 外运行相同的代码时未收到消息, 则意味着包未安装到 SQL Server 所使用的默认库位置。

此错误的发生方式有多种:

- 你在服务器上安装了新包, 但访问被拒绝, 因此 R 将包安装到用户库。

- 安装了 R Services, 然后安装了另一个 R 工具或库集, 包括 Microsoft R Server (独立)、Microsoft R Client、RStudio 等。

若要确定实例所使用的 R 包库的位置, 请打开 SQL Server Management Studio (或任何其他数据库查询工具), 连接到该实例, 然后运行以下存储过程:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>示例结果

*STDOUT message(s) from external script:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\mssql13.mssqlserver。SQL2016\\R_SERVICES "*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解决此问题, 必须将包重新安装到 SQL Server 实例库。

>[!NOTE]
>如果已将 SQL Server 2016 的实例升级为使用最新版本的 Microsoft R, 则默认库位置不同。 有关详细信息, 请参阅[使用 SqlBindR 升级 R Services 的实例](install/upgrade-r-and-python.md)。

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>由于 Dll 不匹配, 快速启动板关闭

如果使用其他功能安装数据库引擎, 修补服务器, 然后使用原始媒体添加机器学习功能, 可能会安装错误的机器学习组件版本。 当启动板检测到版本不匹配时, 它将关闭并创建转储文件。

若要避免此问题, 请确保安装与服务器实例处于相同修补程序级别的任何新功能。

**升级的错误方法:**

1. 安装 SQL Server 2016 (不带 R Services)。
2. 升级 SQL Server 2016 累积更新2。
3. 使用 RTM 媒体安装 R Services (数据库内)。

**升级的正确方法:**

1. 安装 SQL Server 2016 (不带 R Services)。
2. 将 SQL Server 2016 升级到所需的修补程序级别。 例如, 安装 Service Pack 1, 然后安装累积更新2。
3. 若要在正确的修补级别添加功能, 请再次运行 SP1 和 CU2 安装程序, 然后选择 "R Services (数据库内)"。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>如果需要8dot3 表示法, 启动板无法启动

> [!NOTE] 
> 在较早的系统上, 如果存在8dot3 表示法要求, 启动板可能无法启动。 此要求已在以后的版本中删除。 SQL Server 2016 R 服务客户应安装以下各项之一:
> * SQL Server 2016 SP1 和 CU1:[SQL Server 累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、累积更新3以及此[修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)(按需提供)。

为了兼容 R, SQL Server 2016 R Services (数据库内) 需要安装功能的驱动器, 以支持使用*8dot3 表示法*创建短文件名。 8\.3 文件名也称为*短*文件名, 并用于与早期版本的 Microsoft Windows 兼容或用作长文件名的替代项。

如果安装 R 的卷不支持短文件名, 则从 SQL Server 启动 R 的进程可能找不到正确的可执行文件, 并且启动板将无法启动。

作为一种解决方法, 你可以在安装了 SQL Server 的卷上启用8dot3 表示法, 并在其中安装 R Services。 然后，必须提供 R Services 配置文件中工作目录的短名称。

1. 若要启用8dot3 表示法, 请运行包含*8dot3name*参数的 fsutil 实用程序, 如下所述: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 启用8dot3 表示法后, 打开 RLauncher 文件, 并记录的`WORKING_DIRECTORY`属性。 有关如何查找此文件的信息, 请参阅[用于机器学习疑难解答的数据收集](data-collection-ml-troubleshooting-process.md)。

3. 使用带有*file*参数的 fsutil 实用工具为在 WORKING_DIRECTORY 中指定的文件夹指定短文件路径。

4. 编辑配置文件以指定在 WORKING_DIRECTORY 属性中输入的相同工作目录。 或者, 您可以指定一个不同的工作目录, 并选择与8dot3 表示法已兼容的现有路径。


## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知问题](machine-learning-troubleshooting-faq.md)

[计算机学习疑难解答的数据收集](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接疑难解答](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
