---
title: 安装 SQL Server 2017 机器学习在 Windows 上的服务 （数据库） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b2c699a76d0a24bade258109fcee40e9e1f39a7d
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093321"
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>安装 SQL Server 2017 机器学习在 Windows 上的服务 （数据库） 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 的机器学习服务组件将添加数据库中的预测分析、 统计分析、 可视化和机器学习算法。 函数库可在 R 和 Python 中，并作为外部脚本的数据库引擎实例上运行。 

此文章介绍了如何通过运行安装机器学习组件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导和以下屏幕上的提示。

## <a name="bkmk_prereqs"> </a> 预安装清单

+ 如果你想要使用 R、 Python 或这两种语言支持安装机器学习服务，则需要 SQL Server 2017 安装程序。 如果改为您具有 SQL Server 2016 安装介质，则可以安装[SQL Server 2016 R Services （数据库内）](sql-r-services-windows-install.md)获取 R 语言支持。

+ 数据库引擎实例是必需的。 您不能安装 R 或 Python 功能，尽管将它们添加到现有实例的以增量方式。

+ 不要在故障转移群集上安装机器学习服务。 用于隔离 R 和 Python 进程的安全机制不兼容与 Windows Server 故障转移群集环境。

+ 不要在域控制器上安装机器学习服务。 安装程序的机器学习服务部分将会失败。

+ 不安装**共享功能** > **Machine Learning Server （独立版）** 同一台计算机上运行的数据库实例。 独立服务器将争夺相同的资源，从而破坏这两个安装的性能。

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

## <a name="restart-the-service"></a>重新启动服务。

安装完成后下, 一步，启用脚本执行在继续之前重新启动数据库引擎。

此外会自动重新启动 ervice 重启相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

可以使用右键单击该服务重新启动**重新启动**命令，以在 SSMS 中，或使用的实例进行**Services**面板在控制面板中，或通过使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>启用外部脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 可以下载并安装适当版本，在此页中：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 您还可以试用的预览版本[SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)，它支持管理任务和针对 SQL Server 的查询。
  
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

4. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 此外会自动重新启动 SQL Server 服务重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

    可以使用右键单击该服务重新启动**重新启动**命令，以在 SSMS 中，或使用的实例进行**Services**面板在控制面板中，或通过使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>验证安装

使用以下步骤来验证用于启动外部脚本的所有组件正在都运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。
    
2. 打开**Services**面板或 SQL Server 配置管理器，并验证是否**SQL Server Launchpad 服务**正在运行。 应具有一项服务的每个数据库引擎实例具有 R 或 Python 安装。 如果未运行，重新启动服务。 有关详细信息，请参阅[组件来支持 Python 集成](../python/new-components-in-sql-server-to-support-python-integration.md)。 
   
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
    | @shouldalert|


> [!NOTE]
> 在 Python 脚本中使用的标题或列不会返回，通过设计。 若要添加为自己的输出列名称，必须指定返回的数据集的架构。 执行此操作使用 WITH RESULTS 参数的存储过程，命名列和指定的 SQL 数据类型。
> 
> 例如，可以添加以下行以生成任意列名称： `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>其他配置

如果外部脚本执行验证步骤是否成功，你可以从 SQL Server Management Studio、 Visual Studio Code 中或可以向服务器发送 T-SQL 语句的任何其他客户端运行 Python 命令。

如果你在运行命令时收到错误，，查看此部分中的其他配置步骤。 您可能需要对服务或数据库进行相应的其他配置。

需要进行其他更改的常见方案包括：

* [配置 Windows 防火墙以允许入站连接](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [将内置权限扩展到远程用户](#bkmk_configureAccounts)
* [授予运行外部脚本的权限](#permissions-external-script)
* [授予对单个数据库访问权限](#permissions-db)

> [!NOTE]
> 并非所有列出的更改是必需的并无可能要求。 要求取决于您在安装 SQL Server，以及希望用户可以连接到数据库并运行外部脚本的安全架构。 其他故障排除提示可在此处找到：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> 启用为 Launchpad 帐户组的隐式身份验证

在安装期间，已创建一些新的 Windows 用户帐户，用于运行 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务的安全令牌下的任务。 当用户从外部客户端，发送的 Python 或 R 脚本时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]激活可用的工作帐户。 然后它将其映射到调用用户的标识，并运行代表用户的脚本。

这称为*隐式身份验证*，和是数据库引擎的服务。 此服务在 SQL Server 2016 和 SQL Server 2017 支持的外部脚本的安全执行。

可以在 Windows 用户组“SQLRUserGroup” 中查看这些账户。 默认情况下，会创建 20 个辅助角色帐户，这通常是足以用于运行外部脚本作业。

> [!IMPORTANT]
> 名为辅助角色组**SQLRUserGroup**无论是否安装 R 或 Python。 没有一个组中的，每个实例。

如果您需要从远程数据科学客户端，运行脚本并使用 Windows 身份验证，有一些其他注意事项。 必须授予这些辅助角色帐户登录的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表你的实例。

1. 在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器中，展开**安全**。 然后右键单击**登录名**，然后选择**新的登录名**。
2. 在中**登录名-新建**对话框中，选择**搜索**。
3. 选择**对象类型**，然后选择**组**。 清除其他所有内容。
4. 在中**输入要选择的对象名称**，类型*SQLRUserGroup*，然后选择**检查名称**。
5. 解析与实例的 Launchpad 服务关联的本地组名称，它应类似于 *instancename\SQLRUserGroup*。 选择“确定”。
6. 默认情况下，组分配给**公共**角色，以及是否有权连接到数据库引擎。
7. 选择“确定”。

> [!NOTE]
> 如果您使用**SQL 登录名**对于在 SQL Server 计算上下文中运行脚本，不需要此额外步骤。

### <a name="permissions-external-script"></a> 向用户授予权限来运行外部脚本

如果您安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您和您自己在你自己的实例中运行 R 或 Python 脚本，通常以管理员身份执行脚本。 因此，各种操作和数据库中的所有数据具有隐式权限。

大多数用户，但是，没有此类提升的权限。 例如，使用 SQL 登录名访问数据库通常在组织中的用户不具有提升的权限。 因此，对于每个用户都使用 R 或 Python，则必须授予用户的机器学习服务将使用的语言中的每个数据库运行外部脚本的权限。 以下是操作方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 权限不特定于支持的脚本语言。 换而言之，没有与 Python 脚本的 R 脚本的单独的权限级别。 如果您需要保持对这些语言的单独权限，在单独的实例上安装 R 和 Python。

### <a name="permissions-db"></a> 对其授予用户读取、 写入或数据定义语言 (DDL) 权限的数据库

在用户运行脚本时，用户可能需要从其他数据库读取数据。 用户可能还需要创建新表以存储结果，并将数据写入到表。

对于每个 Windows 用户帐户或 SQL 登录名运行 R 或 Python 脚本，请确保它对特定数据库具有适当的权限： `db_datareader`， `db_datawriter`，或`db_ddladmin`。

例如，以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，为提供的 SQL 登录名*MySQLLogin*中运行 T-SQL 查询的权限*ML_Samples*数据库。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

有关每个角色中包括的权限的详细信息，请参阅[数据库级别角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源

您可以创建的机器学习数据科学客户端计算机上的解决方案。 如果需要通过使用 SQL Server 计算机作为计算上下文中运行代码，可以使用两个选项： 使用 SQL 登录名访问该实例或通过使用 Windows 帐户。

+ 对于 SQL 登录名： 确保该登录名读取数据的数据库具有适当的权限。 您可以执行此操作通过添加*连接到*并*选择*权限，或通过添加到该登录名`db_datareader`角色。 若要创建的对象，将分配`DDL_admin`权限。 如果必须将数据保存到表中，将添加到`db_datawriter`角色。

+ 为 Windows 身份验证： 你可能需要指定实例名称和其他连接信息的数据科学客户端上创建 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建议的优化

现在，所有工作已经完成，你可能还想要优化服务器以支持机器学习中，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果希望有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="optimize-the-server-for-script-execution"></a>优化用于执行脚本的服务器

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序旨在优化的各种数据库引擎，这可能包括提取、 转换和加载 (ETL) 进程、 报告、 审核所支持的服务的服务器的余额和使用的应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。 因此，默认设置下，可能会发现为机器学习的资源的有时限制或受限制，尤其是在占用大量内存的操作。

若要确保机器学习作业的优先级别并其分配相应资源，我们建议使用 SQL Server 资源调控器配置外部资源池。 您可能还需要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库的保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过启动的 R 帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，请参阅[修改机器学习的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用的标准版，但没有资源调控器，可以使用动态管理视图 (Dmv) 和扩展事件，以及 Windows 事件监视来帮助管理服务器资源。 有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)并[监视和管理 Python 服务](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建 R 解决方案可以调用基本 R 函数，从装有 SQL Server 和第三方开放源代码 R SQL Server 安装的版本兼容的 R 包 properietary packes 函数。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果必须单独安装 R 的计算机上，或包安装到用户库，你将无法使用 T-SQL 中的这些包。

不同 SQL Server 2016 和 SQL Server 2017 中安装和管理 R 包的过程。 在 SQL Server 2016 中，数据库管理员必须安装 R 包，用户需要。 在 SQL Server 2017 中，可以设置用户组共享每个数据库级别上的包或配置数据库角色，以使用户能够安装其自己的包。 有关详细信息，请参阅[在 SQL Server 中安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。


## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查的实例的安装状态并解决常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
