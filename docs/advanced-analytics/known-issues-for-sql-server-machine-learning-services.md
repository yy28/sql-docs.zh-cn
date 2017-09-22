---
title: "机器学习服务中的已知问题 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2d21756a05e9e51379faa194ec331517e510988d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="known-issues-in-machine-learning-services"></a>机器学习服务中的已知的问题

本文介绍了已知的问题或限制机器学习作为 SQL Server 2016 和 SQL Server 自 2017 年中的一个选项提供的组件。

此处的信息适用于所有以下内容，除非明确指定：

* SQL Server 2016

  - R Services (数据库中)
  - Microsoft R Server（独立版）

* SQL Server 2017

  - 机器学习 （数据库） 的服务
  - 机器学习 Python （数据库） 的服务
  - 机器学习服务器（独立）

## <a name="setup-and-configuration-issues"></a>安装和配置问题

进程和与初始设置和配置相关的常见问题的说明，请参阅[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含有关升级、 通过并行安装和安装新的 R 或 Python 组件的信息。

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>无法在脱机安装的 SQL Server 自 2017 年 1 CTP 2.0 或更高版本中安装 Python 组件

如果在没有 internet 访问的计算机上安装 SQL Server 自 2017 年的预发行版本，安装程序可能无法显示页面，提示输入下载 Python 组件的位置。 在这种情况下，你可以安装机器学习服务功能，但不是 Python 组件。

在发布版本中修复此问题。 如果遇到此问题，一种解决方法，你可以暂时的安装程序的持续时间内启用 internet 访问权限。 此限制不适用于。

**适用于：**使用 Python 的 SQL Server 自 2017 年 1

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安装最新的服务版本，以确保与 Microsoft R 客户端的兼容性

如果你安装 Microsoft R 客户端的最新版本，并使用它 R SQL Server 上运行远程计算上下文中，你可能会如下所示的错误：

>*你与 Microsoft R Server 版本 8.x.x 不兼容的计算机上运行 Microsoft R 客户端版本的 9.x.x。请下载并安装兼容版本。

SQL Server 2016 需要客户端上的 R 库与服务器上的 R 库完全匹配。 限制已被撤除版本晚于 R Server 9.0.1。 但是，如果你遇到此错误，则验证 R 库，可供你的客户端和服务器，并如有必要，更新客户端与服务器版本匹配的版本。

每次安装的 SQL Server 服务发行版时，被更新的版本与 SQL Server R Services 安装的 R。 若要确保你始终具有最新版本的 R 组件，请确保安装所有 service pack。

若要确保与 Microsoft R 客户端 9.0.0 的兼容性，安装更新所述，在此[支持文章](https://support.microsoft.com/kb/3210262)。

若要避免与 R 包的问题，还可以升级安装在服务器上，通过更改为中所述的现代生命周期策略的 R 库版本[下一节](#bkmk_sqlbindr)。 执行此操作时，更新的版本与 SQL Server 安装的 R 是在同一个计划的 Microsoft R Server，这将确保服务器和客户端始终具有最新版本的 Microsoft。 发布更新

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="bkmk_sqlbindr"></a>当你从连接到旧版本的 SQL Server R Services 客户端使用的不兼容版本警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

当在 SQL Server 2016 计算上下文中运行 R 代码和以下两个语句之一为 true，你可能会看到如下错误：
* 您在通过使用安装向导的情况下将在客户端计算机上安装 R Server （独立） [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。
* 通过安装 Microsoft R Server[单独的 Windows installer](https://docs.microsoft.com/r-server/install/r-server-install-windows)。

>*计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

你可以使用_绑定_中 Microsoft R Server 9.0 和更高版本升级 SQL Server 2016 实例中的 R 组件。 若要确定是否支持升级为可用，有关你的 R 服务版本，请参阅[使用 SqlBindR.exe R Services 的实例升级](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

当你安装累积更新，或在未连接到 internet 的计算机上安装 SQL Server 2016 service pack 时，安装向导可能无法显示提示，你可以通过使用下载的 CAB 文件中更新的 R 组件。 与数据库引擎一起安装多个组件时，通常会发生此失败。

一种解决方法，你可以通过使用命令行和指定安装服务版本*/MRCACHEDIRECTORY*参数在此示例中，它会安装 CU1 更新所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取的最新的安装程序，请参阅[安装没有 internet 访问权限的机器学习组件](r/installing-ml-components-without-internet-access.md)。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>快速启动板服务启动失败，则如果版本与不同的 R 版本

如果从数据库引擎，单独安装 SQL Server R Services 和生成版本不同，你可能会看到系统事件日志中的以下错误：

>_SQL Server 快速启动板服务启动因以下错误而失败： 服务未响应及时启动或控制请求。_

例如，此错误可能会发生如果使用的版本安装数据库引擎、 应用修补程序来升级数据库引擎，和使用的版本，然后将添加 R Services 功能。

若要避免此问题，请确保所有组件的版本号都相同。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

若要查看的所需的每个版本的 SQL Server 2016 的 R 版本数字列表，请参阅[没有 internet 访问权限的安装 R 组件](r/installing-ml-components-without-internet-access.md)。

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>由在 Azure 虚拟机运行的 SQL Server 实例中在防火墙阻止远程计算上下文

如果你已安装[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]在 Windows Azure 虚拟机，你可能无法使用需要虚拟机的工作区中使用的计算上下文。 原因是在默认情况下，Azure 虚拟机上的防火墙包含阻止网络本地 R 用户帐户访问的规则。

解决方法是，在 Azure VM 上，打开**高级安全 Windows 防火墙**，选择**出站规则**，并禁用以下规则：**阻止 R 中的本地用户帐户的网络访问权限SQL Server 实例 MSSQLSERVER**。 此外可以将启用，该规则保留，但更改到的安全属性**允许安全情况**。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 中的隐式身份验证

当运行 R 作业从远程数据科学工作站使用集成 Windows 身份验证时，SQL Server 使用*默示身份验证*生成的脚本可能需要任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。

若要解决此问题，建议升级到更高的 Service Release。

如果无法升级，可以使用 SQL 登录名运行可能需要嵌入式 ODBC 调用的远程 R 作业。

**适用于：** SQL Server 2016 R Services 速成版

### <a name="performance-limits-when-r-libraries-are-called-from-other-r-tools"></a>从其他 R 工具调用 R 库时的性能限制

很可能要调用的 R 工具和从 RGui 之类的外部 R 应用程序中为 SQL Server 安装的库。 安装新包时或在很短的代码示例运行即席测试时，此调用可能很方便。

但是，请注意外部 SQL Server，性能可能会受到限制。 例如，即使你购买 SQL Server 的企业版，R 在单线程模式下运行时通过使用外部工具运行 R 代码。 性能应该可以通过启动 SQL Server 连接并使用运行 R 代码的情况下更好[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，从而为您调用 R 库。

* 请避免调用从外部 R 工具使用由 SQL Server 的 R 库。
* 如果需要 SQL Server 计算机上运行大量的 R 代码，而不使用 SQL Server 安装 R，如 Microsoft R 客户端的单独实例，然后确保你的 R 开发工具将指向新的库。

有关详细信息，请参阅 [创建独立的 R Server](r/create-a-standalone-r-server.md)。

### <a name="the-r-script-is-throttled-due-to-resource-governance-default-values"></a>R 脚本限制由于资源调控默认值

在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些早期的发布版本，无法分配给 R 进程的最大内存为 20%。 因此，如果在服务器有 32 GB RAM，R 可执行文件 （RTerm.exe 和 BxlServer.exe） 可以使用单个请求中的最大 6.4 GB。

如果你遇到资源限制，请检查当前的默认值。 如果 20%是不够的请参阅的文档[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]如何更改此值。

**适用于：** SQL Server 2016 R Services，Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>R 代码执行和包或函数的问题

本部分包含特定于 SQL Server 上运行 R 的已知的问题，以及一些与 R 库和工具是 Microsoft，包括 RevoScaleR 发布的相关的问题。

有关可能会影响 R 解决方案的更多已知问题，请转到[Microsoft R Server 站点](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)。

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作业的处理器关联限制

在 SQL Server 2016 的初始版本生成、 你可以设置处理器关联，仅为第一个 k 组中的 Cpu。 例如，如果服务器是具有两个 k 组的 2 套接字机，从第一个 k 组的唯一处理器用于 R 进程。 配置资源调控的 R 脚本作业时，将应用相同的限制。

此问题已在 SQL Server 2016 Service Pack 1 中解决。 我们建议你升级到最新的服务版本。

**适用于：** SQL Server 2016 R Services RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>在 SQL Server 计算环境中读取数据时，无法更改列类型

如果计算环境设置为 SQL Server 实例，则无法在 R 代码中使用 _colClasses_ 参数（或其他类似参数）来更改列的数据类型。

例如，如果列 CRSDepTimeStr 尚不是整数，则以下语句将导致错误：

```r
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
```

一种解决方法，您可以重新编写 SQL 查询使用强制转换或转换，然后将数据提交给 R 中，通过使用正确的数据类型。 一般情况下，性能是更好地处理时数据通过使用 SQL 中，而不是通过更改在 R 代码中的数据。

**适用于：** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>避免当执行中的 R 代码时，清除工作区[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文

如果你使用 R 命令中运行 R 代码时清除你的对象的工作区[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算上下文，或如果清除工作区作为 R 脚本的一部分调用通过使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，您可能会得到错误： 

>*工作区 revoScriptConnection 找不到对象*

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

一种解决方法，避免不加选择地清除的变量和其他对象时你正在中运行 R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 尽管在 R 控制台中工作时，清除工作区中均相同，但它可以有意想不到的后果。

* 若要删除特定变量，使用 R*删除*函数： `remove('name1', 'name2', ...)`。
* 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作为输入提供给 R 脚本的数据的限制

你无法在 R 脚本中使用以下类型的查询结果：

- 引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
- 引用屏蔽列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>自变量*varsToKeep*和*varsToDrop*不支持 SQL Server 数据源

当你使用 rxDataStep 函数将结果写入到一个表时，使用*varsToKeep*和*varsToDrop*是指定要包括或排除操作的一部分的列的便捷方式。 但是，这些自变量不支持为 SQL Server 数据源。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>中的 SQL 数据类型的有限的支持`sp_execute_external_script`

SQL 中支持的数据类型并非全都可在 R 中使用。解决方法之一是考虑在将数据传递给 sp_execute_external_script 之前，将不受支持的数据类型强制转换为受支持的数据类型。

有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>可能的字符串损坏

中的字符串数据的任何往返行程[!INCLUDE[tsql](../includes/tsql-md.md)]到 R，然后执行到[!INCLUDE[tsql](../includes/tsql-md.md)]试可能会导致损坏。 这是因为在 R 和使用的编码不同[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以及各种排序规则和在 R 中支持的语言和[!INCLUDE[tsql](../includes/tsql-md.md)]。 采用非 ASCII 编码的任何字符串可能不会得到正确处理。

当你将字符串数据发送到 R 时，将其转换为 ASCII 表示形式，如有可能。

此限制适用于以及 SQL Server 和 Python 之间传递数据。 多字节字符应传递为 utf-8，并存储为 Unicode。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一个值类型的`raw`可以从返回`sp_execute_external_script`

当二进制数据类型 (R**原始**数据类型) 从返回 R，必须在输出数据框架中发送的值。

使用数据类型以外**原始**，只需通过添加 OUTPUT 关键字，可以返回以及存储过程的结果的参数值。 有关详细信息，请参阅[使用输出参数返回数据](https://technet.microsoft.com/library/ms187004.aspx)。

如果你想要使用包含值的类型值的多个输出集**原始**，其中一个可能的解决方法是以执行多个调用存储过程中，或将结果集发回到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 ODBC。

### <a name="loss-of-precision"></a>精度损失

因为[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支持不同的数据类型，数值数据类型可能会降低精度的转换的过程。

有关隐式数据类型转换的详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>变量范围错误，当你使用 transformFunc 参数时：*分析样本数据集具有任何变量*

若要将数据转换时对进行建模，你可以传递*transformFunc*如函数中的参数`rxLinmod`或`rxLogit`。 但是，嵌套的函数调用可能导致出现范围错误在 SQL Server 计算上下文中，即使在调用在本地计算上下文中正常工作。

例如，假定你已经定义了两个函数，`f`和`g`，在你本地全局环境中，和`g`调用`f`。 在包含 `g`的分布式或远程调用中，对 `g` 的调用可能会失败，因为找不到 `f` ，即使你已同时将 `f` 和 `g` 传递给远程调用。

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

如果你使用 R 控制台（例如，在 rgui.exe 或 rterm.exe 中），可以通过键入以下命令，将 max-ppsize 的值设置为 500000：

```r
R --max-ppsize=500000
```

如果你使用[!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)]环境中，你可以设置`max-ppsize`标志通过对 RevoIDE 可执行文件的以下调用：

```
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函数的问题

`rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是，数字数据自动装箱。

有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本部分列出了特定于 R 连接、 开发和由 Revolution Analytics 提供的性能工具的问题。 这些工具的较早的预发行版本中未提供[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。

通常情况下，我们建议你卸载这些早期版本和安装最新版本的 SQL Server 或 Microsoft R Server。

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>运行的并行版本的 Revolution R Enterprise

安装的任何版本的 Revolution R Enterprise 并排[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]不支持。

如果你有其他版本的 Revolution R Enterprise 的许可证，你不能将该版本安装在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例所在的同一台计算机上，也不能安装在用于连接 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的任何工作站上。

### <a name="the-use-of-an-r-productivity-environment-is-not-supported"></a>不支持 R 工作效率环境的使用

某些预发行版本的[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]的窗口，由 Revolution Analytics 中包含的 R 开发环境。 不再提供此工具，但不支持。

为了与兼容[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我们强烈建议而不是 Revolution Analytics 工具安装 Microsoft R 客户端或 Microsoft R Server。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)和[Visual Studio Code](https://code.visualstudio.com/)还支持 Microsoft R 解决方案。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题

修订 0.92 SQLite ODBC 驱动程序是与 RevoScaleR 不兼容。 修订 0.88 0.91 和 0.93 和更高版本都已知为兼容。

## <a name="python-code-execution-or-python-package-issues"></a>Python 代码执行，或者 Python 包问题

本部分包含特定于 SQL Server，以及与 Microsoft，发布的 Python 包相关的问题上运行 Python 的已知的问题包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).


## <a name="see-also"></a>另请参阅

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server 中的故障排除机器学习](machine-learning-troubleshooting-faq.md)

