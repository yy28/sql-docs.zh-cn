---
title: 初始配置（PowerPivot for SharePoint） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ba58e81cb802f3debe1c481443751de1947c595e
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798115"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>初始安装 (PowerPivot for SharePoint)
  使用本主题中的步骤可以配置 PowerPivot for SharePoint 的初始安装。 配置初始安装的最简单方法是使用 PowerPivot 配置工具。 该工具自动完成下述所有配置步骤。  
  
 或者，如果您想要增强对配置服务器的方式的控制，则可以使用管理中心和本文中的信息单独执行各步骤。  
  
 
  
## <a name="prerequisites"></a>必备条件  
 必须已使用 SharePoint 安装程序中的“服务器场”安装选项安装了 SharePoint 服务器。 不支持使用内置数据库的独立 SharePoint 服务器。 有关详细信息，请参阅[在 SharePoint 2010 场中使用 SQL SERVER BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)。  
  
> [!IMPORTANT]  
>  必须首先安装 SharePoint 2010 SP1，然后您才能配置 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 数据库服务器的 SharePoint 场。 如果您尚未安装 Service Pack，则应立即安装 Service Pack，然后再开始配置服务器。  
  
 必须安装 PowerPivot for SharePoint。 至少，必须部署场解决方案。 使用 PowerPivot 配置工具或 PowerShell 脚本部署场解决方案。 本主题中提供针对该步骤的说明。  
  
 必须将计算机加入到域中。 为服务指定的帐户必须是域用户帐户。 至少需要一个用于 PowerPivot 服务应用程序的帐户。 如果您配置其他服务（如 Excel Services），则对于您设置的每项服务应具有单独的帐户。  
  
 您必须是场管理员才能向场中添加 PowerPivot for SharePoint。 您必须知道用于向场添加服务器和应用程序的通行短语。  
  
##  <a name="deploywsp"></a>步骤1：部署 PowerPivot 解决方案  
 有两个必须安装和部署的解决方案：场解决方案和 Web 应用程序解决方案。  
  
### <a name="install-and-deploy-the-farm-solution"></a>安装和部署场解决方案
  
 在以前的版本中，SQL Server 安装程序安装和部署了场解决方案。 在此版本中，您必须使用 PowerPivot 配置工具或 PowerShell 脚本部署场解决方案。 不能使用管理中心部署场解决方案。 这是 PowerPivot for SharePoint 配置中不能在管理中心中执行的唯一步骤。 在部署场解决方案后，您可以使用管理中心和本文中的步骤配置 PowerPivot for SharePoint 安装。  
  
 在此步骤中，您将运行 PowerShell 以便安装和部署场解决方案。 有关详细信息，请参阅[使用 Windows PowerShell 的 PowerPivot 配置](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)。  
  
1.  使用 **“以管理员身份运行”** 选项打开 SharePoint 2010 Management Shell。  
  
2.  运行第一个 cmdlet：  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     该 cmdlet 返回解决方案的名称、其解决方案 ID 和 Deployed=False。 在下一步骤中，您将部署解决方案。  
  
3.  运行第二个 cmdlet 以便部署解决方案：  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
### <a name="deploy-the-web-application-solution"></a>部署 web 应用程序解决方案
  
1.  单击 "开始" 按钮，选择 "**所有程序**"，选择 " **Microsoft SharePoint Products 2010**"，然后选择 " **SharePoint 2010 管理中心**"。  
  
2.  在 SharePoint 2010 管理中心的“系统设置”中，单击 **“管理场解决方案”** 。  
  
     您应该看到两个不同的解决方案包：powerpivotfarm.wsp 和 powerpivotwebapp.wsp。 第一个解决方案 (powerpivotfarm.wsp) 必须已部署。 一旦部署该解决方案后，就永远不需要再次部署它。 为管理中心部署第二个解决方案 (powerpivotwebapp.wsp)，但是，您必须为将支持 PowerPivot 数据访问的每个 SharePoint Web 应用程序手动部署此解决方案。  
  
3.  单击 **“powerpivotwebapp.wsp”** 。  
  
4.  单击 "**部署解决方案"。**  
  
5.  在 **"部署到？** " 中，选择要向其添加 PowerPivot 功能支持的 SharePoint web 应用程序。  
  
6.  单击 **“确定”** 中创建非聚集索引。  
  
7.  对也要支持 PowerPivot 数据访问的其他 SharePoint Web 应用程序重复此过程。  
  
##  <a name="Geneva"></a>步骤2：在服务器上启动服务  
 PowerPivot for SharePoint 部署要求您的场包括以下服务：Excel Calculation Services、Secure Store Service 和 Claims to Windows Token Service。  
  
 Claims to Windows Token Service 对于 Excel Services 和 PowerPivot for SharePoint 是必需的。 使用它可以通过当前 SharePoint 用户的 Windows 标识建立与外部数据源的连接。 此服务必须在已启用了 Excel Services 或 PowerPivot for SharePoint 的每台 SharePoint 服务器上运行。 如果该服务尚未启动，您必须立即启动它，以便使 Excel Services 将经过身份验证的请求转发到 PowerPivot 系统服务。  
  
1.  在管理中心的“系统设置”中，单击 **“管理服务器上的服务”** 。  
  
2.  启动 Claims to Windows Token Service。  
  
3.  启动 Excel Calculation Services。  
  
4.  启动 Secure Store Service。  
  
5.  验证 SQL Server Analysis Services 和 SQL Server PowerPivot 系统服务是否都已启动。  
  
##  <a name="createapp"></a>步骤3：创建 PowerPivot 服务应用程序  
 下一步骤是创建 PowerPivot 服务应用程序。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。  
  
2.  在 **“服务应用程序”** 功能区中，单击 **“新建”** 。  
  
3.  选择**SQL Server PowerPivot 服务应用程序**。 如果该服务应用程序未在列表中出现，则 PowerPivot for SharePoint 未安装或者解决方案未部署。  
  
4.  在 "**创建新的 PowerPivot 服务应用程序**" 页中，输入应用程序的名称。 默认值为 Get-powerpivotserviceapplication\<号 >。 如果您创建多个 PowerPivot 服务应用程序，则说明性的名称将有助于其他管理员理解应用程序的使用方式。  
  
5.  在“应用程序池”中，创建一个新的应用程序池并且为其选择一个安全帐户。 域用户帐户是必需的。  
  
6.  在 "**数据库服务器**" 中，选择要在其上创建服务应用程序数据库的数据库服务器。 默认值是承载场配置数据库的 SQL Server 数据库引擎实例。  
  
7.  在 "**数据库名称**" 中，默认值为 PowerPivotServiceApplication1_\<guid >。 默认数据库名称对应于服务应用程序的默认名称。 如果您输入了唯一的服务应用程序名称，则遵循您的数据库名称的类似命名约定，以便可以一起管理它们。  
  
8.  在 **“数据库身份验证”** 中，默认值是 “Windows 身份验证”。 如果您选择 **“SQL 身份验证”** ，请参考 SharePoint 管理员指南以便了解有关如何在 SharePoint 部署中使用此身份验证类型的最佳实践。  
  
9. 选中 "**将此 PowerPivot 服务应用程序的代理添加到默认代理组**" 复选框。 这会将该服务应用程序连接添加到默认服务连接组。 您必须在默认连接组中具有至少一个 PowerPivot 服务应用程序。  
  
     如果某一 PowerPivot 服务应用程序已在默认连接组中列出，则不要向该组中添加第二个服务应用程序。 向默认连接组中添加两个类型相同的服务应用程序不是支持的配置。 有关如何在连接组中使用附加服务应用程序的详细信息，请参阅[将 PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)。  
  
10. 单击 **“确定”** 。 。该服务将在场的服务应用程序列表中与其他托管服务显示在一起。  
  
##  <a name="ExcelServ"></a>步骤4：启用 Excel Services  
 PowerPivot for SharePoint 要求 Excel Services 支持场中的 PowerPivot 数据访问。 您可以通过确认 Excel Services 应用程序是否出现在管理中心的服务应用程序列表中，确定 Excel Services 是否已启用。 如果 Excel Services 未列出，则执行以下步骤以便立即启用它。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。  
  
2.  在 "服务应用程序" 功能区中的 "创建" 中，单击 "**新建**"。  
  
3.  选择 " **Excel Services 应用程序**"。  
  
4.  在“创建新的 Excel Services 应用程序”中，指定一个名称（例如“Excel Services 应用程序”）。  
  
5.  在“应用程序池”中，选择“创建”以便创建一个新的应用程序池并且为其提供一个说明性名称（例如“Excel Services 应用程序池”）。  
  
6.  在“可配置”中，为此应用程序池标识选择一个 Windows 域用户帐户。  
  
7.  保持默认复选框，该复选框将服务应用程序代理添加到默认服务连接列表。  
  
8.  单击 **“确定”** 中创建非聚集索引。  
  
9. 单击您刚创建的 Excel Services 应用程序。  
  
10. 单击 "**受信任的文件位置**"，并在此页上选择你的可信位置。 （通常，此列在地址列中作为**http://** 列出。）若要确保 Excel Services 和 PowerPivot 服务都有权访问该工作簿，您必须将 SharePoint 作为 Excel Services 受信任位置包括在内。 PowerPivot 系统服务无法访问在 SharePoint 场的外部存储的工作簿。  
  
11. 在 "工作簿属性" 区域中，将 "**最大工作簿大小**" 设置为50。  
  
12. 在 "外部数据" 中，将 "**允许外部数据**" 设置为**受信任的数据连接库和嵌入**。 此设置是工作簿中 PowerPivot 数据访问所必需的。  
  
13. 清除 "**数据刷新时警告**" 复选框，以允许在 PowerPivot 库中预览单个工作表。 如果您选择保留该警告并且工作簿设置指定在打开时刷新，则可能得到的是警告的单个预览图像，而非工作簿中的页面。  
  
14. 单击 **“确定”** 中创建非聚集索引。  
  
##  <a name="SSS"></a>步骤5：启用 Secure Store Service 和配置数据刷新  
 PowerPivot for SharePoint 要求 Secure Store Service 以便存储凭据和无人参与的执行帐户以便用于数据刷新。 您可以通过确认安全存储区服务是否出现在服务应用程序的列表中，确定安全存储区服务是否已启用。  
  
> [!IMPORTANT]  
>  即使安全存储区服务已启用，您仍要确认是否已为其生成了主密钥。 有关说明，请参阅以下过程中的“第二部分：生成主密钥”。  
  
 如果安全存储区服务未列出，则执行以下步骤以便立即启用它。 通过启用安全存储区服务，工作簿作者和文档所有者在为其发布的工作簿计划数据刷新时间时，可以访问范围更广的数据源连接选项。  
  
##### <a name="part-1-enable-secure-store-service"></a>第一部分：启用 Secure Store Service  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。  
  
2.  在 "服务应用程序" 功能区中的 "创建" 中，单击 "**新建**"。  
  
3.  选择**Secure Store Service**。  
  
4.  在 "**创建安全存储区应用程序**" 页中，输入应用程序的名称。  
  
5.  在 "**数据库**" 中，指定将承载此服务应用程序的数据库的 SQL Server 实例。 默认值是承载场配置数据库的 SQL Server 数据库引擎实例。  
  
6.  在 "**数据库名称**" 中，输入服务应用程序数据库的名称。 默认值为 Secure_Store_Service_DB_\<guid >。 该默认名称对应于服务应用程序的默认名称。 如果您输入了唯一的服务应用程序名称，则遵循您的数据库名称的类似命名约定，以便可以一起管理它们。  
  
7.  在 **“数据库身份验证”** 中，默认值是 “Windows 身份验证”。 如果您选择“SQL 身份验证”，请参考 SharePoint 管理员指南中有关如何在场中使用该身份验证类型的说明。  
  
8.  在 "应用程序池" 中，选择 "**新建应用程序池"。** 请指定一个说明性名称，这将帮助其他服务器管理员标识使用此应用程序池的方式。  
  
9. 为应用程序池选择一个安全帐户。 指定要使用域用户帐户的托管帐户。  
  
10. 接受剩余的默认值，然后单击 **"确定"。** 服务应用程序将在场的服务应用程序列表中与其他托管服务显示在一起。  
  
##### <a name="part-2-generate-the-master-key"></a>第二部分：生成主密钥  
  
1.  单击列表中的 Secure Store Service 务应用程序。  
  
2.  在 "服务应用程序" 功能区中，单击 "**管理**"。  
  
3.  在 "密钥管理" 中，单击 "**生成新密钥**"。  
  
4.  输入然后确认通行短语。 该通行短语将用于添加其他安全存储区共享服务应用程序。  
  
5.  单击 **“确定”** 中创建非聚集索引。  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>第三部分：配置无人参与的 PowerPivot 数据刷新帐户  
 为 PowerPivot 数据访问创建无人参与的数据刷新帐户通常是数据刷新期间外部数据访问所必需的。 例如，如果未启用 Kerberos，则您必须创建 PowerPivot 服务可用于连接到外部数据源的无人参与的帐户。  
  
 有关如何创建无人参与的 PowerPivot 数据刷新帐户或在数据刷新中使用的其他存储凭据的说明，请参阅[配置 PowerPivot 无人参与&#40;的&#41;数据刷新帐户 PowerPivot for SharePoint](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md)和[配置用于 PowerPivot 数据刷新&#40;PowerPivot for SharePoint&#41;的存储凭据](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
##  <a name="Usage"></a>步骤6：启用使用情况数据收集  
 PowerPivot for SharePoint 使用 SharePoint 使用情况数据收集基础结构来收集与 PowerPivot 在整个场中的使用情况有关的信息。 尽管使用情况数据始终是 SharePoint 安装的一部分，但可能需要首先启用它，然后才能使用它。 有关说明，请参阅[为&#40;PowerPivot for SharePoint 配置使用情况数据收集](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint)。  
  
##  <a name="Upload"></a>步骤7：增加 SharePoint Web 应用程序和 Excel Services 的最大上载大小  
 因为 PowerPivot 工作簿可能很大，所以，您可能要增加最大文件大小。 有两个要配置的文件大小设置：针对 Web 应用程序的“最大上载大小”和 Excel Services 中的“最大工作簿大小”。 在这两个应用程序中，最大文件大小应该设置为相同值。 有关说明，请参阅[配置最大文件&#40;上&#41;传大小 PowerPivot for SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)。  
  
##  <a name="activatePP"></a>步骤8：为网站集激活 PowerPivot 功能集成  
 网站集级别的功能激活使应用程序页和模板可用于您的站点，包括用于计划的数据刷新的配置页以及用于 PowerPivot 库和数据馈送库的应用程序页。  
  
1.  在 SharePoint 站点上，单击 **“网站操作”** 。  
  
     默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着，你通常可以通过输入 http://\<计算机名 > 来访问 SharePoint 站点以打开根网站集。  
  
2.  单击 **“网站设置”** 。  
  
3.  在“网站集管理”中，单击 **“网站集功能”** 。  
  
4.  向下滚动页面，直至找到 " **PowerPivot 集成网站集功能**"。  
  
5.  单击 **“激活”** 。  
  
6.  通过打开各站点并单击 **“网站操作”** ，对于其他网站集重复上述操作。  
  
 有关详细信息，请参阅[在管理中心为网站集激活 PowerPivot 功能集成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)。  
  
##  <a name="bkmk_redist"></a>步骤9：在 SQL Server 2012 PowerPivot for SharePoint 实例上安装 OLE DB 提供程序的 SQL Server 2008 R2 版本  
 如果您想要在同一台服务器上并行运行 PowerPivot 工作簿的较旧版本和较新版本，则必须在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint 服务器上安装 SQL Server 2008 R2 中随附的 Analysis Services OLE DB 访问接口。  
  
 安装该访问接口后，将允许在数据连接字符串中引用 MSOLAP.4 的工作簿在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot 服务器上按预期方式工作。 安装 SQL Server 2008 R2 OLE DB 访问接口是升级在 PowerPivot for Excel 的早期版本中创建的工作簿的另一种方法。  
  
 可以从[SQL Server 2008 R2 功能包 "页](https://go.microsoft.com/fwlink/?LinkId=159570)下载提供程序。 查找 microsoft **® Analysis Services OLE DB Provider For microsoft® SQL Server® 2008 R2**，然后下载 `SQLServer2008_ASOLEDB10.msi` 安装程序的 x64 包。  
  
 有关安装提供程序的详细信息，包括验证步骤，请参阅[在 SharePoint 服务器上安装 Analysis Services OLE DB Provider](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
##  <a name="verifyinstall"></a>步骤10：验证安装  
 当用户或应用程序打开包含 PowerPivot 数据的 Excel 工作簿时，在场中发生 PowerPivot 查询处理。 至少，您可以检查 SharePoint 网站上的页面以便确认 PowerPivot 功能可用。 但是，若要完全验证某一安装，您必须具有可发布到 SharePoint 并从库中访问的 PowerPivot 工作簿。 出于测试目的，您可以发布已包含 PowerPivot 数据的示例工作簿并使用它来确认 SharePoint 集成已正确配置。  
  
 若要验证 PowerPivot 与 SharePoint 网站的集成，请执行以下操作：  
  
1.  在浏览器中，打开您创建的 Web 应用程序。 如果使用了默认值，则可以在 URL 地址中指定 http://\<计算机名 >。  
  
2.  验证 PowerPivot 数据访问和处理功能在应用程序中可用。 您可以通过验证 PowerPivot 提供的库模板是否存在来验证此可用性：  
  
    1.  在 "网站操作" 上，单击 "**更多选项 ...** "  
  
    2.  在 "库" 中，应会看到 "**数据馈送库**" 和 " **PowerPivot 库**"。 这些库模板由 PowerPivot 功能提供，并且在正确集成了该功能的情况下在“库”列表中将可见。  
  
 若要验证服务器上的 PowerPivot 数据访问，请执行以下操作：  
  
1.  将 PowerPivot 工作簿上载到 PowerPivot 库或任何 SharePoint 库。  
  
2.  单击该文档以便从库中打开它。  
  
3.  单击某个切片器或对数据进行筛选以启动 PowerPivot 查询。 该服务器将在后台加载 PowerPivot 数据并返回结果。 在下一步骤中，您将连接到该服务器以便确认数据已加载并且缓存。  
  
4.  从“开始”菜单中的 Microsoft SQL Server 2008 R2 程序组启动 SQL Server Management Studio。 如果未在您的服务器上安装此工具，则可以跳到最后一步以便确认缓存文件是否存在。  
  
5.  在“服务器类型”中，选择 **“Analysis Services”** 。  
  
6.  在 "服务器名称" 中，输入 **\<server-name > \powerpivot**，其中 **\<Server name >** 是具有 PowerPivot for SharePoint 安装的计算机的名称。  
  
7.  单击 **“连接”** 。  
  
8.  在对象资源管理器中，单击 "**数据库**" 查看加载的 PowerPivot 数据文件的列表。  
  
9. 在计算机文件系统上，检查以下文件夹以便确定文件是否已缓存到磁盘。 存在缓存文件将进一步证实您的部署正常工作。 若要查看文件缓存，请转到 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 文件夹。  
  
##  <a name="nextsteps"></a>安装后步骤  
 在验证了安装后，通过创建 PowerPivot 库或优化单独的配置设置完成服务配置。 为了充分利用您刚安装的服务器组件，可以下载 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 以便创建然后发布您的第一个 PowerPivot 工作簿。  
  
### <a name="install-data-providers-used-for-data-refresh"></a>安装用于数据刷新的数据访问接口  
 如果启用了刷新数据，则服务器将需要通过 PowerPivot 客户端应用程序用来导入原始数据的相同数据访问接口来进行外部数据访问（例如，如果最初导入数据时使用的是 32 位访问接口，则当服务器端数据刷新访问相同的外部数据源时，也需要 32 位访问接口）。 有关详细信息，请参阅[通过 SharePoint 2010 进行 PowerPivot 数据刷新](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)。  
  
### <a name="install-adonet-data-services"></a>安装 ADO.NET Data Services  
 如果您想要将 SharePoint 列表作为数据馈送导出，则必须安装 ADO.NET Data Services 3.5 SP1。 有关说明，请参阅[安装 ADO.NET Data Services 以支持 SharePoint 列表的数据馈送导出](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
### <a name="create-a-powerpivot-gallery"></a>创建 PowerPivot 库  
 PowerPivot 库是包括预览和展示选项以便在 SharePoint 网站上查看 PowerPivot 工作簿的一种库。 使用 PowerPivot 库可以发布和查看为其预览功能推荐的 PowerPivot 工作簿。 此外，如果您还将 Reporting Services 部署到了同一 SharePoint 服务器上，则 PowerPivot 库将简化创建报表的工作。 您可以从 PowerPivot 库内启动报表生成器，以便在已发布的 PowerPivot 工作簿的基础上创建新的报表。 有关创建和使用库的详细信息，请参阅[创建和自定义 Powerpivot 库](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery)并[使用 powerpivot 库](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)。  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>在 Excel Services 中创建其他可信站点  
 您可以在 Excel Services 中添加可信站点，以便在提供 Excel 工作簿和 PowerPivot 数据的站点上改变权限和配置设置。 有关详细信息，请参阅 [Create a trusted location for PowerPivot sites in Central Administration](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration)。  
  
### <a name="tune-configuration-settings"></a>优化配置设置  
 PowerPivot 服务应用程序使用默认属性和值创建。 您可以修改单独服务应用程序的配置设置，以便更改分配请求所采用的方法、设置服务器超时、更改查询响应报告事件的阈值或者指定保留多长时间的使用情况数据。 有关管理中心中的配置或者在 SharePoint Web 应用程序中使用 PowerPivot 功能的详细信息，请参阅[在管理中心中管理和配置 Powerpivot 服务器](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)。  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>安装 PowerPivot for Excel 和生成 PowerPivot 工作簿  
 在您在场中安装了服务器组件后，可以创建使用嵌入的 PowerPivot 数据的第一个 Excel 2010 工作簿，然后将其发布到 Web 应用程序中的 SharePoint 库。 在您可以生成包含 PowerPivot 数据的 Excel 工作簿前，必须从安装 Excel 2010 开始，然后安装 PowerPivot for Excel 外接程序，该外接程序扩展 Excel 以便支持 PowerPivot 数据导入和内容丰富。  
  
### <a name="add-servers-or-applications"></a>添加服务器或应用程序  
 在您部署 PowerPivot 解决方案时，对于 Web 应用程序中的所有网站集，将在网站集级别激活功能集成。 一段时间后在您创建新的 Web 应用程序时，必须将 powerpivotwebapp 解决方案部署到各应用程序。 有关说明，请参阅[将 PowerPivot 解决方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)。  
  
 根据您配置 PowerPivot 服务应用程序的方式，PowerPivot 系统服务将添加到默认的连接组中，并且它将可用于使用默认连接的所有 Web 应用程序。 但是，如果您配置了 Web 应用程序以便使用自定义服务应用程序连接列表，则需要将 PowerPivot 服务应用程序添加到您想要为其启用 PowerPivot 数据处理的各 SharePoint Web 应用程序中。 有关详细信息，请参阅[将 PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)。  
  
 一段时间后，如果您确定需要附加的数据存储和处理能力，则可以将第二个 PowerPivot for SharePoint 服务器实例添加到场中。 安装过程与您添加第一个服务器所执行的步骤几乎完全相同，只有在对如何指定实例名称和服务帐户信息的要求方面除外。 有关说明，请参阅[部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014   的版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
 [配置 PowerPivot 服务帐户](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [在管理中心中创建和配置 PowerPivot 服务应用程序](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca)   
 [将 PowerPivot 解决方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)   
 [在管理中心中为网站集激活 PowerPivot 功能集成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)   
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
