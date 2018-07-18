---
title: 机器学习服务中的已知问题 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c334671fb9afaa4596688658e6beadbf8c9e6cc8
ms.sourcegitcommit: 7d2b34c64f97206861ec9ad8d6a6201ac20a4af1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36297433"
---
# <a name="known-issues-in-machine-learning-services"></a>机器学习服务中的已知的问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了已知的问题或限制机器学习作为 SQL Server 2016 和 SQL Server 自 2017 年中的一个选项提供的组件。

此处的信息适用于所有以下内容，除非另有说明：

SQL Server 2016

- R Services（数据库内）
- Microsoft R Server（独立版）

SQL Server 2017

- 机器学习 （数据库） 的服务
- 机器学习 Python （数据库） 的服务
- 机器学习服务器（独立）

## <a name="setup-and-configuration-issues"></a>安装和配置问题

进程和与初始设置和配置相关的常见问题的说明，请参阅[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含有关升级、 通过并行安装和安装新的 R 或 Python 组件的信息。

### <a name="r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>R 脚本的运行时错误 （SQL Server 自 2017 年 CU5 CU7 倒退）

对于 SQL Server 2017 中累积更新 5 到 7，没有中的回归**rlauncher.config**其中的临时目录文件路径包含空格的文件。 此回归是在 CU8 中更正。

运行 R 脚本时将看到此错误包含以下消息：

> *无法与 'R' 脚本的运行时进行通信。请检查 'R' 运行时的要求。*
>
> 来自外部脚本的 STDERR 消息： 
>
> *错误： 无法创建 R_TempDir*

**解决方法**

它可用时，请应用 CU8。 或者，你可以重新创建**rlauncher.config**通过运行**registerrext**上提升的命令提示符卸载/安装。 

```text
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

下面示例演示具有默认实例"MSSQL14 命令。MSSQLSERVER"安装到"C:\Program Files\Microsoft SQL Server\":

```text
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>无法在域控制器上安装 SQL Server 机器学习功能

如果你尝试在域控制器上安装 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习服务，安装程序将失败，出现以下错误：

> *在功能的安装过程中出错*
> 
> *找不到具有标识的组*
> 
> *组件错误代码： 0x80131509*

出现失败的原因在于，在域控制器上，该服务无法创建运行机器学习所需的 20 本地帐户。 一般情况下，我们不建议在域控制器上安装 SQL Server。 有关详细信息，请参阅[支持公告 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安装最新的服务版本，以确保与 Microsoft R 客户端的兼容性

如果你安装 Microsoft R 客户端的最新版本，并使用它 R SQL Server 上运行远程计算上下文中，你可能会如下所示的错误：

> *你与 Microsoft R Server 版本 8.x.x 不兼容的计算机上运行 Microsoft R 客户端版本的 9.x.x。请下载并安装兼容版本。

SQL Server 2016 需要客户端上的 R 库与服务器上的 R 库完全匹配。 限制已被撤除版本晚于 R Server 9.0.1。 但是，如果你遇到此错误，则验证 R 库，可供你的客户端和服务器，并如有必要，更新客户端与服务器版本匹配的版本。

每次安装的 SQL Server 服务发行版时，被更新的版本与 SQL Server R Services 安装的 R。 若要确保你始终具有最新版本的 R 组件，请确保安装所有 service pack。

若要确保与 Microsoft R 客户端 9.0.0 的兼容性，安装更新所述，在此[支持文章](https://support.microsoft.com/kb/3210262)。

若要避免与 R 包的问题，还可以升级安装在服务器上，通过更改以使用现代的生命周期支持策略中，你维护协议中所述的 R 库版本[下一节](#bkmk_sqlbindr)。 执行此操作时，按相同的计划用于机器学习服务器 (以前称为 Microsoft R Server) 的更新进行更新的版本与 SQL Server 安装的 R。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="r-components-missing-from-cu3-setup"></a>从 CU3 安装程序缺少的 R 组件

如果没有应包含在 SQL Server R 安装文件设置有限的数量的 Azure 虚拟机。 此问题适用于在从 2018年-01-05 2018年-01-23 到期间设置的虚拟机。 如果你应用 SQL Server 2017 CU3 更新期间从 2018年-01-05 2018年-01-23 到，则此问题可能也会影响在本地安装。

包括 R 安装文件的正确版本提供了服务版本。

+ [SQL Server 自 2017 年 KB4052987 的累积更新包 3](https://www.microsoft.com/en-us/download/details.aspx?id=56128)。

若要安装组件并修复 SQL Server 自 2017 年 1 CU3，必须卸载 CU3，然后重新安装的更新的版本：

1. 下载更新的 CU3 安装文件，其中包含 R 安装程序。
2. 卸载 CU3。 在 Control Panel 中，搜索**卸载的更新**，然后选择"SQL Server 2017 (KB4052987) （64 位） 的修补 3015 程序"。 继续执行卸载步骤。
3. 重新安装 CU3 更新中，双击 KB4052987 刚下载的更新： `SQLServer2017-KB4052987-x64.exe`。 按照安装说明进行操作。

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>无法在脱机安装的 SQL Server 自 2017 年 1 CTP 2.0 或更高版本中安装 Python 组件

如果在没有 internet 访问的计算机上安装 SQL Server 自 2017 年的预发行版本，安装程序可能无法显示页面，提示输入下载 Python 组件的位置。 在这种情况下，你可以安装机器学习服务功能，但不是 Python 组件。

在发布版本中修复此问题。 此外，此限制不适用于 R 组件。

**适用于：** 使用 Python 的 SQL Server 自 2017 年 1

### <a name="bkmk_sqlbindr"></a> 当你从连接到旧版本的 SQL Server R Services 客户端使用的不兼容版本警告 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

当在运行 R 代码 SQL Server 2016 计算上下文，你可能会看到以下错误：

> *计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

如果以下两个语句之一为 true，，显示此消息

+ 您在通过使用安装向导的情况下将在客户端计算机上安装 R Server （独立） [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。
+ 通过安装 Microsoft R Server[单独的 Windows installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

若要确保服务器和客户端使用相同的版本可能需要使用_绑定_，支持的 Microsoft R Server 9.0 和更高版本升级 SQL Server 2016 实例中的 R 组件。 若要确定是否支持升级为可用，有关你的 R 服务版本，请参阅[使用 SqlBindR.exe R Services 的实例升级](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

当你安装累积更新，或在未连接到 internet 的计算机上安装 SQL Server 2016 service pack 时，安装向导可能无法显示提示，你可以通过使用下载的 CAB 文件中更新的 R 组件。 与数据库引擎一起安装多个组件时，通常会发生此失败。

一种解决方法，你可以通过使用命令行和指定安装服务版本`MRCACHEDIRECTORY`参数在此示例中，它会安装 CU1 更新所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取的最新的安装程序，请参阅[安装没有 internet 访问权限的机器学习组件](install/sql-ml-component-install-without-internet-access.md)。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>快速启动板服务启动失败，则如果版本与不同的 R 版本

如果从数据库引擎，单独安装 SQL Server R Services 和生成版本不同，你可能会看到系统事件日志中的以下错误：

> *SQL Server 快速启动板服务启动因以下错误而失败： 服务未响应及时启动或控制请求。*

例如，此错误可能会发生如果使用的版本安装数据库引擎、 应用修补程序来升级数据库引擎，和使用的版本，然后将添加 R Services 功能。

若要避免此问题，使用实用程序在文件管理器如比较与版本的 SQL 二进制文件，如 sqldk.dll Launchpad.exe 的版本。 所有组件应都具有相同的版本号。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

快速启动板中查找`Binn`实例文件夹。 例如，在默认安装的 SQL Server 2016 中，路径可能为`C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`。 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>由在 Azure 虚拟机运行的 SQL Server 实例中在防火墙阻止远程计算上下文

如果你已安装[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]在 Windows Azure 虚拟机，你可能无法使用需要虚拟机的工作区中使用的计算上下文。 原因是在默认情况下，Azure 虚拟机上的防火墙包含阻止网络本地 R 用户帐户访问的规则。

解决方法是，在 Azure VM 上，打开**高级安全 Windows 防火墙**，选择**出站规则**，并禁用以下规则：**阻止 R 中的本地用户帐户的网络访问权限SQL Server 实例 MSSQLSERVER**。 此外可以将启用，该规则保留，但更改到的安全属性**允许安全情况**。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 中的隐式身份验证

当运行 R 作业从远程数据科学工作站使用集成 Windows 身份验证时，SQL Server 使用*默示身份验证*生成的脚本可能需要任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。

若要解决此问题，建议升级到更高的 Service Release。

如果升级不是可行的一种解决方法，使用 SQL 登录名运行可能需要嵌入的 ODBC 调用的远程 R 作业。

**适用于：** SQL Server 2016 R Services 速成版

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>从其他工具调用 SQL Server 使用的库时的性能限制

就可以调用机器学习库从外部应用程序，如 RGui 为 SQL Server 安装。 执行此操作可能是最方便的方法来完成某些任务，如安装新包时，或在很短的代码示例中运行即席测试。 但是，SQL Server 外部性能可能会受到限制。 

例如，即使你使用的 SQL Server 的企业版，R 在单线程模式下运行时通过使用外部工具运行 R 代码。 若要获取 SQL Server 中的性能好处，请启动 SQL Server 连接，并使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)以调用外部脚本运行时。

一般情况下，避免调用机器学习库通过外部工具使用的 SQL Server。 如果你需要调试 R 或 Python 代码，则通常很容易为此 SQL Server 外部。 若要获取 SQL Server 中的同一个库，你可以安装 Microsoft R 客户端， [SQL Server 自 2017 年 1 机器学习服务器 （独立）](install/sql-machine-learning-standalone-windows-install.md)，或[SQL Server 2016 R Server （独立）](install/sql-r-standalone-windows-install.md)。

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>SQL Server Data Tools 不支持外部脚本所需权限

当你使用 Visual Studio 或 SQL Server Data Tools 发布数据库项目，如果任何主体拥有权限特定于外部脚本执行时，你可能会与此类似的错误：

> *TSQL 模型： 在反向工程数据库时检测到错误。权限未被识别，并不导入。*

当前 DACPAC 模型不支持使用 R Services 或机器学习服务，例如授予任意外部脚本或执行任意外部脚本的权限。 更高版本将会解决此问题。

解决方法是，额外授予在运行语句后期部署脚本。

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>外部脚本执行限制由于资源调控默认值

在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些早期的发布版本，无法分配给 R 进程的最大内存为 20%。 因此，如果在服务器有 32 GB RAM，R 可执行文件 （RTerm.exe 和 BxlServer.exe） 可以使用单个请求中的最大 6.4 GB。

如果你遇到资源限制，请检查当前的默认值。 如果 20%是不够的请参阅的文档[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]如何更改此值。

**适用于：** SQL Server 2016 R Services，Enterprise Edition

## <a name="r-script-execution-issues"></a>R 脚本执行问题

本部分包含特定于 SQL Server 上运行 R 的已知的问题，以及一些与 R 库和工具是 Microsoft，包括 RevoScaleR 发布的相关的问题。

有关可能会影响 R 解决方案的更多已知问题，请参阅[机器学习服务器](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站点。

### <a name="access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>在非默认位置中的 SQL Server 上执行 R 脚本时，则拒绝警告

如果 SQL Server 的实例已安装到非默认位置，如外部`Program Files`文件夹中，当你尝试运行安装包的脚本时引发 ACCESS_DENIED 警告。 例如：

> *在`normalizePath(path.expand(path), winslash, mustWork)`： 路径 [2] ="~ExternalLibraries/R/8/1": 访问被拒绝*

R 函数尝试进行读取的路径，而且如果失败，原因是内置的用户组**SQLRUserGroup**，不具有读取权限。 引发警告不会阻止执行当前的 R 脚本，但警告可能重复发生，每当用户在运行任何其他 R 脚本。

如果在你安装 SQL Server 的默认位置，此错误不会发生，因为所有的 Windows 用户具有读取权限上`Program Files`文件夹。

Ia 在即将发布的服务版本中解决此问题。 一种解决方法，提供组， **SQLRUserGroup**，具有针对所有父文件夹的读取访问`ExternalLibraries`。

### <a name="serialization-error-between-old-and-new-versions-of-revoscaler"></a>RevoScaleR 版本旧和新版本之间的序列化错误

如果你通过使用远程 SQL Server 实例的序列化的格式的模型，你可能会出现错误： 

> *MemDecompress 中的错误 (数据、 类型 = 解压缩) memDecompress(2) 中的内部错误-3。*

如果保存模型时使用了新版本的序列化函数中，会出现此错误[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，但其中你进行反序列化模型的 SQL Server 实例已 RevoScaleR Api，请从 SQL 的旧版本Server 2017 CU2 或更早版本。

一种解决方法，你可以升级到 CU3 或更高版本的 SQL Server 2017 实例。

如果 API 版本是相同的或者如果你在迁移到使用序列化 API 的较新版本的服务器的较旧的序列化函数使用保存的模型未出现错误。

换而言之，将相同版本的 RevoScaleR 用于序列化和反序列化的操作。

### <a name="real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>实时评分不正确处理_learningRate_树和林模型中的参数

如果你使用决策树或决策林方法创建模型，并指定学习速率，则可能出现不一致的结果时使用`sp_rxpredict`或 SQL`PREDICT`函数，与使用相比`rxPredict`。

原因是该序列化的进程模型的 API 中的错误，并仅限于`learningRate`参数： 例如，在[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)，或

在即将发布的服务版本中解决此问题。

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作业的处理器关联限制

在 SQL Server 2016 的初始版本生成、 你可以设置处理器关联，仅为第一个 k 组中的 Cpu。 例如，如果服务器是具有两个 k 组的 2 套接字机，从第一个 k 组的唯一处理器用于 R 进程。 配置资源调控的 R 脚本作业时，将应用相同的限制。

此问题已在 SQL Server 2016 Service Pack 1 中解决。 我们建议你升级到最新的服务版本。

**适用于：** SQL Server 2016 R Services RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>在 SQL Server 计算环境中读取数据时，无法更改列类型

如果计算环境设置为 SQL Server 实例，则无法在 R 代码中使用 _colClasses_ 参数（或其他类似参数）来更改列的数据类型。

例如，如果列 CRSDepTimeStr 尚不是整数，则以下语句将导致错误：

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

一种解决方法，您可以重新编写 SQL 查询使用强制转换或转换，然后将数据提交给 R 中，通过使用正确的数据类型。 一般情况下，性能是更好地处理时数据通过使用 SQL 中，而不是通过更改在 R 代码中的数据。

**适用于：** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>序列化模型的大小限制

当模型保存到一个 SQL Server 表中时，你必须序列化模型，并将其保存以二进制格式。 理论上可以使用此方法存储模型的最大大小为 2 GB，这是 SQL Server 中的 varbinary 列的最大大小。

如果你需要使用更大的模型，将用下列解决方法：

+ 采取措施来减少你的模型的大小。 一些开放源代码 R 包中的模型对象，包括大量的信息和很多此信息可以删除部署。 
+ 使用功能选择来删除不必要的列。
+ 如果你使用的开放源代码算法，请考虑使用 MicrosoftML 或 RevoScaleR 中的对应算法一个类似的实现。 这些包经过优化的部署方案。
+ 已合理化模型并使用前面的步骤减小大小后，请参阅如果[memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)基 R 中的函数可以用于减小然后再将它传递到 SQL Server 的模型的大小。 接近的 2 GB 限制模型时，此选项是最佳的。
+ 对于更大的模型，你可以使用 SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md)功能来存储模型中，而不是使用 varbinary 列。

    若要使用 Filetable，必须添加防火墙例外，因为在 Filetable 中存储的数据由 SQL Server 中的 Filestream 文件系统驱动程序和默认防火墙规则阻止网络文件访问。 有关详细信息，请参阅[启用 FileTable 的先决条件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。 

    启用 FileTable 之后，若要编写模型，您获取路径从 SQL 使用 FileTable 的 API，，然后将该模型在代码中写入到该位置。 当你需要进行读取模型时，您获取路径从 SQL，然后调用模型使用从你的脚本的路径。 有关详细信息，请参阅[使用文件输入输出 Api 访问 Filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>避免当执行中的 R 代码时，清除工作区[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文

如果你使用 R 命令中运行 R 代码时清除你的对象的工作区[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文，或如果清除工作区作为 R 脚本的一部分调用通过使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，可能会出现此错误:*工作区中找不到的对象 revoScriptConnection*

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

一种解决方法，避免不加选择地清除的变量和其他对象时你正在中运行 R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 尽管在 R 控制台中工作时，清除工作区中均相同，但它可以有意想不到的后果。

* 若要删除特定变量，使用 R`remove`函数： 例如， `remove('name1', 'name2', ...)`
* 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作为输入提供给 R 脚本的数据的限制

你无法在 R 脚本中使用以下类型的查询结果：

- 引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
- 引用屏蔽列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>使用的字符串，如因素会导致性能下降

使用字符串类型变量，如因素会大大增加用于 R 操作的内存量。 这一般情况下，是使用 R 的已知的问题，有关该主题有许多其他文章。 例如，请参阅[因素不是在 R 中，通过 John 装载，正在 r-bloggers 的极佳地处理)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)或[stringsAsFactors： 未经授权的简介、 通过 Roger 华鹏](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)。 

虽然问题不是特定于 SQL Server 的它可以极大地影响在 SQl Server 中运行的 R 代码的性能。 字符串通常存储为 varchar 或 nvarchar，并且如果字符串数据的列应用了多个唯一值，内存分配错误甚至可以造成内部将这些到整数并返回到通过 R 的字符串进行转换的过程。

如果你不绝对需要字符串数据类型对其他操作，将字符串值映射到一个数字 （整数） 数据类型为数据准备的部分将会从性能和可扩展性的角度来看非常有益。

有关此问题，以及其他提示的讨论，请参阅[R Services-数据优化的性能](r/r-and-data-optimization-r-services.md)。

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>自变量*varsToKeep*和*varsToDrop*不支持 SQL Server 数据源

当你使用 rxDataStep 函数将结果写入到一个表时，使用*varsToKeep*和*varsToDrop*是指定要包括或排除操作的一部分的列的便捷方式。 但是，这些自变量不支持为 SQL Server 数据源。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>对 sp 中的 SQL 数据类型的支持有限\_执行\_外部\_脚本

并非所有在 SQL 中支持的数据类型可用在。作为一种解决方法，请考虑为受支持的数据类型将不支持的数据类型强制转换然后再将数据传递到 sp\_执行\_外部\_脚本。

有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>可能的字符串损坏

中的字符串数据的任何往返行程[!INCLUDE[tsql](../includes/tsql-md.md)]到 R，然后执行到[!INCLUDE[tsql](../includes/tsql-md.md)]试可能会导致损坏。 这是因为在 R 和使用的编码不同[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以及各种排序规则和在 R 中支持的语言和[!INCLUDE[tsql](../includes/tsql-md.md)]。 采用非 ASCII 编码的任何字符串可能不会得到正确处理。

当你将字符串数据发送到 R 时，将其转换为 ASCII 表示形式，如有可能。

此限制适用于以及 SQL Server 和 Python 之间传递数据。 多字节字符应传递为 utf-8，并存储为 Unicode。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一个值类型的`raw`可以从返回 `sp_execute_external_script`

当二进制数据类型 (R**原始**数据类型) 从返回 R，必须在输出数据框架中发送的值。

使用数据类型以外**原始**，你可以通过添加输出关键字来返回参数值以及存储过程的结果。 有关详细信息，请参阅[参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果你想要使用包含值的类型值的多个输出集**原始**，其中一个可能的解决方法是以执行多个调用存储过程中，或将结果集发回到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 ODBC。

### <a name="loss-of-precision"></a>精度损失

因为[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支持不同的数据类型，数值数据类型可能会降低精度的转换的过程。

有关隐式数据类型转换的详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>变量范围错误，当你使用 transformFunc 参数

若要将数据转换时对进行建模，你可以传递*transformFunc*如函数中的参数`rxLinmod`或`rxLogit`。 但是，嵌套的函数调用可能导致出现范围错误在 SQL Server 计算上下文中，即使在调用在本地计算上下文中正常工作。

> *分析示例数据集具有任何变量*

例如，假定你已经定义了两个函数，`f`和`g`，在你本地全局环境中，和`g`调用`f`。 在分布式或远程调用涉及`g`，调用`g`可能失败，此错误，因为`f`找不到，即使你已通过同时`f`和`g`给远程调用。

如果遇到此问题，你可以通过在 `f` 的定义中（ `g`可正常调用 `g` 的任何位置）嵌入 `f`的定义来解决该问题。

例如：

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

若要避免错误，重写，如下所示定义:

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>使用 RevoScaleR 导入和操作数据

当**varchar**列从数据库读取，裁剪掉空格。 为了避免这种情况，请将字符串包含在非空格字符中。

当函数如`rxDataStep`用于创建数据库表具有**varchar**列，列宽度估计基于数据的示例。 如果宽度可能会变化，可能需要所有字符串都填补到公共长度。

使用 `rxImport` 或 `rxTextToXdf` 的重复调用来导入和追加行，并将多个输入文件合并为单个.xdf 文件时，不支持使用转换来更改变量的数据类型。

### <a name="limited-support-for-rxexec"></a>对 rxExec 的支持有限

SQL Server 2016 中`rxExec`函数，仅在单线程模式下则提供由 RevoScaleR 包可用。

并行度`rxExec`跨多个进程计划在将来的版本。

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>增加最大参数大小以支持 rxGetVarInfo

如果使用数据集具有极大量的变量 （例如，通过 40000) 时，设置`max-ppsize`标志时启动 R，使用函数如`rxGetVarInfo`。 `max-ppsize` 标志指定指针保护堆栈的最大大小。

如果你正在使用 R 控制台 （例如，RGui.exe 或 RTerm.exe），则可以设置的值_最大 ppsize_到 500000 通过键入：

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函数的问题

`rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是，数字数据自动装箱。

有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。

## <a name="python-script-execution-issues"></a>Python 脚本执行问题

本部分包含特定于 SQL Server，以及与 Microsoft，发布的 Python 包相关的问题上运行 Python 的已知的问题包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>预先训练的模型调用失败，如果对模型的路径太长

如果在早期版本的 SQL Server 2017 中安装的预先训练的模型，训练的模型文件的完整路径可能太长，Python 读取。 此限制被固定的更高版本的服务版本。

有几种可能的解决方法： 

+ 在安装的预先训练的模型时，选择自定义位置。
+ 如果可能，请使用较短的路径，例如 C:\SQL\MSSQL14 安装自定义安装路径下的 SQL Server 实例。MSSQLSERVER。
+ 使用 Windows 实用工具[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)以创建将模型文件映射到较短的路径的硬链接。
+ 更新到最新的服务版本。

### <a name="error-when-saving-serialized-model-to-sql-server"></a>错误保存时序列化到 SQL Server 的模型

当您将模型传递到远程 SQL Server 实例，并尝试读取二进制模型使用`rx_unserialize`函数中[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)，可能会出现错误： 

> *NameError： 未定义名称 rx_unserialize_model*

如果保存模型时使用了新版本的序列化函数，但其中你进行反序列化模型的 SQL Server 实例不能识别序列化 API，则会出现此错误。

若要解决此问题，升级到 CU3 或更高版本的 SQL Server 2017 实例。

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>无法初始化 varbinary 变量中 BxlServer 导致的错误

如果在使用 SQL Server 中运行 Python 代码`sp_execute_external_script`，并且代码具有输出类型 varbinary （max）、 varchar （max） 或类似的类型的变量，必须初始化变量，或将其设置为你的脚本的一部分。 否则，数据 exchange 组件，BxlServer，将引发错误，停止工作。

将在即将发布的服务版本中解决此限制。 解决方法是，确保将变量初始化 Python 脚本中。 可以使用任何有效的值，如以下示例所示：

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>在成功执行 Python 代码的遥测警告

从 SQL Server 自 2017 年 CU2 开始，即使 Python 代码，否则为任务成功运行，可能会出现以下消息：

> *来自外部脚本的 STDERR 消息：*
> **~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state 是全局声明之前使用*


在 SQL Server 自 2017 年 1 累积更新 3 (CU3) 中已修复此问题。 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本部分列出了特定于 R 连接、 开发和由 Revolution Analytics 提供的性能工具的问题。 这些工具的较早的预发行版本中未提供[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。

通常情况下，我们建议你卸载这些早期版本和安装最新版本的 SQL Server 或 Microsoft R Server。

### <a name="revolution-r-enterprise-is-not-supported"></a>不支持 revolution R Enterprise

安装的任何版本的 Revolution R Enterprise 并排[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]不支持。

如果你有现有的许可证 Revolution R Enterprise，则必须将其从这两个单独的计算机置于[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例和你想要用于连接到任何工作站[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。

某些预发行版本的[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]的窗口，由 Revolution Analytics 中包含的 R 开发环境。 此工具不再提供，并不支持。

为了与兼容[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我们建议你改为安装 Microsoft R 客户端。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)和[Visual Studio Code](https://code.visualstudio.com/)还支持 Microsoft R 解决方案。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题

修订 0.92 SQLite ODBC 驱动程序是与 RevoScaleR 不兼容。 修订 0.88 0.91 和 0.93 和更高版本都已知为兼容。

## <a name="see-also"></a>另请参阅

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server 中的故障排除机器学习](machine-learning-troubleshooting-faq.md)
