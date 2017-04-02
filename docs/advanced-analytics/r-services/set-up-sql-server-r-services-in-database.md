---
title: "安装 SQL Server R Services（数据库中） | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "安装 SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# 安装 SQL Server R Services（数据库中）
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和更高版本中，可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导安装与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相关的所有组件。  
 
 
 安装完成后，可能需要执行一些其他步骤以启用 R Services 功能、配置帐户，并向用户授予特定数据库的权限。   
  
如果安装完成后遇到数据库访问问题，或需要卸载以前的版本，请参阅[升级和安装常见问题解答 (SQL Server R Services)](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。  

> [!NOTE]
> 若要安装 R Services（数据库内），则安装该功能的驱动器必须支持使用 8dot3 表示法创建短文件名。 否则，从 SQL Server 启动 R 的进程可能无法启动。 安装 R Services 之前，请务必在卷上启用 8dot3 表示法。 更高版本中将删除此限制。

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a>步骤 1：在 SQL Server 2016 或更高版本上安装 R Services（数据库内）  
   
  
1.  运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。  
  
    有关如何执行无人参与安装的信息，请参阅 [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md)。  
  
2.  在“安装”  选项卡上，单击“全新 SQL Server 独立安装或向现有安装添加功能” 。  
  
    > [!NOTE]  
    >  不能在故障转移群集上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 但是，可以在使用 AlwaysOn 且属于可用性组的独立计算机上安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 有关在 AlwaysOn 可用性组中使用 R Services 的详细信息，请参阅 [AlwaysOn 可用性组：互操作性](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)。  
  
3.  在“功能选择”  页上，选择以下选项：  
  
    -   **数据库引擎服务**  
  
         至少需要一个数据库引擎实例才能使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 可以使用默认实例或命名实例。  
  
    -   **R Services（数据库内）**  
  
         此选项配置 R 作业所用的数据库服务，并安装支持外部脚本和过程的扩展。  
    > [!NOTE]
    > 
    > 如果需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行 R 代码，请务必安装 **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]**。 
    > 
    > 与此相反，Microsoft R Server（独立版）选项允许在未运行 SQL Server 的 Windows 计算机上使用 Scale R 库。 建议在用于 R 开发的笔记本电脑或其他计算机上安装 Microsoft R Server（独立版），以创建 R 解决方案，稍后可将该 R 解决方案部署到运行 R Services（数据库内）的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。
 
  
4.  在“同意安装 Microsoft R Open”页面上，单击“接受”。  
  
     需要此许可证协议方可下载 Microsoft R Open，Microsoft R Open 包含开放源代码 R 基础包和工具的分发，以及 Revolution Analytics 提供的增强 R 包和连接提供程序。  
  
    > [!NOTE]  
    >  如果正在使用的计算机无法访问 Internet，可以先暂停安装，并单独下载此处所述的安装程序：[在没有连接到 Internet 的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
     单击“接受”，等到“下一步”按钮可用时，单击“下一步”。  
  
5.  在“准备安装”页面上，验证是否已包括这些选择，然后单击“安装”。  
  
     **功能**  
  
     数据库引擎服务  
  
     R Services (数据库中)  
  
6.  安装完成后，重启计算机。   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a>步骤 2：启用 R Services 并验证本地 R 脚本执行运行正常  
  
  
1. 打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果尚未安装，可以返回 SQL Server 安装向导，打开下载链接并安装。  
  
2. 连接安装了 R Services（数据库内）的实例，然后运行以下命令，以显式方式启用 R Services 功能；否则，即使安装程序已安装此功能，也无法调用 R 脚本。  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例重启 SQL Server 服务。 此操作也会自动重启相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。 可以使用控制面板中的“服务”面板或使用 SQL Server 配置管理器重启服务。  
  
9. SQL Server 服务可用后，运行以下命令并检查 *run_value* 是否已设置为 1，以验证是否启用了 R 功能：  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   （可选）打开“服务”面板并验证实例的 Launchpad 服务是否正在运行。 每个实例都有自己的 Launchpad 服务。
   
10. 现在，应能运行简单的 R 脚本，如下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中所示：  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    结果  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  如果需要访问 SQL Server 数据，或从远程数据科学客户端运行 R 命令，需要执行一些额外步骤。 以下步骤详细描述了这些额外要求。
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a>步骤 3：为 Launchpad 帐户启用隐式身份验证  
   
  
在安装期间，创建了 20 个新的 Windows 用户帐户，用以运行 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务的安全令牌下的任务。 用户从外部客户端发送 R 脚本时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会激活可用的辅助角色帐户，将其映射到调用用户标识，并以用户名义运行 R 脚本。 数据库引擎的一项新服务叫做隐式身份验证，支持外部脚本的安全执行。 

可以在 Windows 用户组“SQLRUserGroup”中查看这些账户。  如果需要从远程数据科学客户端运行 R 脚本，并且使用 Windows 身份验证，必须授予这些辅助角色帐户以你的身份登录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的权限。  
  
1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的“对象资源管理器”中，展开“安全性”，右键单击“登录名”，然后选择“新建登录名”。  
2. 在“登录名 - 新建”对话框中，单击“搜索”。  
3. 单击“对象类型”，然后选择“组”。 取消选择所有其他内容。  
4. 在“输入要选择的对象名”中，键入 *SQLRUserGroup*，然后单击“检查名称”。  
5. 解析与实例的 Launchpad 服务关联的本地组名称，它应类似于 *instancename\SQLRUserGroup*。 单击 **“确定”**。  
6. 默认情况下，将登录名分配到**公共**角色，且有权连接到数据库引擎。 
7. 单击 **“确定”**。  
  
> [!NOTE] 如果在 SQL Server 计算上下文中使用 SQL 登录名运行 R 脚本，则无需此额外步骤。
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>第 4 步：授予非管理员用户 R 脚本权限  
  
如果自行安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并在自己的实例中运行 R 脚本，则通常以管理员身份执行脚本，因此对数据库中的各种操作和所有数据具有隐式权限，并能根据需要安装新的 R 包。  
  
但是在企业方案中，大多数用户（包括使用 SQL 登录名访问数据库的用户）不具有这种提升的权限。 因此，必须向将要运行外部脚本的每个用户授予权限，使其能够在要使用 R 的每个数据库中运行 R 脚本。   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] 需要有关安装程序的帮助？ 不确定是否已执行所有步骤？
>
> 使用这些自定义报表，检查 R Services 的安装状态。 有关详细信息，请参阅[使用自定义报表监视 R Services](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)。    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a>可选修改  
  
本部分介绍实例或数据科学客户端配置中可做的其他更改，以支持 R 脚本执行。
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>修改 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 使用的辅助角色帐户数目
  
如果将经常使用 R，或预期会有很多用户同时运行脚本，则可以增加分配给 Launchpad 服务的辅助角色帐户数目。 有关详细信息，请参阅[修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>在其他数据库中根据需要向 R 用户或登录名授予读取、写入或 DDL 权限  
  
运行 R 脚本时，用户帐户可能需要从其他数据库读取数据、创建新表以存储结果，并将数据写入表中。 
     
对于每个将执行 R 脚本的用户，请确保用户帐户对特定数据库具有 **db_datareader**、**db_datawriter** 或 **db_ddladmin** 权限。   
       
例如，以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句为 SQL 登录名 *MySQLLogin* 提供在 *RSamples* 数据库中运行 T-SQL 查询的权限。 若要运行此语句，SQL 登录名必须已经存在于服务器的安全上下文中。  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
若要详细了解每个角色包括的权限，请参阅[数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>为数据科学客户端上的实例创建 ODBC 数据源  
  
如果在数据科学客户端计算机上创建 R 解决方案，且需要连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机作为计算上下文，可以使用 SQL 登录名或集成式 Windows 身份验证。  
  
如果使用 SQL 登录名，请确保该登录名对要读取数据的数据库具有适当权限。 通过添加连接和选择权限，或将登录名添加到 **db_datareader** 角色，可完成此操作。 如果需要创建对象，则需要 **DDL_admin** 权限。  若要将数据保存到表中，请将登录名添加到 **db_datawriter** 角色。  
  
如果使用 Windows 身份验证，必须在指定该实例名称和其他连接信息的数据科学客户端上配置 ODBC 数据源。  
  
有关详细信息，请参阅[使用 ODBC 数据源管理器](http://windows.microsoft.com/windows/using-odbc-data-source-administrator)。  
  
### <a name="optimize-the-server-for-r"></a>优化 Server for R  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的默认设置旨在为数据库引擎支持的各种服务（包括 ETL 进程、报告、审核和使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的应用程序）优化服务器平衡。 因此，在默认设置下，可能会发现 R 操作（尤其是占用大量内存的操作）的资源被限制或被阻止。  
  
 若要确保 R 任务的优先级别并为其分配相应资源，建议使用 Resource Governor 配置特定于 R 操作的外部资源池。 可能还需要更改分配到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的内存数量，或增加 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务下运行的帐户数。  
  
-   配置用于管理外部资源的资源池  
  
     [创建外部资源池 (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   更改为数据库引擎保留的内存量  
  
     [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   更改可以通过 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 启动的 R 帐户数  
  
     [修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>获取 R 源代码（可选）  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包括开放源代码 R 基础包的分发。  
  
（可选）单击下面的一个链接，立即开始下载已修改的 GPL/LGPL 源代码。 与 GNU 通用公共许可证相符合的源代码可供使用，但无需安装或使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。  
  
-   与 RC2 兼容：下载存档 [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 
  
-   与 RC3 兼容：下载存档 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 

-   与 RTM 兼容：下载存档 [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771)
  
## <a name="troubleshooting"></a>故障排除  
 遇到问题？ 安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的预发行版本时，请参阅此常见问题列表  
  
 [升级和安装常见问题解答 (SQL Server R Services)](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [设置数据科学客户端](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [创建 R Server（独立版）](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  