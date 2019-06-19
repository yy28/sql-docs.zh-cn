---
title: 安装 SQL Server 2016 R Services （数据库内） 的 SQL Server 机器学习
description: 添加 R 编程语言支持添加到 Windows 上的 SQL Server 2016 R Services 上的数据库引擎。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bc9762470b6e2a836c29f53ebfc3ffeadbcc381f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454692"
---
# <a name="install-sql-server-2016-r-services"></a>安装 SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何安装和配置 SQL Server 2016 R Services。  如果你有 SQL Server 2016，请安装此功能以在 SQL Server 中执行 R 代码。

在 SQL Server 2017 中，[机器学习服务](../r/r-server-standalone.md)中提供了 R 集成，体现出添加了 Python。 如果要集成 R 并拥有 SSQL Server 2017 安装介质，请参阅[安装 SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)来添加该功能。 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>预安装清单

+ 需要数据库引擎实例。 不能只安装 R，但可以将其逐步添加到现有实例。

+ 实现业务连续性[Always On 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)R Services 支持。 您必须安装 R Services 和配置包，每个节点上。

+ 不要在故障转移群集上安装 R Services。 用于隔离 R 进程的安全机制与 Windows Server 故障转移群集环境不兼容。

+ 不要在域控制器上安装 R Services 。 安装程序的 R Services 部分将失败。

+ \+ 不要在运行数据库内实例的同一台计算机上安装“共享功能” > “R Server（独立版）” 。   

  可以与其他版本的 R 和 Python 并行安装，因为 SQL Server 实例使用自己的开源 R 和 Anaconda 发行版的副本。 但是，在 SQL Server 外部的 SQL Server 计算机上运行使用 R 和 Python 的代码可能会导致各种问题：
    
  + 与在 SQL Server 中运行相比，你使用不同的库和不同的可执行文件，并获得不同的结果。
  + 外部库中运行的 R 和 Python 脚本不能由 SQL Server 管理，这会导致资源争用。
  
如果使用任何早期版本的 Revolution Analytics 开发环境或 RevoScaleR 软件包，或者安装了 SQL Server 2016 的任何预发行版本，则必须将其卸载。 不支持运行较旧和较新版本的 RevoScaleR 和其他专有包。 删除以前版本的帮助，请参阅[升级和安装常见问题解答的 SQL Server 机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安装完成后，请确保完成本文中描述的其他配置后步骤。 这些步骤包括使 SQL Server 能够使用外部脚本，以及为 SQL Server 添加代表你运行R作业所需的帐户。 配置更改通常需要重新启动实例，或者重新启动 Launchpad 服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 安装向导。

2. 在“安装”选项卡上，选择“新的 SQL Server 独立安装或向现有安装添加功能”。  
    
   ![安装 R Services （数据库内）](media/2016-setup-installation-rsvcs.png "启动数据库引擎的安装与 R 服务")
   
3. 在“功能选择”页面上，选择以下选项： 

   - 选择**数据库引擎服务**。 选择“数据库引擎服务”。每个使用机器学习的实例都需要数据库引擎。
   - 选择“R Services (数据库内)” 。对在数据库内使用 R 的安装支持。  安装 R 的数据库中使用的支持
    
     ![R Services 功能选择](media/2016setup-rsvcs-features.png "选择这些功能的 R Services 中的数据库")

    > [!IMPORTANT]
    > 不要同时安装 R Server 和 R Services。 通常会安装 R Server（独立版）来创建数据科学家或开发人员用来连接 SQL Server 和部署 R 解决方案的环境。 因此，无需在同一台计算机上安装两者。

4.  在“同意安装 Microsoft R Open”页上，单击“接受”。  
  
    下载 Microsoft R Open，其中包括开放源代码 R 基础包和工具，以及增强型的 R 包和 Microsoft R 开发团队的连接提供程序的分发时需要此许可协议。
  
5. 接受许可协议后，安装程序准备就绪时会暂停一下。 按钮可用时单击“下一步”。 

6. 在“已准备好安装”页上，验证是否包含以下项，然后选择“安装”。  

   + 数据库引擎服务
   + R Services（数据库内）

    请注意路径 `..\Setup Bootstrap\Log` 下的文件夹位置，配置文件存储在此位置。 安装完成后，可以在摘要文件中查看已安装的组件。

7. 安装完成后，如果系统指示重启计算机，请立即重启。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

## <a name="set-environment-variables"></a>设置环境变量

对于仅 R 功能集成，应设置**MKL_CBWR**环境变量[确保一致的输出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)从 Intel Math Kernel Library (MKL) 的计算。

1. 在控制面板中，单击**系统和安全** > **系统** > **高级系统设置** >  **环境变量**。

2. 创建一个新的用户或系统变量。 

  + 到组变量名称 `MKL_CBWR`
  + 将变量的值设置为 `AUTO`

此步骤需要重新启动服务器。 如果你是要启用脚本执行，您可以在重启保持，直到完成所有配置工作。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>启用脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 可以下载并安装适当版本，在此页：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 还可以试用 [Azure Data Studio](../../azure-data-studio/what-is.md) 的预览版，它支持针对 SQL Server 的管理任务和查询。
  
2. 连接到安装了机器学习服务的实例，单击“新建查询”以打开查询窗口，然后运行以下命令： 

   ```sql
   sp_configure
   ```
    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为该功能默认情况下处于关闭状态。 在运行 R 或 Python 脚本之前，必须由管理员显式启用该功能。
     
3. 若要启用外部脚本编写功能，请运行以下语句：
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新启动服务。

安装完成后，重新启动数据库引擎，然后继续执行下一步，启用脚本执行。

重新启动该服务还会自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

要想重启该服务，可以在 SSMS 中右键单击实例的“重启”命令、使用“控制面板”中的“服务”面板，或使用 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。  

## <a name="verify-installation"></a>验证安装

使用[自定义报告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)查看实例的安装状态。

使用以下步骤验证用于启动外部脚本的所有组件是否正在运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。

2. 打开“服务”面板或 SQL Server 配置管理器，验证“SQL Server Launchpad 服务”是否正在运行。   应具备针对安装了 R 或 Python 的每个数据库引擎实例的一项服务。 有关该服务的更多信息，请参阅[可扩展性框架](../concepts/extensibility-framework.md)。

7. 如果 Launchpad 正在运行，应该能够运行简单的 R 来验证外部脚本运行时是否可以与 SQL Server 通信。 

    在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开一个新的“查询”窗口，然后运行如下脚本： 
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    对于第一次加载外部脚本运行时，脚本可能需要一段时间才能运行。 结果应如下所示：

    | Hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

我们建议将最新的累积更新应用到数据库引擎和机器学习组件。

在连接 Internet 的设备上，通常通过 Windows Update 应用累积更新，但也可以使用以下步骤进行受控更新。 应用数据库引擎的更新时，安装程序会为在同一实例上安装的 R 库提取累积更新。 

在断开连接的服务器上，需要执行额外步骤。 有关更多信息，请参阅[在没有 internet 访问权限的计算机上安装 > 应用累积更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 使用已安装的基线实例启动：SQL Server 2016 初始版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2。

2. 请转到累积更新列表：[SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 选择最新的累积更新。 可执行文件将自动下载和提取。

4. 运行安装程序。 接受许可条款，然后在功能选择页面上，查看应用累积更新的功能。 应该看到为当前实例安装的每个功能，包括 R Services。 安装程序会下载更新所有功能所需的 CAB 文件。

5. 继续完成向导，接受 R 分发版的许可条款。 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>其他配置

如果外部脚本验证步骤成功，则可以从 SQL Server Management Studio、Visual Studio 代码或可以向服务器发送 T-SQL 语句的任何其他客户端运行 Python 命令。

如果在运行命令时出错，请查看本节中的其他配置步骤。 可能需要对服务或数据库进行其他适当的配置。

在实例级别，可能包括其他配置：

* [SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [管理磁盘配额](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)以避免外部脚本正在运行的任务已经用完了磁盘空间

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

在数据库中，则可能需要以下配置更新：

* [授予用户对 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)
* [将 SQLRUserGroup 添加为数据库用户](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> 并非所有列出的更改都是必需的，可能不需要任何更改。 要求取决于安全架构、安装 SQL Server 的位置以及希望用户如何连接到数据库并运行外部脚本。 其他故障排除提示可在此处找到：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>建议的优化

现已完成了所有工作，你可能还希望优化服务器以支持机器学习，或者安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果认为可能大量使用 R，或者可能有多位用户同时运行脚本，则可以增加分配给 Launchpad 服务的工作人员帐户的数量。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../administration/modify-user-account-pool.md)。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>优化执行外部脚本的服务器

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的默认设置旨在针对数据库引擎支持的各种服务优化服务器的平衡，这些服务可能包括提取、转换和加载 (ETL) 流程、报告、审计以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的应用程序。 因此，在默认设置下，你可能会发现机器学习的资源有时会受到限制或阻止，尤其是在内存密集型操作中。

若要确保机器学习作业的优先级别并其分配相应资源，我们建议使用 SQL Server 资源调控器配置外部资源池。 您可能还需要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 启动的 R 帐户数量，请参阅[修改机器学习的用户帐户池](../administration/modify-user-account-pool.md)。

如果使用的是 Standard Edition 并且没有资源调控器，则可以使用动态管理视图 (DMV) 和扩展事件以及 Windows 事件监视来帮助管理 R 使用的服务器资源。有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建的R解决方案可以调用基本 R 函数、与 SQL Server 一起安装的专有包中的函数以及与 SQL Server 安装的开源 R 版本兼容的第三方 R 包。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果在计算机上单独安装 R，或者将软件包安装到用户库，则无法使用 T-SQL 中的这些包。

在 SQL Server 2016 和 SQL Server 2017 中，安装和管理 R 包的过程是不同的。 在 SQL Server 2016 中，数据库管理员必须安装用户需要的 R 包。 在 SQL Server 2017 中，可以设置用户组以在每个数据库级别上共享包，或者配置数据库角色以使用户能够安装自己的包。 有关更多信息，请参阅[安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程：R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看基于实际场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。