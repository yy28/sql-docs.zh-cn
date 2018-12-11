---
title: 安装 SQL Server 2016 R Services （数据库） |Microsoft Docs
description: 当在 Windows 上安装 SQL Server 2016 R Services，SQL Server 中的 R 才可用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f4ba4e28a17b0a025b48d41b077d4a536a9be8e9
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878120"
---
# <a name="install-sql-server-2016-r-services"></a>安装 SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何安装和配置**SQL Server 2016 R Services**。如果您有SQL Server 2016，请安装此功能以在SQL Server中执行R代码。

在SQL Server 2017中，在[机器学习服务](../r/r-server-standalone.md)中提供了R集成，体现了Python的添加。如果您想要集成R并拥有SSQL Server 2017安装介质，请参见I[安装 SQL Server 2017 机器学习服务](sql-machine-learning-services-windows-install.md)添加该功能。 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>预安装清单

+ 需要数据库引擎实例。您不能只安装R，尽管可以将其逐步添加到现有实例。 

+ 不要在故障转移群集上安装R服务。用于隔离R进程的安全机制与Windows Server故障转移群集环境不兼容。

+ 不要在域控制器上安装R服务。设置的R服务部分将失败。

+ 不要在运行数据库内实例的同一台计算机上安装**共享功能** > **R Server （独立版）**。

   可以与其他版本的R和Python并行安装，因为SQL Server实例使用自己的开源R和Anaconda发行版的副本。但是，在SQL Server外部的SQL Server计算机上运行使用R和Python的代码可能会导致各种问题：

  + 与在SQL Server中运行时相比，您使用不同的库和不同的可执行文件，并获得不同的结果。
  + SQL Server无法管理在外部库中运行的R和Python脚本，从而导致资源争用。
  
如果您使用任何早期版本的Revolution Analytics开发环境或RevoScaleR软件包，或者您安装了SQL Server 2016的任何预发行版本，则必须将其卸载。不支持运行较旧版本的RevoScaleR和其他专有软件包。有关删除以前版本的帮助，请参阅[SQL Server机器学习服务的升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安装完成后，请确保完成本文中描述的其他配置后步骤。这些步骤包括使SQL Server能够使用外部脚本，以及为SQL Server添加代表您运行R作业所需的帐户。配置更改通常需要重新启动实例，或者重新启动Launchpad服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 安装向导。

2. 在**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。
    
   ![安装 R Services （数据库内）](media/2016-setup-installation-rsvcs.png "启动数据库引擎的安装与 R 服务")
   
3. 在**功能选择**页面上，选择以下选项：

   - 选择**数据库引擎服务**。每个使用机器学习的实例都需要数据库引擎。
   - 选择**R Services （数据库内）**。安装支持数据库内使用R。
    
     ![R Services 功能选择](media/2016setup-rsvcs-features.png "选择这些功能的 R Services 中的数据库")

    > [!IMPORTANT]
    > 不要同时安装R Server和R Services。您通常会安装R Server（独立）来创建数据科学家或开发人员用来连接SQL Server和部署R解决方案的环境。因此，无需在同一台计算机上安装两者。

4.  在**同意安装 Microsoft R Open**页上，单击**接受**。
  
    需要此许可协议才能下载Microsoft R Open，其中包括开源R基础软件包和工具的分发，以及Microsoft R开发团队的增强R软件包和连接提供程序。
   
5. 接受许可协议后，安装程序准备就绪时会暂停一下。按钮可用时单击**下一步**。

6. 在**已准备好安装**页上，验证是否包含以下项，然后选择**安装**。

   + 数据库引擎服务
   + R Services（数据库内）

    请注意路径下的文件夹位置`..\Setup Bootstrap\Log`存储配置文件的位置。安装完成后，您可以在摘要文件中查看已安装的组件。

7. 安装完成后，如果指示您重新启动计算机，请立即重启。安装完成后，阅读安装向导中的消息非常重要。有关更多信息，请参阅[View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>启用脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 您可以从此页面下载并安装相应的版本：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 您还可以试用A[Azure Data Studio](../../azure-data-studio/what-is.md)的预览版，它支持针对SQL Server的管理任务和查询。
  
2. 连接到安装了机器学习服务的实例，单击**新建查询**以打开查询窗口，然后运行以下命令：

   ```SQL
   sp_configure
   ```
   `external scripts enabled` 的属性值目前应为 **0**。 这是因为默认情况下该功能已关闭。在运行R或Python脚本之前，必须由管理员明确启用该功能。
   
3. 若要启用外部脚本编写功能，请运行以下语句：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新启动服务。

安装完成后，重新启动数据库引擎，然后继续执行下一步，启用脚本执行。

重新启动该服务还会自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

您可以使用SSMS中实例的右键单击**重新启动**命令，或使用“控制面板”中的“服务”面板或使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).重新启动服务。

## <a name="verify-installation"></a>验证安装

使用[自定义报告](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。检查实例的安装状态。


使用以下步骤验证用于启动外部脚本的所有组件是否正在运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。

2. 打开**Services**面板或SQL Server配置管理器，并验证**SQL Server Launchpad 服务**是否正在运行。对于安装了R或Python的每个数据库引擎实例，您应该有一个服务。有关该服务的更多信息，请参阅[可扩展性框架](../concepts/extensibility-framework.md)。

7. 如果Launchpad正在运行，您应该能够运行简单的R来验证外部脚本运行时是否可以与SQL Server通信。

    在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中打开一个新的**查询**窗口，然后运行如下脚本：
 
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
    第一次加载外部脚本运行时，脚本可能需要一段时间才能运行。结果应该是这样的：    

    | Hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

我们建议将最新的累积更新应用到数据库引擎和机器学习组件。

在连接Internet的设备上，通常通过Windows Update应用累积更新，但您也可以使用以下步骤进行受控更新。应用数据库引擎的更新时，安装程序会为您在同一实例上安装的R库提取累积更新。 

在断开连接的服务器上，需要额外的步骤。有关更多信息，请参见[在没有 internet 访问权限的计算机上安装 > 应用累积更新](sql-ml-component-install-without-internet-access.md#apply-cu)。。
在断开连接的服务器上，需要额外的步骤有关详细信息，请参阅在无法访问Internet的计算机上安装>应用累积更新。

1. 从已安装的基准实例开始：SQL Server 2016初始版本，SQL Server 2016 SP 1或SQL Server 2016 SP 2。

2. 转到累积更新列表： [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 选择最新的累积更新。自动下载并提取可执行文件。

4. 运行安装程序。接受许可条款，然后在功能选择页面上，查看应用累积更新的功能。您应该看到为当前实例安装的每个功能，包括R服务。安装程序会下载更新所有功能所需的CAB文件。


5. 继续完成向导，接受R分发的许可条款。

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>其他配置

如果外部脚本验证步骤成功，则可以从SQL Server Management Studio，Visual Studio代码或可以向服务器发送T-SQL语句的任何其他客户端运行Python命令。

如果在运行命令时出错，请查看本节中的其他配置步骤。您可能需要对服务或数据库进行其他适当的配置。

在实例级别，可能包括其他配置：

* [SQL Server 机器学习服务的防火墙配置](../../advanced-analytics/security/firewall-configuration.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

在数据库中，则可能需要以下配置更新：

* [授予用户对 SQL Server 机器学习服务的权限](../../advanced-analytics/security/user-permission.md)
* [将 SQLRUserGroup 添加为数据库用户](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> 并非所有列出的更改都是必需的，可能不需要任何更改。要求取决于您的安全架构，安装SQL Server的位置以及您希望用户如何连接到数据库并运行外部脚本。可在此处找到其他疑难解答提示：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>建议的优化

现在您已经完成了所有工作，您可能还希望优化服务器以支持机器学习，或者安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果您认为可能会大量使用R，或者您希望很多用户同时运行脚本，则可以增加分配给Launchpad服务的工作人员帐户的数量。有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../administration/modify-user-account-pool.md)。

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>优化执行外部脚本的服务器

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序的默认设置旨在针对数据库引擎支持的各种服务优化服务器的平衡，这些服务可能包括提取、转换和加载(ETL)流程、报告、审计以及使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据的应用程序。因此，在默认设置下，您可能会发现机器学习的资源有时会受到限制或受限制，尤其是在内存密集型操作中。


为了确保机器学习作业的优先级和资源适当，我们建议您使用SQL Server资源调控器来配置外部资源池。您可能还希望更改分配给[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎的内存量，或者增加在[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务下运行的帐户数。

若要确保机器学习作业的优先级别并其分配相应资源，我们建议使用 SQL Server 资源调控器配置外部资源池。 您可能还需要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]启动的 R 帐户数量，请参阅[修改机器学习的用户帐户池](../administration/modify-user-account-pool.md)。

如果您使用的是Standard Edition并且没有资源调控器，则可以使用动态管理视图（DMV）和扩展事件以及Windows事件监视来帮助管理R使用的服务器资源。有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

您为SQL Server创建的R解决方案可以调用基本R函数，与SQL Server一起安装的专有软件包中的函数，以及与SQL Server安装的开源R版本兼容的第三方R软件包。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果在计算机上单独安装R，或者将软件包安装到用户库，则无法使用T-SQL中的这些软件包。


在SQL Server 2016和SQL Server 2017中，安装和管理R软件包的过程是不同的。在SQL Server 2016中，数据库管理员必须安装用户需要的R软件包。在SQL Server 2017中，您可以设置用户组以在每个数据库级别上共享包，或者配置数据库角色以使用户能够安装自己的包。有关更多信息，请参阅[安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
