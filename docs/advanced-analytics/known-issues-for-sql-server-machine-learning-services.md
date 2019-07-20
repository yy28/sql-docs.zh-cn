---
title: R 语言和 Python 集成的已知问题
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 547a567b00474f0c1538d907d70d8a808bebf851
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344939"
---
# <a name="known-issues-in-machine-learning-services"></a>机器学习服务中的已知问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了机器学习组件的已知问题或限制, 作为[SQL Server 2016 R Services](install/sql-r-services-windows-install.md)中提供的选项, 以及[R 和 Python SQL Server 2017 机器学习服务](install/sql-machine-learning-services-windows-install.md)中提供。

## <a name="setup-and-configuration-issues"></a>安装和配置问题

有关与初始设置和配置相关的过程和常见问题的说明, 请参阅[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含有关升级、并行安装和安装新的 R 或 Python 组件的信息。

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1.由于缺少环境变量导致了 MKL 计算中的结果不一致

**适用范围：** R_SERVER 二进制文件9.0、9.1、9.2 或9.3。

R_SERVER 使用 Intel 数学内核库 (MKL)。 对于涉及到 MKL 的计算, 如果系统缺少环境变量, 则可能会出现不一致的结果。 

设置环境变量`'MKL_CBWR'=AUTO` , 以确保在 R_SERVER 中设置条件数字的可再现性。 有关详细信息, 请参阅[条件数值可再现性 (CNR) 简介](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

**解决方法**

1. 在控制面板中, 单击 "**系统和安全** > **系统** > " "**高级系统设置** > " "**环境变量**"。

2. 创建新的用户或系统变量。 

  + 将变量名称设置为 "MKL_CBWR"。
  + 将 "变量值" 设置为 "AUTO"。

3. 重新启动 R_SERVER。 在 SQL Server 上, 你可以重新启动 SQL Server Launchpad 服务。

> [!NOTE]
> 如果要在 Linux 上运行 SQL Server 2019 预览版, 请在用户的主目录中编辑或*bash_profile* , 并添加行`export MKL_CBWR="AUTO"`。 在 bash 命令提示符下`source .bash_profile`键入以执行此文件。 在 R 命令提示符`Sys.getenv()`下键入以重新启动 R_SERVER。

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2.R 脚本运行时错误 (SQL Server 2017 CU5-CU7 回归)

对于 SQL Server 2017, 在累积更新5到7中, **rlauncher**文件中存在一个回归, 其中 temp 目录文件路径包含空格。 此回归在 CU8 中得到更正。

运行 R 脚本时显示的错误包括以下消息:

> *无法与 "R" 脚本的运行时通信。请检查 ' R ' 运行时的要求。*
>
> 来自外部脚本的 STDERR 消息: 
>
> *错误: 无法创建 "R_TempDir"*

**解决方法**

当 CU8 可用时应用它。 或者, 你可以通过在提升的命令提示符下通过卸载/安装运行**registerrext.exe**来重新创建**rlauncher。** 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

下面的示例显示了带有默认实例 "MSSQL14." 的命令。MSSQLSERVER "已安装到" C:\Program Files\Microsoft\"SQL Server:

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3.无法在域控制器上安装 SQL Server 机器学习功能

如果尝试在域控制器上安装 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务, 则安装程序将失败, 并出现以下错误:

> *此功能的安装过程中出现错误*
> 
> *找不到具有标识的组*
> 
> *组件错误代码:0x80131509*

发生此失败的原因是, 在域控制器上, 该服务无法创建运行机器学习所需的20个本地帐户。 通常, 我们建议不要在域控制器上安装 SQL Server。 有关详细信息, 请参阅[支持公告 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4.安装最新的服务版本以确保与 Microsoft R Client 的兼容性

如果安装最新版本的 Microsoft R Client, 并使用它在远程计算上下文中的 SQL Server 上运行 R, 可能会收到如下错误:

> *你在计算机上运行的是 Microsoft R Client 版本 1.x, 这与 Microsoft R Server 版本8不兼容。采用2.x.x。请下载并安装兼容版本。*

SQL Server 2016 要求客户端上的 R 库与服务器上的 R 库完全匹配。 此限制已在 R Server 9.0.1 之后的版本中被删除。 但是, 如果遇到此错误, 请验证客户端和服务器使用的 R 库的版本, 并根据需要更新客户端以匹配服务器版本。

只要安装了 SQL Server service release, 就会更新随 SQL Server R Services 一起安装的 R 版本。 若要确保始终具有最新版本的 R 组件, 请确保安装所有 service pack。

若要确保与 Microsoft R Client 9.0.0 兼容, 请安装本[支持文章](https://support.microsoft.com/kb/3210262)中所述的更新。

若要避免 R 包出现问题, 你还可以通过将维护协议更改为使用现代生命周期支持策略来升级服务器上安装的 R 库的版本, 如[以下部分](#bkmk_sqlbindr)中所述。 当你执行此操作时, 将按用于机器学习服务器更新的相同计划 (以前称为 Microsoft R Server) 更新随 SQL Server 一起安装的 R 版本。

**适用范围：** SQL Server 2016 R Services, 具有 R Server 9.0.0 或更早版本

### <a name="5-r-components-missing-from-cu3-setup"></a>5.CU3 安装程序中缺少 R 组件

预配有限数量的 Azure 虚拟机, 而不使用应包含在 SQL Server 中的 R 安装文件。 此问题适用于在2018-01-05 到2018-01-23 期间预配的虚拟机。 如果在2018-01-05 到2018-01-23 期间应用了 SQL Server 2017 的 CU3 更新, 此问题也可能会影响本地安装。

提供了一个服务发布, 其中包含正确的 R 安装文件版本。

+ [SQL Server 2017 的累积更新包 3 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128)。

若要安装组件并修复 SQL Server 2017 CU3, 必须卸载 CU3, 并重新安装更新的版本:

1. 下载更新的 CU3 安装文件, 其中包含 R 安装程序。
2. 卸载 CU3。 在 "控制面板" 中, 搜索 "**卸载更新**", 然后选择 "修补程序 3015 for SQL Server 2017 (KB4052987) (64 位)"。 继续执行卸载步骤。
3. 双击刚刚下载的 KB4052987 的更新, 重新安装 CU3 更新: `SQLServer2017-KB4052987-x64.exe`。 按照安装说明进行操作。

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6.无法在 SQL Server 2017 CTP 2.0 或更高版本的脱机安装中安装 Python 组件

如果在没有 internet 访问权限的计算机上安装 SQL Server 2017 的预发行版本, 则安装程序可能无法显示提示输入下载的 Python 组件位置的页面。 在这种情况下, 你可以安装机器学习服务功能, 但不能安装 Python 组件。

此问题已在发布版本中得到解决。 此外, 此限制不适用于 R 组件。

**适用范围：** SQL Server 2017 与 Python

### <a name="bkmk_sqlbindr"></a>当你通过使用从客户端连接到较旧版本的 SQL Server R Services 时出现不兼容版本的警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

在 SQL Server 2016 计算上下文中运行 R 代码时, 可能会看到以下错误:

> *计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。*

如果以下两个语句均为 true, 则会显示此消息。

+ 使用的安装向导[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]在客户端计算机上安装 R Server (独立版)。
+ 你使用[单独的 Windows 安装程序](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)安装 Microsoft R Server。

若要确保服务器和客户端使用相同的版本, 你可能需要使用 Microsoft R Server 9.0 和更高版本支持的_绑定_, 以便升级 SQL Server 2016 实例中的 R 组件。 若要确定对你的 R Services 版本是否支持升级, 请参阅[使用 SqlBindR 升级 R services 的实例](install/upgrade-r-and-python.md)。

**适用范围：** SQL Server 2016 R Services, 具有 R Server 9.0.0 或更早版本

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7.安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

在未连接到 internet 的计算机上安装累积更新或安装 SQL Server 2016 的 Service Pack 时, 安装向导可能无法显示允许您使用下载的 CAB 文件更新 R 组件的提示。 如果将多个组件与数据库引擎一起安装, 通常会发生此故障。

作为一种解决方法, 你可以通过使用命令行并指定参数 (如本`MRCACHEDIRECTORY`示例中所示) 来安装服务版本, 该参数将安装 CU1 更新:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取最新的安装程序, 请参阅在[不访问 internet 的情况下安装机器学习组件](install/sql-ml-component-install-without-internet-access.md)。

**适用范围：** SQL Server 2016 R Services, 具有 R Server 9.0.0 或更早版本

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8.如果版本与 R 版本不同, 则启动板服务无法启动

如果你从数据库引擎单独安装 SQL Server R Services, 并且生成版本不同, 则你可能会在系统事件日志中看到以下错误:

> *由于以下错误, 无法启动 SQL Server Launchpad 服务:该服务未及时响应启动请求或控制请求。*

例如, 如果你使用发布版本安装数据库引擎, 应用修补程序来升级数据库引擎, 然后使用发布版本添加 R Services 功能, 则可能出现此错误。

若要避免此问题, 请使用实用程序 (如文件管理器) 将 sqldk 版本与 SQL 二进制文件 (如) 的版本进行比较。 所有组件都应有相同的版本号。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

在实例的文件夹中`Binn`查找 "快速启动板"。 例如, 在 SQL Server 2016 的默认安装中, 路径可能是`C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`。 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9.远程计算上下文被 Azure 虚拟机上运行的 SQL Server 实例中的防火墙阻止

如果已在 microsoft [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Azure 虚拟机上安装, 则可能无法使用要求使用虚拟机工作区的计算上下文。 这是因为, 默认情况下, Azure 虚拟机上的防火墙包含一个规则, 该规则阻止本地 R 用户帐户的网络访问。

解决方法: 在 Azure VM 上打开 "**高级安全 Windows 防火墙**", 选择 "**出站规则**", 并禁用以下规则:**阻止对 SQL Server 实例 MSSQLSERVER 中的 R 本地用户帐户进行网络访问**。 还可以启用规则, 但将安全属性**更改为 "** 安全"。

### <a name="10-implied-authentication-in-sqlexpress"></a>10.SQLEXPRESS 中的隐式身份验证

使用集成 Windows 身份验证从远程数据科学工作站运行 R 作业时, SQL Server 使用*隐含的身份验证*来生成脚本可能需要的任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。

若要解决此问题，建议升级到更高的 Service Release。

如果升级不可行, 作为一种解决方法, 可以使用 SQL 登录名来运行可能需要嵌入 ODBC 调用的远程 R 作业。

**适用范围：** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11.在从其他工具调用 SQL Server 使用的库时的性能限制

可以从外部应用程序 (例如 Rgui.exe) 调用为 SQL Server 安装的机器学习库。 这样做可能是完成某些任务 (如安装新包或在非常简短的代码示例上运行即席测试) 的最简便方法。 但是, 在 SQL Server 之外, 性能可能会受到限制。 

例如, 即使您使用的是 SQL Server 的企业版, 当您使用外部工具运行 R 代码时, R 也将在单线程模式下运行。 若要在 SQL Server 中获得性能优势, 请启动 SQL Server 连接, 并使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)调用外部脚本运行时。

一般情况下, 应避免调用由外部工具 SQL Server 使用的机器学习库。 如果需要调试 R 或 Python 代码, 通常可以更轻松地在 SQL Server 之外执行此操作。 若要获取 SQL Server 中的相同库, 可以安装 Microsoft R Client、 [SQL Server 2017 Machine Learning Server (独立)](install/sql-machine-learning-standalone-windows-install.md)或[SQL Server 2016 R Server (独立版)](install/sql-r-standalone-windows-install.md)。

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12.SQL Server Data Tools 不支持外部脚本所需的权限

使用 Visual Studio 或 SQL Server Data Tools 发布数据库项目时, 如果有任何主体具有特定于外部脚本执行的权限, 则可能会收到类似于下面的错误:

> *TSQL 模型:对数据库进行反向工程时检测到错误。权限未被识别且未导入。*

当前 DACPAC 模型不支持 R Services 或机器学习服务使用的权限, 例如 GRANT 任何外部脚本或执行任何外部脚本。 更高版本将会解决此问题。

解决方法是在后期部署脚本中运行其他 GRANT 语句。

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13.由于资源调控默认值, 外部脚本执行已中止

在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些早期版本的版本中, 可分配给 R 进程的最大内存为 20%。 因此, 如果服务器的 RAM 为 32 GB, 则 R 可执行文件 (Rterm.exe 和 BxlServer) 在单个请求中最多可以使用 6.4 GB。

如果遇到资源限制, 请检查当前的默认值。 如果 20% 不够, 请参阅有关如何更改此[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]值的文档。

**适用范围：** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>R 脚本执行问题

本部分包含特定于在 SQL Server 上运行 R 的已知问题, 以及由 Microsoft 发布的 R 库和工具 (包括 RevoScaleR) 相关的一些问题。

有关可能会影响 R 解决方案的其他已知问题, 请参阅[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站点。

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1.在非默认位置的 SQL Server 上执行 R 脚本时出现 "拒绝访问" 警告

如果 SQL Server 的实例已安装到非默认位置 (如`Program Files`文件夹外), 则当你尝试运行安装包的脚本时, 将引发警告 ACCESS_DENIED。 例如：

> *In `normalizePath(path.expand(path), winslash, mustWork)` : path [2] = "~ ExternalLibraries/R/8/1":拒绝访问*

这是因为 R 函数尝试读取路径, 如果内置用户组**SQLRUserGroup**没有读取权限, 则会失败。 引发的警告不会阻止当前 R 脚本的执行, 但每当用户运行任何其他 R 脚本时, 该警告都可能重复出现。

如果已将 SQL Server 安装到默认位置, 则不会发生此错误, 因为所有 Windows 用户对该`Program Files`文件夹都具有读取权限。

此问题 ia 在即将发布的服务版本中解决。 作为一种解决方法, 提供组**SQLRUserGroup**, 对的`ExternalLibraries`所有父文件夹具有读取权限。

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2.旧版本和新版本的 RevoScaleR 之间的序列化错误

使用序列化格式将模型传递到远程 SQL Server 实例时, 可能会收到以下错误: 

> *MemDecompress 中的错误 (数据, 类型 = 解压缩) 在 memDecompress 中出现内部错误-3 (2)。*

如果使用最新版本的序列化函数[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)保存了模型, 但反序列化模型的 SQL Server 实例的 RevoScaleR api 版本早于 SQL SERVER 2017 CU2 或更早版本, 则会引发此错误。

解决方法之一是, 可以将 SQL Server 2017 实例升级到 CU3 或更高版本。

如果 API 版本相同, 或者要将使用较旧序列化函数保存的模型移到使用较新版本序列化 API 的服务器, 则不会出现此错误。

换言之, 使用相同版本的 RevoScaleR 同时用于序列化和反序列化操作。

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3.实时评分无法正确处理树和林模型中的_learningrate 超出_参数

如果使用决策树或决策林方法创建模型并指定学习速率, 则在使用`sp_rxpredict`或 SQL `PREDICT`函数时, 可能会出现不一致的结果, 这与使用`rxPredict`有关。

原因是 API 中处理序列化模型的错误, 并且仅限于`learningRate`参数: 例如, 在[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)中, 或

即将发布的服务版本中解决了此问题。

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4.R 作业的处理器关联限制

在 SQL Server 2016 的初始发布版本中, 你只能为第一个 k 组中的 Cpu 设置处理器关联。 例如, 如果服务器是具有两个 k 组的2插槽计算机, 则只有第一个 k 组中的处理器用于 R 进程。 为 R 脚本作业配置资源调控时, 相同的限制也适用。

此问题已在 SQL Server 2016 Service Pack 1 中解决。 建议升级到最新的服务版本。

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

作为一种解决方法, 你可以通过使用正确的数据类型重写 SQL 查询以使用 CAST 或 CONVERT, 并向 R 提供数据。 通常, 使用 SQL 而不是在 R 代码中更改数据时, 性能会更好。

**适用范围：** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6.序列化模型大小限制

将模型保存到 SQL Server 表时, 必须序列化模型并将其保存为二进制格式。 理论上, 可使用此方法存储的模型的最大大小为 2 GB, 这是 SQL Server 中 varbinary 列的最大大小。

如果需要使用更大的模型, 可使用以下解决方法:

+ 采取措施减小模型大小。 一些开源 R 包在模型对象中包含大量的信息, 而这些信息可用于部署。 
+ 使用 "功能选择" 可删除不必要的列。
+ 如果使用开源算法, 请考虑使用 MicrosoftML 或 RevoScaleR 中的相应算法的类似实现。 这些包已针对部署方案进行了优化。
+ 模型经过合理化并且使用前面的步骤降低了大小后, 请查看是否可使用[memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)函数在将模型传递到 SQL Server 之前减小其大小。 当模型接近 2 GB 限制时, 此选项是最佳选择。
+ 对于更大的模型, 可以使用 SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md)功能来存储模型, 而不使用 varbinary 列。

    若要使用 Filetable, 你必须添加防火墙例外, 因为存储在 Filetable 中的数据是由中的 Filestream filesystem 驱动程序管理的 SQL Server, 默认防火墙规则阻止网络文件访问。 有关详细信息, 请参阅[启用 FileTable 的先决条件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。

    启用 FileTable 后, 若要编写模型, 可以使用 FileTable API 从 SQL 获取路径, 然后从代码将模型写入该位置。 如果需要读取模型, 可以从 SQL 获取路径, 然后使用脚本中的路径调用模型。 有关详细信息, 请参阅[使用文件输入输出 Api 访问 filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7.在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文中执行 R 代码时避免清除工作区

如果在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文中运行 r 代码时使用 r 命令清除了对象的工作区, 或者清除了工作区作为使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)调用的 r 脚本的一部分, 则可能会收到此错误:*工作区找不到对象 revoScriptConnection*

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

解决方法是在中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]运行 R 时避免任意清除变量和其他对象。 虽然在 R 控制台中工作时清除工作区很常见, 但它可能会产生意外后果。

* 若要删除特定的变量, 请`remove`使用 R 函数: 例如,`remove('name1', 'name2', ...)`
* 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8.可作为输入提供给 R 脚本的数据的限制

你无法在 R 脚本中使用以下类型的查询结果：

- 引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
- 引用屏蔽列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9.将字符串用作因素可能会导致性能下降

使用字符串类型变量作为因素可以极大地增加用于 R 操作的内存量。 这是通常在使用 R 时的一个已知问题, 在主题上有很多相关文章。 例如, [[在 r 中, 通过 John Mount、r-博主 (r) 或 stringsAsFactors 中所述的因素不是第一类公民](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/):未经授权的事迹, 作者:](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)Roger Peng。 

尽管此问题并不特定于 SQL Server, 但它可能会显著影响 SQl Server 中运行的 R 代码的性能。 字符串通常存储为 varchar 或 nvarchar, 并且如果字符串数据的列有多个唯一值, 则通过 R 将这些值内部转换为整数并返回到字符串的过程甚至可能导致内存分配错误。

如果不是绝对需要用于其他操作的字符串数据类型, 则在执行数据准备过程中将字符串值映射为数值 (整数) 数据类型将从性能和缩放角度来受益。

有关此问题的讨论以及其他提示, 请参阅[R Services-数据优化的性能](r/r-and-data-optimization-r-services.md)。

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10.SQL Server 数据源不支持参数*varsToKeep*和*varsToDrop*

使用 rxDataStep 函数将结果写入表时, 使用*varsToKeep*和*varsToDrop*是指定要包含或排除作为运算一部分的列的便捷方法。 但 SQL Server 数据源不支持这些参数。

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11.对 sp\_执行\_外部\_脚本中的 SQL 数据类型的有限支持

并非 SQL 支持的所有数据类型都可在 R 中使用。解决方法是在将数据传递到 sp\_执行\_外部\_脚本之前, 将不支持的数据类型转换为支持的数据类型。

有关详细信息, 请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12.使用 varchar 列中的 unicode 字符串可能会损坏字符串

将 varchar 列中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unicode 数据传递到 R/Python 可能导致字符串损坏。 这是由于排序规则中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]这些 unicode 字符串的编码可能与 R/Python 中使用的默认 utf-8 编码不匹配。 

若要将任何非 ASCII 字符串数据从[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]发送到 R/Python, 请使用 utf-8 编码 (在中[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]提供) 或对相同使用 nvarchar 类型。

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13.只能从中返回一个`raw`类型的值`sp_execute_external_script`

从 R 返回二进制数据类型 (R **raw**数据类型) 时, 必须在输出数据帧中发送该值。

除了**raw**之外的数据类型之外, 还可以通过添加 OUTPUT 关键字返回参数值以及存储过程的结果。 有关详细信息, 请参阅[参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果要使用包含类型为**raw**的值的多个输出集, 一个可能的解决方法是对存储过程执行多个调用, 或者使用 ODBC 将结果集发送[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]回。

### <a name="14-loss-of-precision"></a>14.精度损失

由于[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支持不同的数据类型, 因此在转换过程中数值数据类型的精度可能会降低。

有关隐式数据类型转换的详细信息, 请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15.使用 transformFunc 参数时出现变量范围错误

若要在建模时转换数据, 可以在函数 (  如`rxLinmod`或`rxLogit`) 中传递 transformFunc 参数。 但是, 嵌套的函数调用可能会导致 SQL Server 计算上下文中出现范围错误, 即使调用在本地计算上下文中正常工作也是如此。

> *用于分析的示例数据集没有变量*

例如, 假设`f`你在`g`本地全局环境中定义了两`g`个函数, 并且调用`f`了。 在涉及`g`的分布式或远程调用中, 对`g`的调用可能会因此错误`f`而失败, 因为找不到, 即使你`f`已`g`同时将和传递给远程调用。

如果遇到此问题，你可以通过在 `f` 的定义中（ `g`可正常调用 `g` 的任何位置）嵌入 `f`的定义来解决该问题。

例如：

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

若要避免此错误, 请重写定义, 如下所示:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16.使用 RevoScaleR 导入和操作数据

当从数据库中读取**varchar**列时, 空格将被剪裁掉。 为了避免这种情况，请将字符串包含在非空格字符中。

当使用等`rxDataStep`函数创建具有**varchar**列的数据库表时, 将根据数据的样本估算列宽。 如果宽度可能会变化, 则可能需要将所有字符串填充到一个公用长度。

使用 `rxImport` 或 `rxTextToXdf` 的重复调用来导入和追加行，并将多个输入文件合并为单个.xdf 文件时，不支持使用转换来更改变量的数据类型。

### <a name="17-limited-support-for-rxexec"></a>17.对 rxExec 的有限支持

在 SQL Server 2016 中, `rxExec` RevoScaleR 包提供的函数只能在单线程模式下使用。

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18.增加最大参数大小以支持 rxGetVarInfo

如果使用的数据集具有极大的变量 (例如, 超过 40000), 则在启动 R `max-ppsize`时设置标志以使用`rxGetVarInfo`等函数。 `max-ppsize` 标志指定指针保护堆栈的最大大小。

如果你使用 R 控制台 (例如, Rgui.exe 或 Rterm.exe), 则可以通过键入以下内容将_最大值 max-ppsize_的值设置为 500000:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19.RxDTree 函数的问题

`rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是, 数值数据会自动装箱。

有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20.在 R 中作为 OutputDataSet 的数据表

在 SQL Server 2017 `OutputDataSet`累积更新 13 (CU13) 和更早版本中, 不支持将用作R。`data.table` 可能会出现以下消息:

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table`SQL Server 2017 `OutputDataSet`累积更新 14 (CU14) 和更高版本支持中的作为中的。

## <a name="python-script-execution-issues"></a>Python 脚本执行问题

本部分包含特定于在 SQL Server 上运行 Python 的已知问题, 以及由 Microsoft 发布的 Python 包 (包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)) 相关的问题。

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1.如果模型的路径太长, 则调用预先训练模型失败

如果在 SQL Server 2017 的早期版本中安装了预先训练模型, 则训练的模型文件的完整路径可能太长, 因此无法读取 Python。 此限制在稍后的服务版本中已修复。

有几种可能的解决方法: 

+ 安装预先训练模型时, 请选择自定义位置。
+ 如果可能, 请在具有较短路径的自定义安装路径下安装 SQL Server 实例, 如 C:\SQL\MSSQL14。MSSQLSERVER.
+ 使用 Windows 实用工具[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)创建将模型文件映射到较短路径的硬链接。
+ 更新到最新的服务版本。

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2.将序列化模型保存到 SQL Server 时出错

如果将模型传递到远程 SQL Server 实例, 并尝试使用`rx_unserialize` [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)中的函数读取二进制模型, 则可能会收到以下错误: 

> *NameError: 未定义名称 "rx_unserialize_model"*

如果使用最新版本的序列化函数保存了模型, 但反序列化模型的 SQL Server 实例无法识别序列化 API, 则会引发此错误。

若要解决此问题, 请将 SQL Server 2017 实例升级到 CU3 或更高版本。

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3.初始化 varbinary 变量失败会导致 BxlServer 中出现错误

如果在 SQL Server 中使用`sp_execute_external_script`运行 Python 代码, 并且代码具有类型为 varbinary (max)、varchar (max) 或类似类型的输出变量, 则必须将该变量作为脚本的一部分进行初始化或设置。 否则, 数据交换组件 BxlServer 将引发错误并停止工作。

此限制将在即将发布的服务版本中得到解决。 作为一种解决方法, 请确保在 Python 脚本中初始化变量。 可以使用任何有效的值, 如以下示例中所示:

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4.在成功执行 Python 代码时出现遥测警告

从 SQL Server 2017 CU2 开始, 即使 Python 代码成功运行, 也可能出现以下消息:

> *来自外部脚本的 STDERR 消息*：
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state 是全局声明之前使用*

此问题已在 SQL Server 2017 累积更新 3 (CU3) 中得到解决。 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5.不支持 Numeric、decimal 和 money 数据类型

从 SQL Server 2017 累积更新 12 (CU12) 开始, 在将 Python 与`sp_execute_external_script`结合使用时, 不支持使用结果集中的 numeric、decimal 和 money 数据类型。 可能会出现以下消息:

> *编写39004, SQL 状态:S1000] 执行 of'sp_execute_external_script 时出现 "Python" 脚本错误, HRESULT 0x80004004。*

> *编写39019, SQL 状态:S1000] 发生外部脚本错误:*
> 
> *SqlSatelliteCall 错误:输出架构中的类型不受支持。支持的类型: 位、smallint、int、datetime、smallmoney、real 和 float。char、varchar 是部分受支持的。*

SQL Server 2017 累积更新 14 (CU14) 已修复此项。

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本部分列出了由革命 Analytics 提供的 R 连接、开发和性能工具特定的问题。 在的[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]早期预发布版本中提供了这些工具。

通常, 我们建议卸载以前的版本并安装最新版本的 SQL Server 或 Microsoft R Server。

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1.不支持革命 R Enterprise

不支持与任何版本的[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]并行安装革命 R Enterprise。

如果你有一个适用于革命 R Enterprise 的现有许可证, 则必须将其放在用于连接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到实例的实例和任何工作站的不同计算机上。

的一些预发行版本包含[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]了一种由革命 Analytics 创建的适用于 Windows 的 R 开发环境。 此工具不再提供, 不受支持。

为了与[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]兼容, 建议改为安装 Microsoft R Client。 [针对 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)和[Visual Studio Code](https://code.visualstudio.com/)还支持 Microsoft R 解决方案。

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2.SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题

SQLite ODBC 驱动程序的修订版0.92 与 RevoScaleR 不兼容。 已知版本 0.88-0.91 和0.93 及更高版本是兼容的。

## <a name="see-also"></a>请参阅

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server 中的机器学习疑难解答](machine-learning-troubleshooting-faq.md)
