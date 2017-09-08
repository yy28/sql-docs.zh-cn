---
title: "机器学习服务的已知问题 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>机器学习服务的已知的问题

本主题描述了已知的问题或限制机器学习作为 SQL Server 2016 和 SQL Server 自 2017 年中的一个选项提供的组件。

除非明确指定，则适用于所有以下：

+ SQL Server 2016

  - R Services (数据库中)
  - Microsoft R Server（独立版）

+ SQL Server 2017

  - 机器学习 （数据库） 的服务
  - 机器学习 Python （数据库） 的服务
  - 机器学习服务器（独立）

## <a name="setup-and-configuration-issues"></a>安装和配置问题

这里列出了处理和常见初始设置和配置相关的问题的说明：[升级和安装常见问题](r/upgrade-and-installation-faq-sql-server-r-services.md)。

另请参阅此文章，以升级、 通过并行安装和安装新的 R 或 Python 组件相关信息。

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>无法安装中处于脱机状态的 Python 组件安装的 SQL Server 自 2017 年

如果在没有 Internet 访问的计算机上安装 SQL Server 自 2017 年，安装程序可能无法显示页面，提示输入下载的 Python 组件; 的位置因此，你将能够机器学习服务功能，但不是 Python 组件安装。

将在即将发布的版本中修复此问题。 一种解决方法，可以临时启用的安装程序的持续时间的 Internet 访问。 此限制不适用于。

**适用于：**使用 Python 的 SQL Server 自 2017 年 1

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安装最新的 Service Release，以确保与 Microsoft R Client 兼容

如果你安装 Microsoft R 客户端的最新版本，并使用它在上运行 R 使用远程 SQL Server 计算上下文，你可能会如下所示的错误：

*你与 Microsoft R Server 版本 8.x.x 不兼容的计算机上运行 Microsoft R 客户端版本的 9.x.x。请下载并安装兼容版本。

SQL Server 2016 需要客户端上的 R 库与服务器上的 R 库完全匹配。 限制已被取消的晚于 R Server 9.0.1 释放。 但是，如果你遇到此错误，验证 R 库的版本由你的客户端和服务器，如有必要，nad 更新客户端与服务器版本匹配。

每次安装的 SQL Server 服务发行版时，被更新的版本与 SQL Server R Services 安装的 R。 因此，若要确保你始终具有最新版本的 R 组件，应安装所有 service pack。

为了与 Microsoft R Client 9.0.0 兼容，必须安装本 [支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。

若要避免与 R 包的问题，还可以升级安装在服务器上，通过更改为的现代生命周期策略中所述的 R 库版本[本节](#bkmk_sqlbindr)。 执行此操作时，将 R 与 SQL Server 安装的版本更新的 Microsoft R Server，确保服务器和客户端可以始终获得最新版本的 Microsoft。 发布更新在同一个计划

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="bkmk_sqlbindr"></a>从使用的客户端连接到旧版本的 SQL Server R Services 时不兼容版本的警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

如果使用 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安装向导或新的 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)独立安装程序在客户端计算机上安装 Microsoft R Server，并且在使用 SQL Server R Services 早期版本的计算环境中运行 R 代码，则可能看到如下错误：

*计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

Microsoft R Server 9.0 版本中提供 **SqlBindR.exe** 工具，以支持将 SQL Server 实例升级到兼容的 9.0 版本。 在即将发布的 Service Release 中，会在 SQL Server 中增加一项支持，允许将 R Services 实例升级到 9.0。 适用于将来的升级的版本包括 SQL Server 2016 RTM CU3 + 和 SP1 + 中，以及 SQL Server 自 2017 年 1 CTP 1.1。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

在未连接到 Internet 的计算机上安装累积更新或安装 SQL Server 2016 的 Service Pack 时，安装向导可能无法显示使用下载的 CAB 文件更新 R 组件的提示。 将多个组件与数据库引擎一起安装时，通常会发生这种情况。

一种解决方法，你可以通过使用命令行和指定安装服务版本*/MRCACHEDIRECTORY*参数在此示例中，它会安装 CU1 更新所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取的最新的安装程序，请参阅[安装机器学习 Components without Internet Access](r/installing-ml-components-without-internet-access.md)。

**适用于：** SQL Server 2016 R Services，与 R Server 9.0.0 版或更早版本

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>当版本与 R 版本不同时，Launchpad 服务无法启动

如果从数据库引擎，单独安装 R Services 和生成版本不同，可能会看到系统事件日志中的出现此错误： _SQL Server 快速启动板服务启动因以下错误而失败： 服务未响应中及时的启动或控制请求。_

例如，如果使用发行版本安装数据库引擎，应用修补程序升级数据库引擎，然后使用发行版本添加 R Services，则可能出现此错误。

若要避免此问题，请确保所有组件的版本号都相同。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

若要查看每个版本的 SQL Server 2016 所需的 R 版本号列表，请参阅 [在没有 Internet 连接的情况下安装 R 组件](r/installing-ml-components-without-internet-access.md)。

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>远程计算上下文被 Azure 虚拟机上运行的 SQL Server 实例中的防火墙阻止

如果已经在 Windows Azure 虚拟机上安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ，你可能无法使用需使用虚拟机工作区的计算上下文。 原因是在默认情况下，Azure VM 防火墙包含一项规则，该规则阻止本地 R 用户帐户的网络访问。

解决方法之一是在 Azure VM 上打开“高级安全 Windows 防火墙” ，选择“出站规则” ，并禁用以下规则：“阻止 SQL Server 实例 MSSQLSERVER 中的 R 本地用户帐户进行网络访问”。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 中的隐式身份验证

使用 Windows 集成身份验证从远程数据科学工作站运行 R 作业时，SQL Server 将使用隐式身份验证  生成脚本可能需要的任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。

若要解决此问题，建议升级到更高的 Service Release。

如果无法升级，可以使用 SQL 登录名运行可能需要嵌入式 ODBC 调用的远程 R 作业。

**适用于：** SQL Server 2016 R Services 速成版

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>性能限制时从独立 R 工具调用 R 库

很可能要调用的 R 工具和从 RGui 之类的外部 R 应用程序中为 SQL Server R Services 安装的库。 安装新包时，或在很短的代码示例中运行即席测试时，这可能是很方便。

但是，请注意外部 SQL Server，性能将受到限制。 例如，即使你购买 SQL Server 的企业版，R 将运行在单线程模式下运行 R 代码使用外部工具。 将 R 代码运行时启动 SQL Server 连接和使用高级性能[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，这将为您调用 R 库。

+ 避免从外部 R 工具调用 SQL Server 使用的 R 库。
+ 如果需要 SQL Server 计算机上运行大量的 R 代码，而不使用 SQL server 安装 Microsoft R 客户端，如 R 的单独实例，然后确保你的 R 开发工具将指向新的库。

有关详细信息，请参阅 [创建独立的 R Server](r/create-a-standalone-r-server.md)。

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>由于资源调控默认值限制的 R 脚本

在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些早期发行版本中，无法分配给 R 进程的最大内存为 20%。 因此，如果服务器有 32 GB 的 RAM，则 R 可执行文件 (RTerm.exe and BxlServer.exe) 可在单个请求中使用最大 6.4 GB。

如果遇到资源限制，请检查当前默认值，如果 20% 不够的话，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的文档，了解如何更改此值。

**适用于：** SQL Server 2016 R Services，Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>执行 R 代码和包或函数问题

本部分包含特定于 SQL Server 上运行 R 的已知的问题以及 R 库和工具是 Microsoft，包括 RevoScaleR 发布的相关的一些问题。

有关更多的已知的问题可能会影响 R 解决方案，请参阅 Microsoft R Server 站点：[与 Microsoft R Server 的已知问题](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作业的处理器关联限制

在 SQL Server 2016 的初始版本生成、 你可以设置处理器关联，仅为第一个 k 组中的 Cpu。 例如，如果服务器是包含两个 k 组的双套接字计算机，则仅将第一个 k 组中的处理器用于 R 进程。 配置 R 脚本作业的资源调控时，将应用相同的限制。

此问题已在 SQL Server 2016 Service Pack 1 中解决。

**适用于：** SQL Server 2016 R Services RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>在 SQL Server 计算环境中读取数据时，无法更改列类型

如果计算环境设置为 SQL Server 实例，则无法在 R 代码中使用 _colClasses_ 参数（或其他类似参数）来更改列的数据类型。

例如，如果列 CRSDepTimeStr 尚不是整数，则以下语句将导致错误：

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

更高版本将会解决此问题。

解决方法之一是将 SQL 查询重新编写为使用 CAST 或 CONVERT，并使用正确的数据类型将数据呈现给 R。 一般情况下，与在 R 代码中更改数据相比，使用 SQL 处理数据可以获得更好的性能。

**适用于：** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 计算环境中执行 R 代码时，请避免清除工作区

如果在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 计算环境中运行 R 代码时使用 R 命令清除对象的工作区，或者如果在使用 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)调用 R 脚本的过程中清除工作区，则可能收到如下错误：找不到工作区对象“revoScriptConnection” 

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

解决方法之一是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中运行 R 时，避免随意清除变量和其他对象。 尽管在 R 控制台中工作时清除工作区很常见，但却可能产生意外的后果。

+ 若要删除特定的变量，请使用 R remove  函数： `remove('name1', 'name2', ...)`
+ 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作为输入提供给 R 脚本的数据的限制

你无法在 R 脚本中使用以下类型的查询结果：

- 引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
- 引用屏蔽列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询中的数据。
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>自变量*varsToKeep*和*varsToDrop* SQL Server 数据源不支持

当你使用 rxDataStep 函数将结果写入到一个表时，使用*varsToKeep*和*varsToDrop*是指定要包括或排除操作的一部分的列的便捷方式。 目前，这些自变量不支持为 SQL Server 数据源。

在更高版本的版本中，将取消此限制。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>中的 SQL 数据类型的有限的支持`sp_execute_external_script`

SQL 中支持的数据类型并非全都可在 R 中使用。解决方法之一是考虑在将数据传递给 sp_execute_external_script 之前，将不受支持的数据类型强制转换为受支持的数据类型。

有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>可能的字符串损坏

将字符串数据从 [!INCLUDE[tsql](../includes/tsql-md.md)] 转换为 R，然后再转换回到 [!INCLUDE[tsql](../includes/tsql-md.md)] 可能会导致损坏。 这是因为 R 与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中使用的编码不同，并且 R 与 [!INCLUDE[tsql](../includes/tsql-md.md)]支持的排序规则和语言不同。 采用非 ASCII 编码的任何字符串可能不会得到正确处理。

在将字符串数据发送到 R 时，请尽量将其转换为 ASCII 表示形式。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一个值类型的`raw`可以从返回`sp_execute_external_script`

从 R 返回二进制数据类型（R **raw** 数据类型）时，值必须是输出数据框架中的值。

后续版本中将会添加对多个 **raw** 输出的支持。

如果需要多个输出集，一个可能的解决方法是多次调用存储过程，然后使用 ODBC 将结果集发回到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。

请注意，只需添加 OUTPUT 关键字，便可将参数值与存储过程的结果一起返回。 有关详细信息，请参阅 [使用 OUTPUT 参数返回数据](https://technet.microsoft.com/library/ms187004.aspx)。

### <a name="loss-of-precision"></a>精度损失

[!INCLUDE[tsql](../includes/tsql-md.md)] 和 R 支持不同的数据类型，因此，在转换期间，数字数据类型的精度可能会降低。

有关隐式数据类型转换的详细信息，请参阅 [Working with R Data Types](r/r-libraries-and-data-types.md)。

### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>使用 transformFunc 参数时出现变量范围错误“用于分析的示例数据集没有变量”

在建模时，你可以在函数（例如 *rxLinmod* 或 `rxLinmod` ）中传递 `rxLogit` to transf）中传递m the data while modelling. 但是，嵌套的函数调用可能会导致 SQL Server 计算上下文中出现范围错误，即使调用能够在本地计算上下文中正常工作。

例如，假设你在本地全局环境中定义了 `f` 和 `g` 这两个函数，其中 `g` 调用 `f`。 在包含 `g`的分布式或远程调用中，对 `g` 的调用可能会失败，因为找不到 `f` ，即使你已同时将 `f` 和 `g` 传递给远程调用。

如果遇到此问题，你可以通过在 `f` 的定义中（ `g`可正常调用 `g` 的任何位置）嵌入 `f`的定义来解决该问题。

例如：

```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  


若要避免错误，重写，如下所示：

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>使用 RevoScaleR 导入和操作数据

从数据库读取 **varchar** 列时，将会截掉空格。 为了避免这种情况，请将字符串包含在非空格字符中。

使用 `rxDataStep` 等函数创建包含 **varchar** 列的数据库表时，将会根据数据样本估算列宽。 如果宽度可能会变化，则可能需要将所有字符串填补到公共长度。

使用 `rxImport` 或 `rxTextToXdf` 的重复调用来导入和追加行，并将多个输入文件合并为单个.xdf 文件时，不支持使用转换来更改变量的数据类型。

### <a name="limited-support-for-rxexec"></a>对 rxExec 的支持有限

SQL Server 2016 中`rxExec`可以仅在单线程模式下使用 RevoScaleR 包所提供的函数。

将来的版本会增加跨多个进程的 `rxExec` 并行度。

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>增加最大参数大小以支持 rxGetVarInfo

如果你使用变量数极多（例如，超过 40,000 个）的数据集，需在启动 R 时设置 `max-ppsize` 标志才能使用 `rxGetVarInfo`等函数。  `max-ppsize` 标志指定指针保护堆栈的最大大小。

如果你使用 R 控制台（例如，在 rgui.exe 或 rterm.exe 中），可以通过键入以下命令，将 max-ppsize 的值设置为 500000：

```  
R --max-ppsize=500000  
```  
  
如果你使用 [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] 环境，可以通过对 RevoIDE 可执行文件执行以下调用来设置 `max-ppsize` 标志：

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函数的问题

`rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是，数字数据将自动装箱。

有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本部分列出 Revolution Analytics 提供的 R 连接、开发和性能工具特定的问题。 在  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的早期预发布版本中提供了这些工具。 

通常情况下，我们建议你卸载这些早期版本和安装最新版本的 SQL Server 或 Microsoft R Server。

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>同时运行 Revolution R Enterprise 的多个版本

不支持并行安装 Revolution R Enterprise 与任何版本的 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 。

如果你有其他版本的 Revolution R Enterprise 的许可证，你不能将该版本安装在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例所在的同一台计算机上，也不能安装在用于连接 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的任何工作站上。

### <a name="use-of-r-productivity-environment-not-supported"></a>不支持的 R Productivity Environment 的使用

[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 的一些预发行版本包含 Revolution Analytics 创建的适用于 Windows 的 R 开发环境。 此工具不会再提供，不支持。

为了与兼容[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我们强烈建议而不是 Revolution Analytics 工具安装 Microsoft R 客户端或 Microsoft R Server。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 是支持 Microsoft R 解决方案的另一个建议客户端。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题

SQLite ODBC 驱动程序修订版 0.92 与 RevoScaleR 不兼容；修订版 0.88-0.91 和 0.93 及更高版本已知兼容。

## <a name="see-also"></a>另请参阅

[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)


