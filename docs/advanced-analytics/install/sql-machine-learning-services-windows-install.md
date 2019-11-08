---
title: 在 Windows 上安装 SQL Server 机器学习服务（Python、R）
titleSuffix: ''
description: 本文介绍如何在 Windows 上安装 SQL Server 机器学习服务。 可使用机器学习服务在数据库中执行 Python 和 R 脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 448bb460d3cb3d041fd44b582a383037fecb98d4
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532634"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-windows"></a>在 Windows 上安装 SQL Server 机器学习服务（Python 和 R）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在 Windows 上安装 SQL Server 机器学习服务。 可使用机器学习服务在数据库中执行 Python 和 R 脚本。

## <a name="bkmk_prereqs"> </a> 安装前清单

+ 需要数据库引擎实例。 不能只安装 R 或 Python 功能，但可以将它们逐渐添加到现有实例。

+ 为了实现业务连续性，机器学习服务支持 [Always On 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。 必须在每个节点上安装机器学习服务并配置包。

+ SQL Server 2017 中的故障转移群集不支持安装机器学习服务  。 但 SQL Server 2019 却支持  。 
 
+ 不要在域控制器上安装机器学习服务。 安装程序的机器学习服务部分将失败。

+ 不要在运行数据库内实例的同一台计算机上安装“共享功能” > “Machine Learning Server（独立）”   。 一个独立服务器将争夺相同的资源，从而降低这两个安装的性能。

+ 支持并行安装其他版本的 R 和 Python，但不建议这样做。 之所以支持，是因为 SQL Server 实例使用自己的开源 R 和 Anaconda 分发副本。 但不建议这样做，因为在 SQL Server 外部的 SQL Server 计算机上运行使用 R 和 Python 的代码可能会导致各种问题：
    
  + 你将使用不同于在 SQL Server 中运行时使用的库和可执行文件，因此会获得不同的结果。
  + SQL Server 无法管理在外部库中运行的 R 和 Python 脚本，从而导致资源争用。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
+ 默认情况下，机器学习服务安装在 SQL Server 大数据群集上。 如果使用大数据群集，则无需按照本文中的步骤进行操作。 有关详细信息，请参阅[在大数据群集上使用机器学习服务（Python 和 R）](../../big-data-cluster/machine-learning-services.md)。
::: moniker-end

> [!IMPORTANT]
> 安装完成后，请务必完成本文中所述的配置后步骤。 这些步骤包括启用 SQL Server 以使用外部脚本，以及以你的名义添加 SQL Server 运行 R 和 Python 作业所需的帐户。 配置更改通常需要重启实例或重启 Launchpad 服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 的安装向导。
  
1. 在“安装”选项卡上，选择“全新 SQL Server 独立安装或向现有安装添加功能”   。

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![全新 SQL Server 独立安装](media/2017setup-installation-page-mlsvcs.png)
   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![全新 SQL Server 独立安装](media/2019setup-installation-page-mlsvcs.png)
   ::: moniker-end

1. 在“功能选择”  页上，选择以下选项：

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

   - **数据库引擎服务**
     
     若要将 R 和 Python 与 SQL Server 结合使用，则必须安装数据库引擎实例。 可使用默认实例或命名实例。

   - **机器学习服务（数据库内）**
     
     此选项安装支持 R 和 Python 脚本执行的数据库服务。

   ::: moniker-end

   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

   - **数据库引擎服务**
     
     若要将 R、Python 和 Java 与 SQL Server 结合使用，则必须安装数据库引擎实例。 可使用默认实例或命名实例。

   - **机器学习服务（数据库内）**
     
     此选项安装支持 R、Python 和 Java 脚本执行的数据库服务。

   ::: moniker-end

   - **R**
     
     选中此选项可添加 Microsoft R 包、解释器和开源 R。 
     
   - **Python**
     
     选中此选项可添加 Microsoft Python 包、Python 3.5 可执行文件以及从 Anaconda 分发中选择库。
     
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   - **Java**
     
     选中此选项可安装 SQL 随附的 Open JRE，或提供不同版本的 JDK 或 JRE 的位置。
   ::: moniker-end
   
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![R 和 Python 的功能选项](media/2017setup-features-page-mls-rpy.PNG "R 和 Python 的安装选项")
   ::: moniker-end
   
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![R、Python 的功能选项](media/2019setup-features-page-mls-rpy.png "R、Python 和 Java 的安装选项")
   ::: moniker-end
   
   > [!NOTE]
   > 
   > 不要选择 Machine Learning Server（独立）对应的选项  。 在“共享功能”下安装 Machine Learning Server 的选项适用于在单独的计算机上使用  。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

4. 在“同意安装 Microsoft R Open”页上，选择“接受”，然后选择“下一步”    。 该许可协议涵盖 Microsoft R Open，其中包括分发开源 R 基础包和工具，以及 Microsoft 开发团队提供的增强型 R 包和连接提供程序。

1. 在“同意安装 Python”页上，选择“接受”，然后选择“下一步”    。 Python 开源许可协议还涵盖了 Anaconda 和相关工具，以及 Microsoft 开发团队提供的一些新 Python 库。

   > [!NOTE]
   >  如果正在使用的计算机无法访问 Internet，则可以在此时暂停安装以单独下载安装程序。 有关详细信息，请参阅[在没有 Internet 连接的情况下安装机器学习组件](../install/sql-ml-component-install-without-internet-access.md)。

1. 在“准备安装”页面上，验证是否已包括这些选择，然后选择“安装”   。
  
   + 数据库引擎服务
   + 机器学习服务（数据库内）
   + R 和/或 Python

   请注意配置文件存储路径 `..\Setup Bootstrap\Log` 下的文件夹位置。 安装完成后，可以在“摘要”文件中查看已安装的组件。

1. 安装完成后，如果收到重启计算机的指示，请立即重启。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [查看和读取 SQL Server 安装程序日志文件](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

::: moniker-end

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

1. 在“同意安装 Microsoft R Open”页上，选择“接受”，然后选择“下一步”    。 该许可协议涵盖 Microsoft R Open，其中包括分发开源 R 基础包和工具，以及 Microsoft 开发团队提供的增强型 R 包和连接提供程序。

1. 在“同意安装 Python”页上，选择“接受”，然后选择“下一步”    。 Python 开源许可协议还涵盖了 Anaconda 和相关工具，以及 Microsoft 开发团队提供的一些新 Python 库。

1. 在“Java 安装位置”页上，可以安装 SQL 随附的 Open JRE 版本，也可以提供自己的 JDK 或 JRE 安装位置  。 然后选择“下一步”  。

   > [!NOTE]
   >  如果正在使用的计算机无法访问 Internet，则可以在此时暂停安装以单独下载安装程序。 有关详细信息，请参阅[在没有 Internet 连接的情况下安装机器学习组件](../install/sql-ml-component-install-without-internet-access.md)。

1. 在“准备安装”页面上，验证是否已包括这些选择，然后选择“安装”   。
  
   + 数据库引擎服务
   + 机器学习服务（数据库内）
   + R、Python 和/或 Java

   请注意配置文件存储路径 `..\Setup Bootstrap\Log` 下的文件夹位置。 安装完成后，可以在“摘要”文件中查看已安装的组件。

1. 安装完成后，如果收到重启计算机的指示，请立即重启。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [查看和读取 SQL Server 安装程序日志文件](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

::: moniker-end

## <a name="set-environment-variables"></a>设置环境变量

（仅适用于 R 功能集成）应设置“MKL_CBWR”环境变量，以确保从 Intel 数学核心函数库 (MKL) 计算得到[一致的输出结果](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)  。

1. 在“控制面板”中，单击“系统和安全” > “系统” > “高级系统设置” > “环境变量”     。

2. 创建新的用户或系统变量。 

   + 将变量名称设置为 `MKL_CBWR`
   + 将变量值设置为 `AUTO`

此步骤需要重启服务器。 如果要启用脚本执行，则可以在完成所有配置工作之前暂停重启。

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>启用脚本执行

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
    
3.  若要启用外部脚本编写功能，请运行以下语句：
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果已为 R 语言启用此功能，请不要对 Python 再次运行 reconfigure 命令。 基础扩展性平台支持这两种语言。

## <a name="restart-the-service"></a>重新启动服务。

安装完成后，请先重启数据库引擎，然后再继续执行下一步，以启用脚本执行。

重启服务也会自动重启相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。

可以使用右键单击 SSMS 中实例的“重启”命令、使用“控制面板”中的“服务”面板，或者使用 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)来重启服务   。

## <a name="verify-installation"></a>验证安装

检查[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)或安装程序日志中实例的安装状态。

使用以下步骤验证用于启动外部脚本的所有组件是否都在运行。

1. 在 SQL Server Management 中打开新的“查询”窗口，然后运行以下命令：
    
   ```sql
   EXECUTE sp_configure  'external scripts enabled'
   ```

   **run_value** 现在应已设置为 1。
    
2. 打开“服务”面板或 SQL Server 配置管理器，并验证“SQL Server Launchpad”是否正在运行   。 应该为每个安装了 R 或 Python 的数据库引擎实例提供一项服务。 有关该服务的详细信息，请参阅[扩展性框架](../concepts/extensibility-framework.md)。 
   
3. 如果 Launchpad 正在运行，则应该能够运行简单的 R 和 Python 脚本，以验证外部脚本运行时是否可以与 SQL Server 通信。

   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开新的“查询”窗口，然后运行如下脚本  ：
   
   + 对于 R
   
     ```sql
     EXEC sp_execute_external_script  @language =N'R',
     @script=N'
     OutputDataSet <- InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
     
   + 对于 Python
     
     ```sql
     EXEC sp_execute_external_script  @language =N'Python',
     @script=N'
     OutputDataSet = InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
   
   **结果**

   如果是首次加载外部脚本运行时，则该脚本可能需要一些时间才能运行。 结果应如下所示：

   | Hello |
   |----|
   | 1|

> [!NOTE]
> 根据设计，系统不会返回 Python 脚本中使用的列或标题。 若要在输出结果中添加列名称，则必须为返回数据集指定架构。 为此，请使用存储过程的 WITH RESULTS 参数，命名列并指定 SQL 数据类型。
> 
> 例如，可以添加以下行来生成任意列名：`WITH RESULT SETS ((Col1 AS int))`

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
<!-- There are no updates yet available for 2019, and there's no 2019 update list site. When updates become available, add 2019 information to this section. -->

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

建议将最新的累积更新应用于数据库引擎和机器学习组件。

在连接 Internet 的设备上，累积更新通常通过 Windows 更新进行应用，但也可以使用以下步骤进行可控更新。 为数据库引擎应用更新时，安装程序将为你在同一实例上安装的任何 R 或 Python 功能拉取累积更新。 

在断开连接的服务器上，需要执行额外的步骤。 有关详细信息，请参阅 [在没有 Internet 连接的计算机上安装 > 应用累积更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 开始使用已安装的基线实例：SQL Server 2017 初始版本

2. 请转到累积更新列表：[SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 选择最新的累积更新。 自动下载并提取可执行文件。

4. 运行安装程序。 接受许可条款，然后在“功能选择”页上，查看应用了累积更新的功能。 应看到为当前实例安装的每个功能，包括机器学习功能。 安装程序会下载更新所有功能所需的 CAB 文件。

   ![已安装功能的摘要](media/cumulative-update-feature-selection.png)

5. 继续执行向导，接受 R 和 Python 分发的许可条款。 

::: moniker-end

## <a name="additional-configuration"></a>其他配置

如果外部脚本验证步骤成功，则可以从 SQL Server Management Studio、Visual Studio Code 或者能够向服务器发送 T-SQL 语句的其他任何客户端运行 R 或 Python 命令。

如果在运行命令时遇到错误，请查看本部分中的其他配置步骤。 服务或数据库可能需要进行其他适当的配置。

在实例级别，其他配置可能包括：

* [SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [为 SQLRUserGroup 创建登录名](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [管理磁盘配额](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)以避免外部脚本运行耗尽磁盘空间的任务

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
在 Windows 上的 SQL Server 2019 中，隔离机制已发生更改。 这会影响 **SQLRUserGroup**、防火墙规则、文件权限和默示身份验证。 有关详细信息，请参阅 [机器学习服务的隔离更改](sql-server-machine-learning-services-2019.md)。
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

数据库上可能需要以下配置更新：

* [向用户授予 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> 是否需要其他配置取决于安全架构、SQL Server 的安装位置，以及期望用户以何方式连接到数据库和运行外部脚本。

## <a name="suggested-optimizations"></a>建议的优化

现在所有工作已顺利进行，可能还需要优化服务器以支持机器学习，或安装预先训练的模型。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>添加更多辅助角色帐户

如果预期会有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[在 SQL Server 机器学习服务中扩展外部脚本的并发执行](../administration/scale-concurrent-execution-external-scripts.md)。
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>优化服务器执行脚本

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的默认设置旨在为数据库引擎支持的各种服务（可能包括提取、转换和加载 (ETL) 进程、报告、审核和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的应用程序）优化服务器平衡。 因此，在默认设置下，可能会发现机器学习（尤其是占用大量内存的操作）的资源有时被限制或被阻止。

若要确保机器学习作业的优先级并为其分配适当资源，建议使用 SQL Server Resource Governor 配置外部资源池。 可能还要更改分配到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的内存量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务下运行的帐户数。

- 要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改为数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 启动的 R 帐户数，请参阅[在 SQL Server 机器学习服务中扩展外部脚本的并发执行](../administration/scale-concurrent-execution-external-scripts.md)。

如果使用的是 Standard Edition 且没有 Resource Governor，则可以使用动态管理视图 (DMV) 和扩展事件以及 Windows 事件监视来帮助管理服务器资源。 有关详细信息，请参阅[监视和管理 R 服务](../r/managing-and-monitoring-r-solutions.md)和[监视和管理 Python 服务](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-python-and-r-packages"></a>安装其他 Python 和 R 包

为 SQL Server 创建的 Python 和 R 解决方案可以调用基本功能、随 SQL Server 一起安装的专有包中的功能以及与 SQL Server 安装的开源 Python 和 R 版本兼容的第三方包。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果在计算机上单独安装了 Python 或 R，或者将包安装到了用户库，则无法从 T-SQL 使用这些包。

若要安装和管理其他包，可以将用户组设置为共享每个数据库级别的包，或者通过配置数据库角色使用户能够安装自己的包。 有关详细信息，请参阅[安装 Python 包](../package-management/install-additional-python-packages-on-sql-server.md)和[安装新的 R 包](../package-management/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 一起使用：

+ [教程：在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [教程：适用于 Python 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于真实场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
