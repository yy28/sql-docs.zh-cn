---
title: 快速启动板服务和 SQL Server 中的外部脚本执行的常见问题 |Microsoft Docs
ms.prod: sql
ms.technology: mlserver
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b480c400ae2068bb6701192e77d97672ddeb024e
ms.sourcegitcommit: b29745051be2326268f165cf72f5eb95dc893564
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50254443"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>使用快速启动板服务和 SQL Server 中的外部脚本执行常见的问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server Trusted Launchpad 服务对 R 和 Python 支持外部脚本执行。 在 SQL Server 2016 R Services，SP1 将提供服务。 SQL Server 2017 包括快速启动板 ervice 作为开头几安装的一部分。

多个问题会阻止从开始，包括配置问题或更改，或缺少的网络协议的快速启动板。 本文提供许多问题的疑难解答的指引。 对于任何我们错过了，您可以发布到的问题[Machine Learning Server 论坛](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)。

**适用于：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务

## <a name="determine-whether-launchpad-is-running"></a>确定是否正在运行快速启动板

1. 打开**Services**面板 (Services.msc)。 或者，从命令行中，键入**SQLServerManager13.msc**或**SQLServerManager14.msc**以打开[SQL Server 配置管理器](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 请记下运行快速启动板服务帐户。 启用了 R 或 Python 每个实例应具有它自己的 Launchpad 服务的实例。 例如，对于命名实例的服务可能类似于_MSSQLLaunchpad$ InstanceName_。

3. 如果该服务已停止，重新启动它。 在重新启动，如果有任何配置问题，在系统事件日志中发布消息，并再次停止该服务。 检查系统事件日志服务停止的原因有关的详细信息。

4. 查看内容 RSetup.log，并确保在安装程序中没有任何错误。 例如，消息*退出代码 0*指示服务启动失败。

5. 若要查找其他错误，请查看 rlauncher.log 的内容。

## <a name="check-the-launchpad-service-account"></a>检查快速启动板服务帐户

可能是默认服务帐户"NT Service\$SQL2016"或"NT Service\$SQL2017"。 最后的部分可能有所不同，具体取决于你的 SQL 实例名称。

快速启动板服务 (Launchpad.exe) 通过使用低特权服务帐户运行。 但是，若要启动 R 和 Python 和数据库实例通信，快速启动板服务帐户需要以下用户权限：

- 以服务身份登录 (SeServiceLogonRight)
- 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)
- 跳过遍历检查 (SeChangeNotifyPrivilege)
- 调整进程 (SeIncreaseQuotaSizePrivilege) 的内存配额

有关这些用户权限的信息，请参阅中的"Windows 特权和权限"部分[配置 Windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

> [!TIP]
> 如果已熟悉 SQL Server 的诊断使用支持诊断平台 (SDP) 工具，可以使用 SDP 若要查看名为 MachineName_UserRights.txt 输出文件。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Launchpad 的用户组不能在本地登录

安装过程中的机器学习服务，SQL Server 创建的 Windows 用户组**SQLRUserGroup**和设置与 launchpad 能够连接到 SQL Server 并运行外部脚本作业所需的所有权限。 如果启用此用户组，则它还用于执行 Python 脚本。

但是，在组织中实施更严格限制性安全策略的情况，此组所需的权限可能已被手动删除，或者它们可能会自动吊销策略。 如果已移除的权限，快速启动板可以不再连接到 SQL Server 和 SQL Server 不能调用外部运行时。

若要解决此问题，请确保组 **SQLRUserGroup** 拥有系统权限“允许本地登录”。

有关详细信息，请参阅[配置 Windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

## <a name="permissions-to-run-external-scripts"></a>运行外部脚本的权限

即使快速启动板配置正确，它将返回错误，如果用户不具有运行 R 或 Python 脚本的权限。

如果您安装了 SQL Server 作为数据库管理员或数据库所有者，会自动授予此权限。 但是，其他用户通常具有更有限的权限。 如果他们尝试运行 R 脚本，它们获得快速启动板错误。

若要解决此问题，在 SQL Server Management Studio，安全管理员可以 SQL 登录名或 Windows 用户帐户修改通过运行以下脚本：

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

有关详细信息，请参阅[GRANT (Transact SQL](../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>快速启动板的常见错误

本部分列出了快速启动板返回的最常见错误消息。

## <a name="unable-to-launch-runtime-for-r-script"></a>"无法启动的 R 脚本运行时"

如果 R 用户 （也用于 Python） 的 Windows 组不能登录到运行 R Services 的实例，可能会看到以下错误：

- 当你尝试运行 R 脚本时，生成的错误：

    * *无法启动“R”脚本的运行时。请检查“R”运行时的配置。

    * *发生外部脚本错误。无法启动运行时。

- 生成的错误[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服务：

    * 无法初始化启动器 RLauncher.dll

    * 未注册任何启动器 dll！

    * *安全日志指示帐户 NT 服务无法登录*

有关如何授予此用户组所需的权限的信息，请参阅[安装 SQL Server 2016 R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制。

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"登录失败： 未授予用户请求的登录类型"

默认情况下[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]在启动时使用以下帐户： `NT Service\MSSQLLaunchpad`。 通过配置的帐户[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安装程序以具有所有必需的权限。

如果将不同的帐户分配到快速启动板，或删除 SQL Server 计算机上的某个策略，该帐户可能没有必要的权限，并可能会看到此错误：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登录失败: 未授予用户在此计算机上的请求登录类型。*

若要授予对新的服务帐户所需的权限，请使用本地安全策略应用程序，并更新该帐户的权限，包括以下权限：

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"无法与 Launchpad 服务通信"

如果已安装并启用机器学习，但当您尝试运行 R 或 Python 脚本时收到此错误，该实例的 Launchpad 服务可能已停止运行。

1. 通过 Windows 命令提示符打开 SQL Server 配置管理器。 有关详细信息，请参阅 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 对于实例，右键单击 SQL Server 快速启动板，然后选择**属性**。

3. 选择**服务**选项卡，然后验证该服务正在运行。 如果未运行，更改**启动模式**到**自动**，然后选择**应用**。

4. 重新启动该服务通常解决了问题，以便可以运行机器学习脚本。 如果在重新启动未解决此问题，请注意的路径和中的自变量**二进制文件路径**属性，然后执行以下操作：

    A. 查看启动程序的.config 文件，并确保工作目录无效。

    B. 确保 Launchpad 使用的 Windows 组可以连接到 SQL Server 实例，如中所述[上一节](#bkmk_LaunchpadTS)。

    c. 如果服务属性的任何更改，重新启动 Launchpad 服务。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"错误 tmpFile 创建失败"

在此方案中，您已成功安装机器学习功能，并快速启动板正在运行。 尝试运行一些简单的 R 或 Python 代码，但快速启动板失败并出现错误如下所示： 

>*无法与 R 脚本的运行时进行通信。请检查 R 运行时的要求。*

同时，外部脚本运行时作为 STDERR 消息的一部分写入以下消息： 

>*错误： tmpfile 失败的创建。*

此错误指示快速启动板尝试使用的帐户不具有登录到数据库的权限。 当实现严格的安全策略时，会发生此情况。 若要确定这是否是这种情况，请查看 SQL Server 日志，并检查以查看 MSSQLSERVER01 帐户已拒绝在登录时。 特定于 R 的日志中提供的相同信息\_服务或 PYTHON\_服务。 查找 ExtLaunchError.log。

默认情况下，20 个帐户设置中，并与 Launchpad.exe 过程中，使用名称 MSSQLSERVER01 MSSQLSERVER20 通过相关联。 如果进行大量使用 R 或 Python，则可以增加帐户数。

若要解决此问题，请确保该组中已*允许本地登录*到机器学习功能已安装并启用其中的本地实例的权限。 在某些环境中，此权限级别可能需要从网络管理员的 GPO 异常。

## <a name="not-enough-quota-to-process-this-command"></a>"无法执行该命令没有足够配额"

此错误可能意味着以下内容之一：

- 快速启动板可能不足以运行外部查询的外部用户。 例如，如果同时运行 20 个以上的外部查询，并且仅有 20 个默认用户，一个或多个查询可能会失败。

- 没有足够的内存是可用于处理 R 任务。 在默认环境中，其中 SQL Server 使用的可能最高 70%的计算机的资源最经常发生此错误。 有关如何修改服务器配置为支持更多地利用的资源的信息，请参阅[实施 R 代码](r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>"找不到包"

如果你在 SQL Server 中运行 R 代码并收到此消息，但未获得消息，在运行 SQL Server 外部的相同代码时，则表示到 SQL Server 使用的默认库位置未安装包。

在许多方面，则会发生此错误：

- 在服务器上安装新包，但访问被拒绝，因此，R 到用户库安装包。

- 您安装了 R Services，然后安装其他 R 工具或库，包括 Microsoft R Server （独立版），Microsoft R Client，RStudio、 设置等。

若要确定实例使用的 R 包库的位置，打开 SQL Server Management Studio （或任何其他数据库查询工具），连接到的实例，然后运行以下存储的过程：

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>示例结果

*STDOUT message(s) from external script:*

*[1]"c:\\程序文件\\Microsoft SQL Server\\MSSQL13。SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解决此问题，必须重新安装到 SQL Server 实例库包。

>[!NOTE]
>如果已升级为使用 Microsoft R 的最新版本的 SQL Server 2016 的实例，则默认库位置会不同。 有关详细信息，请参阅[使用 SqlBindR 升级 R Services 的实例](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>由于不匹配的 Dll 而关闭的快速启动板

如果您使用其他功能，修补程序服务器上，安装数据库引擎，然后通过使用原始媒体更高版本添加机器学习功能，可能会安装错误版本的机器学习组件。 当快速启动板检测到版本不匹配时，它会关闭，并创建转储文件。

若要避免此问题，请确保与服务器实例安装在相同的修补程序级别的任何新功能。

**升级错误的处理方式：**

1. 安装 SQL Server 2016 不使用 R 服务。
2. 升级 SQL Server 2016 累积更新 2。
3. 使用 RTM 介质安装 R Services （数据库内）。

**升级的正确方法：**

1. 安装 SQL Server 2016 不使用 R 服务。
2. 将 SQL Server 2016 升级到所需的修补程序级别。 例如，安装 Service Pack 1 和累积更新 2。
3. 若要添加正确的修补程序级别的功能，请运行 SP1 并 CU2 重新，安装程序，然后选择 R Services （数据库内）。 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>快速启动板无法启动 8dot3 表示法是必需的

> [!NOTE] 
> 在较旧系统中，快速启动板可能无法启动如果 8dot3 表示法要求。 更高版本中已删除此要求。 SQL Server 2016 R Services 的客户应安装以下项之一：
> * SQL Server 2016 SP1 和 CU1: [for SQL Server 累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、 累积更新 3 和这[修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)，这是按需提供。

使用 R 的兼容性，SQL Server 2016 R Services （数据库） 所需位置安装该功能以支持通过使用短文件名创建的驱动器*8dot3 表示法*。 8.3 文件名也称为*短文件名*，并用与早期版本的 Microsoft Windows 或作为长文件名的替代方法的兼容性。

如果要安装 R 的卷不支持短文件名，从 SQL Server 启动 R 的进程可能无法再找到正确的可执行文件，并快速启动板将不会启动。

作为一种解决方法，可以启用 8dot3 表示法在卷上的，安装 SQL Server 和安装了 R Services。 然后，必须提供 R Services 配置文件中工作目录的短名称。

1. 若要启用 8dot3 表示法，请运行 fsutil 实用程序用于*8dot3name*如下所述的参数： [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 启用 8dot3 表示法后，打开 RLauncher.config 文件，并记下的属性`WORKING_DIRECTORY`。 有关如何查找此文件的信息，请参阅[机器学习进行故障排除的数据收集](data-collection-ml-troubleshooting-process.md)。

3. Fsutil 实用程序用于*文件*参数，以指定在 WORKING_DIRECTORY 中指定的文件夹的短文件路径。

4. 编辑配置文件来指定在 WORKING_DIRECTORY 属性中输入相同的工作目录。 或者，可以指定不同的工作目录，并选择已与 8dot3 表示法兼容的路径。


## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知的问题](machine-learning-troubleshooting-faq.md)

[数据收集以进行故障排除机器学习](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接进行故障排除](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
