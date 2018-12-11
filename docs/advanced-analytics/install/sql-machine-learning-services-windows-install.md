---
title: 安装 SQL Server 机器学习在 Windows 上的服务 （数据库） |Microsoft Docs
description: 当您在 Windows 上安装 SQL Server 2017 机器学习服务，SQL Server 或 SQL Server 上的 Python 中的 R 才可用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7f96c2acbca436ff18ccb6a12421d84bda965e4d
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878090"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>安装 SQL Server 机器学习在 Windows 上的服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

从SQL Server 2017开始，SQL Server机器学习服务提供了对数据库内分析的R和Python支持，SQL Server机器学习服务是SQL Server 2016中引入的[SQL Server R Services](../r/sql-server-r-services.md)的后续版本。函数库在R和Python中可用，并作为外部脚本运行在数据库引擎实例上。


本文介绍如何通过运行SQL Server安装向导并按照屏幕上的提示安装机器学习组件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="bkmk_prereqs"> </a> 预安装清单

+ 如果要使用R，Python或Java语言支持安装机器学习服务，则需要SQL Server 2017（或更高版本）安装程序。如果您拥有SQL Server 2016安装介质，则可以安装[SQL Server 2016 R Services （数据库内）](sql-r-services-windows-install.md)以获得R语言支持。

+ 数据库引擎实例是必需的。您不能仅安装R或Python功能，可以将它们逐步添加到现有实例中。

- SQL Server 2017中的故障转移群集*不支持*安装机器学习服务。但是，SQL Server 2019*支持*。
 
+ 不要在域控制器上安装机器学习服务。 安装程序的机器学习服务部分将会失败。

+ 不要在运行数据库内实例的同一台计算机上安装**共享功能** > **Machine Learning Server （独立版）**。独立服务器将竞争相同的资源，从而破坏两个安装的性能。

+ 支持与其他版本的 R 和 Python 的并行安装，但不是建议这样做。 它支持，因为 SQL Server 实例使用其自己的开放源代码 R 和 Anaconda 分发版的副本。 但建议不要因为运行 SQL Server 外部的 SQL Server 计算机使用 R 和 Python 的代码可能会导致各种问题：
    
  + 使用不同的库和其他可执行文件，并获取不同的结果，比您在 SQL Server 中运行时。
  + 不能由 SQL Server，从而导致资源争用管理外部库中运行的 R 和 Python 脚本。
  
> [!IMPORTANT]
> 安装程序完成后，请确保要完成本文中所述的配置后步骤。 这些步骤包括启用 SQL Server 以使用外部脚本，并添加所需的 SQL Server，你的名义运行 R 和 Python 的作业帐户。 配置更改通常需要重新启动实例或重新启动 Launchpad 服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2017 安装向导。 您可以下载 
  
2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

   ![安装机器学习服务中的数据库](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在“功能选择”  页上，选择以下选项：
  
    -   **数据库引擎服务**
  
         若要使用 R 和 Python 与 SQL Server，必须安装数据库引擎的实例。 您可以使用默认值或命名的实例。
  
    -   **机器学习服务（数据库内）**
  
         此选项将安装支持 R 的数据库服务和 Python 脚本执行。

    -   **R**

        选中此选项可添加 Microsoft R 包、 解释器和开放源代码。 

    -   **Python**

        选中此选项可添加 Microsoft Python 包，Python 3.5 可执行文件，然后从 Anaconda 分发版中选择库。
        
        ![功能对 R 和 Python 选项](media/2017setup-features-page-mls-rpy.png "安装用于 Python 的选项")

        > [!NOTE]
        > 
        > 未选择的选项**Machine Learning Server （独立版）**。 安装 Machine Learning Server 下的选项**共享功能**旨在用于不同的计算机上。

4. 上**同意安装 R**页上，选择**接受**。 此许可协议涵盖了 Microsoft R Open，其中包括开放源代码 R 基础包和工具，以及增强型的 R 包和 Microsoft 开发团队的连接提供程序的分发。

5. 上**同意安装 Python**页上，选择**接受**。 Anaconda 和相关的工具，以及 Microsoft 开发团队的某些新 Python 库，还介绍了 Python 开放源代码许可协议。
     
     ![到 Python 许可协议](media/2017setup-python-license.png "许可适用于 Python 的协议")
  
    > [!NOTE]
    >  如果正在使用的计算机没有 internet 访问权限，可先暂停安装，此时若要单独下载安装程序。 有关详细信息，请参阅[安装没有 internet 访问权限的机器学习组件](../install/sql-ml-component-install-without-internet-access.md)。
  
     选择**Accept**，等待，直到**下一步**按钮将变为活动状态，并选择**下一步**。
  
6. 上**已准备好安装**页上，验证这些选择是包括在内，然后选择**安装**。
  
    + 数据库引擎服务
    + 机器学习服务（数据库内）
    + R 和/或 Python

    记下的路径下的文件夹位置`..\Setup Bootstrap\Log`存储配置文件。 安装程序完成后，你可以查看摘要文件中已安装的组件。

7. 安装完成时，如果要求您重新启动计算机后请立即登录。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>启用脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 可以下载并安装适当版本，在此页中：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 您还可以试用的预览版本[Azure Data Studio](../../azure-data-studio/what-is.md)，它支持管理任务和针对 SQL Server 的查询。
  
2. 连接到安装机器学习服务的实例中，单击**新查询**打开查询窗口中，并运行以下命令：

   ```SQL
   sp_configure
   ```

    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为默认情况下关闭功能。 在可以运行 R 或 Python 脚本之前，必须由管理员显式启用该功能。
    
3.  若要启用外部脚本编写功能，请运行以下语句：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果启用了 R 语言的功能，不会运行重新配置适用于 Python 的第二次。 底层扩展性平台支持这两种语言。

## <a name="restart-the-service"></a>重新启动服务。

安装完成后下, 一步，启用脚本执行在继续之前重新启动数据库引擎。

重新启动该服务还会自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

可以使用右键单击该服务重新启动**重新启动**命令，以在 SSMS 中，或使用的实例进行**Services**面板在控制面板中，或通过使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>验证安装

检查中的实例的安装状态[自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)或安装程序日志。

使用以下步骤来验证用于启动外部脚本的所有组件正在都运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。
    
2. 打开**Services**面板或 SQL Server 配置管理器，并验证是否**SQL Server Launchpad 服务**正在运行。 应具有一项服务的每个数据库引擎实例具有 R 或 Python 安装。 有关服务的详细信息，请参阅[可扩展性框架](../concepts/extensibility-framework.md)。 
   
3. 如果 Launchpad 正在运行，您应能够运行简单的 R 和 Python 脚本，以验证外部脚本的运行时可以与 SQL Server 进行通信。

   打开一个新**查询**窗口中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后运行如下所示的脚本：
    
    + 适用于 R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + 用于 Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

 **结果**

    该脚本可以需要一段时间来首次运行外部脚本运行时加载。 结果应类似于此：

    | Hello |
    |----|
    | 1|


> [!NOTE]
> 在 Python 脚本中使用的标题或列不会返回，通过设计。 若要添加为自己的输出列名称，必须指定返回的数据集的架构。 执行此操作使用 WITH RESULTS 参数的存储过程，命名列和指定的 SQL 数据类型。
> 
> 例如，可以添加以下行以生成任意列名称： `WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

我们建议将最新的累积更新应用到数据库引擎和机器学习组件。

在连接 internet 的设备上通常可通过 Windows 更新应用累积更新，但还可以使用以下步骤，受控的更新。 当在应用于数据库引擎更新时，安装程序中取出同一实例安装任何 R 或 Python 功能的累积的更新。 

断开连接的服务器上执行额外的步骤是必需的。 有关详细信息，请参阅[在没有 internet 访问权限的计算机上安装 > 应用累积更新](sql-ml-component-install-without-internet-access.md#apply-cu)。

1. 开始使用已安装的基线实例： SQL Server 2017 初始版本

2. 转到累积更新列表： [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 选择最新的累积更新。 可执行文件是自动下载并提取。

4. 运行安装程序。 接受许可条款，然后在功能选择页上，查看为其应用累积更新的功能。 应会看到每一项功能为当前实例，包括机器学习功能安装。 安装程序将下载更新的所有功能所必需的 CAB 文件。

  ![](media/cumulative-update-feature-selection.png)

5. 继续完成向导，接受 R 和 Python 分发版的许可条款。 

## <a name="additional-configuration"></a>其他配置

如果外部脚本执行验证步骤是否成功，你可以从 SQL Server Management Studio、 Visual Studio Code 中或可以向服务器发送 T-SQL 语句的任何其他客户端运行 R 或 Python 命令。

如果你在运行命令时收到错误，，查看此部分中的其他配置步骤。 您可能需要对服务或数据库进行相应的其他配置。

在实例级别，可能包括其他配置：

* [SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

在数据库中，则可能需要以下配置更新：

* [授予用户对 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)
* [将 SQLRUserGroup 添加为数据库用户](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> 是否需要其他配置取决于您在安装 SQL Server，以及希望用户可以连接到数据库并运行外部脚本的安全架构。

## <a name="suggested-optimizations"></a>建议的优化

现在，所有工作已经完成，你可能还想要优化服务器以支持机器学习中，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果希望有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../administration/modify-user-account-pool.md)。

### <a name="optimize-the-server-for-script-execution"></a>优化用于执行脚本的服务器

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序旨在优化的各种数据库引擎，这可能包括提取、 转换和加载 (ETL) 进程、 报告、 审核所支持的服务的服务器的余额和使用的应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。 因此，默认设置下，可能会发现为机器学习的资源的有时限制或受限制，尤其是在占用大量内存的操作。

若要确保机器学习作业的优先级别并其分配相应资源，我们建议使用 SQL Server 资源调控器配置外部资源池。 您可能还需要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库的保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过启动的 R 帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，请参阅[修改机器学习的用户帐户池](../administration/modify-user-account-pool.md)。

如果您使用的标准版，但没有资源调控器，可以使用动态管理视图 (Dmv) 和扩展事件，以及 Windows 事件监视来帮助管理服务器资源。 有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)并[监视和管理 Python 服务](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建 R 解决方案可以调用基本 R 函数，函数从 SQL Server 一起安装的专属包和第三方 R 包与 SQL Server 安装的开放源代码 R 版本兼容。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果必须单独安装 R 的计算机上，或包安装到用户库，你将无法使用 T-SQL 中的这些包。

不同 SQL Server 2016 和 SQL Server 2017 中安装和管理 R 包的过程。 在 SQL Server 2016 中，数据库管理员必须安装 R 包，用户需要。 在 SQL Server 2017 中，可以设置用户组共享每个数据库级别上的包或配置数据库角色，以使用户能够安装其自己的包。 有关详细信息，请参阅[在 SQL Server 中安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。


## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
