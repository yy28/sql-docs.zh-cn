---
title: "设置 SQL Server 计算机学习 Services （数据库） |Microsoft 文档"
ms.custom: 
ms.date: 11/15/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 SQL Server R Services"
- "安装 SQL Server 计算机学习 Services"
- "设置 R Services"
- "安装 SQL 机器学习"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 04f2502853e21968f2edaac927247eb45730d000
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>设置 SQL Server 计算机学习 Services （数据库）

本主题介绍如何安装和配置以下机器学习支持在 SQL Server 中的数据库中分析的功能：

+ **SQL Server 2016 R Services （数据库）**。 如果你有 SQL Server 2016，安装此功能以启用 SQL Server 中的 R 代码的执行。 需要数据库引擎。

    [设置 SQL Server 2016 中的机器学习](#bkmk_2016top)

+ **SQL Server 自 2017 年 1 机器学习服务 （数据库）**。 如果你有 SQL Server 自 2017 年，安装此项可在 SQL Server 中运行 R （或 Python） 代码。 需要数据库引擎。 

    [设置 SQL Server 自 2017 年中的机器学习](#bkmk_2017top)

+ 具有的机器学习服务器**没有**SQL Server

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序还包括机器学习组件，不需要数据库引擎，并且不会运行在 SQL Server 中的"独立"版本安装的选项。  我们通常建议你安装而不是托管 SQL Server 计算机的其他计算机上的此选项。
    
    [设置独立机器学习服务器](create-a-standalone-r-server.md)。

本指南介绍了安装程序使用的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导。 有关命令行安装，或要下载安装程序要在脱机服务器中使用，请参阅以下文章：

+ [从命令行安装 SQL Server R](unattended-installs-of-sql-server-r-services.md)
+ [从命令行中安装 SQL Server 的 Python](../python/unattended-installs-of-sql-server-python-services.md)
+ [从命令行安装独立机器学习服务器](install-microsoft-r-server-from-the-command-line.md)
+ [没有 internet ace 的服务器上安装机器学习组件](installing-ml-components-without-internet-access.md)

**适用于：** SQL Server 2016、 SQL Server 自 2017 年 1

## <a name="bkmk_prereqs"></a>预安装清单

+ 机器学习中的数据库需要 SQL Server 2016 或更高版本。 

+ 支持的语言： 

    + SQL Server 2016 仅支持 R。 

    + R 是还可作为在 Azure SQL 数据库中，有一些限制的预览功能。 有关详细信息，请参阅[Azure SQL 数据库中使用 R](using-r-in-azure-sql-database.md)

    + 若要使用 Python 需要 2017年或更高版本的 SQL Server。

+ 如果你使用任何早期版本的 Revolution Analytics 开发环境或 RevoScaleR 包中，或者如果你安装 SQL Server 2016 的所有预发行版本，你必须卸载它们。 不支持通过并行安装。 正在删除以前版本的帮助，请参阅[升级和安装适用的 SQL Server 机器学习服务的常见问题](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

+ 无法在域控制器上安装 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services。 安装程序的 R Services 或机器学习服务部分将会失败。

+ 无法安装机器学习故障转移群集上的功能。 用于隔离外部脚本进程的安全机制不与 Windows Server 故障转移群集环境兼容。 一种解决方法，您可以执行以下任一操作：
    * 使用复制将必要的表复制到的 SQL Server 实例，使用启用的机器学习。
    * 使用 AlwaysOn 并且可用性组的一部分的独立计算机上安装机器学习。

+ 在安装完成后，机器学习框架需要额外配置。 确切步骤取决于你的组织和安全策略、 服务器配置和预期的用户。 我们建议你查看所有步骤，并确定你的环境中可能需要的其他配置。

## <a name="bkmk2016top"></a>安装 SQL Server 2016 R Services （数据库）

> [!div class="checklist"]
> * 安装数据库引擎和机器学习功能
> * 所需安装后步骤： 启用机器学习中，并重新启动
> * 可选的安装后步骤： 添加防火墙规则、 添加用户、 更改或配置服务帐户设置远程数据科学客户端

**使用 SQL Server 2016 安装程序向导**

1. 运行 SQL Server 安装向导。

2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

    
     ![安装 R Services （数据库）](media/2016-setup-installation-rsvcs.png "带有 R Services 启动数据库引擎的安装")
   
3. 上**功能选择**页上，选择以下选项：

   - 选择**数据库引擎服务**。 数据库引擎使用机器学习每个实例中需要。
   - 选择**R Services （数据库）**。 安装。 数据库中使用的支持
    
     ![R Services 功能选择](media/2016setup-rsvcs-features.png "选择对于 R 服务数据库中的这些功能")

    > [!IMPORTANT]
    > 确实在同一时间安装 R Server 和 R 服务。 通常，你将安装 R Server （独立） 创建环境，数据科研人员或开发人员用来连接到 SQL Server 和部署 R 解决方案。 因此，不需要在同一台计算机上安装这两个组件。

4.  上**同意安装 Microsoft R Open**页上，单击**接受**。
  
    此许可协议需要下载 Microsoft R Open，其中包括的开放源代码 R 基程序包和工具，以及增强的 R 包和 Microsoft R 开发团队的连接提供商的分布。
  
    如果你正在使用的计算机没有 internet 访问权限，你可以暂停安装程序在此点以下载安装程序中所述单独[没有 internet 访问权限的安装 R 组件](installing-ml-components-without-internet-access.md)。
  
5. 已接受许可协议后，没有是短暂的暂停准备安装。 单击**下一步**按钮变为可用时。

6. 上**已准备好安装**页上，验证以下各项都包括在内，然后选择**安装**。

   + 数据库引擎服务
   + R Services（数据库内）

7. 安装完成后，重新启动计算机。


## <a name="bkmk2017top"></a>安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）

> [!div class="checklist"]
> * 安装数据库引擎和机器学习功能
> * 所需安装后步骤： 启用机器学习中，并重新启动
> * 可选的安装后步骤： 添加防火墙规则、 添加用户、 更改或配置服务帐户设置远程数据科学客户端。

**入门**

1. 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。
  
2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

     ![安装机器学习服务 （数据库）](media/2017setup-installation-page-mlsvcs.png "使用机器学习服务启动数据库引擎的安装")

3. 上**功能选择**页上，选择以下选项：
   
    + 选择**数据库引擎服务**。 数据库引擎使用机器学习每个实例中需要。

    + 选择**机器学习服务 （数据库）**。 此选项将安装。 数据库中使用的支持选择此选项后，你可以选择机器学习语言。 你可以选择仅 R，或者你可以添加 R 和 Python。
   
    ![机器学习服务功能选择](media/2017setup-features-page-mls-rpy.png "选择对于 R 服务数据库中的这些功能")

    如果不选择 R 或 Python 语言选项，安装向导正在安装仅扩展性框架，其中包括 SQL Server 受信任的快速启动板并不安装任何特定于语言的组件。  通常，我们建议你开始安装至少一种语言。 但是，如果你想要立即使用绑定过程来升级机器学习组件可能使用此选项。 有关详细信息，请参阅[使用 SqlBindR 升级 R Services 的实例](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

    我们建议你**不这样做**在同一台计算机上安装的独立应用程序和数据库中的功能并永远不会在同一时间安装它们。 部署解决方案时，你通常将到 SQL Server 安装机器学习 Server （独立） 创建环境，数据科研人员或开发人员用来连接。 因此，不需要在同一台计算机上安装这两个组件。

4.  许可协议对机器学习： 具体取决于要安装的语言，你必须接受 R 和 / 或 Python 的许可协议。

    + ： 此许可协议的许可条款介绍 Microsoft R Open，其中包括的开放源代码 R 基程序包和工具，以及增强的 R 包和 Microsoft 开发团队的连接提供商的分布。
  
    + Python 的许可条款。 Python 开放源代码许可协议还介绍 Anaconda 和相关的工具，以及 Microsoft 开发团队的某些新的 Python 库。

    单击**接受**以指示您的协议。 没有是短暂的暂停时准备组件，则**下一步**按钮将变为可用。

    如果你正在使用的计算机没有 internet 访问权限，你可以暂停安装此时程序如下所述单独下载安装程序：[安装没有 internet 访问权限的机器学习组件](installing-ml-components-without-internet-access.md)。

6. 上**已准备好安装**页上，验证以下各项都包括在内，然后选择**安装**。

   - 数据库引擎服务
   - 机器学习服务（数据库内）
   - R 和/或 Python

7. 安装完成后，记下的安装程序日志位置，然后重新启动计算机。

###  <a name="bkmk_enableFeature"></a>所必需的安装后步骤

出于安全原因，机器学习功能未启用默认情况下即使安装的功能。 服务器管理员必须启用该功能，并重新启动实例。 

本部分介绍如何重新配置机器学习的实例。 配置设置外部服务帐户，然后启动快速启动板服务。

1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果尚未安装，可以返回 SQL Server 安装向导，打开下载链接并安装。
  
2. 连接到安装机器学习的实例，然后运行以下命令：

   ```SQL
   sp_configure
   ```

    查找的值**启用外部脚本**属性，它应**0**。 这是因为默认情况下以减少外围应用关闭功能。
     
3. 若要启用外部脚本功能，请运行以下语句：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 此外会自动重新启动 SQL Server 服务重启相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

    可以通过重新启动服务**服务**面板控制面板中或通过使用 SQL Server 配置管理器。

5. 若要验证启用外部脚本执行服务，请在 SQL Server Management Studio，打开一个新**查询**窗口中，并再次运行以下命令：
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    **run_value** 现在应已设置为 1。
    
6. 打开**服务**面板，并验证你的实例的快速启动板服务正在运行。 如果安装了多个实例，每个实例都有其自身的 Launchpad 服务。

7. 它是一个好办法运行一个简单的脚本来验证外部脚本的运行时可以与 SQL Server 通信。 

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

    该脚本时，会稍有若要运行，第一次请加载外部脚本运行。 结果应类似如下内容：

    | Hello |
    |----|
    | @shouldalert|


8. 如果出现任何错误，继续执行到描述可能需要使后安装已完成，或者请参阅疑难解答指南的其他 （可选） 更改的部分：

    + [可选的安装后步骤： 配置服务和权限](#bkmk_FollowUp) 
    + [SQL Server 中的故障排除机器学习](upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="bkmk_FollowUp"></a>可选的安装后步骤

具体取决于机器学习你用例，你可能需要对服务器、 防火墙、 使用的服务或数据库权限的帐户进行其他更改。 你必须作出更改因大小写。

需要其他更改的常见方案包括：

* 更改防火墙规则以允许入站的连接到 SQL Server。
* 启用其他网络协议。
* 确保服务器支持远程连接。
* 启用*默示身份验证*，如果用户从远程数据科学客户端访问 SQL Server 数据，并通过使用 RODBC 包或其他 ODBC 提供程序执行的代码。
* 向用户提供对个别数据库权限。
* 修复阻止与快速启动板服务进行通信的安全问题。
* 确保用户有权运行代码，也安装包。

> [!NOTE]
> 并非所有列出的更改可能需要。 但是，我们建议你查看所有项，以查看它们是否适用于你的方案。

其他故障排除提示可在此处找到：[升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>启用快速启动板帐户组的隐式身份验证

在安装期间，某些新的 Windows 用户帐户创建为运行下的安全令牌的任务[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务。 当用户从外部客户端，发送 R 脚本时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]激活可用的工作帐户、 将其映射到的调用用户的标识和运行 R 脚本代表用户。 这一新的数据库引擎服务支持调用的外部脚本的安全执行*默示身份验证*。

你可以在 Windows 用户组中查看这些帐户**SQLRUserGroup**。 默认情况下，被创建 20 工作人员帐户，这通常是绰绰有余用于运行 R 作业。

但是，如果你需要从远程数据科学客户端运行 R 脚本，且正在使用 Windows 身份验证，你必须授予这些辅助帐户权限登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表你的实例。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。
2. 在**登录名-新建**对话框中，选择**搜索**。
3. 选择**对象类型**和**组**复选框，并清除所有其他复选框。
4. 单击**高级**，验证，要搜索的位置为当前计算机，然后单击**立即查找**。
5. 直到找到一个开头的服务器上的组帐户的列表中滚动`SQLRUserGroup`。
    
    + 与的快速启动板服务关联组的名称_默认实例_只始终是**SQLRUserGroup**。 选择此帐户仅对于默认实例。
    + 如果你使用_命名实例_，实例名称追加到默认名称， `SQLRUserGroup`。 因此，如果你的实例名为"MLTEST"，此实例的默认用户组名称将**SQLRUserGroupMLTest**。
5. 单击**确定**以关闭高级的搜索对话框中，并验证你已选择正确的帐户的实例。 每个实例可以使用其自己的快速启动板服务和为该服务创建的组。
6. 单击**确定**一次以关闭**选择用户或组**对话框。
7. 在**登录名-新建**对话框中，单击**确定**。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。

### <a name="bkmk_AllowLogon"></a>向用户授予的权限来运行外部脚本

> [!NOTE]
> 如果在 SQL Server 计算上下文中运行 R 脚本使用 SQL 登录名，则不需要此步骤。

如果你安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在您自己的实例，你通常将执行脚本以管理员身份，或者至少为数据库的所有者，并因此具有隐式权限各种操作，该数据库，并且能够安装新包中的所有数据根据需要。

但是，在企业方案中，大多数用户来说，包括通过使用 SQL 登录名访问数据库的用户不具有这种提升的权限。 因此，对于每个用户都将运行 R 或 Python 脚本，必须授予用户权限来将在其中外部脚本使用在每个数据库运行脚本。

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 需要有关安装程序的帮助？ 不确定是否已执行所有步骤？ 使用这些自定义报表以检查安装状态和运行其他步骤。 
> 
> [监视使用自定义报表的机器学习服务](monitor-r-services-using-custom-reports-in-management-studio.md)。

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>确保 SQL Server 计算机支持远程连接

如果你无法从远程计算机连接，请检查以查看服务器是否允许远程连接。 默认情况下，有时被禁用远程连接。

此外检查防火墙是否允许访问 SQL Server。 默认情况下，防火墙通常会阻止 SQL Server 使用的端口。 如果你正在使用 Windows 防火墙，请参阅[为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>授予用户读取、 写入或对数据库的 DDL 权限

用于运行 R 或 Python 的用户帐户可能需要从其他数据库，读取数据创建新表来存储结果，并将数据写入到表。 因此，对于每个用户都将执行 R 或 Python 脚本，请确保用户对数据库具有适当的权限： *db_datareader*， *db_datawriter*，或*db_ddladmin*。

例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句为 SQL 登录名 *MySQLLogin* 提供在 *RSamples* 数据库中运行 T-SQL 查询的权限。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

有关每个角色中包含的权限的详细信息，请参阅[数据库级角色](../../relational-databases/security/authentication-access/database-level-roles.md)。

### <a name="use-machine-learning-in-an-azure-vm"></a>在 Azure VM 中使用机器学习

如果你在 Azure 虚拟机上安装了机器学习服务 （或 R Services），你可能需要更改某些其他默认设置。 有关详细信息，请参阅[安装 Azure 虚拟机上 SQL Server 机器学习](installing-sql-server-r-services-on-an-azure-virtual-machine.md)。

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源

如果你的数据科学客户端计算机上创建 R 解决方案，并且需要通过使用 SQL Server 计算机作为计算上下文来运行代码，你可以使用 SQL 登录名或集成的 Windows 身份验证。

* 对于 SQL 登录名：确保该登录名对要读取数据的数据库拥有相应的权限。 你可以通过添加实现*连接到*和*选择*权限，或通过添加登录到*db_datareader*角色。 对于需要创建对象的登录名，添加*DDL_admin*权限。 必须将数据保存到表的登录名添加到的登录名为*db_datawriter*角色。

* 对于 Windows 身份验证： 你可能需要指定实例名称和其他连接信息的数据科学客户端上配置 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

## <a name="next-steps"></a>后续步骤

验证脚本执行功能，在 SQL Server 中工作后，你可以从 SQL Server Management Studio、 Visual Studio 代码或可以向服务器发送的 T-SQL 语句的任何其他客户端运行 R 和 Python 的命令。 在这样做之前, 可能需要对系统配置，以支持使用大量的机器学习中，或添加新的 R 包进行一些更改。

本部分列出了一些常见的优化和机器学习的学习活动。

### <a name="add-more-worker-accounts"></a>添加更多的辅助角色帐户

如果您认为可能很大程度，使用 R，或者如果希望多个用户同时处于正在运行的脚本，则可以增加分配给快速启动板服务的工作帐户数。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](modify-the-user-account-pool-for-sql-server-r-services.md)。

### <a name="bkmk_optimize"></a>优化外部脚本执行的服务器

默认设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序旨在优化各种受数据库引擎，这可能包括提取、 转换和加载 (ETL) 过程，reporting、 审核的服务的服务器的余额和应用程序使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据。 因此，在默认设置，你可能会发现以及有时限制或限制，尤其是在内存密集型操作的机器学习的资源。

若要确保机学习作业优先级别，并相应地资源，我们建议你使用 SQL Server 资源调控器来配置外部资源池。 你可能还想要更改分配给的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，或增加下运行的帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]服务。

- 若要配置用于管理外部资源的资源池，请参阅[创建外部资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。
  
- 若要更改数据库保留的内存量，请参阅[服务器内存配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。
  
- 若要更改可以通过启动的 R 帐户数[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]，请参阅[修改用户帐户池的机器学习](modify-the-user-account-pool-for-sql-server-r-services.md)。

如果你使用的标准版并没有资源调控器，则可以使用动态管理视图 (Dmv) 和扩展事件，以及监视，以帮助管理。 通过使用服务器资源的 Windows 事件有关详细信息，请参阅[监视和管理 R Services](managing-and-monitoring-r-solutions.md)。

### <a name="install-additional-r-packages"></a>安装其他 R 包

花费片刻时间安装要使用的其他任何 R 包。

要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果你有 R 的单独安装的计算机上，或包安装到用户库，你将无法使用从 T-SQL 的这些包。

安装和管理 R 包的过程中是不同 SQL Server 2016 和 SQL Server 自 2017 年。 例如，在 SQL Server 自 2017 年，可以将用户组设置为共享上的每个数据库级别，包或配置数据库角色，以使用户能够安装其自己的包。 有关详细信息，请参阅[包管理](r-package-management-for-sql-server-r-services.md)。

在 SQL Server 2016 中，数据库管理员必须安装用户需要的 R 包。

管理访问权限，也需要在实例库中安装的其他 Python 软件包。

### <a name="upgrade-the-machine-learning-components"></a>升级机器学习组件

在机器学习功能安装在 SQL Server 中时，你将获取已发布的版本或服务包时最新的 R 或 Python 组件的版本。 修补或升级服务器，每次机器学习组件将同时升级。

但是，你可以升级机器学习不支持的方式更快的定期的组件通过 SQL Server 版本中，通过使用此过程称为_绑定_。 在绑定的 SQL Server 实例时，你同时升级的 R 或 Python 版本中，并将更改为不同的支持策略，来支持更频繁地升级。 

此类升级可能包括：

* 新的 R 包
+ Microsoft 的新 Api 包[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。
* [预先训练模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)对图像分类和文本分析。

有关如何升级的 SQL Server 实例的信息，请参阅[通过绑定升级机器学习组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。


### <a name="tutorials"></a>教程

若要开始使用一些简单的示例，并了解 R 如何使用 SQL Server 的基础知识，请参阅[TRANSACT-SQL 中的使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。

### <a name="troubleshooting"></a>故障排除

遇到问题？ 尝试升级？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题-机器学习服务](upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并修复常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](\r\monitor-r-services-using-custom-reports-in-management-studio.md)
