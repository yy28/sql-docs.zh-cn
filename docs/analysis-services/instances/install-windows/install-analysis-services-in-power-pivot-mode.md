---
title: 在 Power Pivot 模式下安装 Analysis Services |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e3e973c30ea178a544b9da3501d88f43cf9b1ddb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63054777"
---
# <a name="install-analysis-services-in-power-pivot-mode"></a>在 Power Pivot 模式下安装 Analysis Services。
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本主题中的过程将指导你以适用于 SharePoint 部署的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式在单台服务器上安装 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务器。 涉及的步骤包括运行 SQL Server 安装向导以及使用 SharePoint 管理中心的配置任务。  
  
##  <a name="bkmk_background"></a> 背景  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 是在 SharePoint 2016 或 SharePoint 2013 场中提供 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 数据访问的中间层和后端服务的集合。  
  
-   **后端服务：** 如果您使用[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]for Excel 来创建包含分析数据的工作簿，则必须[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]for SharePoint 才能访问服务器环境中的数据。 你可以在安装了 SharePoint Server 的计算机上或没有 SharePoint 软件的其他计算机上运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对 SharePoint 没有任何依赖关系。  
  
     **注意：** 本主题介绍安装[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服务器和后端服务。  
  
-   **中间层：** 增强功能[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]中包括 SharePoint 体验[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]库、 计划数据刷新、 管理仪表板和数据访问接口。 有关安装和配置中间层的详细信息，请参阅下面的内容：  
  
    -   [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [配置 Power Pivot 和部署解决方案 (SharePoint 2016)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> 先决条件  
  
1.  你必须为本地管理员才能运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序。  
  
2.  SharePoint Server 企业版是 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 所必需的。 您也可以使用评估企业版。  
  
3.  必须将计算机加入到与 Office Online Server (SharePoint 2016) 或 Excel Services (SharePoint 2013) 相同的 Active Directory 林中的域。  
  
4.  必须提供 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 实例名称。 在你要在其上以 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式安装 Analysis Services 的计算机上，你无法拥有现有的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 命名实例。  
  
     **注意：** 实例名称必须为 POWERPIVOT。  
  
5.  查看 [SharePoint 模式下的 Analysis Services 服务器的硬件和软件要求](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)。  
  
6.  请在 [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md)中查看发行说明。  
  
###  <a name="bkmk_sqleditions"></a> SQL Server 版本要求  
 并不是所有的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]版本中都提供了商业智能功能。 有关详细信息，请参阅[功能支持的 Analysis Services SQL Server 2016 各个版本](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)并[SQL Server 2016 的组件和版本](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
##  <a name="InstallSQL"></a> 步骤 1：安装 Power Pivot for SharePoint  
 在此步骤中，你将运行 SQL Server 安装程序以在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式下安装 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务器。 在后续步骤中，将 Excel Services 配置为使用此服务器的工作簿数据模型。  
  
1.  运行 SQL Server 安装向导 (Setup.exe)。  
  
2.  在左侧导航中，选择“安装”  。  
  
3.  选择“全新 SQL Server 独立安装或向现有安装添加功能”  。  
  
4.  如果看到 **“产品密钥”** 页，请指定 Evaluation Edition 或者为 Enterprise Edition 的许可副本输入产品密钥。 选择“下一步”  。 有关版本的详细信息，请参阅 [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
5.  查看并接受 Microsoft 软件许可协议条款，然后选择“下一步”  。  
  
6.  如果显示 **“全局规则”** 页，请查看安装向导显示的所有规则信息。  
  
7.  在“Microsoft Update”  页上，建议你使用 Microsoft Update 检查更新，然后选择“下一步”  。  
  
8.  **“安装安装程序文件”** 页将运行几分钟。 查看所有规则警告或失败的规则，然后选择“下一步”  。  
  
9. 如果看到其他的“安装程序支持规则”  ，则查看所有警告并选择“下一步”  。  
  
     **注意：** 因为启用了 Windows 防火墙，您将看到打开端口以便启用远程访问的警告。  
  
10. 在“安装角色”  页上，选择“SQL Server 功能安装”  。  
  
     选择“**下一步**”。  
  
11. 在“功能选择”页上，选择“Analysis Services”  。 此选项允许你安装三种 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式中的任何一种。 在后续步骤中将选择该模式。 选择“下一步”  。  
  
12. 在“实例配置”  页上，选择“命名实例”  ，然后对实例名称键入“POWERPIVOT”  。单击“下一步”  。  
  
     ![SQL 安装程序的登录页的实例配置](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "SQL 安装程序的登录页的实例配置")  
  
13. 在 **“服务器配置”** 页上，为自动的 **启动类型**配置所有服务。 为 **SQL Server Analysis Services**指定所需的域帐户和密码，即下图中的 **(1)** 。  
  
    -   对于 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，您可使用 **域用户** 帐户或 **NetworkService** 帐户。 请勿使用 LocalSystem 或 LocalService 帐户。  
  
    -   如果您添加了 SQL Server 数据库引擎和 SQL Server 代理，则可以将服务配置为在域用户帐户或者默认虚拟帐户下运行。  
  
    -   切勿使用您自己的域用户帐户来设置服务帐户。 这样做会向服务器授予您在网络中对资源拥有的相同权限。 如果恶意用户威胁服务器，则该用户将基于您的域凭据登录。 并且该用户有权下载或使用您所能下载或使用的相同数据和应用程序。  
  
     选择“**下一步**”。  
  
     ![SQL 安装程序-服务器配置登陆页面](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "SQL 安装程序-服务器配置登陆页面")  
  
14. 如果安装 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]，则将显示 **“数据库引擎配置”** 页。 在“ [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 配置”中，选择“添加当前用户”  以授予你的用户帐户对数据库引擎实例的管理员权限。  
  
     选择“**下一步**”。  
  
15. 在“Analysis Services 配置”  页上，在“服务器模式”  下选择“PowerPivot 模式”   
  
     ![SQL 安装程序-Analysis Services 配置登录页](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "SQL 安装程序的登录页上的 Analysis Services 配置")  
  
16. 在“Analysis Services 配置”  页上，选择“添加当前用户”  以向你的用户帐户授予管理权限。 在完成安装程序后，您将需要管理权限以便对服务器进行配置。  
  
    -   在同一页中，添加也要求管理权限的任何人士的 Windows 用户帐户。 例如，如果用户想要在 [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] 中连接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 实例以便排除数据库连接问题，则任何此类用户都必须具有系统管理员权限。 添加可能需要立即排除服务器问题或管理服务器的任何人士的用户帐户。  
  
    -   > [!NOTE]  
        >  所有需要具有对 Analysis Services 服务器实例的访问权限的服务应用程序均需要具有 Analysis Services 管理权限。 例如，分别为 Excel Services、Power View 和 Performance Point Services 添加服务帐户。 此外，添加 SharePoint 场帐户，该帐户用作承载管理中心的 Web 应用程序的标识。  
  
     选择“**下一步**”。  
  
17. 在“错误报告”  页上，选择“下一步”  。  
  
18. 在“准备安装”  页上，选择“安装”  。  
  
19. 如果你看到了“需要重新启动计算机”  对话框，选择“确定”  。  
  
20. 安装完毕后，选择“关闭”  。  
  
21. 重新启动计算机。  
  
22. 如果您的环境中有防火墙，请阅读 SQL Server 联机丛书主题 [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
### <a name="verify-the-sql-server-installation"></a>验证 SQL Server 安装  
 验证 Analysis Services 服务是否正在运行。  
  
1.  在 Microsoft Windows 中，单击“开始”  ，选择“所有程序”  和“Microsoft SQL Server 2016”  组。  
  
2.  选择“SQL Server Management Studio”  。  
  
3.  连接到 Analysis Services 实例，例如 **[你的服务器名称]\POWERPIVOT**。 如果您可连接到该实例，则验证服务是否正在运行。  
  
##  <a name="bkmk_config"></a> 步骤 2：配置基本 Analysis Services SharePoint 集成  
 下列步骤介绍与 SharePoint 文档库中的 Excel 高级数据模型交互所需的配置更改。 在安装 SharePoint 和 SQL Server Analysis Services 之后完成这些步骤。  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Excel Services 已从 SharePoint 2016 中删除，而使用了用于托管 Excel 的 Office Online Server。  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>授予 Office Online Server 计算机帐户对 Analysis Services 的管理权限  
 如果在 Analysis Services 安装过程中，你已将 Office Online Server 计算机帐户添加为 Analysis Services 管理员，则无需完成此部分。  
  
1.  在 Analysis Services 服务器上，启动 SQL Server Management Studio 并连接到 Analysis Services 实例，例如 `[MyServer]\POWERPIVOT`。  
  
2.  在“对象资源管理器”中，右键单击实例名称，然后选择“属性”  。  
  
     ![查看 SSAS 服务器的属性](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "查看 SSAS 服务器的属性")  
  
3.  在左窗格中，选择“安全性”  。 添加在其上安装 Office Online Server 的计算机账户。  
  
     ![SSAS 服务器的安全设置](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "SSAS 服务器的安全设置")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>将 Analysis Services 服务器注册到 Office Online Server  
 你将希望在 Office Online Server 上执行这些步骤。  
  
-   以管理员身份打开 PowerShell 命令窗口。  
  
-   加载 `OfficeWebApps` PowerShell 模块。  
  
     `Import-Module OfficeWebApps`  
  
-   添加 Analysis Services 服务器，例如 `[MyServer]\POWERPIVOT`。  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>授予对 Analysis Services 的 Excel Services 服务器管理权限  
 如果在 Analysis Services 安装过程中，您将 Excel Services 应用程序服务帐户添加为 Analysis Services 管理员，则无需完成此部分。  
  
1.  在 Analysis Services 服务器上，启动 SQL Server Management Studio 并连接到 Analysis Services 实例，例如 `[MyServer]\POWERPIVOT`。  
  
2.  在“对象资源管理器”中，右键单击实例名称，然后选择“属性”  。  
  
     ![查看 SSAS 服务器的属性](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "查看 SSAS 服务器的属性")  
  
3.  在左窗格中，选择“安全性”  。 添加您在步骤 1 中为 Excel Services 应用程序配置的域登录名。  
  
     ![SSAS 服务器的安全设置](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "SSAS 服务器的安全设置")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>为 Analysis Services 集成配置 Excel Services  
  
1.  在 SharePoint 管理中心的“应用程序管理”组中，单击 **“管理服务应用程序”** 。  
  
2.  单击服务应用程序的名称，默认名称为 **“Excel 服务应用程序”** 。  
  
3.  在 **“管理 Excel Services 应用程序”** 页上，单击 **“数据模型设置”** 。  
  
4.  单击 **“添加服务器”** 。  
  
5.  在“服务器名称”  中，键入 Analysis Services 服务器名称和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 实例名称。 例如 `MyServer\POWERPIVOT`。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 实例名称是必需的。  
  
     键入说明。  
  
6.  单击 **“确定”** 。  
  
7.  更改将在几分钟后生效，您也可以 **“停止”** 和 **“启动”** 服务 **“Excel Calculation Services”** 。 若要  
  
     另一个选项是使用管理权限打开命令提示符，并键入 `iisreset /noforce`。  
  
     您可通过查看 ULS 日志中的条目来验证 Excel Services 是否能识别服务器。 您将看到类似于以下内容的条目：  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> 步骤 3：验证集成  
 下列步骤指导你创建和上载新的工作簿以验证 Analysis Services 集成。 您将需要 SQL Server 数据库才能完成这些步骤。  
  
1.  **注意：** 如果您已具有包含切片器或筛选器的高级工作簿，可以将其上载到 SharePoint 文档库并验证您是否能与切片器和筛选器进行交互通过文档库视图。  
  
2.  在 Excel 中启动新的工作簿。  
  
3.  在“数据”选项卡上，选择“获取外部数据”  中功能区上的“从其他源”  。  
  
4.  选择 **“从 SQL Server”** 。  
  
5.  在 **“数据连接向导”** 中，输入包含您要使用的数据库的 SQL Server 实例的名称。  
  
6.  在登录凭据下，验证是否选择了“使用 Windows 身份验证”  ，然后选择“下一步”  。  
  
7.  选择要使用的数据库。  
  
8.  验证是否选中了 **“连接到特定表”** 复选框。  
  
9. 选择“启用多表选择并将表添加到 Excel 数据模型”  复选框。  
  
10. 选择要导入的表。  
  
11. 选择“导入所选表之间的关系”  复选框，然后选择“下一步”  。 从关系数据库中导入多个表使您可使用已关联的表。 您可省略步骤，因为您无需手动构建关系。  
  
12. 在向导的“保存数据连接文件并完成”  页中，键入连接的名称并选择“完成”  。  
  
13. 将出现 **“导入数据”** 对话框。 选择“数据透视表”  ，然后选择“确定”  。  
  
14. 数据透视表字段列表将出现在工作簿中。   
    在该字段列表上，选择“全部”  选项卡  
  
15. 向该字段列表的行、列和值区域添加字段。  
  
16. 将切片器或筛选器添加到数据透视表。 **请勿跳过此步骤**。 切片器或筛选器是将帮助您验证 Analysis Services 安装的元素。  
  
17. 将工作簿保存到 SharePoint 场中的文档库。 你还可将工作簿保存到文件共享，然后将其上传到 SharePoint 文档库。  
  
18. 选择工作簿的名称以在 Excel Online 中查看它，然后单击切片器或更改之前添加的筛选器。 如果出现数据更新，你将知道 Analysis Services 已安装并且可用于 Excel。 如果在 Excel 中打开工作簿，您将使用缓存副本，而不使用 Analysis Services 服务器。  
  
##  <a name="bkmk_firewall"></a> 将 Windows 防火墙配置为允许 Analysis Services 访问  
 使用主题 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 中的信息确定你是否需要在防火墙中取消阻止端口，以便允许对 Analysis Services 或 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 所必需的。 您可以采用本主题中提供的步骤来配置端口和防火墙设置。 实际上，您应该一起执行这些步骤以便能够访问您的 Analysis Services 服务器。  
  
##  <a name="bkmk_upgrade_workbook"></a> 升级工作簿和计划的数据刷新  
 升级在以前版本的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 中创建的工作簿所需的步骤取决于创建该工作簿的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 版本。 有关详细信息，请参阅 [升级工作簿和计划的数据刷新 (SharePoint 2013)](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_multiple_servers"></a> 单服务器安装之外-Power Pivot for Microsoft SharePoint  
 **Web 前端 (WFE)** 或**中间层：** :若要使用[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]SharePoint 模式下在更大的 SharePoint 场，以安装其他服务器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]功能到场中，运行安装程序包**spPowerPivot16.msi (SharePoint 2016) 或 spPowerPivot.msi (SharePoint2013)，** 每台 SharePoint 服务器上。 spPowerPivot16.msi 或 spPowerPivot.msi 安装所需的数据提供程序以及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016（或 2013）配置工具。  
  
 有关安装和配置中间层的详细信息，请参阅下面的内容：  
  
-   [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   若要下载 .msi，请参阅 [Microsoft SQL Server 2016 Power Pivot for Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **冗余性和服务器负荷：** 安装第二个或更多[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的服务器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式下将提供的冗余[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服务器功能。 附加的服务器还将在各服务器上分散负荷。 有关详细信息，请参见以下内容：  
  
-   [配置用于处理 Excel Services (SharePoint 2013) 中的数据模型的 Analysis Services](http://technet.microsoft.com/library/jj614437(v=office.15))。  
  
-   [管理 Excel Services 数据模型设置 (SharePoint 2013)](http://technet.microsoft.com/library/jj219780(v=office.15))。  
  
 ![SharePoint 设置](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")[提交反馈和联系信息通过 SQL Server 反馈](https://feedback.azure.com/forums/908035-sql-server)。  
  
## <a name="see-also"></a>请参阅  
 [将 Power Pivot 迁移到 SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [升级工作簿和计划的数据刷新 (SharePoint 2013)](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
