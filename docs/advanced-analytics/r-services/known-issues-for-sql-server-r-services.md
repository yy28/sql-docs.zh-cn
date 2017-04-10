---
title: "SQL Server R Services 的已知问题 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 52
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 49
---
# SQL Server R Services 的已知问题
  本主题介绍 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 及其相关组件的限制与问题。  
  
> [!NOTE]
> 此处列出了与初始安装和配置相关的其他问题：[升级和安装常见问题解答](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。  
  
## <a name="r-services-in-database"></a>R Services (数据库中)  
 本部分列出支持 R 集成的数据库引擎功能的特定问题。  

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安装最新的 Service Release，以确保与 Microsoft R Client 兼容

如果安装最新版本的 Microsoft R Client，并使用它在远程计算机环境中的 SQL Server 上运行 R，则可能收到以下错误：

计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

通常情况下，随 SQL Server R Services 一起安装的 R 版本会在发布 Service Release 后进行更新。 若要确保始终拥有最新版本的 R 组件，请安装所有 Service Pack。 为了与 Microsoft R Client 9.0.0 兼容，必须安装本[支持文章](https://support.microsoft.com/kb/3210262)中介绍的更新。 
  
### <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>进行无人参与的安装需要使用 R 组件的新许可协议  
 如果使用命令行来安装装有 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的 SQL Server 实例，则必须编辑命令行以使用新的许可协议参数 */IACCEPTROPENLICENSEAGREEMENT*。 不使用正确的参数可能会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装失败。  
  
### <a name="warning-of-incompatible-version-when-connecting-to-older-version-of-sql-server--r-services-from-a-client-using-includesssqlv14mdtokensqlv14sssqlv14mdmd"></a>从使用 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 的客户端连接到旧版 SQL Server R Services 时，出现版本不兼容的警告 

如果使用 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 安装向导或新的 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) 独立安装程序在客户端计算机上安装 Microsoft R Server，并且在使用 SQL Server R Services 早期版本的计算环境中运行 R 代码，则可能看到如下错误：

计算机上运行的 Microsoft R Client 版本为 9.0.0，与 8.0.3 版的 Microsoft R Server 不兼容。请下载并安装兼容版本。

Microsoft R Server 9.0 版本中提供 **SqlBindR.exe** 工具，以支持将 SQL Server 实例升级到兼容的 9.0 版本。 在即将发布的 Service Release 中，会在 SQL Server 中增加一项支持，允许将 R Services 实例升级到 9.0。 将来升级的候选版本包括 SQL Server 2016 RTM CU3+ 和 SP1+，以及 SQL Server vNext CTP 1.1。 

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>安装了 SQL Server 2016 Service Release 可能无法安装较新版本的 R 组件

在未连接到 Internet 的计算机上安装累积更新或安装 SQL Server 2016 的 Service Pack 时，安装向导可能无法显示使用下载的 CAB 文件更新 R 组件的提示。 将多个组件与数据库引擎一起安装时，通常会发生这种情况。
 
解决方法之一是通过使用命令行并为 CU1 指定 /MRCACHEDIRECTORY 参数（如本示例所示）来安装 Service Release： 

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要获取最新的 CAB 文件，请参阅[在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。

### <a name="windows-group-created-for-launchpad-must-have-an-account-in-the-sql-server-instance"></a>为 LaunchPad 创建的 Windows 组必须在 SQL Server 实例中有一个帐户
 安装 SQL Server R Services 时，将创建一个默认名为 **SQLRUsers** 的 Windows 用户组，由受信任的 Launchpad 用于运行 R 作业。 如果需要从使用 Windows 集成身份验证的远程客户端运行 R 作业，则必须授予此 Windows 用户组权限，以登录启用了 R 的 SQL Server 实例。

在 **SQLRUsers** 组没有此权限的环境中，可能会看到以下错误：  
  
-   尝试运行 R 脚本时：  
  
     无法启动“R”脚本的运行时。请检查“R”运行时的配置。  
  
     发生外部脚本错误。无法启动运行时。  
  
-   [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务生成的错误：  
  
     无法初始化启动器 RLauncher.dll  
  
     未注册任何启动器 dll！  
  
-   安全日志指示帐户 NT SERVICE\MSSQLLAUNCHPAD 无法登录。  
 
> [!NOTE]
> 如果使用共享内存在 SQL Server Management Studio 中运行 R 作业，则可能不会遇到此限制，直到 R 作业使用嵌入的 ODBC 调用。 
> 
> 如果从远程工作站使用 SQL 登录名，则不需要此解决方法。

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>当版本与 R 版本不同时，Launchpad 服务无法启动
如果从数据库引擎单独安装 R Services，并且版本不同，则可能会在系统事件日志中看到如下错误：SQL Server Launchpad 服务因以下错误而无法启动：服务未及时响应开始或控制请求。

例如，如果使用发行版本安装数据库引擎，应用修补程序升级数据库引擎，然后使用发行版本添加 R Services，则可能出现此错误。

若要避免此问题，请确保所有组件的版本号都相同。 如果升级一个组件，请务必向其他所有已安装的组件应用相同的升级。

若要查看每个版本的 SQL Server 2016 所需的 R 版本号列表，请参阅[在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。


### <a name="service-account-for-launchpad-requires-permission-replace-process-level-token"></a>LaunchPad 的服务帐户需要“替换进程级令牌”权限
 安装 SQL Server R Services 时，将使用帐户 NT Service\MSSQLLaunchpad 启动受信任的 Launchpad，默认情况下，该帐户设置有必要的权限。 但是，如果使用其他帐户或者更改与此帐户关联的权限，则可能无法启动 Launchpad。
 
 若要确保 Launchpad 服务帐户可以登录，请向该帐户授予权限：`Replace Process Level Token`。 有关详细信息，请参阅 [Replace a process level token](https://technet.microsoft.com/itpro/windows/keep-secure/replace-a-process-level-token)（替换进程级令牌）。

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>远程计算上下文被 Azure 虚拟机上运行的 SQL Server 实例中的防火墙阻止  
 如果已经在 Windows Azure 虚拟机上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，你可能无法使用需使用虚拟机工作区的计算上下文。 原因是在默认情况下，Azure VM 防火墙包含一项规则，该规则阻止本地 R 用户帐户的网络访问。  
  
 解决方法之一是在 Azure VM 上打开“高级安全 Windows 防火墙”，选择“出站规则”，并禁用以下规则：“阻止 SQL Server 实例 MSSQLSERVER 中的 R 本地用户帐户进行网络访问”。  
  
### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 中的隐式身份验证
使用 Windows 集成身份验证从远程数据科学工作站运行 R 作业时，SQL Server 将使用隐式身份验证生成脚本可能需要的任何本地 ODBC 调用。 但是，此功能在 RTM 版 SQL Server Express Edition 中不起作用。 

若要解决此问题，建议升级到更高的 Service Release。

如果无法升级，可以使用 SQL 登录名运行可能需要嵌入式 ODBC 调用的远程 R 作业。 

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作业的处理器关联限制 
 
在 RTM 版 SQL Server 2016 中，可以仅对第一个 k 组中的 CPU 设置处理器关联。 例如，如果服务器是包含两个 k 组的双套接字计算机，则仅将第一个 k 组中的处理器用于 R 进程。 配置 R 脚本作业的资源调控时，将应用相同的限制。

此问题已在 SQL Server 2016 Service Pack 1 中解决。

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
  
### <a name="resource-governance-default-values"></a>资源调控默认值  
在 Enterprise Edition 中，可以使用资源池管理外部脚本进程。 在某些版本中，可以分配给 R 进程的最大内存为 20%。 因此，如果服务器有 32 GB 的 RAM，则 R 可执行文件 (RTerm.exe and BxlServer.exe) 可在单个请求中使用最大 6.4 GB。 

如果遇到资源限制，请检查当前默认值，如果 20% 不够的话，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的文档，了解如何更改此值。  

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversiontokenssnoversionmdmd-compute-context"></a>在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算环境中执行 R 代码时，请避免清除工作区  
 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算环境中运行 R 代码时使用 R 命令清除对象的工作区，或者如果在使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 调用 R 脚本的过程中清除工作区，则可能收到如下错误：找不到工作区对象“revoScriptConnection”

`revoScriptConnection` 是 R 工作区中的对象，它包含有关从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用的 R 会话的信息。 但是，如果 R 代码包含清除工作区的命令（例如 `rm(list=ls()))`，则将同时清除有关会话以及 R 工作区中其他对象的所有信息。

解决方法之一是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行 R 时，避免随意清除变量和其他对象。 尽管在 R 控制台中工作时清除工作区很常见，但却可能产生意外的后果。 

+ 若要删除特定的变量，请使用 R remove函数：`remove('name1', 'name2', ...)` 
+ 若要删除多个变量，请将临时变量的名称保存到列表中，然后执行定期的垃圾回收。 
   
### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作为输入提供给 R 脚本的数据的限制  
 你无法在 R 脚本中使用以下类型的查询结果：  
  
-   引用 AlwaysEncrypted 列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询中的数据。  
  
-   引用屏蔽列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询中的数据。  
  
     如果你需要在 R 脚本中使用屏蔽数据，一种可能的解决方法是在临时表中创建该数据的副本，然后改为使用该数据。  
   
  
## <a name="microsoft-r-server-standalone"></a>Microsoft R Server（独立版）  
 本部分列出了 Microsoft R Server 独立版特定的问题。 
  
### <a name="multiple-r-libraries-and-executables-are-installed-if-you-install-both-standalone-and-in-database"></a>如果同时安装独立版和数据库内 Microsoft R Server，则会安装多个 R 库和可执行文件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序包含用于安装 Microsoft R Server（独立版）的选项。 可在 Enterprise Edition 中使用 Microsoft R Server（独立版）选项，以安装支持 R 但不需要与 SQL Server 进行交互的独立 Windows Server。    

> [!TIP] **不**需要此独立选项，便可以将 R 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 一起使用。
> 
> 如果需要安装可以连接到 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 或 Microsoft R Server（独立版）的数据科学客户端计算机，建议安装 [Microsoft R Client](http://go.microsoft.com/fwlink/?LinkId=799768)。  

请注意，如果在同一台计算机上同时安装了 R Services（数据库内）和 Microsoft R Server（独立版），则将针对启用了 R 的每个 SQL Server 实例以及 Microsoft R Server（独立版）创建单独的 R 实例。  例如，如果已安装默认实例、命名实例和 R Server（独立版），则同一台计算机上可能包含三个 R 实例：  
  
-   **独立版：**C:\Program Files\Microsoft SQL Server\130\R_SERVER  
  
-   **默认实例：**C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES  
  
-   **命名实例：**C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES  
  
> [!NOTE] 
> 
> 请只在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 环境中使用与数据库实例相关联的 R 库和工具。 如果需要使用其他 R 工具运行 R，请务必引用 R Server（独立版）引用的 R 库，后者默认安装在 C:\Program Files\Microsoft SQL Server\130\R_SERVER 位置。  

### <a name="performance-limits-when-r-services-libraries-are-called-from-standalone-r-tools"></a>从独立的 R 工具调用 R Services 库时的性能限制

SQL Server R Services 使用的 R 库默认安装在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES 位置。 可能从外部 R 应用程序（如 RGui）调用针对 SQL Server R Services 安装的 R 工具和库。 

但是，如果这样做，则性能将受到限制。 例如，即使已购买 Enterprise Edition 版 SQL Server，但如果使用外部工具运行 R 代码，则 R 将以单线程模式运行。 如果通过启动 SQL Server 连接并使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 来运行 R 代码（这将调用 R Services 库），则性能将更佳。

+ 避免从外部 R 工具调用 SQL Server 使用的 R 库。 
+ 如果需要使用外部工具在 SQL Server 计算机上运行 R，应安装一个单独的 R 实例，然后确保 R 工具指向新的库。 
+ 如果使用 Enterprise Edition，则建议在 SQL Server 计算机上安装 Microsoft R Server（独立版）。 然后，从用于运行 R 代码的外部工具引用 R Server 的库，该库默认安装在 C:\Program Files\Microsoft SQL Server\<version number>\R_SERVER 位置。 

有关详细信息，请参阅[创建独立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  
  
  
## <a name="general-r-issues"></a>一般性 R 问题  

 本部分列出了 R 连接和性能工具特定的问题。  
  
### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>sp_execute_external_script 中 SQL 数据类型的有限支持  

 SQL 中支持的数据类型并非全都可在 R 中使用。解决方法之一是考虑在将数据传递给 sp_execute_external_script 之前，将不受支持的数据类型强制转换为受支持的数据类型。  
  
 有关详细信息，请参阅[使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)。  
  
### <a name="possible-string-corruption"></a>可能的字符串损坏  

 将字符串数据从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 转换为 R，然后再转换回到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可能会导致损坏。 这是因为 R 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用的编码不同，并且 R 与 [!INCLUDE[tsql](../../includes/tsql-md.md)]支持的排序规则和语言不同。 采用非 ASCII 编码的任何字符串可能不会得到正确处理。  
  
 在将字符串数据发送到 R 时，请尽量将其转换为 ASCII 表示形式。  
  
### <a name="only-one-raw-value-can-be-returned-from-spexecuteexternalscript"></a>只能从 sp_execute_external_script 返回一个原始值  

 从 R 返回二进制数据类型（R **raw** 数据类型）时，值必须是输出数据框架中的值。  
  
 后续版本中将会添加对多个 **raw** 输出的支持。  
  
 如果需要多个输出集，一个可能的解决方法是多次调用存储过程，然后使用 ODBC 将结果集发回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 请注意，只需添加 OUTPUT 关键字，便可将参数值与存储过程的结果一起返回。 有关详细信息，请参阅[使用 OUTPUT 参数返回数据](https://technet.microsoft.com/library/ms187004.aspx)。
  
### <a name="loss-of-precision"></a>精度损失  

 [!INCLUDE[tsql](../../includes/tsql-md.md)]和 R 支持不同的数据类型，因此，在转换期间，数字数据类型的精度可能会降低。  
  
 有关隐式数据类型转换的详细信息，请参阅 [Working with R Data Types](../../advanced-analytics/r-services/working-with-r-data-types.md)。  
  
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
  
 为了避免出错，请重新编写为：  
  
```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

  
## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open 
 
 本部分列出 Revolution Analytics 提供的 R 连接、开发和性能工具特定的问题。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的早期预发布版本中提供了这些工具。 

一般情况下，建议卸载这些早期版本并安装最新版本的 SQL Server R Services、Microsoft R Server 或 Microsoft R Client。
  
### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>同时运行 Revolution R Enterprise 的多个版本  

 不支持并行安装 Revolution R Enterprise 与任何版本的 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。  
  
 如果你有其他版本的 Revolution R Enterprise 的许可证，你不能将该版本安装在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所在的同一台计算机上，也不能安装在用于连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的任何工作站上。  
  
### <a name="limited-support-for-revoscaler-rxexec"></a>对 RevoScaleR rxExec 的支持有限  

 从 RC0 开始，只能在单线程模式下使用 `rxExec` 提供的 [!INCLUDE[rsql_rre-short](../../includes/rsql-rre-short-md.md)] 函数。  
  
 将来的版本会增加跨多个进程的 `rxExec` 并行度。  
  
### <a name="data-import-and-manipulation-using-revoscaler"></a>使用 RevoScaleR 导入和操作数据  

 从数据库读取 **varchar** 列时，将会截掉空格。 为了避免这种情况，请将字符串包含在非空格字符中。  
  
 使用 `rxDataStep` 等函数创建包含 **varchar** 列的数据库表时，将会根据数据样本估算列宽。 如果宽度可能会变化，则可能需要将所有字符串填补到公共长度。  
  
 使用 `rxImport` 或 `rxTextToXdf` 的重复调用来导入和追加行，并将多个输入文件合并为单个.xdf 文件时，不支持使用转换来更改变量的数据类型。  
  
### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>增加最大参数大小以支持 rxGetVarInfo  

 如果你使用变量数极多（例如，超过 40,000 个）的数据集，需在启动 R 时设置 `max-ppsize` 标志才能使用 `rxGetVarInfo`等函数。  `max-ppsize` 标志指定指针保护堆栈的最大大小。  
  
 如果你使用 R 控制台（例如，在 rgui.exe 或 rterm.exe 中），可以通过键入以下命令，将 max-ppsize 的值设置为 500000：  
  
```  
R --max-ppsize=500000  
```  
  
 如果你使用 [!INCLUDE[rsql_developr](../../includes/rsql-developr-md.md)] 环境，可以通过对 RevoIDE 可执行文件执行以下调用来设置 `max-ppsize` 标志：  
  
```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  
  
### <a name="issues-with-rxdtree-function"></a>rxDTree 函数的问题  

 `rxDTree` 函数目前不支持公式内转换。 具体而言，不支持使用 `F()` 语法即时创建系数。 但是，数字数据将自动装箱。  
  
 有序系数被视为与所有 RevoScaleR 分析函数（ `rxDTree`除外）中的系数相同。  
  
### <a name="using-the-r-productivity-environment"></a>使用 R Productivity Environment  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的一些预发行版本包含 Revolution Analytics 创建的适用于 Windows 的 R 开发环境。 

但是，若要与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 兼容，强烈建议安装 Microsoft R Client 或 Microsoft R Server，而非 Revolution Analytics 工具。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 是支持 Microsoft R 解决方案的另一个建议客户端。
  
### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驱动程序与 RevoScaleR 的兼容性问题  
 SQLite ODBC 驱动程序修订版 0.92 与 RevoScaleR 不兼容；修订版 0.88-0.91 和 0.93 及更高版本已知兼容。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 2016 中的新增功能](../../sql-server/what-s-new-in-sql-server-2016.md)
  