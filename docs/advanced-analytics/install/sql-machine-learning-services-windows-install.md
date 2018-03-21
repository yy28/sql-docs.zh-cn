---
title: "安装 SQL Server 自 2017 年 1 机器学习在 Windows 上的服务 （数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 1904517351a23bfa736549a249d77be2932b3c07
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>安装 SQL Server 自 2017 年 1 机器学习在 Windows 上的服务 （数据库） 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 的计算机学习服务组件将添加数据库中预测分析、 统计分析、 可视化和机器学习算法。 函数库的 R 和 Python 提供了，并作为外部脚本的数据库引擎实例上运行。 

此文章介绍了如何通过运行安装机器学习组件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导中和以下屏幕上的提示。

## <a name="bkmk_prereqs"> </a> 预安装清单

+ SQL Server 2017 是必需的。 如果你有 SQL Server 2016，请安装[SQL Server 2016 R Services （数据库）](sql-r-services-windows-install.md)相反。

+ 数据库引擎实例是必需的。 无法安装仅 R 或 Python 功能，虽然你可以将它们添加以增量方式向现有实例。

+ 不要在故障转移群集上安装机器学习服务。 隔离 R 和 Python 的进程使用的安全机制不与 Windows Server 故障转移群集环境兼容。

+ 不要在域控制器上安装机器学习服务。 安装程序的机器学习服务部分将会失败。

+ 请不要安装**共享功能** > **机器学习 Server （独立）**同一台计算机上运行数据库中实例。 独立服务器会争用同一资源，从而损坏这两个安装的性能。

+ 支持但不是建议使用其他版本的 R 和 Python 的通过并行安装。 它支持，因为 SQL Server 实例使用其自己的开放源代码 R 和 Anaconda 分发版的副本。 但不是建议因为运行 SQL Server 外部 SQL Server 计算机使用 R 和 Python 的代码会导致各种问题：
    
  + 你使用不同的库和不同的可执行文件，并获取不同的结果，不是你在 SQL Server 中运行时执行的操作。
  + 不能由 SQL Server，从而导致资源争用管理外部库中运行的 R 和 Python 脚本。
  
> [!IMPORTANT]
> 安装程序完成后，请务必完成本文中所述的后配置步骤。 这些步骤包括启用 SQL Server 以使用外部脚本和添加 SQL Server 以你的名义运行 R 和 Python 作业所需的帐户。 配置更改通常需要重新启动实例或重新启动快速启动板服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2017 年 1 安装向导。 你可以下载 
  
2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

   ![安装机器学习服务数据库中](media/2017setup-installation-page-mlsvcs.PNG)
   
3. 在“功能选择”  页上，选择以下选项：
  
    -   **数据库引擎服务**
  
         若要使用 SQL Server R 和 Python，必须安装数据库引擎的实例。 你可以使用默认或命名的实例。
  
    -   **机器学习服务 （数据库）**
  
         此选项将安装支持 R 的数据库服务和 Python 脚本执行。

    -   **R**

        检查此选项以添加 Microsoft R 包、 解释器和开放源代码。 

    -   **Python**

        检查此选项以添加 Microsoft Python 包，Python 3.5 可执行文件，然后从 Anaconda 分发选择库。
        
        ![功能 R 和 Python 选项](media/2017setup-features-page-mls-rpy.png "的设置选项 Python")

        > [!NOTE]
        > 
        > 未选择的选项**机器学习 Server （独立）**。 此选项以安装下的机器学习服务器**共享功能**适用于在单独的计算机上使用。

4. 上**同意安装 R**页上，选择**接受**。 此许可协议涵盖 Microsoft R Open，其中包括的开放源代码 R 基程序包和工具，以及增强的 R 包和 Microsoft 开发团队的连接提供商的分布。

5. 上**同意安装 Python**页上，选择**接受**。 Python 开放源代码许可协议还介绍 Anaconda 和相关的工具，以及 Microsoft 开发团队的某些新的 Python 库。
     
     ![Python 许可证协议](media/2017setup-python-license.png "许可协议的 Python")
  
    > [!NOTE]
    >  如果你使用的计算机没有 internet 访问权限，您可以暂停安装程序在此时进行单独下载安装程序。 有关详细信息，请参阅[安装没有 internet 访问权限的机器学习组件](../install/sql-ml-component-install-without-internet-access.md)。
  
     选择**接受**，请等待，直到**下一步**按钮将变为活动状态，，然后选择**下一步**。
  
6. 上**已准备好安装**页上，验证这些选择都包括在内，然后选择**安装**。
  
    + 数据库引擎服务
    + 机器学习服务（数据库内）
    + R 和/或 Python

    记下的路径下的文件夹位置`..\Setup Bootstrap\Log`存储配置文件。 安装程序完成后，你可以查看摘要文件中的已安装的组件。

## <a name="restart-the-service"></a>重新启动服务。

安装完成后，重新启动数据库引擎，然后继续到下一行，启用脚本执行。

此外会自动重新启动 ervice 重启相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

你可以重新启动服务使用右击**重新启动**实例在 SSMS 中，或通过使用命令**服务**面板在 Control Panel 中，或使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>启用外部脚本执行

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 

    > [!TIP]
    > 你可以下载并安装在此页中的相应版本：[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
    > 
    > 你还可以试用的预览版本[SQL 操作 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)，它支持管理任务和针对 SQL Server 查询。
  
2. 连接到安装机器学习服务的实例，单击**新查询**来打开查询窗口中，并运行以下命令：

   ```SQL
   sp_configure
   ```

    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为默认情况下关闭功能。 你可以运行 R 或 Python 脚本之前，必须由管理员显式启用该功能。
    
3.  若要启用外部脚本功能，请运行以下语句：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    如果已启用 R 语言功能，如果不是通过运行第二次重新配置 Python。 基础的扩展性平台支持这两种语言。

4. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 此外会自动重新启动 SQL Server 服务重启相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

    你可以重新启动服务使用右击**重新启动**实例在 SSMS 中，或通过使用命令**服务**面板在 Control Panel 中，或使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>验证安装

使用以下步骤来验证用于启动外部脚本的所有组件正在都运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。
    
2. 打开**服务**面板或 SQL Server 配置管理器，并验证**SQL Server 快速启动板服务**正在运行。 你应具有一个包含 R 每个数据库引擎实例的服务或 Python 安装。 如果未运行，请重新启动服务。 有关详细信息，请参阅[组件来支持 Python 集成](../python/new-components-in-sql-server-to-support-python-integration.md)。 
   
3. 如果正在快速启动板，你应能够运行简单的 R 和 Python 脚本，以验证外部脚本的运行时可以与 SQL Server 通信。

   打开一个新**查询**中的窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后运行以下脚本：
    
    + R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + For Python
    
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

    该脚本时，会稍有若要运行，第一次请加载外部脚本运行。 结果应类似如下内容：

    | Hello |
    |----|
    | 1|


> [!NOTE]
> 列或 Python 脚本中使用的标题将不返回，设计使然。 若要添加你的输出的列名称，必须指定返回的数据集的架构。 执行此操作使用存储的过程中，命名列和指定的 SQL 数据类型的与结果参数。
> 
> 例如，你可以添加以下行以生成任意列名称： `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>其他配置

如果外部脚本执行验证步骤成功，你可以从 SQL Server Management Studio、 Visual Studio 代码或可以向服务器发送的 T-SQL 语句的任何其他客户端运行 Python 命令。

如果你在运行命令时收到错误，，查看此部分中的其他配置步骤。 你可能需要对服务或数据库进行其他适当的配置。

需要其他更改的常见方案包括：

* [配置 Windows 防火墙以便进行入站连接](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [将内置权限扩展到远程用户](#bkmk_configureAccounts)
* [授予的权限来运行外部脚本](#permissions-external-script)
* [授予对单个数据库访问权限](#permissions-db)

> [!NOTE]
> 并非所有列出的更改是必需的且无可能需要。 要求取决于安全架构，安装 SQL Server，以及希望用户连接到数据库和运行外部脚本的位置。 其他故障排除提示可在此处找到：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> 启用快速启动板帐户组的隐式身份验证

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

### <a name="permissions-external-script"></a> 向用户授予的权限来运行外部脚本

如果你安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你自己，以及你自己的实例中运行 R 或 Python 脚本，你通常以管理员身份执行脚本。 这样，你便可以隐式权限通过各种操作和数据库中的所有数据。

大多数用户来说，但是，没有此类提升的权限。 例如，使用 SQL 登录名来访问数据库通常在组织中的用户不具有提升的权限。 因此，对于 R 或 Python 使用每个用户，你必须授予机器学习服务的用户权限运行外部脚本在每个数据库将使用的语言。 以下是操作方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 权限并不特定于受支持的脚本语言。 换而言之，具有不与 Python 脚本的 R 脚本的单独的权限级别。 如果你需要保持对这些语言的单独权限，在单独的实例上安装 R 和 Python。

### <a name="permissions-db"></a> 对其授予用户读取、 写入或数据定义语言 (DDL) 权限数据库

在用户运行脚本时，用户可能需要从其他数据库中读取数据。 用户可能还需要创建新表以存储结果，并将数据写入表。

对于每个 Windows 用户帐户或 R 或 Python 脚本运行的 SQL 登录名中，确保它具有特定的数据库的适当的权限： `db_datareader`， `db_datawriter`，或`db_ddladmin`。

例如，以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，为提供的 SQL 登录名*MySQLLogin*中运行 T-SQL 查询的权限*ML_Samples*数据库。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

有关每个角色中包含的权限的详细信息，请参阅[数据库级角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源

你可以创建机器学习数据科学客户端计算机上的解决方案。 如果你需要通过使用 SQL Server 计算机作为计算上下文来运行代码，则有两个选项： 通过使用 SQL 登录名，访问实例或通过使用 Windows 帐户。

+ 为 SQL 登录名： 确保该登录名在其中您正在读取数据的数据库上具有适当权限。 你可以执行此操作通过添加*连接到*和*选择*权限，或通过添加登录到`db_datareader`角色。 若要创建对象，将分配`DDL_admin`权限。 如果必须将数据保存到表中，将添加到`db_datawriter`角色。

+ 对于 Windows 身份验证： 你可能需要在指定实例名称和其他连接信息的数据科学客户端上创建 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建议的优化

现在，你已使用的所有内容，你可能还想要优化的服务器以支持机器学习中，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果希望多个用户以会同时运行脚本，则可以增加分配给快速启动板服务的工作帐户数。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="optimize-the-server-for-script-execution"></a>优化的服务器脚本执行

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序旨在优化各种受数据库引擎，这可能包括提取、 转换和加载 (ETL) 过程，reporting、 审核的服务的服务器的余额和应用程序使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。 因此，在默认设置，你可能会发现以及有时限制或限制，尤其是在内存密集型操作的机器学习的资源。

若要确保机学习作业优先级别，并相应地资源，我们建议你使用 SQL Server 资源调控器来配置外部资源池。 你可能还想要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过启动的 R 帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，请参阅[修改用户帐户池的机器学习](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果你使用的标准版并没有资源调控器，你可以使用动态管理视图 (Dmv) 和扩展事件，以及监视，以帮助管理服务器资源的 Windows 事件。 有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)和[监视和管理 Python 服务](../python/managing-and-monitoring-python-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建 R 解决方案可以调用基本 R 函数，从装有 SQL Server 和第三方 R 包的开放源代码 R SQL Server 安装的版本兼容的 properietary packes 函数。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果你有 R 的单独安装的计算机上，或包安装到用户库，你将无法使用从 T-SQL 的这些包。

安装和管理 R 包的过程中是不同 SQL Server 2016 和 SQL Server 自 2017 年。 在 SQL Server 2016 中，数据库管理员必须安装用户需要的 R 包。 在 SQL Server 自 2017 年，可以将用户组设置为共享上的每个数据库级别，包或配置数据库角色，以使用户能够安装其自己的包。 有关详细信息，请参阅[包管理](../r/r-package-management-for-sql-server-r-services.md)。


## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并修复常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何使用 SQL Server 的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [针对 R 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 用于 SQL Server 按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
