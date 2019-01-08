---
title: R 语言和 Python 集成-SQL Server 机器学习服务的已知的问题
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/13/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6dc02c56bda3cdf904e0c53115d4fbbfcfafe9fc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645513"
---
# <a name="known-issues-in-machine-learning-services"></a>机器学习服务中的已知的问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了已知的问题或作为中的一个选项提供的机器学习组件的限制[SQL Server 2016 R Services](install/sql-r-services-windows-install.md)和[SQL Server 2017 机器学习服务使用 R 和 Python](install/sql-machine-learning-services-windows-install.md).

## <a name="setup-and-configuration-issues"></a>安装和配置问题

进程和与初始安装和配置相关的常见问题的说明，请参阅[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含有关升级、 通过并行安装，以及新的 R 或 Python 组件的安装信息。

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1.由于缺少环境变量的 MKL 计算中不一致的结果

**适用范围：** 9.0、 9.1、 9.2 或 9.3，二进制 R_SERVER 文件。

R_SERVER 使用 Intel Math Kernel Library (MKL)。 有关涉及 MKL 的计算，如果您的系统缺少的环境变量，会出现不一致的结果。 

设置环境变量`'MKL_CBWR'=AUTO`以确保在 R_SERVER 条件数字可再现性。 有关详细信息，请参阅[简介到条件数字可再现性 (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

**解决方法**

1. 在控制面板中，单击**系统和安全** > **系统** > **高级系统设置** >  **环境变量**。

2. 创建一个新的用户或系统变量。 

  + 设置到 MKL_CBWR 变量名称。
  + 设置为自动的变量值。

3. 重新启动 R_SERVER。 SQL Server 上，可以重新启动 SQL Server 快速启动板服务。

> [!NOTE]
> 如果运行的 SQL Server 2019 预览版在 Linux 上，编辑或创建 *.bash_profile*用户主目录中添加的代码行`export MKL_CBWR="AUTO"`。 通过键入来执行此文件`source .bash_profile`bash 命令提示符处。 通过键入来重新启动 R_SERVER `Sys.getenv()` R 命令提示符处。

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2.R 脚本运行时错误 （SQL Server 2017 CU5 CU7 回归）

对于 SQL Server 2017 累积更新 5 到 7，在没有中的回归**rlauncher.config**文件位置的临时目录文件路径包含空格。 CU8 解决了此回归。

运行 R 脚本时将看到此错误还包含以下消息：

> *无法与 'R' 脚本的运行时进行通信。请检查 'R' 运行时的要求。*
>
> 来自外部脚本的 STDERR 消息： 
>
> *错误： 无法创建 R_TempDir*

**解决方法**

当它可用时，将应用 CU8。 或者，你可以重新创建**rlauncher.config**通过运行**registerrext**上提升的命令提示符卸载/安装。 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

下面示例演示具有默认实例"MSSQL14 命令。MSSQLSERVER"安装到"C:\Program Files\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3.无法在域控制器上安装 SQL Server 机器学习功能

如果尝试在域控制器上安装 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务，安装失败，这些错误：

> *该功能在安装过程出错*
> 
> *找不到具有标识的组*
> 
> *组件的错误代码：0x80131509*

失败的原因，在域控制器上，服务无法创建所需运行机器学习的 20 本地帐户。 一般情况下，我们不建议在域控制器上安装 SQL Server。 有关详细信息，请参阅[支持公告 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4.安装最新的服务版本，以确保与 Microsoft R 客户端的兼容性

如果安装 Microsoft R 客户端的最新版本，并使用它来在远程计算上下文中运行 SQL Server 上的 R，可能会收到如下错误：

> *您与 Microsoft R Server 版本 8.x.x 不兼容的计算机上运行 Microsoft R Client 版本的 9.x.x。请下载并安装兼容版本。*

SQL Server 2016 要求在客户端上的 R 库与在服务器上的 R 库完全匹配。 限制已删除版本晚于 R Server 9.0.1。 但是，如果遇到此错误，验证由您的客户端和服务器，并如有必要，更新客户端以匹配服务器版本的 R 库版本。

每次安装 SQL Server 服务版本更新的安装与 SQL Server R Services 的 R 版本。 若要确保始终具有最新版本的 R 组件，请确保安装所有 service pack。

若要确保与 Microsoft R Client 9.0.0 兼容，在此安装所述的更新[支持文章](https://support.microsoft.com/kb/3210262)。

若要避免出现问题的 R 包，还可以升级安装的服务器，通过更改服务协议为使用新式生命周期支持策略，如中所述的 R 库的版本[下一步部分](#bkmk_sqlbindr)。 当你执行此操作时，用于更新机器学习服务器 (以前称为 Microsoft R Server) 在同一个计划更新的 SQL Server 一起安装的 R 版本。

**适用范围：** SQL Server 2016 R Services，使用 R Server 9.0.0 版或更早版本

### <a name="5-r-components-missing-from-cu3-setup"></a>5.缺少 CU3 安装 R 组件

不应包含在 SQL Server 的 R 安装文件的情况下预配有限的数量的 Azure 虚拟机。 此问题适用于虚拟机中从 2018年-01-05 到 2018年-01-23 期间预配。 此问题也可能会影响在本地安装，如果 SQL Server 2017 cu3 开始更新期间从 2018年-01-05 对应用 2018年-01-23。

包括 R 安装文件的正确版本提供了服务版本。

+ [SQL Server 2017 KB4052987 的累积更新包 3](https://www.microsoft.com/download/details.aspx?id=56128)。

若要安装的组件和修复 SQL Server 2017 cu3 开始，您必须卸载 cu3 开始，并重新安装的更新的版本：

1. 下载更新后的 CU3 安装文件，其中包括 R 安装程序。
2. 卸载 CU3。 在控制面板中，搜索**卸载更新**，然后选择"Hotfix 3015 SQL server 2017 (KB4052987) （64 位）"。 继续执行卸载步骤。
3. 重新安装 cu3 开始，通过双击 KB4052987 刚下载的更新： `SQLServer2017-KB4052987-x64.exe`。 按照安装说明进行操作。

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6.无法在脱机安装的 SQL Server 2017 CTP 2.0 或更高版本中安装 Python 组件

如果在没有 internet 访问的计算机上安装 SQL Server 2017 的预发布版本，安装程序可能无法显示页面来提示输入下载的 Python 组件的位置。 在这种情况下，可以安装机器学习服务功能，但不是包含 Python 组件。

发行版本中修复此问题。 此外，此限制不适用于 R 组件。

**适用范围：** 与 Python 配合使用的 SQL Server 2017

### <a name="bkmk_sqlbindr"></a> 当你使用连接到 SQL Server R Services 的较旧版本从客户端版本不兼容的警告 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

SQL Server 2016 计算上下文中运行 R 代码时，它们可能会看到以下错误：

> *计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。*

如果以下两个语句之一为 true，，显示此消息

+ 通过使用安装向导的上的客户端计算机上安装 R Server （独立版） [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。
+ 使用安装了 Microsoft R Server[单独的 Windows 安装程序](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

若要确保服务器和客户端使用相同的版本可能需要使用_绑定_、 受支持的 Microsoft R Server 9.0 和更高版本升级 SQL Server 2016 实例中的 R 组件。 若要确定是否支持升级为提供有关你的 R Services 版本，请参阅[实例的 R Services 使用 SqlBindR.exe 升级](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

**适用范围：** SQL Server 2016 R Services，使用 R Server 9.0.0 版或更早版本

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7.安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

当您安装累积更新或 service pack 的 SQL Server 2016 安装在未连接到 internet 的计算机上时，安装向导可能无法显示使您可以通过使用下载的 CAB 文件更新 R 组件的提示。 与数据库引擎一起安装多个组件时，通常会发生此失败。

解决此问题，可以通过使用命令行和指定安装 service release`MRCACHEDIRECTORY`参数在此示例中，它将安装 CU1 更新所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取最新的安装程序，请参阅[安装没有 internet 访问权限的机器学习组件](install/sql-ml-component-install-without-internet-access.md)。

**适用范围：** SQL Server 2016 R Services，使用 R Server 9.0.0 版或更早版本

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8.快速启动板服务无法启动的版本是 R 版本不同

如果从数据库引擎单独安装 SQL Server R Services，并且生成版本不同，可能会看到系统事件日志中的以下错误：

> *SQL Server Launchpad 服务启动因以下错误而失败：该服务未响应及时的开始或控制请求。*

例如，此错误可能发生，如果使用发行版本安装数据库引擎、 应用修补程序来升级数据库引擎，然后使用发行版本添加 R Services 功能。

若要避免此问题，使用实用程序等文件管理器将使用版本的 SQL 二进制文件，例如 sqldk.dll Launchpad.exe 的版本。 所有组件应都具有相同的版本号。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

快速启动板中查找`Binn`实例的文件夹。 例如，在默认安装的 SQL Server 2016 中，其路径可能为`C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`。 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9.Azure 虚拟机运行的 SQL Server 实例中的防火墙阻止远程计算上下文

如果已安装[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]上 Windows Azure 虚拟机，你可能无法使用需要虚拟机的工作区使用的计算上下文。 原因是，默认情况下，Azure 虚拟机上的防火墙包含阻止网络访问本地 R 用户帐户的规则。

解决方法是，Azure VM 上打开**高级安全 Windows 防火墙**，选择**出站规则**，并禁用以下规则：**阻止 SQL Server 实例 MSSQLSERVER 中的 R 本地用户帐户的网络访问**。 您还可以将启用，该规则保留，但更改到的安全属性**允许在安全**。

### <a name="10-implied-authentication-in-sqlexpress"></a>10.SQLEXPRESS 中的隐式身份验证

当从远程数据科学工作站运行 R 作业，通过使用集成 Windows 身份验证时，使用 SQL Server*隐式身份验证*生成脚本可能所需的任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。

若要解决此问题，建议升级到更高的 Service Release。

如果升级不是可行的作为一种解决方法，使用 SQL 登录名运行可能需要嵌入式的 ODBC 调用的远程 R 作业。

**适用范围：** SQL Server 2016 R Services 速成版

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11.使用 SQL Server 的库从其他工具中调用时的性能限制

就可以调用机器学习库，适用于 SQL Server 安装从外部应用程序，如 RGui。 执行此操作可能是最方便的方法来完成某些任务，例如安装新的包，或在很短的代码示例上运行即席测试。 但是，SQL Server 之外，性能可能会受到限制。 

例如，即使使用 SQL Server Enterprise Edition，R 在单线程模式下运行时使用外部工具运行 R 代码。 若要获取 SQL Server 中的性能优势，请启动 SQL Server 连接并使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来调用外部脚本运行时。

一般情况下，避免调用机器学习库通过 SQL Server 用于从外部工具。 如果需要调试 R 或 Python 代码，则通常更容易进行 SQL Server 外部执行此操作。 若要获取在 SQL Server 中的同一个库，可以安装 Microsoft R Client [SQL Server 2017 机器学习服务器 （独立版）](install/sql-machine-learning-standalone-windows-install.md)，或[SQL Server 2016 R Server （独立版）](install/sql-r-standalone-windows-install.md)。

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12.SQL Server Data Tools 不支持所需权限的外部脚本

当你使用 Visual Studio 或 SQL Server Data Tools 以发布数据库项目，如果任何主体具有特定于执行外部脚本的权限时，可能会收到如下错误：

> *TSQL 模型：反向工程数据库时检测到错误。权限未被识别和未导入。*

当前 DACPAC 模型不支持使用 R Services 或机器学习服务，例如授予任意外部脚本或执行任意外部脚本的权限。 更高版本将会解决此问题。

解决此问题，其他 GRANT 语句中运行后期部署脚本。

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13.外部脚本执行限制由于资源调控默认值

在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些早期发行版本中，可以分配给 R 进程的最大内存的 20%。 因此，如果服务器有 32 GB RAM，R 可执行文件 （RTerm.exe 和 BxlServer.exe） 可以使用单个请求中的最大 6.4 GB。

如果遇到资源限制，请检查当前的默认值。 如果 20%不够，请参阅的文档[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]如何更改此值。

**适用范围：** SQL Server 2016 R Services，企业版

## <a name="r-script-execution-issues"></a>R 脚本执行问题

本部分包含特定于 SQL Server 上运行 R 的已知的问题，以及与 R 库和工具由 Microsoft，包括 RevoScaleR 发布相关的一些问题。

可能会影响 R 解决方案的更多已知问题，请参阅[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站点。

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1.在非默认位置中的 SQL Server 中执行 R 脚本时，访问被拒绝警告

如果 SQL Server 实例已安装到非默认位置，如外部`Program Files`文件夹中，当您尝试运行安装包的脚本时引发 ACCESS_DENIED 警告。 例如：

> *在`normalizePath(path.expand(path), winslash, mustWork)`： 路径 [2] ="~ExternalLibraries/R/8/1":访问被拒绝*

原因是 R 函数尝试读取该路径，且如果失败的内置用户组**SQLRUserGroup**，不具有读取访问权限。 引发的警告不会阻止执行当前的 R 脚本，但警告可能会重复发生，每当用户在运行任何其他 R 脚本。

如果你安装 SQL Server 的默认位置，此不会出现错误，因为所有 Windows 用户具有都读取权限上`Program Files`文件夹。

Ia 在即将推出的服务的版本中解决此问题。 解决此问题，请提供组， **SQLRUserGroup**，具有读取访问权限的所有父文件夹`ExternalLibraries`。

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2.旧的和新版本的 RevoScaleR 之间序列化错误

如果通过使用远程 SQL Server 实例的序列化的格式的模型，可能会收到错误： 

> *MemDecompress 中的错误 (数据、 类型 = 解压缩) memDecompress(2) 中的出现内部错误-3。*

如果保存在模型中使用最新版本的序列化函数，则会引发此错误[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，但其中你模型反序列化的 SQL Server 实例具有较旧版本的 RevoScaleR Api，从 SQLServer 2017 CU2 或更早版本。

作为一种解决方法，可以升级到 CU3 或更高版本的 SQL Server 2017 实例。

如果 API 版本是相同的或如果在迁移到使用序列化 API 的较新版本的服务器的较旧的序列化函数使用保存的模型，不会显示错误。

换而言之，使用相同版本的 RevoScaleR 序列化和反序列化操作。

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3.实时评分不会正确处理_learningRate_树和林模型中的参数

如果您使用决策树或决策林方法创建模型，并指定学习速率，使用时，可能会看到不一致的结果`sp_rxpredict`或 SQL`PREDICT`函数，相比使用`rxPredict`。

原因是 API 中的错误的序列化的进程模型，并仅限于`learningRate`参数： 例如，在[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)，或

在即将推出的服务的版本中解决此问题。

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4.R 作业的处理器关联限制

在 SQL Server 2016 的初始版本生成，你可以设置只为第一个 k 组中的 Cpu 处理器关联。 例如，如果服务器是具有两个 k 组的双套接字计算机，从第一个 k 组的唯一处理器用于 R 进程。 配置 R 脚本作业的资源调控时，将应用相同的限制。

此问题已在 SQL Server 2016 Service Pack 1 中解决。 我们建议您升级到最新的服务版本。

**适用范围：** SQL Server 2016 R Services RTM 版本

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5.在 SQL Server 计算环境中读取数据时，无法更改列类型

如果计算环境设置为 SQL Server 实例，则无法在 R 代码中使用 _colClasses_ 参数（或其他类似参数）来更改列的数据类型。

例如，如果列 CRSDepTimeStr 尚不是整数，则以下语句将导致错误：

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

解决方法是，您可以重新编写 SQL 查询使用 CAST 或 CONVERT，并使用正确的数据类型在 R 中表示该数据。 一般情况下，性能是更好地处理数据使用 SQL，而不是通过将 R 代码中的数据更改。

**适用范围：** SQL Server 2016 R 服务

### <a name="6-limits-on-size-of-serialized-models"></a>6.序列化模型大小限制

当您将模型保存到 SQL Server 表时，必须将模型序列化并将其保存以二进制格式。 从理论上可以使用此方法存储的模型的最大大小为 2 GB，这是 SQL Server 中的 varbinary 列的最大大小。

如果您需要使用更大的模型，提供了以下解决方法：

+ 采取措施来降低您的模型的大小。 一些开放源代码 R 包中的模型对象，包含大量的信息，并且可以为部署中删除其中许多信息。 
+ 使用功能选择来删除不必要的列。
+ 如果使用开放源代码算法，请考虑使用 MicrosoftML 或 RevoScaleR 中的对应算法一个类似的实现。 这些包已针对部署方案进行了优化。
+ 已从合理化模型并使用上述步骤，可以减小大小后，请参阅如果[memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)中基础 R 函数可用于减少模型的大小，然后再将它传递到 SQL Server。 此选项最适合当模型接近 2 GB 的限制。
+ 对于较大的模型，可以使用 SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md)功能来存储模型，而不使用 varbinary 列。

    若要使用 Filetable，必须添加防火墙例外，因为在 Filetable 中存储的数据由 SQL Server 中的 Filestream 文件系统驱动程序，默认的防火墙规则阻止网络文件的访问。 有关详细信息，请参阅[启用 FileTable 的先决条件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。

    在已启用 FileTable，若要编写模型，使用 FileTable 的 API，从 SQL 获取路径模型然后写入该位置中从您的代码后。 当您需要读取模型时，您从 SQL 获取路径，然后再调用在模型中使用从您的脚本的路径。 有关详细信息，请参阅[使用文件输入输出 Api 访问 Filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7.避免在执行中的 R 代码时清除工作区[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文

如果你使用 R 命令清除对象的工作区中运行 R 代码时[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文，或如果清除在工作区作为 R 脚本的一部分通过调用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，可能会收到此错误:*找不到工作区对象 revoScriptConnection*

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

解决此问题，避免随意清除变量和其他对象运行 R 时[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 尽管在 R 控制台中工作时，清除工作区很常见，但它可以有意外的结果。

* 若要删除特定的变量，使用 R`remove`函数： 例如， `remove('name1', 'name2', ...)`
* 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8.可作为输入提供给 R 脚本的数据的限制

你无法在 R 脚本中使用以下类型的查询结果：

- 引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
- 引用屏蔽列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9.使用的字符串，如因素会导致性能下降

使用字符串类型变量，如因素可以极大地提高 R 操作使用的内存量。 通常情况下，这是使用 R 的已知的问题和有关该主题有许多文章。 例如，请参阅[因素不是 John 装载点，在 R 博客作者提供的 R 中的一等公民)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)或[stringsasfactors 设：未经授权的简介、 由 Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)。 

虽然此问题不是特定于 SQL Server，则会极大地影响运行 SQl Server 中的 R 代码的性能。 字符串通常存储为 varchar 或 nvarchar，和字符串数据的列有许多唯一值，如果在内部将这些整数并返回到的字符串转换的过程，甚至会导致内存分配错误。

如果您不绝对需要字符串数据类型对于其他操作，将字符串值映射为数字 （整数） 数据类型为数据准备过程中的会很有益从性能和规模的角度来看。

有关此问题，以及其他提示的讨论，请参阅[R Services-数据优化的性能](r/r-and-data-optimization-r-services.md)。

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10.自变量*varsToKeep*并*varsToDrop*不适用于 SQL Server 数据源

当您使用 rxDataStep 函数将结果写入表时，使用*varsToKeep*并*varsToDrop*是指定要包括或排除操作的一部分的列的简便方法。 但是，对于 SQL Server 数据源不支持这些参数。

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11.有限的支持的 SQL 数据类型在 sp\_执行\_外部\_脚本

并非所有在 SQL 中支持的数据类型可在。作为一种解决方法，请考虑为受支持的数据类型不受支持的数据类型转换之前将数据传递给 sp\_执行\_外部\_脚本。

有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12.Varchar 列中使用 unicode 字符串的可能的字符串损坏

Varchar 列中传递 unicode 数据[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 R/Python 可能会导致字符串损坏。 这是因为这些 unicode 字符串中的编码[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]排序规则可能与 R/Python 中使用的默认 utf-8 编码不匹配。 

若要发送的任何非 ASCII 字符串数据[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到 R/Python 使用 utf-8 编码 (中提供[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) 或 nvarchar 类型用于相同。

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13.只有一个值类型的`raw`可以从返回 `sp_execute_external_script`

二进制数据类型时 (R**原始**数据类型) 从 R 返回，则值必须发送输出数据帧中。

为数据类型以外**原始**，可以通过添加 OUTPUT 关键字来返回参数值以及将存储过程的结果。 有关详细信息，请参阅[参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果你想要使用包含类型的值的多个输出集**原始**，一个可能的解决方法是为存储过程的多个调用，或若要将结果发送回设置为[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 ODBC。

### <a name="14-loss-of-precision"></a>14.精度损失

因为[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支持不同的数据类型，数值数据类型可能会降低精度的转换过程。

有关隐式数据类型转换的详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15.变量范围错误，当使用 transformFunc 参数时

若要转换的数据，而您建模时，可以将传递*transformFunc*中如函数自变量`rxLinmod`或`rxLogit`。 但是，嵌套的函数调用可能会导致出现范围错误在 SQL Server 计算上下文中，即使该调用在本地计算上下文中正常工作。

> *用于分析的示例数据集具有任何变量*

例如，假定您已经定义了两个函数`f`并`g`，在本地全局环境中，并`g`调用`f`。 在分布式或远程调用涉及`g`，调用`g`可能会出现以下错误失败，因为`f`找不到，即使已通过同时`f`和`g`给远程调用。

如果遇到此问题，你可以通过在 `f` 的定义中（ `g`可正常调用 `g` 的任何位置）嵌入 `f`的定义来解决该问题。

例如：

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

若要避免此错误，请按如下所示重写定义：

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16.使用 RevoScaleR 导入和操作数据

当**varchar**列从数据库中读取，裁剪掉空格。 为了避免这种情况，请将字符串包含在非空格字符中。

当之类的函数`rxDataStep`用于创建数据库表具有**varchar**列宽度的列会根据数据样本估算。 如果宽度可能会变化，可能需要所有字符串都填补到公共长度。

使用 `rxImport` 或 `rxTextToXdf` 的重复调用来导入和追加行，并将多个输入文件合并为单个.xdf 文件时，不支持使用转换来更改变量的数据类型。

### <a name="17-limited-support-for-rxexec"></a>17.对 rxExec 的支持有限

SQL Server 2016 中`rxExec`只能在单线程模式下是可使用 RevoScaleR 包提供的函数。

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18.增加最大参数大小以支持 rxGetVarInfo

如果使用数据集具有极其大量的变量 （例如，超过 40,000 个） 时，设置`max-ppsize`标志时启动 R 使用函数如`rxGetVarInfo`。 `max-ppsize` 标志指定指针保护堆栈的最大大小。

如果使用 R 控制台 （例如，RGui.exe 或 RTerm.exe 中），可以设置的值_最大 ppsize_为 500000 通过键入：

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19.RxDTree 函数的问题

`rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是，自动装箱数值数据。

有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。

## <a name="python-script-execution-issues"></a>Python 脚本执行问题

本部分包含特定于在 SQL Server，以及与 Microsoft 发布的 Python 包相关的问题上运行 Python 的已知的问题包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1.预先训练的模型调用失败，如果模型的路径太长

如果在早期版本的 SQL Server 2017 中安装的预先训练的模型，训练的模型文件的完整路径可能对 Python 读取而言太长。 更高版本的服务版本中修复了此限制。

有几个可能的解决方法： 

+ 安装预先训练的模型时，选择自定义位置。
+ 如果可能，请使用较短的路径，例如 C:\SQL\MSSQL14 安装自定义安装路径下的 SQL Server 实例。MSSQLSERVER。
+ 使用 Windows 实用工具[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)若要创建映射到较短的路径的模型文件的硬链接。
+ 更新到最新的服务版本。

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2.错误保存时序列化模型到 SQL Server

当您将模型传递到远程 SQL Server 实例，并尝试读取二进制模型使用`rx_unserialize`函数，在[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)，可能会收到错误： 

> *NameError： 未定义名称 rx_unserialize_model*

如果保存在模型中使用最新版本的序列化函数，但其中你模型反序列化的 SQL Server 实例不能识别序列化 API，则会引发此错误。

若要解决此问题，请升级到 CU3 或更高版本的 SQL Server 2017 实例。

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3.未能初始化 varbinary 变量 BxlServer 中导致错误

如果在使用 SQL Server 中运行 Python 代码`sp_execute_external_script`，和代码具有输出类型 varbinary （max）、 varchar （max） 或类似的类型的变量时，必须初始化变量，或将其设置为您的脚本的一部分。 否则，数据 exchange 组件，BxlServer，将产生一个错误，并停止工作。

将在即将推出的服务的版本中解决此限制。 解决此问题，请确保该变量进行初始化的 Python 脚本中。 可以使用任何有效的值，如以下示例所示：

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4.在成功执行 Python 代码的遥测数据警告

从 SQL Server 2017 CU2 开始，即使已成功运行 Python 代码，否则为可能会出现以下消息：

> *来自外部脚本的 STDERR 消息*：
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state 是全局声明之前使用*


在 SQL Server 2017 累积更新 3 (CU3) 中已修复此问题。 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本部分列出了特定于 R 连接、 开发和 Revolution Analytics 提供的性能工具问题。 早期预发布版本中提供了这些工具[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。

一般情况下，我们建议你卸载这些早期版本和安装最新版本的 SQL Server 或 Microsoft R Server。

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1.不支持 revolution R 企业版

与任何版本的安装 Revolution R Enterprise 并排[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]不受支持。

如果你有 Revolution R Enterprise 的现有许可证，必须将其放在从这两个单独的计算机上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例和你想要用于连接到任何工作站[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。

某些预发布版本的[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]包含 Revolution Analytics 创建的 Windows 的 R 开发环境。 此工具不再提供，并不受支持。

与的兼容性[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我们建议你改为安装 Microsoft R 客户端。 [针对 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)并[Visual Studio Code](https://code.visualstudio.com/)还支持 Microsoft R 解决方案。

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2.SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题

SQLite ODBC 驱动程序修订版 0.92 与 RevoScaleR 不兼容。 修订版 0.88-0.91 和 0.93 和更高版本已知兼容。

## <a name="see-also"></a>另请参阅

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

[故障排除 SQL Server 中的机器学习](machine-learning-troubleshooting-faq.md)
