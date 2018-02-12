---
title: "安装和配置 Python 机学习服务 |Microsoft 文档"
ms.custom: 
ms.date: 12/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 9ecd54dcb1fe829c51e0e05346abf04d80af3cf9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="set-up-python-machine-learning-services-in-database"></a>设置 Python 机器学习服务 （数据库）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本文介绍如何安装 Python 通过运行所需的组件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导中，并按照交互式提示。

## <a name="machine-learning-options-in-sql-server-setup"></a>机器学习中 SQL Server 安装程序选项

选择**机器学习服务**功能，并选择**Python**为语言。

**共享功能**部分包含一个单独的安装选项，**机器学习 Server （独立）**。 此选项不具有 SQL Server，或不需要的 SQL Server 计算上下文使用的服务器上支持操作化的 Python 代码。 因此，我们建议你*不这样做*安装此客户端在与 SQL Server 实例在同一台计算机上。 相反，在单独的计算机上安装机器学习 Server （独立）。

安装完成后，重新配置以允许使用外部的可执行文件的脚本执行的实例。 你可能需要进行其他更改到服务器以支持机器学习工作负荷。 配置更改通常需要重新启动实例或重新启动快速启动板服务。

### <a name="prerequisites"></a>必要條件

+ SQL Server 2017 是必需的。 在以前版本的 SQL Server 上不支持 Python 集成。
+ 请务必安装数据库引擎。 运行 Python 脚本数据库中需要的 SQL Server 实例。
+ Python 组件安装的一部分安装必备组件。
+ 不能与故障转移群集上的 Python 服务安装机器学习。 隔离 Python 进程使用的安全机制不与 Windows Server 故障转移群集环境兼容。
   
  一种解决方法，你可以使用复制将必要的表复制到使用 Python 服务的独立 SQL Server 实例。 或者，你可以与使用 AlwaysOn 设置中，并且是可用性组的一部分的独立计算机上的 Python 服务安装机器学习。

+ 可能的与其他版本的 Python 通过并行安装是因为 SQL Server 实例使用其自己的 Anaconda 分发副本。 但是，运行 SQL Server 外部 SQL Server 计算机使用 Python 的代码可能导致各种问题：
    
    - 你使用不同的库和不同的可执行文件，并获取不同的结果，不是你在 SQL Server 中运行时执行的操作。
    - 不能由 SQL Server，从而导致资源争用管理外部库中运行的 Python 脚本。
  
> [!IMPORTANT]
> 安装程序完成后，请务必完成本文中所述的其他后配置步骤。 这些步骤包括启用 SQL Server 以使用外部脚本和添加 SQL Server 以你的名义运行 Python 作业所需的帐户。

### <a name="unattended-installation"></a>无人参与的安装

若要执行无人参与的安装，使用 SQL Server 安装程序和特定于 Python 的自变量的命令行选项。 有关详细信息，请参阅[无人参与安装的 SQL Server 的 Python 机器学习服务](unattended-installs-of-sql-server-python-services.md)。

##  <a name="bkmk_installPythonInDatabase"></a>步骤 1： 安装机器学习 SQL 服务器上的服务 （数据库）

1. 运行 SQL Server 2017 年 1 安装向导。
  
2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

    ![安装 Python 数据库中](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在“功能选择”  页上，选择以下选项：
  
    -   **数据库引擎服务**
  
         若要使用 SQL Server Python，必须安装数据库引擎的实例。 你可以使用默认或命名的实例。
  
    -   **机器学习服务 （数据库）**
  
         此选项将安装支持 Python 脚本执行的数据库服务。

    -   **Python**选中此选项以获取 Python 3.5 可执行文件并选择从 Anaconda 分发的库。 安装每个实例只有一个语言。
        
        ![功能用于 Python](media/ml-svcs-features-python-highlight.png "的设置选项 Python")

        > [!NOTE]
        > 
        > 未选择的选项**机器学习 Server （独立）**。 此选项以安装下的机器学习服务器**共享功能**适用于在单独的计算机上使用。 例如，你可能想要安装相同版本的机器学习用于项目开发，例如数据科研人员的便携式计算机的其他计算机上的组件。

4. 上**同意安装 Python**页上，选择**接受**。
  
     下载 Python 可执行文件、 从 Anaconda Python 包需要此许可协议。
     
     ![Python 许可证协议](media/ml-svcs-license-python.png "许可协议的 Python")
  
    > [!NOTE]
    >  如果你使用的计算机没有 internet 访问权限，您可以暂停安装程序在此时进行单独下载安装程序。 有关详细信息，请参阅[安装没有 internet 访问权限的组件](../r/installing-ml-components-without-internet-access.md)。
  
     选择**接受**，请等待，直到**下一步**按钮将变为活动状态，，然后选择**下一步**。
  
5. 上**已准备好安装**页上，验证这些选择都包括在内，然后选择**安装**。
  
     + 数据库引擎服务
     + 机器学习服务（数据库内）
     + Python
  
    这些选择代表使用 Python 与所需的最小配置[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。
    
    ![准备好安装 Python](media/ready-to-install-python.png "Python 安装所需组件")

    （可选），记下的路径下的文件夹位置`..\Setup Bootstrap\Log`存储配置文件。 安装程序完成后，你可以查看摘要文件中的已安装的组件。

6. 安装完成后，重启计算机。

##  <a name="bkmk_enableFeature"></a>步骤 2： 启用执行 Python 脚本

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 你可以下载并安装在此页中的相应版本：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 你还可以试用的预览版本[SQL 操作 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)，它支持管理任务和针对 SQL Server 查询。
  
2. 连接到安装机器学习服务的实例并运行以下命令：

   ```SQL
   sp_configure
   ```

    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为默认情况下关闭功能。 你可以运行 R 或 Python 脚本之前，必须由管理员显式启用该功能。
    
3.  若要启用外部脚本功能，可支持 Python，运行以下语句：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果已启用 R 语言功能，如果不是通过运行第二次重新配置 Python。 基础的扩展性平台支持这两种语言。

4. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 此外会自动重新启动 SQL Server 服务重启相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

    可以通过重新启动服务**服务**面板在 Control Panel 中，或使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。

## <a name="step-3-verify-that-the-external-script-execution-feature-is-running"></a>步骤 3： 验证的外部脚本执行功能正在运行

需要一段时间来验证用于启动 Python 脚本的所有组件正在都运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。
    
2. 打开**服务**面板或 SQL Server 配置管理器，并验证你的实例的快速启动板服务正在运行。 如果未运行快速启动板，重新启动服务。
  
    如果已安装多个 SQL Server 实例，具有 R 或 Python 启用任何实例都有其自己的快速启动板服务。

    如果你安装 R 和 Python 的单个实例上，安装只有一个快速启动板。 为每种语言添加单独的、 特定于语言的启动器 DLL。 有关详细信息，请参阅[组件来支持 Python 集成](new-components-in-sql-server-to-support-python-integration.md)。 
   
3. 如果正在快速启动板，你应能够运行类似中的以下简单的 Python 脚本[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'OutputDataSet = InputDataSet',
    @input_data_1 = N'SELECT 1 AS col'
    ```
    
    **结果**
    
    *<code>&nbsp;&nbsp;</code>* *1*

> [!NOTE]
> 列或 Python 脚本中使用的标题将不返回，设计使然。 若要添加你的输出的列名称，必须指定返回的数据集的架构。 执行此操作使用存储的过程中，命名列和指定的 SQL 数据类型的与结果参数。
> 
> 例如，你可以添加以下行以生成任意列名称：`WITH RESULT SETS ((Col1 AS int))`

## <a name="step-4-additional-configuration"></a>步骤 4： 其他配置

如果前一个命令成功，你可以从 SQL Server Management Studio、 Visual Studio 代码或可以向服务器发送的 T-SQL 语句的任何其他客户端运行 Python 命令。

如果你在运行命令时收到错误，，查看下面的列表。 你可能需要对服务或数据库进行其他适当的配置。

> [!NOTE]
> 
> 并非所有列出的更改是必需的且无可能需要。 要求取决于安全架构，安装 SQL Server，以及希望用户连接到数据库和运行外部脚本的位置。

###  <a name="bkmk_configureAccounts"></a>启用快速启动板帐户组的隐式身份验证

在安装期间，已创建一些新的 Windows 用户帐户，用于运行 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务的安全令牌下的任务。 当用户从外部客户端，发送 Python 或 R 脚本时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]激活可用的工作帐户。 然后将其映射到的调用用户的标识，并运行代表用户的脚本。

这称为*默示身份验证*，和是数据库引擎的服务。 此服务中 SQL Server 2016 和 SQL Server 2017 支持安全的外部脚本的执行。

可以在 Windows 用户组“SQLRUserGroup” 中查看这些账户。 默认情况下，被创建 20 工作人员帐户，这通常是绰绰有余用于运行外部脚本的作业。

> [!IMPORTANT]
> 名为辅助角色组**SQLRUserGroup**无论你安装 R 或 Python。 没有为每个实例的单个组。

如果你需要从远程数据科学客户端，运行脚本，且正在使用 Windows 身份验证，有一些其他注意事项。 这些辅助帐户必须有权登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表你的实例。

1. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器中，展开**安全**。 然后右键单击**登录名**，然后选择**新登录名**。
2. 在**登录名-新建**对话框中，选择**搜索**。
3. 选择**对象类型**，然后选择**组**。 清除其他所有内容。
4. 在**输入要选择的对象名称**，类型*SQLRUserGroup*，然后选择**检查名称**。
5. 解析与实例的 Launchpad 服务关联的本地组名称，它应类似于 *instancename\SQLRUserGroup*。 选择“确定”。
6. 默认情况下，组分配给**公共**角色，并且有权连接到数据库引擎。
7. 选择“确定”。

> [!NOTE]
> 如果你使用**SQL 登录名**对于在 SQL Server 计算上下文中运行脚本，不需要此额外步骤。

### <a name="give-users-permission-to-run-external-scripts"></a>授予用户运行外部脚本的权限

如果你安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你自己，以及你自己的实例中运行 Python 脚本，你通常以管理员身份执行脚本。 这样，你便可以隐式权限通过各种操作和数据库中的所有数据。

大多数用户来说，但是，没有此类提升的权限。 例如，使用 SQL 登录名来访问数据库通常在组织中的用户不具有提升的权限。 因此，对于每个用户都使用 Python，你必须授予机器学习服务的用户权限来使用 Python 的位置在每个数据库运行外部脚本。 以下是操作方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 权限并不特定于受支持的脚本语言。 换而言之，具有不与 Python 脚本的 R 脚本的单独的权限级别。 如果你需要保持对这些语言的单独权限，在单独的实例上安装 R 和 Python。

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>对其授予用户读取、 写入或数据定义语言 (DDL) 权限数据库

在用户运行脚本时，用户可能需要从其他数据库中读取数据。 用户可能还需要创建新表以存储结果，并将数据写入表。

对于每个 Windows 用户帐户或 R 或 Python 脚本运行的 SQL 登录名中，确保它具有特定的数据库的适当的权限： `db_datareader`， `db_datawriter`，或`db_ddladmin`。

例如，以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，为提供的 SQL 登录名*MySQLLogin*中运行 T-SQL 查询的权限*ML_Samples*数据库。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

有关每个角色中包含的权限的详细信息，请参阅[数据库级角色](../../relational-databases/security/authentication-access/database-level-roles.md)。

### <a name="ensure-that-the-sql-server-installation-supports-remote-connections"></a>确保 SQL Server 安装支持远程连接

如果你无法从远程计算机连接，请检查防火墙是否允许访问 SQL Server。 在默认安装中，可能会禁用远程连接，或使用 SQL Server 的特定端口可能会被防火墙阻止。 有关详细信息，请参阅[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源

你可以创建机器学习数据科学客户端计算机上的解决方案。 如果你需要通过使用 SQL Server 计算机作为计算上下文来运行代码，则有两个选项： 通过使用 SQL 登录名，访问实例或通过使用 Windows 帐户。

+ 为 SQL 登录名： 确保该登录名在其中您正在读取数据的数据库上具有适当权限。 你可以执行此操作通过添加*连接到*和*选择*权限，或通过添加登录到`db_datareader`角色。 若要创建对象，将分配`DDL_admin`权限。 如果必须将数据保存到表中，将添加到`db_datawriter`角色。

+ 对于 Windows 身份验证： 你可能需要在指定实例名称和其他连接信息的数据科学客户端上创建 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="additional-optimizations"></a>额外的优化

现在，你已使用的所有内容，你可能还想要优化的服务器以支持机器学习中，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果希望多个用户以会同时运行脚本，则可以增加分配给快速启动板服务的工作帐户数。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="optimize-the-server-for-script-execution"></a>优化的服务器脚本执行

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序优化各种服务的服务器的余额。 这些服务包括 ETL 进程、 reporting、 审核和应用程序使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。

如果你使用默认设置，你可能会发现有关运行外部脚本的资源限制，或限制，尤其是在内存密集型操作。 机器学习是优先级，如果更改默认数据库设置，以确保外部脚本作业优先级别，并可相应资源。 这些更改可以包括：

+ 减少分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎。
+ 增加的数量帐户下运行[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。 这不会增加资源，数，但不会增加的可以同时运行的脚本的数量。

如果你有 SQL Server Enterprise Edition 时，使用资源调控器 for Python 中配置的外部资源池。 有关详细信息，请参阅以下文章：

-   配置用于管理外部资源的资源池
  
     [创建外部资源池 (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
  
-   更改为数据库引擎保留的内存量
  
     [服务器内存服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
  
-   更改可以通过启动的辅助帐户数 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
     [为 SQL Server R Services 中修改用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)

如果你使用 SQL Server Standard Edition，并且没有资源调控器，可以使用动态管理视图和扩展的事件来帮助你管理服务器资源。 你还可以使用 Windows 事件监视为此目的。 有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="upgrade-the-machine-learning-components"></a>升级机器学习组件

通过使用 SQL Server 2017 安装机器学习服务时，你在已发布的发行版本时获得的组件的版本。 修补或升级的 SQL Server 实例，每次机器学习组件将同时升级。

你可以升级机器学习不支持的方式更快的定期的组件通过 SQL Server 版本中，通过安装 Microsoft 机器学习 Server。 执行此操作时，你还获得如在机器学习服务器的最新版本中受支持的任何新功能：

+ 更新的 Python 包[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[for Python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。
+ [预先训练模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)对图像分类和文本分析。

有关如何升级实例的信息，请参阅[升级 R 组件通过绑定](..\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="tutorials"></a>教程

请参阅以下教程： 你可以如何使用 Python 与 SQL Server 以生成并部署计算机学习解决方案的一些示例：

[在 T-SQL 中使用 Python](../tutorials/run-python-using-t-sql.md)

[创建使用 revoscalepy 的 Python 模型](../tutorials/use-python-revoscalepy-to-create-model.md)
