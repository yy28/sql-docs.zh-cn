---
title: "升级和安装常见问题解答 (SQL Server R Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7c543f1ff6fc3050dcd695d2c728b3707ca9d4d6
ms.lasthandoff: 04/11/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>升级和安装常见问题解答 (SQL Server R Services)
  本主题解答有关安装和升级的一些常见问题。 此外，还包含有关从 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 预览版进行升级的问题。
  
 如果你是第一次安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，请遵照相关过程安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 R 组件，操作步骤如下所述：[安装 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  

 
  本主题还包含有关安装和升级 R Server（独立版）的问题。 有关其他平台上的 Microsoft R Server 的问题，请参阅 [Microsoft R Server 发行说明](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)和[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 
     
## <a name="important-changes-from-pre-release-versions"></a>预发行版中的重要更改  
 如果安装了 SQL Server 2016 的任何预发行版，或者如果使用先于 SQL Server 2016 公开发行版发布的安装说明，则必须注意预发行版和 RTM 版本的安装过程完全不同。 这些更改包括 SQL Server 安装向导中提供的选项以及安装后的步骤。 
   
> [!WARNING]
> 不再支持重新安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的任何预发行版本。 建议尽快升级。  
+ 如果在 CTP3、CTP3.1、CTP3.2、RC0 或 RC1 中安装了 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ，则将需要重新运行配置后安装脚本，以便卸载早期版本的 R 组件和 R Services。 
+ 提供配置后安装脚本的目的仅仅是帮助客户卸载预发行版本。  安装任何较新的版本时，不要运行该脚本。


## <a name="upgrading-r-components"></a>升级 R 组件

如果实例已包含 R Services 功能，则发行 SQL Server 2016 的修补程序或改进后，还将升级或刷新 R 组件。 

如果安装或升级未连接到 Internet 的服务器，必须先手动下载更新版本的 R 组件，然后开始刷新。 有关详细信息，请参阅 [在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。

如果使用的是 SQL Server vNext，将自动安装 R 组件的升级。

从 2016 年 12 月开始，可以通过将 R Services 的实例_绑定_到新式软件生命周期策略，先于 SQL Server 发布周期一步升级 R 组件。 有关详细信息，请参阅 [Use SqlBindR to Upgrade an Instance of SQL Server R Services](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)（使用 SqlBindR 升级 SQL Server R Services 的实例）

## <a name="support-for-slipstream-upgrades"></a>支持补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点在于，可以在执行安装的同时更新 SQL Server，避免以后单独重新启动。

+ 在 SQL Server 2016 中，可以通过单击 SQL Server Management Studio 中的“工具”，然后选择“检查更新”来启动补充升级。

+ 如果服务器无法访问 Internet，请务必下载 SQL Server 安装程序。 另外，在开始更新过程**之前**，必须单独下载 R 组件安装程序的匹配版本。 有关下载位置，请参阅[Installing R Components without Internet Acccess](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)（在无法访问 Internet 的情况下安装 R 组件）。  

    将所有安装文件复制到本地目录后，在命令行中键入 SETUP.EXE 启动安装实用工具。
      
    - 使用 */UPDATESOURCE* 参数指定包含 SQL Server 更新（例如累积更新或 Service Pack 版本）的本地文件的位置。  
    - 使用 */MRCACHEDIRECTORY* 参数指定包含 R 组件 CAB 文件的文件夹。

有关详细信息，请参阅 R Services 支持团队撰写的以下博客文章：[Deploying R Services on Computers without Internet Access](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)（在无法访问 Internet 的情况下在计算机上部署 R Services）。


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>进行无人参与的安装需要使用 R 组件的新许可协议  
 如果使用命令行来升级已装有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例，则必须修改命令行以使用新的许可协议参数 */IACCEPTROPENLICENSEAGREEMENT*。 
 
 不使用正确的参数可能会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装失败。  
  
## <a name="after-running-setup-includersqlproductnameincludesrsql-productname-mdmd-is-still-not-enabled"></a>运行安装程序后， [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 仍处于未启用状态  
 默认情况下，禁用支持运行外部脚本的功能（即使已安装）。 这是有意为之，目的是减少外围应用。  
  
 若要启用 R 脚本，管理员可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中运行以下语句：  
  
1.  在希望使用 R 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例上运行此语句。  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  重新启动该实例。  
  
3.  重新启动实例后，打开“SQL Server 配置管理器”  或“服务”  面板，并验证 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务是否正在运行。  

> [!TIP]
> 若要安装预先配置的 R Services 实例，请使用包含启用了 R Services 的 Enterprises Edition 的 Azure 虚拟机映像。 有关详细信息，请参阅 [在 Azure 虚拟机上安装 SQL Server R Services](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)。
 

## <a name="setup-of-includersqlproductnameincludesrsql-productname-mdmd-not-available-in-a-failover-cluster"></a>在故障转移群集中不能安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]  
 目前，不能在故障转移群集上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 。  
    
 但是，可以在使用 AlwaysOn 且属于可用性组的独立计算机上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 。 有关在 AlwaysOn 可用性组中使用 R Services 的详细信息，请参阅 [AlwaysOn 可用性组：互操作性](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)。  

另一种做法是在不同的 SQL Server 实例上设置副本，以便运行 R 脚本。 可通过复制或日志传送创建该副本。

## <a name="bkmk_LaunchpadTS"></a>Launchpad 服务无法启动  

可能阻止 Launchpad 启动的几个问题如下。

### <a name="8dot3-notation-is-not-enabled"></a>**未启用 8dot3 表示法**。  

若要安装 R Services（数据库内），则安装该功能的驱动器必须支持使用 **8dot3** 表示法创建短文件名。  8.3 文件名也称作短文件名，用于实现与之前的旧版 Microsoft Windows 兼容或者作为一个长文件名的备用文件名。 

如果安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的卷不支持短文件名，则从 SQL Server 启动 R 的进程可能无法找到正确的可执行文件，且 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 将不会启动。  
  
解决方法之一是应在安装了 SQL Server 和 R Services 的卷上启用 8dot3 表示法。 然后，必须提供 R Services 配置文件中工作目录的短名称。 

1. 若要启用 8dot3 表示法，请运行包含 **8dot3name** 参数的 *fsutil* 实用程序，操作步骤如下所述： [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。
2. 启用 8dot3 表示法后，打开文件 RLauncher.config。 在默认安装中，文件 RLauncher.config 位于 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn
3. 记下 WORKING_DIRECTORY 的属性。
4. 使用包含 *file* 参数的 fsutil 实用程序，以指定在 WORKING_DIRECTORY 中指定的文件夹的短文件路径。
5. 编辑配置文件，以使用 WORKING_DIRECTORY 的短名称。   
     
也可以为 WORKING_DIRECTORY（具有与 8dot3 表示法兼容的路径）指定一个其他目录。     
   
> [!NOTE]
> 以后版本将消除此限制。 如果遇到此问题，请安装以下组件之一：
>
>    + SQL Server 2016 SP1 和 CU1：[SQL Server 累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)
>    + SQL Server 2016 RTM、Service Pack 3，以及此[修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)（按需提供）  
 
### <a name="the-account-that-runs-launchpad-has-been-changed-or-necessary-permissions-have-been-removed"></a>**已更改运行 Launchpad 的帐户或已删除必需的权限。** 

默认情况下，在启动时，[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 将使用以下帐户，该帐户通过 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装程序配置，以便具有所有必需的权限：`NT Service\MSSQLLaunchpad`

因此，如果将不同的帐户分配到 Launchpad，或者权限被 SQL Server 计算机上的某个策略删除，该帐户可能不会获得所需的权限，同时会出现以下错误： 

*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 登录失败: 未授予用户在此计算机上的请求登录类型。*

若要为新服务帐户提供必要的权限，请使用 **本地安全策略** 应用程序并更新帐户的权限，以便包括以下权限：
  + 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
  + 跳过遍历检查 (SeChangeNotifyPrivilege)
  + 以服务身份登录 (SeServiceLogonRight)
  + 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

### <a name="user-group-for-launchpad-is-missing-system-right-allow-log-in-locally"></a>**Launchpad 的用户组缺少系统权限“允许本地登录”**

在安装 R Services 的过程中，SQL Server 将创建 Windows 用户组 **SQLRUserGroup**，并且在默认情况下，为该组预配全部所需的权限，使 Launchpad 能够连接到 SQL Server 并运行外部脚本作业。  
    
但是，在实施更严格限制性安全策略的组织中，此权限可能已手动删除或者被策略吊销。 如果发生这种情况，Launchpad 将无法连接到 SQL Server，并且 R Services 无法正常运行。
    
若要解决此问题，请确保组 **SQLRUserGroup** 拥有系统权限“允许本地登录”。

有关详细信息，请参阅 [配置 Windows 服务帐户和权限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)预览版本升级问题的解答。
  
## <a name="error-unable-to-communicate-with-the-launchpad-service"></a>错误: 无法与 Launchpad 服务通信

如果安装 R Services 并启用该功能，但尝试运行 R 脚本时收到此错误，原因可能是实例的 Launchpad 服务已停止运行。

1. 通过 Windows 命令提示符打开 SQL Server 配置管理器。 有关详细信息，请参阅 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)。
2. 右键单击 R Services 未工作的实例的 SQL Server Launchpad，然后选择“属性”。
3. 单击“服务”选项卡，然后检查该服务是否正在运行。 如果未运行，请将“启动模式”更改为“自动”，然后单击“应用”。
4. 通常，重新启动该服务即可启用 R 脚本。 如果未启用，请记下“二进制路径”属性中的路径和参数。
    + 检查 rlauncher.config 文件，确保工作目录有效
    + 确保 Launchpad 使用的 Windows 组能够连接到 SQL Server 实例，如[上一部分](#bkmk_LaunchpadTS)中所述。 
    + 如果对服务属性做了任何更改，请重新启动 Launchpad 服务。


## <a name="side-by-side-installation-not-supported"></a>不支持并行安装  
 不要使用另一 R 版本或 Revolution Analytics 中的其他版本来创建并行安装。  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>SQL Server 本地化版本的 R 组件的脱机安装 
如果在未连接到 Internet 的计算机上安装 R Services，则必须执行两个额外的步骤：在运行 SQL Server 安装程序之前必须将 R 组件安装程序下载到本地文件夹中，必须编辑该安装程序文件以确保安装正确的语言。 

R 组件使用的语言标识符必须与所安装的 SQL Server 安装程序语言相同，否者“下一步”  按钮将处于禁用状态，且无法完成安装。

有关详细信息，请参阅 [在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>无法启动 R 脚本的运行时
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 会创建一个 Windows 用户组，供 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 用于运行 R 作业。 此用户组必须能够登录到正在运行 R Services 的实例，以便代表使用 Windows 集成身份验证的远程用户执行 R。
  
 在 Windows R 用户组 (**SQLRUsers**) 没有此权限的环境中，可能会看到以下错误：  
  
-   尝试运行 R 脚本时：  
  
     无法启动“R”脚本的运行时。请检查“R”运行时的配置。  
  
     发生外部脚本错误。无法启动运行时。  
  
-   [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务生成的错误：  
  
     无法初始化启动器 RLauncher.dll  
  
     未注册任何启动器 dll！  
  
-   安全日志指示帐户 NT SERVICE\MSSQLLAUNCHPAD 无法登录。  
  
若要了解如何为此用户组提供必要的权限，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制。 

  
## <a name="remote-execution-via-odbc"></a>通过 ODBC 远程执行   
 如果使用数据科学工作站，并连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，以使用 **RevoScaleR** 函数运行 R 命令，则在使用将数据写入到服务器的 ODBC 调用时，可能遇到错误。 
 
 原因与上一节中所述相同：在进行安装时，R Services 将创建一组工作线程帐户，用于运行 R 任务。 不过，如果这些帐户无法连接到服务器，则无法代表用户执行 ODBC 调用。 
 
 请注意，如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制，因为 SQL 登录凭据将从 R Client 显式传递到 SQL Server 实例，再到 ODBC。
  
若要启用隐式身份验证，则必须为这组工作线程帐户提供如下权限：  
    
1. 在运行 R 代码的实例上以管理员身份打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 

2. 运行以下脚本。 如果更改了默认值、计算机和实例名称，请务必编辑用户组名称。
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

有关详细信息以及使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI 来执行此操作的步骤，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。


## <a name="how-to-uninstall-previous-versions-of-r-services"></a>如何卸载早期版本的 R Services

必须按正确的顺序卸载先前版本的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 及其相关 R 组件，尤其是安装了任何预发行版时。

### <a name="step-1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>步骤 1. 卸载以前的组件之前，运行脚本以取消注册 Windows 用户组和组件
如果安装了 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的预发行版本，则必须首先运行包含 `/uninstall` 参数的 `RegisteREext.exe` 脚本。

通过此操作，可以取消注册旧组件，并删除与 Launchpad 相关联的 Windows 用户组。 如果不执行此操作，则将无法为安装的任何新实例创建所需的 Windows 用户组。
  
例如，如果在默认实例上安装 R Services，请从安装脚本的目录位置运行此命令：  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
如果在命名实例上安装 R Services，则在 *INSTANCE:*之后指定实例名称  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

可能需要多次运行该脚本以删除所有组件。

**重要说明**：此脚本的默认位置不同，具体取决于安装的预发行版本。 如果尝试运行该脚本的错误版本，则可能会遇到错误。 

+ **CTP 3.1、3.2 或 3.3**
    
    需要执行附加的步骤来卸载现有组件。 
    1. 首先，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkId=723194)下载更新版本的安装后配置脚本。 更新的脚本支持取消注册旧组件。 
    2. 单击相应的链接并选择“另存为”，以将脚本保存到本地文件夹。  
    3. 重命名现有脚本，然后新脚本复制到执行脚本的文件夹中。 

+ **RC0**
    
    脚本文件位于以下文件夹中：`C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64`  

+ **发行版（13.0.1601.5 或更高版本）**

    无需使用脚本来安装或配置组件。 该脚本应仅用于删除旧组件。 


### <a name="step-2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>步骤 2. 卸载任何较旧版本的 Revolution Enterprise 工具，包括与 CTP 版本一起安装的组件。

卸载 R 组件的顺序非常重要。 请始终首先卸载 [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)] 。 然后再卸载 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]。  

 如果失手先卸载了 R Open，并在尝试卸载 Revolution R 企业版时出现错误，一种解决办法是重新安装 Revolution R Open 或 Microsoft R Open，然后按照正确顺序卸载这两个组件。  

### <a name="step-3-uninstall-any-other-version-of-microsoft-r-open"></a>步骤 3. 卸载任何其他版本的 Microsoft R Open。

最后，卸载其他所有版本的 Microsoft R Open。
 
### <a name="step-4-upgrade-sql-server"></a>步骤 4. 升级 SQL Server  
  
卸载所有预发行组件后，请重新启动计算机。 这是 SQL Server 安装程序的要求，且在重新启动完成之前，将无法继续进行更新的安装。     

完成此操作后，运行 SQL Server 安装程序，并按照以下说明安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]： [安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
不需要任何其他组件；R 包和连接包通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序安装。 

## <a name="problems-uninstalling-older-versions-of-r"></a>卸载旧版 R 的问题  
在某些情况下，卸载过程无法完全删除较旧版本的 Revolution R Open 或 Revolution R Enterprise。  
  
 如果删除较旧版本时遇到问题，也可以编辑注册表以删除相关项。  
  
 打开 Windows 注册表，并找到此项： `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。  
  
 如果存在以下条目且项仅包含单个值 `sEstimatedSize2`，请删除这些条目：  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972（针对 8.0.2）  
  
-   46695879-954E-4072-9D32-1CC84D4158F4（针对 8.0.1）  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B（针对 8.0.0）  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A（针对 7.5.0）  


  
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>将 R Server（独立版）升级到 RC3 需要使用 RC2 安装实用程序进行卸载

 Microsoft R Server（独立版）最先在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 中可用。 若要升级到 RC3 版本的 Microsoft R Server，必须先使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 安装程序进行卸载，然后再使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3 安装程序重新安装。  
  
1.  使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RC2 的 R Server（独立版）。  
  
2.  将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升级到 RC3，然后选择安装 R Services（数据库内）的选项。 此操作可将 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实例升级到 RC3，且无需进行任何额外的配置。  
  
3.  再次运行 RC3 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序，并安装 Microsoft R Server（独立版）。  

> [!NOTE] 
> 在升级到 RTM 版本的 Microsoft R Server 时，不需要此解决方法。 
> 
> 有关 Microsoft R Server 的其他问题，请参阅 [Microoft R Server 发行说明](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)。

## <a name="see-also"></a>另请参阅 
 
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Microsoft R Server（独立版）入门](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

