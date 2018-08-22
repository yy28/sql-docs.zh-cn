---
title: 安装 SQL Server 2016 R Services （数据库） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 75e962b9be2acb1d44451081f0aef2bccd5a09fc
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "40437616"
---
# <a name="install-sql-server-2016-r-services-in-database"></a>安装 SQL Server 2016 R Services (In-Database) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章介绍了如何安装和配置**SQL Server 2016 R Services （数据库内）**。 如果您有 SQL Server 2016，安装此功能以启用 SQL Server 中 R 代码的执行。

## <a name="bkmk_prereqs"> </a> 预安装清单

+ 如果你想要安装 R Services，则需要 SQL Server 2016 安装程序。 如果改为您具有 SQL Server 2017 安装介质，则应安装[SQL Server 2017 机器学习服务 （数据库内）](sql-machine-learning-services-windows-install.md)来获取针对该版本的 SQL Server 的 R 集成。

+ 数据库引擎实例是必需的。 尽管将其添加到现有实例的以增量方式，你不能安装只需 R。

+ 不在故障转移群集上安装 R Services。 用于隔离 R 进程的安全机制不兼容与 Windows Server 故障转移群集环境。

+ 不要在域控制器上安装 R 服务。 安装程序的 R Services 部分将会失败。

+ 不安装**共享功能** > **R Server （独立版）** 同一台计算机上运行的数据库实例。 

+ 因为 SQL Server 实例使用其自己的开放源代码 R 和 Anaconda 分发版副本可能会与其他版本的 R 和 Python 的并行安装。 但是，运行 SQL Server 外部的 SQL Server 计算机使用 R 和 Python 的代码可能会导致各种问题：
    
  + 使用不同的库和其他可执行文件，并获取不同的结果，比您在 SQL Server 中运行时。
  + 不能由 SQL Server，从而导致资源争用管理外部库中运行的 R 和 Python 脚本。
  
如果你使用任何早期版本的 Revolution Analytics 开发环境或 RevoScaleR 包，或如果您安装了 SQL Server 2016 的任何预发行版本，则必须卸载它们。 不支持运行较旧和较新版本的 RevoScaleR 和其他专用包。 删除以前版本的帮助，请参阅[升级和安装常见问题解答的 SQL Server 机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

> [!IMPORTANT]
> 安装程序完成后，请确保要完成本文中所述的其他配置后步骤。 这些步骤包括启用 SQL Server 以使用外部脚本，并添加所需的 SQL Server 用于你的名义运行 R 作业帐户。 配置更改通常需要重新启动实例或重新启动 Launchpad 服务。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

## <a name="bkmk2016top"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 安装向导。

2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。
    
   ![安装 R Services （数据库内）](media/2016-setup-installation-rsvcs.png "启动数据库引擎的安装与 R 服务")
   
3. 上**功能选择**页上，选择以下选项：

   - 选择**数据库引擎服务**。 数据库引擎需要使用机器学习每个实例中。
   - 选择**R Services （数据库内）**。 安装 R 的数据库中使用的支持
    
     ![R Services 功能选择](media/2016setup-rsvcs-features.png "选择这些功能的 R Services 中的数据库")

    > [!IMPORTANT]
    > 并在同时安装 R Server 和 R Services。 通常，您将安装到 SQL Server 的 R Server （独立版） 创建的数据科学家或开发人员用来连接的环境和部署 R 解决方案。 因此，不需要在同一台计算机上安装这两个组件。

4.  上**同意安装 Microsoft R Open**页上，单击**接受**。
  
    下载 Microsoft R Open，其中包括开放源代码 R 基础包和工具，以及增强型的 R 包和 Microsoft R 开发团队的连接提供程序的分发时需要此许可协议。
  
5. 已接受许可协议后，没有短暂暂停时准备好安装程序。 单击**下一步**按钮变为可用时。

6. 上**已准备好安装**页上，验证以下各项是包括在内，然后选择**安装**。

   + 数据库引擎服务
   + R Services（数据库内）

    记下的路径下的文件夹位置`..\Setup Bootstrap\Log`存储配置文件。 安装程序完成后，你可以查看摘要文件中已安装的组件。

7. 安装完成时，如果要求您重新启动计算机后请立即登录。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)。


##  <a name="bkmk_enableFeature"></a>启用外部脚本执行

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
     
3. 若要启用外部脚本编写功能，请运行以下语句：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>重新启动服务。

安装完成后下, 一步，启用脚本执行在继续之前重新启动数据库引擎。

重新启动该服务还会自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

可以使用右键单击该服务重新启动**重新启动**命令，以在 SSMS 中，或使用的实例进行**Services**面板在控制面板中，或通过使用[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>验证安装

使用以下步骤来验证用于启动外部脚本的所有组件正在都运行。

1. 在 SQL Server Management Studio，打开新查询窗口中，并运行以下命令：
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** 现在应已设置为 1。

2. 打开**Services**面板或 SQL Server 配置管理器，并验证是否**SQL Server Launchpad 服务**正在运行。 应具有一项服务的每个数据库引擎实例具有 R 或 Python 安装。 有关详细信息，请参阅[组件来支持 Python 集成](../python/new-components-in-sql-server-to-support-python-integration.md)。

7. 如果 Launchpad 正在运行，您应能够运行简单的 R 来验证外部脚本的运行时可使用 SQL Server 通信。 

    打开一个新**查询**窗口中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后运行如下所示的脚本：
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    该脚本可以需要一段时间来首次运行外部脚本运行时加载。 结果应类似于此：

    | Hello |
    |----|
    | @shouldalert|

## <a name="bkmk_FollowUp"></a> 附加配置

如果外部脚本执行验证步骤是否成功，你可以从 SQL Server Management Studio、 Visual Studio Code 中或可以向服务器发送 T-SQL 语句的任何其他客户端运行 Python 命令。

如果你在运行命令时收到错误，，查看此部分中的其他配置步骤。 您可能需要对服务或数据库进行相应的其他配置。

需要进行其他更改的常见方案包括：

* [配置 Windows 防火墙以允许入站连接](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [启用其他网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [启用远程连接](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [将内置权限扩展到远程用户](#bkmk_configureAccounts)
* [授予运行外部脚本的权限](#bkmk_AllowLogon)
* [授予对单个数据库访问权限](#permissions-db)

> [!NOTE]
> 并非所有列出的更改是必需的并无可能要求。 要求取决于您在安装 SQL Server，以及希望用户可以连接到数据库并运行外部脚本的安全架构。 其他故障排除提示可在此处找到：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>启用为 Launchpad 帐户组的隐式身份验证

在安装期间，某些新的 Windows 用户帐户创建用于运行任务的安全令牌下[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务。 当用户从外部客户端发送 R 脚本时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]激活可用的工作帐户，将其映射到调用用户的标识和运行 R 脚本，代表用户。 数据库引擎的此新服务支持的调用的外部脚本执行安全*隐式身份验证*。

您可以查看这些帐户中的 Windows 用户组**SQLRUserGroup**。 默认情况下，会创建 20 个辅助角色帐户，即通常足以运行 R 作业。

但是，如果您需要从远程数据科学客户端运行 R 脚本，并使用 Windows 身份验证，则必须授予这些辅助角色帐户登录的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表你的实例。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。
2. 在中**登录名-新建**对话框中，选择**搜索**。
3. 选择**对象类型**并**组**复选框，然后清除其他所有复选框。
4. 单击**高级**，验证要搜索的位置是当前计算机，然后单击**立即查找**。
5. 滚动浏览列表，直到找到一个开始在服务器上的组帐户的`SQLRUserGroup`。
    
    + 与的 Launchpad 服务关联的组的名称_默认实例_只是始终**SQLRUserGroup**。 选择此帐户仅对于默认实例。
    + 如果使用的_命名实例_，实例名追加到默认名称， `SQLRUserGroup`。 因此，如果你的实例名为"MLTEST"，此实例的默认用户组名称将是**SQLRUserGroupMLTest**。
5. 单击**确定**以关闭高级的搜索对话框中，并验证已选择正确的实例的帐户。 每个实例可以使用其自己的快速启动板服务和该服务创建的组。
6. 单击**确定**一次以关闭**选择用户或组**对话框。
7. 在中**登录名-新建**对话框中，单击**确定**。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。

### <a name="bkmk_AllowLogon"></a>向用户授予权限来运行外部脚本

> [!NOTE]
> 如果在 SQL Server 计算上下文中运行 R 脚本使用 SQL 登录名，则不需要此步骤。

如果您安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中你自己的实例，您通常会执行脚本以管理员身份，或者至少为数据库的所有者，并因此具有的各种操作，该数据库，并能够安装新的包中的所有数据的隐式权限根据需要。

但是，在企业方案中，大多数用户，包括通过使用 SQL 登录名访问数据库的用户不具有这种提升的权限。 因此，对于每个用户都将运行 R 脚本，必须授予用户权限中，将使用外部脚本在每个数据库中运行脚本。

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 需要有关安装程序的帮助？ 不确定是否已执行所有步骤？ 使用这些自定义报表来检查安装状态，并运行其他步骤。 
> 
> [监视使用自定义报表的机器学习服务](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

### <a name="permissions-db"></a> 授予用户读取、 写入或 DDL 权限访问数据库

用于运行 R 的用户帐户可能需要从其他数据库读取数据创建新表以存储结果，并将数据写入到表。 因此，对于每个用户都将执行 R 脚本，请确保用户对数据库具有适当的权限： *db_datareader*， *db_datawriter*，或*db_ddladmin*.

例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句为 SQL 登录名 *MySQLLogin* 提供在 *RSamples* 数据库中运行 T-SQL 查询的权限。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

有关每个角色中包括的权限的详细信息，请参阅[数据库级别角色](../../relational-databases/security/authentication-access/database-level-roles.md)。


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源

如果你的数据科学客户端计算机上创建 R 解决方案并且需要通过使用 SQL Server 计算机作为计算上下文中运行代码，可以使用 SQL 登录名或集成的 Windows 身份验证。

* 对于 SQL 登录名：确保该登录名对要读取数据的数据库拥有相应的权限。 您为此，可添加*连接到*并*选择*权限，或通过添加到该登录名*db_datareader*角色。 需要创建对象的登录名，将添加*DDL_admin*权限。 对于必须将数据保存到表的登录名添加到该登录名*db_datawriter*角色。

* 为 Windows 身份验证： 你可能需要指定实例名称和其他连接信息的数据科学客户端上配置 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="suggested-optimizations"></a>建议的优化

现在，所有工作已经完成，你可能还想要优化服务器以支持机器学习中，或安装预先训练的模型。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果您认为您可能经常使用 R，或者如果希望有很多用户同时处于正在运行的脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="bkmk_optimize"></a>优化执行外部脚本的服务器

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序旨在优化的各种数据库引擎，这可能包括提取、 转换和加载 (ETL) 进程、 报告、 审核所支持的服务的服务器的余额和使用的应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。 因此，默认设置下，可能会发现为机器学习的资源的有时限制或受限制，尤其是在占用大量内存的操作。

若要确保机器学习作业的优先级别并其分配相应资源，我们建议使用 SQL Server 资源调控器配置外部资源池。 您可能还需要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库的保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过启动的 R 帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，请参阅[修改机器学习的用户帐户池](../r/modify-the-user-account-pool-for-sql-server-r-services.md)。

如果您使用的标准版，但没有资源调控器，则可以使用动态管理视图 (Dmv) 和扩展事件，以及 Windows 事件监视来帮助管理使用的服务器资源有关详细信息，请参阅[监视和管理 R Services](../r/managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

为 SQL Server 创建 R 解决方案可以调用基本 R 函数，函数从 SQL Server 一起安装的专属包和第三方 R 包与 SQL Server 安装的开放源代码 R 版本兼容。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果必须单独安装 R 的计算机上，或包安装到用户库，你将无法使用 T-SQL 中的这些包。

不同 SQL Server 2016 和 SQL Server 2017 中安装和管理 R 包的过程。 在 SQL Server 2016 中，数据库管理员必须安装 R 包，用户需要。 在 SQL Server 2017 中，可以设置用户组共享每个数据库级别上的包或配置数据库角色，以使用户能够安装其自己的包。 有关详细信息，请参阅[安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)。


## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查的实例的安装状态并解决常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。


