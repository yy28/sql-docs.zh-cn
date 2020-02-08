---
title: 安装 SQL Server 2016 R Services (In-Database)
description: 将 R 编程语言支持添加到 Windows 上 SQL Server 2016 R Services 中的数据库引擎。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6fcb4245d4efff00002dea9b490312792e0d83d6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73706995"
---
# <a name="install-sql-server-2016-r-services"></a>安装 SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何安装和配置 SQL Server 2016 R Services  。 如具有 SQL Server 2016，安装此功能即可在 SQL Server 中启用 R 代码的执行。

在 SQL Server 2017 中，[机器学习服务](../r/r-server-standalone.md)提供了 R 集成，这反映出已添加 Python。 如果你想获取 R 集成并具有 SQL Server 2017 安装介质，请参阅[安装 SQL Server 机器学习服务](sql-machine-learning-services-windows-install.md)以添加该功能。 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>安装前清单

+ 需要数据库引擎实例。 不能只安装 R，但可将其以增量方式添加到现有实例。

+ 为实现业务连续性，R Services 支持 [Always On 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。 必须在每个节点上安装 R Services 并配置包。

+ 请勿在故障转移群集上安装 R Services。 用于隔离 R 进程的安全机制与 Windows Server 故障转移群集环境不兼容。

+ 请勿在域控制器上安装 R Services。 安装程序的 R Services 部分将失败。

+ 请勿在运行数据库内实例的同一台计算机上安装“共享功能” > “R Server (独立版)”   。 

  可与其他版本的 R 和 Python 并行安装，因为 SQL Server 实例使用自己的开放源代码 R 和 Anaconda 分发副本。 然而，在 SQL Server 外部的 SQL Server 计算机上运行使用 R 和 Python 的代码可能会导致各种问题：
    
  + 你将使用不同于在 SQL Server 中运行时使用的库和可执行文件，因此会获得不同的结果。
  + SQL Server 无法管理在外部库中运行的 R 和 Python 脚本，从而导致资源争用。
  
如果使用任何早期版本的 Revolution Analytics 开发环境或 RevoScaleR 包，或者已经安装任何预发行版的 SQL Server 2016，必须将其卸载。 不支持运行较旧和较新版本的 RevoScaleR 和其他专用包。 有关删除早期版本的帮助，请参阅[有关升级和安装 SQL Server R Services 的常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安装完成后，请务必完成本文中所述的其他配置后步骤。 这些步骤包括启用 SQL Server 以使用外部脚本，以及以你的名义添加 SQL Server 运行 R 作业所需的帐户。 配置更改通常需要重启实例或重启 Launchpad 服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 的安装向导。

2. 在“安装”选项卡上，选择“全新 SQL Server 独立安装或向现有安装添加功能”   。
    
   ![安装 R Services（数据库内）](media/2016-setup-installation-rsvcs.png "使用 R Services 开始安装数据库引擎")
   
3. 在“功能选择”页上，选择以下选项  ：

   - 选择“数据库引擎服务”  。 使用机器学习的每个实例都需要数据库引擎。
   - 选择“R Services (数据库内)”  。 安装对在数据库中使用 R 的支持。
    
     ![R Services 功能选择](media/2016setup-rsvcs-features.png "为数据库中的 R Services 选择这些功能")

    > [!IMPORTANT]
    > 请勿同时安装 R Server 和 R Services。 通常可安装 R Server（独立版）来创建一个环境，数据科学家或开发人员可使用该环境连接到 SQL Server 并部署 R 解决方案。 因此，不需要在同一台计算机上安装这两个组件。

4.  在“同意安装 Microsoft R Open”  页上，单击“接受”  。
  
    需要此许可协议方可下载 Microsoft R Open，其中包括分发开放源代码 R 基础包和工具，以及 Microsoft R 开发团队提供的增强型 R 包和连接提供程序。
  
5. 接受许可协议后，在安装程序准备期间将出现短暂暂停。 当按钮可用时，单击“下一步”  。

6. 在“准备安装”页上，验证是否包括以下项，然后选择“安装”   。

   + 数据库引擎服务
   + R Services（数据库内）

    请注意配置文件存储路径 `..\Setup Bootstrap\Log` 下的文件夹位置。 安装完成后，可以在“摘要”文件中查看已安装的组件。

7. 安装完成后，如果收到重启计算机的指示，请立即重启。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [查看和读取 SQL Server 安装程序日志文件](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

## <a name="set-environment-variables"></a>设置环境变量

（仅适用于 R 功能集成）应设置“MKL_CBWR”环境变量，以确保从 Intel 数学核心函数库 (MKL) 计算得到[一致的输出结果](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)  。

1. 在“控制面板”中，单击“系统和安全” > “系统” > “高级系统设置” > “环境变量”     。

2. 创建新的用户或系统变量。 

  + 将变量名称设置为 `MKL_CBWR`
  + 将变量值设置为 `AUTO`

此步骤需要重启服务器。 如果要启用脚本执行，则可以在完成所有配置工作之前暂停重启。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>启用脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 可以从此页下载并安装相应的版本：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 还可以使用 [Azure Data Studio](../../azure-data-studio/what-is.md)，它支持管理任务和针对 SQL Server 的查询。
  
2. 连接到安装了机器学习服务的实例，单击“新建查询”打开查询窗口，然后运行以下命令  ：

   ```sql
   sp_configure
   ```
    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为默认情况下该功能处于关闭状态。 必须先由管理员显式启用此功能，然后才能运行 R 或 Python 脚本。
     
3. 若要启用外部脚本编写功能，请运行以下语句：
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新启动服务。

安装完成后，请先重启数据库引擎，然后再继续执行下一步，以启用脚本执行。

重启服务也会自动重启相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。

可以使用右键单击 SSMS 中实例的“重启”命令、使用“控制面板”中的“服务”面板，或者使用 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)来重启服务   。

## <a name="verify-installation"></a>验证安装

使用[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)检查实例的安装状态。

使用以下步骤验证用于启动外部脚本的所有组件是否都在运行。

1. 在 SQL Server Management 中打开新的“查询”窗口，然后运行以下命令：
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。

2. 打开“服务”面板或 SQL Server 配置管理器，并验证“SQL Server Launchpad”是否正在运行   。 应该为每个安装了 R 或 Python 的数据库引擎实例提供一项服务。 有关该服务的详细信息，请参阅[扩展性框架](../concepts/extensibility-framework.md)。

7. 如果 Launchpad 正在运行，则应该能够运行简单的 R，以验证外部脚本运行时是否可以与 SQL Server 通信。 

    在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开新的“查询”窗口，然后运行如下脚本  ：
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    如果是首次加载外部脚本运行时，则该脚本可能需要一些时间才能运行。 结果应如下所示：

    | Hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

建议将最新的累积更新应用于数据库引擎和机器学习组件。

在连接 Internet 的设备上，累积更新通常通过 Windows 更新进行应用，但也可以使用以下步骤进行可控更新。 为数据库引擎应用更新时，安装程序将为你在同一实例上安装的 R 库拉取累积更新。 

在断开连接的服务器上，需要执行额外的步骤。 有关详细信息，请参阅 [在没有 Internet 连接的计算机上安装 > 应用累积更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 开始使用已安装的基线实例：SQL Server 2016 初始版本、SQL Server 2016 SP 1 或 SQL Server 2016 SP 2。

2. 请转到累积更新列表：[SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 选择最新的累积更新。 自动下载并提取可执行文件。

4. 运行安装程序。 接受许可条款，然后在“功能选择”页上，查看应用了累积更新的功能。 应看到为当前实例安装的每个功能，包括 R Services。 安装程序会下载更新所有功能所需的 CAB 文件。

5. 继续执行向导，接受 R 分发的许可条款。 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>其他配置

如果外部脚本验证步骤成功，则可以从 SQL Server Management Studio、Visual Studio Code 或者能够向服务器发送 T-SQL 语句的其他任何客户端运行 Python 命令。

如果在运行命令时遇到错误，请查看本部分中的其他配置步骤。 服务或数据库可能需要进行其他适当的配置。

在实例级别，其他配置可能包括：

* [SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [管理磁盘配额](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)以避免外部脚本运行耗尽磁盘空间的任务

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

数据库上可能需要以下配置更新：

* [向用户授予 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)
* [将 SQLRUserGroup 添加为数据库用户](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> 并非所有列出的更改都是必需的，也可能不需要任何更改。 要求取决于安全架构、SQL Server 的安装位置，以及期望用户以何种方式连接到数据库和运行外部脚本。 有关其他疑难解答提示，请访问此处：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>建议的优化

现在所有工作已顺利进行，可能还需要优化服务器以支持机器学习，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多辅助角色帐户

如果可能经常使用 R，或预期会有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../administration/modify-user-account-pool.md)。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>优化服务器以执行外部脚本

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的默认设置旨在为数据库引擎支持的各种服务（可能包括提取、转换和加载 (ETL) 进程、报告、审核和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的应用程序）优化服务器平衡。 因此，在默认设置下，可能会发现机器学习（尤其是占用大量内存的操作）的资源有时被限制或被阻止。

若要确保机器学习作业的优先级并为其分配适当资源，建议使用 SQL Server Resource Governor 配置外部资源池。 可能还要更改分配到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的内存量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务下运行的帐户数。

- 要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改为数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 要更改可通过 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 启动的 R 帐户数，请参阅[修改机器学习的用户帐户池](../administration/modify-user-account-pool.md)。

如果使用了 Standard Edition 且没有安装资源调控器，可以使用动态管理视图 (DMV) 和扩展事件以及 Windows 事件监视来帮助管理 R 所用的服务器资源。有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建的 R 解决方案可以调用基本 R 函数、随 SQL Server 一起安装的专有包中的函数以及与 SQL Server 安装的开放源代码 R 版本兼容的第三方 R 包。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果在计算机上单独安装了 R，或者将包安装到了用户库，则无法从 T-SQL 使用这些包。

安装和管理 R 包的过程在 SQL Server 2016 和 SQL Server 2017 中有所不同。 在 SQL Server 2016 中，数据库管理员必须安装用户所需的 R 包。 在 SQL Server 2017 中，可通过设置用户组共享每个数据库级别的包，或者通过配置数据库角色使用户能够安装其自己的包。 有关详细信息，请参阅[安装新的 R 包](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看基于真实场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。