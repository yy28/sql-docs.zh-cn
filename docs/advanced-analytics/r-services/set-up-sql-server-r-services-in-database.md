---
title: "安装 SQL Server R Services（数据库内）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4b0c00ed62ac38c9ff28118f42b63d69faa15b64
ms.lasthandoff: 04/11/2017

---
# <a name="set-up-sql-server-r-services-in-database"></a>安装 SQL Server R Services（数据库内）
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和更高版本中，可以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导使用 R 安装所需的组件。 SQL Server 安装程序提供以下选项：
  
  + 连同 SQL Server R Services（数据库内）一起安装数据库引擎，以便在 SQL Server 中运行 R 脚本 

或者：  
  + 安装 Microsoft R Server（独立版）用于创建 R 解决方案的开发环境。 有关详细信息，请参阅 [创建 R Server（独立版）](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  
 

 
## <a name="prerequisites"></a>先决条件

+  我们建议不要一次性同时安装 R Server 和 R Services。 安装 R Server（独立版）的原因往往是想要创建一个环境，让数据科研人员或开发人员用来连接到 SQL Server 和部署 R 解决方案。 因此，不需要在同一台计算机上安装这两个组件。
+ 若要安装低于 SQL Server 2016 SP1 的任何版本，必须使用 8dot3 表示法启用短文件名创建。 这是为了与开源 R 组件兼容。 但是，从 SQL Server 2016 SP1（累积更新 CU3 OD）开始，这项限制已被取消。 

    + [SQL Server 2016 CU3 的修补程序](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)
    + [SQL Server 2016 SP1 累积更新 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)

+ 如果已安装任何早期版本的 Revolution Analytics 开发环境或 RevoScaleR 包，或者已经安装任何预发行版的 SQL Server 2016，应该先卸载这些版本。 不支持并列安装。 有关卸载早期版本的帮助，请参阅 [Upgrade and Installation FAQ for SQL Server R Services](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)（有关升级和安装 SQL Server R Services 的常见问题解答）

+ 不能在故障转移群集上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 。 原因是用于隔离 R 进程的安全机制与 Windows Server 故障转移群集环境不兼容。 解决方法之一是使用复制功能将所需的表复制到包含 R Services 的独立 SQL Server 实例，或者在使用 Always On 或属于可用性组的独立计算机上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 。 

> [!IMPORTANT]    
> 安装完成后，需要执行一些附加步骤来启用 R Services 功能。 根据 R 的用途，可能还需要授予用户对特定数据库的权限、更改或配置帐户，或者设置远程数据科学客户端。 。   

  
##  <a name="bkmk_installRServicesInDatabase"></a> Step 1: Install R Services (In-Database) on SQL Server 2016 or later  


1.  运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。  
  
    有关如何执行无人参与安装的信息，请参阅 [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md)。  
  
2.  在“安装”  选项卡上，单击“全新 SQL Server 独立安装或向现有安装添加功能” 。  
   
3.  在“功能选择”页上选择以下两个选项：  
  
    -   **数据库引擎服务**  
  
         至少需要一个数据库引擎实例才能使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 可以使用默认实例或命名实例。  
  
    -   **R Services（数据库内）**  
  
         此选项配置 R 作业所用的数据库服务，并安装支持外部脚本和过程的扩展。  
        > [!NOTE]
        > 如果需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将解决方案操作化，请务必选择 **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]** 选项。 
        > 
        > 选择“Microsoft R Server (独立版)”选项可在其他计算机（例如，用于 R 开发的笔记本电脑）上安装 R 组件。
 
  
4.  在“同意安装 Microsoft R Open” 页面上，单击“接受” 。  
  
     需要此许可证协议方可下载 Microsoft R Open，Microsoft R Open 包含开放源代码 R 基础包和工具的分发，以及 Revolution Analytics 提供的增强 R 包和连接提供程序。  
  
    > [!NOTE]  
    >  如果正在使用的计算机无法访问 Internet，可以先暂停安装，并单独下载此处所述的安装程序： [在没有连接到 Internet 的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
     单击“接受” ，等到“下一步”  按钮可用时，单击“下一步” 。  
  
5.  在“准备安装”  页面上，验证是否已包括这些选择，然后单击“安装” 。 
  
     + 数据库引擎服务  
  
     + R Services（数据库内）  
  
6.  安装完成后，重启计算机。   
  
  
##  <a name="bkmk_enableFeature"></a>步骤 2：启用 R Services  
  
  
1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果尚未安装，可以返回 SQL Server 安装向导，打开下载链接并安装。  
  
2. 连接到安装 R Services（数据库内）的实例并运行以下命令：

   ```    
   sp_configure    
   ```  

    属性 `external scripts enabled` 的值目前应为 **0**。 这是因为该功能默认已关闭（为了减小外围应用），必须由管理员显式启用。
     
3.  若要启用 R Services 功能，请运行以下语句。  
  
    ```    
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with override    
    ```  
  
10. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 重新启动 SQL Server 服务也会自动重新启动相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。 

    可以使用控制面板中的“服务”面板或使用 SQL Server 配置管理器重新启动服务。  
  
## <a name="step-3-verify-that-script-execution-works-locally"></a>步骤 3. 验证脚本是否在本地正常执行

启动 SQL Server 服务后，请花费片刻时间来验证用于 R Services 的所有组件是否正在运行。

1. 在 SQL Server Management 中打开新的“查询”窗口，然后运行以下命令：  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
    **run_value** 现在应已设置为 1。
    
2. 打开“服务”面板并验证实例的 Launchpad 服务是否正在运行。 如果安装了多个实例，每个实例都有其自身的 Launchpad 服务。
   
3. 如果 Launchpad 正在运行，你应该能够运行以下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中所示的简单 R 脚本：  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **结果**  
  
    *hello*  
    *1*   
  
    + 如果此命令成功，则可以从 SQL Server Management Studio、Visual Studio Code 或者能够向服务器发送 T-SQL 语句的其他任何客户端运行 R 命令。  若要开始体验一些简单的示例并了解有关 R 如何与 SQL Server 配合工作的基础知识，请参阅 [Using R Code in Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)（在 Transact-SQL 中使用 R 代码）。
    + 如果遇到错误，请参阅以下文章中的一些常见问题的列表：[Upgrade and Installation FAQ](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)（升级和安装常见问题解答）。 

4. （可选）花费片刻时间安装所要使用的其他任何 R 包。 

    要通过 SQL Server 使用的包必须安装在实例使用的默认库中。 如果在计算机上单独安装了 R，或者将包安装到了用户库，则无法从 T-SQL 使用这些包。 有关详细信息，请参阅 [Install Additional R Packages on SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)（在 SQL Server 上安装其他 R 包）。

5. 如果需要访问 SQL Server 数据、从 R 代码执行 ODBC 调用，或者从远程数据科学客户端执行 R 命令，请继续阅读后续部分。  
  
##  <a name="bkmk_configureAccounts"></a>步骤 4：为 Launchpad 帐户启用隐式身份验证  
   
  
在安装期间，已创建一些新的 Windows 用户帐户，用于运行 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务的安全令牌下的任务。 用户从外部客户端发送 R 脚本时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会激活可用的辅助角色帐户，将其映射到调用用户标识，并以用户名义运行 R 脚本。 数据库引擎的一项新服务叫做隐式身份验证 ，支持外部脚本的安全执行。 

可以在 Windows 用户组“SQLRUserGroup” 中查看这些账户。  默认会创建 20 个辅助角色帐户，这通常足以运行 R 作业。 

但是，如果需要从远程数据科学客户端运行 R 脚本，并且使用 Windows 身份验证，必须授予这些辅助角色帐户以你的身份登录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的权限。  
  
1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。  
2. 在“登录名 - 新建”  对话框中，单击“搜索” 。  
3. 单击“对象类型”  ，然后选择“组” 。 取消选择所有其他内容。  
4. 在“输入要选择的对象名”中，键入 *SQLRUserGroup*  ，然后单击“检查名称” 。  
5. 解析与实例的 Launchpad 服务关联的本地组名称，它应类似于 *instancename\SQLRUserGroup*。 单击 **“确定”**。  
6. 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。 
7. 单击 **“确定”**。  
  
> [!NOTE]
> 如果在 SQL Server 计算上下文中使用 SQL 登录名运行 R 脚本，则无需此额外步骤。
  
  
## <a name="step-5-give-non-admin-users-r-script-permissions"></a>步骤 5：授予非管理员用户对 R 脚本的权限 
  
如果自行安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并在自己的实例中运行 R 脚本，则通常以管理员身份执行脚本，因此对数据库中的各种操作和所有数据具有隐式权限，并能根据需要安装新的 R 包。  
  
但是在企业方案中，大多数用户（包括使用 SQL 登录名访问数据库的用户）不具有这种提升的权限。 因此，必须向将要运行外部脚本的每个用户授予权限，使其能够在要使用 R 的每个数据库中运行 R 脚本。   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP]
> 需要有关安装程序的帮助？ 不确定是否已执行所有步骤？ 使用这些自定义报表，检查 R Services 的安装状态。 有关详细信息，请参阅 [使用自定义报表监视 R Services](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)。    
  
##  <a name="bkmk_Additional"></a> 其他配置选项 
  
本部分介绍实例或数据科学客户端配置中可做的其他更改，以支持 R 脚本执行。
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadincludesrsql-launchpad-mdmd"></a>修改 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]使用的辅助角色帐户数目
  
如果将经常使用 R，或预期会有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)相关的其他服务进行轻微的配置更改。  
  
  
### <a name="give-your-users-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>在其他数据库中根据需要向用户授予读取、写入或 DDL 权限  
  
运行 R 脚本时，用户帐户或 SQL 登录名可能需要从其他数据库读取数据、创建新表以存储结果，并将数据写入表中。 
     
对于要执行 R 脚本的每个用户帐户或 SQL 登录名，请确保该帐户或登录名对特定数据库拥有 **db_datareader**、**db_datawriter** 或 **db_ddladmin** 权限。   
       
例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句为 SQL 登录名 *MySQLLogin* 提供在 *RSamples* 数据库中运行 T-SQL 查询的权限。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
若要详细了解每个角色包括的权限，请参阅 [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源  
  
如果在数据科学客户端计算机上创建 R 解决方案，并需要使用 SQL Server 计算机作为计算上下文来运行代码，可以使用 SQL 登录名或 Windows 集成身份验证。  
  
+ 对于 SQL 登录名：确保该登录名对要读取数据的数据库拥有相应的权限。 通过添加连接  和选择  权限，或将登录名添加到 **db_datareader** 角色，可完成此操作。 如果需要创建对象，则需要 **DDL_admin** 权限。  若要将数据保存到表中，请将登录名添加到 **db_datawriter** 角色。  
  
+ 对于 Windows 身份验证：必须在指定该实例名称和其他连接信息的数据科学客户端上配置 ODBC 数据源。 有关详细信息，请参阅 [使用 ODBC 数据源管理器](http://windows.microsoft.com/windows/using-odbc-data-source-administrator)。  
  
### <a name="optimize-the-server-for-r"></a>优化 Server for R  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的默认设置旨在为数据库引擎支持的各种服务（包括 ETL 进程、报告、审核和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的应用程序）优化服务器平衡。 因此，在默认设置下，可能会发现 R 操作（尤其是占用大量内存的操作）的资源有时被限制或被阻止。  
  
 若要确保 R 任务的优先级别并为其分配相应资源，建议使用 Resource Governor 配置特定于 R 操作的外部资源池。 可能还需要更改分配到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的内存数量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务下运行的帐户数。  
  
-   配置用于管理外部资源的资源池  
  
     [创建外部资源池 (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   更改为数据库引擎保留的内存量  
  
     [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   更改可以通过 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]启动的 R 帐户数  
  
     [修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

如果使用了 Standard Edition 且没有安装资源调控器，可以使用 DMV 和扩展事件以及 Windows 事件监视来帮助管理 R 所用的服务器资源。有关详细信息，请参阅 [Monitoring and Managing R Services](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)（监视和管理 R Services）。
  
### <a name="get-the-r-source-code-optional"></a>获取 R 源代码（可选）  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包括开放源代码 R 基础包的分发。  
  
（可选）单击下面的一个链接，立即开始下载已修改的 GPL/LGPL 源代码。 与 GNU 通用公共许可证相符合的源代码可供使用，但无需安装或使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。  
  
-   与 RC2 兼容：下载存档 [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 
  
-   与 RC3 兼容：下载存档 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 

-   与 RTM 兼容：下载存档 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771)
  
## <a name="troubleshooting"></a>故障排除  

 遇到问题？ 是否有预发行版的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]？ 参阅此常见问题列表。  
  
 + [升级和安装常见问题解答 (SQL Server R Services)](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
 
 尝试使用这些自定义报告来检查实例的安装状态并解决常见问题。
 
 + [SQL Server R Services 的自定义报告](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)
  
## <a name="see-also"></a>另请参阅  
 [设置数据科学客户端](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [创建 R Server（独立版）](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  

