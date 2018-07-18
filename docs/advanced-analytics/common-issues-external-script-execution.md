---
title: 快速启动板服务和 SQL Server 中的外部脚本执行的常见问题 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 08ab6e2db6d6cde5e41f7ddb88c8afd1da241df7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34706835"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>快速启动板服务和 SQL Server 中的外部脚本执行的常见问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server 受信任的快速启动板服务支持针对 R 和 Python 的外部脚本执行。 在 SQL Server 2016 R Services，SP1 将提供服务。 SQL Server 2017 包括快速启动板 ervice 作为开头几安装的一部分。

多个问题会阻止从开始，包括配置问题或更改，或缺少网络协议的快速启动板。 本文提供了针对很多问题的疑难解答指引。 对于任何我们遗漏，你可以发布到的问题[机器学习 Server 论坛](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="determine-whether-launchpad-is-running"></a>确定是否正在运行快速启动板

1. 打开**服务**面板 (Services.msc)。 或者，从命令行中，键入**SQLServerManager13.msc**或**SQLServerManager14.msc**以打开[SQL Server 配置管理器](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 记下运行快速启动板服务帐户。 启用了 R 或 Python 每个实例应具有自己的快速启动板服务实例。 例如，对于命名实例的服务可能类似于_MSSQLLaunchpad$ InstanceName_。

3. 如果该服务已停止，重新启动它。 在重新启动，如果没有配置任何问题，在系统事件日志中，发布消息，并再次停止服务。 检查系统事件日志中有关服务停止原因的详细信息。

4. 查看 RSetup.log 中的内容，并确保在设置中没有任何错误。 例如，消息*退出代码 0*指示服务启动失败。

5. 若要查找其他错误，请查看 rlauncher.log 的内容。

## <a name="check-the-launchpad-service-account"></a>检查快速启动板服务帐户

默认服务帐户可能是"NT 服务\$SQL2016"或"NT 服务\$SQL2017"。 最后部分可能有所不同，具体取决于你的 SQL 实例名称。

快速启动板服务 (Launchpad.exe) 通过使用低特权服务帐户运行。 但是，若要启动 R 和 Python 和与数据库实例通信，快速启动板服务帐户需要以下用户权限：

- 以服务身份登录 (SeServiceLogonRight)
- 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)
- 跳过遍历检查 (SeChangeNotifyPrivilege)
- 调整进程 (SeIncreaseQuotaSizePrivilege) 的内存配额

有关这些用户权限的信息，请参阅中的"Windows 特权和权限"部分[配置 Windows 服务帐户和权限](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

> [!TIP]
> 如果你熟悉支持诊断平台 (SDP) 工具用于 SQL Server 诊断，你可以使用 SDP 来查看 MachineName_UserRights.txt 同名输出文件。

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>快速启动板的用户组不能在本地登录

安装过程中的机器学习服务，SQL Server 创建 Windows 用户组**SQLRUserGroup** ，然后将其设置使用快速启动板来连接到 SQL Server 和运行外部脚本作业所需的所有权限。 如果启用了此用户组，它还用于执行 Python 脚本。

但是，在组织中限制性更强的安全策略实施的情况，此组所需的权限可能已被手动删除，或者它们可能会自动吊销的策略。 如果删除了权限，快速启动板可以不再连接到 SQL Server，并且 SQL Server 不能调用外部运行时。

若要解决此问题，请确保组 **SQLRUserGroup** 拥有系统权限“允许本地登录”。

有关详细信息，请参阅[配置 Windows 服务帐户和权限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。

## <a name="permissions-to-run-external-scripts"></a>运行外部脚本的权限

即使快速启动板已正确配置，它将返回错误，如果用户没有权限来运行 R 或 Python 脚本。

如果您安装 SQL Server 作为数据库管理员或数据库所有者，你会自动将授予此权限。 但是，其他用户通常具有更受限制的权限。 如果用户尝试运行 R 脚本时，它们会获得快速启动板错误。

若要解决此问题，在 SQL Server Management Studio，安全管理员可以修改的 SQL 登录名或 Windows 用户帐户通过运行以下脚本：

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

有关详细信息，请参阅[GRANT (Transact SQL](../t-sql/statements/grant-transact-sql.md)。

## <a name="common-launchpad-errors"></a>常见的快速启动板错误

本部分列出的快速启动板返回的最常见的错误消息。

## <a name="unable-to-launch-runtime-for-r-script"></a>"无法启动 R 脚本的运行时"

如果 Windows 组 （也用于 Python） 的 R 用户无法登录到运行 R Services 的实例，你可能会看到以下错误：

- 当你尝试运行 R 脚本时生成的错误：

    * *无法启动“R”脚本的运行时。请检查“R”运行时的配置。

    * *发生外部脚本错误。无法启动运行时。

- 生成的错误[!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]服务：

    * 无法初始化启动器 RLauncher.dll

    * 未注册任何启动器 dll！

    * *安全日志指示 NT 服务的帐户无法登录*

有关如何授予必要的权限的此用户组的信息，请参阅[安装 SQL Server 2016 R Services](install/sql-r-services-windows-install.md)。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制。

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"登录失败： 尚未授予用户请求的登录类型"

默认情况下，[!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)]在启动时使用以下帐户： `NT Service\MSSQLLaunchpad`。 帐户由配置[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]安装程序以具有所有必需的权限。

如果将不同的帐户分配给快速启动板，或右删除的 SQL Server 计算机上的策略，该帐户可能没有必要的权限，并且你可能会看到此错误：

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登录失败: 未授予用户在此计算机上的请求登录类型。*

若要授予必要的权限来的新的服务帐户，使用本地安全策略应用程序，并更新该帐户的权限，以便包括以下权限：

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"无法与快速启动板服务通信"

如果你事先安装并随后启用机器学习中，但当你尝试运行 R 或 Python 脚本时出现此错误，针对该实例快速启动板服务可能已停止运行。

1. 通过 Windows 命令提示符打开 SQL Server 配置管理器。 有关详细信息，请参阅 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)。

2. 对于实例，右键单击 SQL Server 快速启动板，然后选择**属性**。

3. 选择**服务**选项卡上，然后验证该服务正在运行。 如果未运行，更改**启动模式**到**自动**，然后选择**应用**。

4. 重新启动服务通常可以解决问题，以便计算机学习脚本可以运行。 如果在重新启动操作未修复问题，请注意的路径和中的自变量**二进制路径**属性，并执行以下：

    A. 查看启动器的.config 文件，并确保工作目录无效。

    B. 确保使用快速启动板的 Windows 组可以连接到 SQL Server 实例中所述[上一节](#bkmk_LaunchpadTS)。

    c. 如果你更改任何服务属性，请重新启动快速启动板服务。

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"错误 tmpFile 创建失败"

在此方案中，你已成功安装机器学习功能，并快速启动板正在运行。 您尝试运行一些简单的 R 或 Python 代码，但快速启动板失败并出现错误如下所示： 

>*无法与 R 脚本的运行时进行通信。请检查 R 运行时的要求。*

同时，外部脚本运行时作为 STDERR 消息的一部分编写以下消息： 

>*错误： 创建 tmpfile 失败。*

此错误指示快速启动板尝试要使用的帐户不具有登录到数据库的权限。 当实现严格的安全策略时，会发生此情况。 若要确定这是否是这种情况，请查看 SQL Server 日志中，并检查以查看是否 MSSQLSERVER01 帐户被拒绝在登录。 在日志中特定于 R 提供的相同信息\_服务或 PYTHON\_服务。 查找 ExtLaunchError.log。

默认情况下，20 帐户设置和与 Launchpad.exe 过程中，与通过 MSSQLSERVER20 名称 MSSQLSERVER01 关联。 如果你进行大量使用 R 或 Python，则可以增加的帐户的数量。

若要解决此问题，请确保组具有*允许本地登录*到机器学习功能已安装并启用其中的本地实例的权限。 在某些环境中，此权限级别可能需要从网络管理员 GPO 异常。

## <a name="not-enough-quota-to-process-this-command"></a>"没有足够无法处理此命令的配额"

此错误可能意味着几种方法之一：

- 快速启动板可能会有足够的外部用户来运行外部查询。 例如，如果与此同时，你正在使用 20 个以上的外部查询，并且仅有 20 个的默认用户，则一个或多个查询可能会失败。

- 内存不足，便可处理 R 任务。 在默认环境中，其中 SQL Server 可能会使用为达 70%的计算机的资源通常发生此错误。 有关如何修改服务器配置，以支持更好地利用的资源的信息，请参阅[实现 R 代码](r/operationalizing-your-r-code.md)。

## <a name="cant-find-package"></a>"找不到程序包"

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

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

若要解决此问题，你必须重新安装 SQL Server 实例库的程序包。

>[!NOTE]
>如果你已升级的 SQL Server 2016，以便使用最新版本的 Microsoft R 实例，则默认库位置会不同。 有关详细信息，请参阅[使用 SqlBindR 升级 R Services 的实例](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>由于不匹配的 Dll 而关闭的快速启动板

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

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>快速启动板无法启动是否需要 8.3 文件名表示法

> [!NOTE] 
> 较旧系统上快速启动板可能无法启动如果 8.3 文件名表示法要求。 此要求更高版本中已删除。 SQL Server 2016 R Services 客户都应安装以下项之一：
> * SQL Server 2016 SP1 和 CU1: [for SQL Server 的累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)。
> * SQL Server 2016 RTM、 累积更新 3 和这[修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)，即可以根据需要使用。

为了与 R 兼容，SQL Server 2016 R Services （数据库） 所需功能安装以使用支持的短文件名创建的驱动器*8.3 文件名表示法*。 8.3 文件名也被称为*的短文件名*，并且它适用于使用早期版本的 Microsoft Windows 或作为长文件名的替代方法的兼容性。

如果你安装 R 的卷不支持短文件名，启动 R 从 SQL Server 的进程可能无法找到正确的可执行文件，并快速启动板将不会启动。

一种解决方法，你可以启用卷上的 8.3 文件名表示法，其中安装 SQL Server 和 R Services 的安装位置。 然后，必须提供 R Services 配置文件中工作目录的短名称。

1. 若要启用 8.3 文件名表示法，运行 fsutil 实用程序用于*8dot3name*参数如下所述： [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

2. 8.3 文件名表示法启用后，打开 RLauncher.config 文件并记下的属性`WORKING_DIRECTORY`。 有关如何查找此文件的信息，请参阅[用于机器学习故障排除数据收集](data-collection-ml-troubleshooting-process.md)。

3. 将 fsutil 实用程序用于*文件*参数来指定 WORKING_DIRECTORY 中指定的文件夹的短文件名路径。

4. 编辑配置文件以指定在 WORKING_DIRECTORY 属性中输入相同的工作目录。 或者，可以指定不同的工作目录，并选择已 8.3 文件名表示法与兼容的路径。


## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知的问题](machine-learning-troubleshooting-faq.md)

[进行故障排除机器学习的数据收集](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接进行故障排除](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
