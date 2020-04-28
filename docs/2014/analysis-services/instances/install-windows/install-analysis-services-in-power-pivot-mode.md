---
title: PowerPivot for SharePoint 2013 安装 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95642654da9492087b3720e1b85c369131b55ed2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487388"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>PowerPivot for SharePoint 2013 安装
  本主题中的过程将指导您以 SharePoint 部署模式在单台服务器上安装 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器。 涉及的步骤包括运行 SQL Server 安装向导以及使用 SharePoint 2013 管理中心的配置任务。  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 |SharePoint 201  
  
 **本主题内容：**  
  
 [背景](#bkmk_background)  
  
 [先决条件](#bkmk_prereq)  
  
 [步骤 1：安装 PowerPivot for SharePoint](#InstallSQL)  
  
 [步骤 2：配置基本 Analysis Services SharePoint 集成](#bkmk_config)  
  
 [步骤 3：验证集成](#bkmk_verify)  
  
 [配置 Windows 防火墙以允许 Analysis Services 访问](#bkmk_firewall)  
  
 [升级工作簿和计划的数据刷新](#bkmk_upgrade_workbook)  
  
 [除单服务器安装之外-PowerPivot for Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="background"></a><a name="bkmk_background"></a> 背景  
 PowerPivot for SharePoint 是在 SharePoint 2013 场中提供 PowerPivot 数据访问的中间层和后端服务的集合。  
  
-   **后端服务：** 如果您使用 PowerPivot for Excel 来创建包含分析数据的工作簿，则必须具有 PowerPivot for SharePoint 才能在服务器环境中访问这些数据。 您可在安装了 SharePoint Server 2013 的计算机上或没有 SharePoint 软件的其他计算机上运行 SQL Server 安装程序。 Analysis Services 对 SharePoint 没有任何依赖关系。  
  
     **注意：** 本主题介绍 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器和后端服务的安装。  
  
-   **中间层：** 增强 SharePoint 中 PowerPivot 体验的各项功能，包括 PowerPivot 库、计划数据刷新、管理面板和数据访问接口。 有关安装和配置中间层的详细信息，请参阅下面的内容：  
  
    -   [在 SharePoint 2013 &#40;安装或卸载 PowerPivot for SharePoint 加载项&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
    -   [&#40;SharePoint 2013&#41;配置 PowerPivot 和部署解决方案](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a>先决条件  
  
1.  您必须是本地管理员才能运行 SQL Server 安装程序。  
  
2.  SharePoint Server 2013 企业版是 PowerPivot for SharePoint 所必需的。 您也可以使用评估企业版。  
  
3.  计算机必须加入与 Excel Services 相同的 Active Directory 林中的域。  
  
4.  必须提供 PowerPivot 实例名称。 在您要在其上以 SharePoint 模式安装 Analysis Services 的计算机上，您无法拥有现有的 PowerPivot 命名实例。  
  
5.  [在 SharePoint 模式下查看 Analysis Services 服务器的硬件和软件要求 &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md)。  
  
6.  查看[SQL Server 2012 Service Pack 1 发行说明](https://go.microsoft.com/fwlink/?LinkID=248389)（https://go.microsoft.com/fwlink/?LinkID=248389)）中的发行说明。  
  
###  <a name="sql-server-edition-requirements"></a><a name="bkmk_sqleditions"></a> SQL Server 版本要求  
 并不是所有的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]版本中都提供了商业智能功能。 有关详细信息，请参阅[SQL Server 2012 的版本支持的功能https://go.microsoft.com/fwlink/?linkid=232473) （](https://go.microsoft.com/fwlink/?linkid=232473)以及[SQL Server 2014 的版本和组件](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
 当前发行说明可在[SQL Server 2012 SP1 发行说明](https://go.microsoft.com/fwlink/?LinkID=248389)（https://go.microsoft.com/fwlink/?LinkID=248389)。  
  
 [Microsoft SQL Server 2012 发行说明（https://go.microsoft.com/fwlink/?LinkId=236893)](https://go.microsoft.com/fwlink/?LinkId=236893)。  
  
##  <a name="step-1-install-powerpivot-for-sharepoint"></a><a name="InstallSQL"></a>步骤1：安装 PowerPivot for SharePoint  
 在此步骤中，您将运行 SQL Server 安装程序以便在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。 在后续步骤中，将 Excel Services 配置为使用此服务器的工作簿数据模型。  
  
1.  运行 SQL Server 安装向导 (Setup.exe)。  
  
2.  在左侧导航中，单击 **“安装”** 。  
  
3.  单击 **“全新 SQL Server 独立安装或向现有安装添加功能”**。  
  
4.  如果看到 **“产品密钥”** 页，请指定 Evaluation Edition 或者为 Enterprise Edition 的许可副本输入产品密钥。 单击“下一步”。  有关版本的详细信息，请参阅 [Editions and Components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
5.  查看并接受 Microsoft 软件许可协议条款，然后单击 **“下一步”**。  
  
6.  如果显示 **“全局规则”** 页，请查看安装向导显示的所有规则信息。  
  
7.  在 **“Microsoft Update”** 页上，建议您使用 Microsoft Update 检查更新，然后单击 **“下一步”**。  
  
8.  **“安装安装程序文件”** 页将运行几分钟。 查看所有规则警告或失败的规则，然后单击 **“下一步”**。  
  
9. 如果看到其他 **“安装程序支持规则”**，请查看所有警告并单击 **“下一步”**。  
  
     **注意：** 因为启用了 Windows 防火墙，所以您将看到打开端口以便允许进行远程访问的警告。  
  
10. 在 **“设置角色”** 页中，选择 **“SQL Server PowerPivot for SharePoint”**。 此选项将在 SharePoint 模式下安装 Analysis Services。  
  
     或者，您可以向您的安装添加数据库引擎的实例。 设置新场时，可以添加数据库引擎，并需要数据库服务器来运行该场的配置和内容数据库。 此选项也将安装 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
     如果添加数据库引擎，则将其作为 **PowerPivot** 命名实例安装。 在指定此实例的连接时，按以下格式输入数据库名称：[`servername`]\PowerPivot。  
  
     单击“下一步”。   
  
     ![设置角色](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "安装角色")  
  
11. “功能选择”中会显示功能的只读列表以便供您参考。 不能添加或删除为此角色预先选择的项。 单击“下一步”。   
  
12. 在 **“实例配置”** 页中，将显示“PowerPivot”的只读实例名称供您参考。 该实例名称是必需的并且不能修改。 但是，您可以输入唯一的实例 ID 以便指定说明性的目录名称和注册表项。 单击“下一步”。   
  
13. 在 **“服务器配置”** 页上，为自动的 **启动类型**配置所有服务。 为 **SQL Server Analysis Services**指定所需的域帐户和密码，即下图中的 **(1)** 。  
  
    -   对于 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，您可使用 **域用户** 帐户或 **NetworkService** 帐户。 请勿使用 LocalSystem 或 LocalService 帐户。  
  
    -   如果您添加了 SQL Server 数据库引擎和 SQL Server 代理，则可以将服务配置为在域用户帐户或者默认虚拟帐户下运行。  
  
    -   切勿使用您自己的域用户帐户来设置服务帐户。 这样做会向服务器授予您在网络中对资源拥有的相同权限。 如果恶意用户威胁服务器，则该用户将基于您的域凭据登录。 并且该用户有权下载或使用您所能下载或使用的相同数据和应用程序。  
  
     单击“下一步”。   
  
     ![SSAS Server 配置](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS Server 配置")  
  
14. 如果安装 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]，则将显示 **“数据库引擎配置”** 页。 在“ [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 配置”中，单击 **“添加当前用户”** 以便授予您的用户帐户对数据库引擎实例的管理员权限。  
  
     单击“下一步”。   
  
15. 在 **“Analysis Services 配置”** 页中，单击 **“添加当前用户”** 以便向您的用户帐户授予管理权限。 在完成安装程序后，您将需要管理权限以便对服务器进行配置。  
  
    -   在同一页中，添加也要求管理权限的任何人士的 Windows 用户帐户。 例如，如果用户想要在 [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] 中连接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 实例以便排除数据库连接问题，则任何此类用户都必须具有系统管理员权限。 添加可能需要立即排除服务器问题或管理服务器的任何人士的用户帐户。  
  
    -   > [!NOTE]  
        >  所有需要具有对 Analysis Services 服务器实例的访问权限的服务应用程序均需要具有 Analysis Services 管理权限。 例如，分别为 Excel Services、Power View 和 Performance Point Services 添加服务帐户。 此外，添加 SharePoint 场帐户，该帐户用作承载管理中心的 Web 应用程序的标识。  
  
     单击“下一步”。   
  
16. 在“错误报告”**** 页上，单击“下一步”****。  
  
17. 在 "**准备安装**" 页上，单击 "**安装**"。  
  
18. 如果您看到 **“需要重新启动计算机”** 对话框，请单击 **“确定”**。  
  
19. 安装完成后，单击 **“关闭”**。  
  
20. 重新启动计算机。  
  
21. 如果您的环境中有防火墙，请阅读 SQL Server 联机丛书主题 [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
### <a name="verify-the-sql-server-installation"></a>验证 SQL Server 安装  
 验证 Analysis Services 服务是否正在运行。  
  
1.  在 Microsoft Windows 中，依次单击 **“开始”**、 **“所有程序”** 和 **“Microsoft SQL Server 2012”** 组。  
  
2.  单击 **“SQL Server Management Studio”**。  
  
3.  连接到 Analysis Services 实例，例如 **[你的服务器名称]\POWERPIVOT**。 如果您可连接到该实例，则验证服务是否正在运行。  
  
##  <a name="step-2-configure-basic-analysis-services-sharepoint-integration"></a><a name="bkmk_config"></a>步骤2：配置基本 Analysis Services SharePoint 集成  
 下列步骤介绍与 SharePoint 文档库中的 Excel 高级数据模型交互所需的配置更改。 在安装 SharePoint Server 2013 和 SQL Server Analysis Services 之后完成这些步骤。  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>授予对 Analysis Services 的 Excel Services 服务器管理权限  
 如果在 Analysis Services 安装过程中，您将 Excel Services 应用程序服务帐户添加为 Analysis Services 管理员，则无需完成此部分。  
  
1.  在 Analysis Services 服务器上，启动 SQL Server Management Studio 并连接到 Analysis Services 实例，例如 `[MyServer]\POWERPIVOT`。  
  
2.  在对象资源管理器中，右键单击实例名称，再单击 **“属性”**。  
  
     ![查看 SSAS 服务器的属性](../../../sql-server/install/media/as-ssms-proeprties.gif "查看 SSAS 服务器的属性")  
  
3.  在左窗格中，单击 **“安全性”**。 添加您在步骤 1 中为 Excel Services 应用程序配置的域登录名。  
  
     ![SSAS 服务器的安全设置](../../../sql-server/install/media/as-ssms-security.gif "SSAS 服务器的安全设置")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>为 Analysis Services 集成配置 Excel Services  
  
1.  在 SharePoint 管理中心的“应用程序管理”组中，单击 **“管理服务应用程序”**。  
  
2.  单击服务应用程序的名称，默认名称为 **“Excel 服务应用程序”**。  
  
3.  在 **“管理 Excel Services 应用程序”** 页上，单击 **“数据模型设置”**。  
  
4.  单击 **“添加服务器”**。  
  
5.  在 **“服务器名称”** 中，键入 Analysis Services 服务器名称和 PowerPivot 实例名称。 例如，`MyServer\POWERPIVOT`。 需要 PowerPivot 实例名称。  
  
     键入说明。  
  
6.  单击“确定”  。  
  
7.  更改将在几分钟后生效，您也可以 **“停止”** 和 **“启动”** 服务 **“Excel Calculation Services”**。 功能  
  
     另一个选项是使用管理权限打开命令提示符，并键入 `iisreset /noforce`。  
  
     您可通过查看 ULS 日志中的条目来验证 Excel Services 是否能识别服务器。 您将看到类似于以下内容的条目：  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="step-3-verify-the-integration"></a><a name="bkmk_verify"></a>步骤3：验证集成  
 下列步骤指导你创建和上载新的工作簿以验证 Analysis Services 集成。 您将需要 SQL Server 数据库才能完成这些步骤。  
  
1.  **注意：** 如果您已具有包含切片器或筛选器的高级工作簿，则可将其上载到 SharePoint 文档库并验证您是否能通过文档库视图与切片器和筛选器进行交互。  
  
2.  在 Excel 中启动新的工作簿。  
  
3.  在“数据”选项卡上，单击 **“获取外部数据”** 中功能区上的 **“从其他源”**。  
  
4.  选择 **“从 SQL Server”**。  
  
5.  在 **“数据连接向导”** 中，输入包含您要使用的数据库的 SQL Server 实例的名称。  
  
6.  或使用凭据登录，验证是否选择了 **“使用 Windows 身份验证”** ，然后单击 **“下一步”**。  
  
7.  选择要使用的数据库。  
  
8.  验证是否选中了 **“连接到特定表”** 复选框。  
  
9. 单击 **“启用多表选择并将表添加到 Excel 数据模型”** 复选框。  
  
10. 选择要导入的表。  
  
11. 单击 **“导入所选表之间的关系”** 复选框，然后单击 **“下一步”**。 从关系数据库中导入多个表使您可使用已关联的表。 您可省略步骤，因为您无需手动构建关系。  
  
12. 在向导的 **“保存数据连接文件并完成”** 页中，键入连接的名称并单击 **“完成”**。  
  
13. 将出现 **“导入数据”** 对话框。 选择 **“数据透视表”**，然后单击 **“确定”**。  
  
14. 数据透视表字段列表将出现在工作簿中。   
    在该字段列表上，单击 **“全部”** 选项卡  
  
15. 向该字段列表的行、列和值区域添加字段。  
  
16. 将切片器或筛选器添加到数据透视表。 **请勿跳过此步骤**。 切片器或筛选器是将帮助您验证 Analysis Services 安装的元素。  
  
17. 将工作簿保存到已配置 Excel Services 的 SharePoint Server 2013 上的文档库中。 您还可将工作簿保存到文件共享，然后将其上载到 SharePoint Server 2013 文档库。  
  
18. 单击工作簿的名称以在 SharePoint 中查看它，单击切片器或更改之前添加的筛选器。 如果出现数据更新，则您将知道 Analysis Services 已安装并且可用于 Excel Services。 如果在 Excel 中打开工作簿，您将使用缓存副本，而不使用 Analysis Services 服务器。  
  
##  <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a><a name="bkmk_firewall"></a>将 Windows 防火墙配置为允许 Analysis Services 访问  
 使用主题 [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md) 中的信息可以确定您是否需要在防火墙中取消阻止端口，以便允许对 Analysis Services 或 PowerPivot for SharePoint 的访问。 您可以采用本主题中提供的步骤来配置端口和防火墙设置。 实际上，您应该一起执行这些步骤以便能够访问您的 Analysis Services 服务器。  
  
##  <a name="upgrade-workbooks-and-scheduled-data-refresh"></a><a name="bkmk_upgrade_workbook"></a>升级工作簿和计划的数据刷新  
 升级在以前版本的 PowerPivot 中创建的工作簿所需的步骤取决于创建了该工作簿的 PowerPivot 的版本。 有关详细信息，请参阅 [升级工作簿和计划的数据刷新 (SharePoint 2013)](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)。  
  
##  <a name="beyond-the-single-server-installation--powerpivot-for-microsoft-sharepoint"></a><a name="bkmk_multiple_servers"></a>除单服务器安装之外-PowerPivot for Microsoft SharePoint  
 **Web 前端 (WFE)** 或 **中间层**：若要在更大的 SharePoint 场中在 SharePoint 模式下使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器，以及将其他 PowerPivot 功能安装到场中，请在每台 SharePoint 服务器上运行安装程序包 **spPowerPivot.msi** 。 spPowerPivot.msi 安装所需的数据访问接口以及 PowerPivot for SharePoint 2013 配置工具。  
  
 有关安装和配置中间层的详细信息，请参阅下面的内容：  
  
-   [在 SharePoint 2013 &#40;安装或卸载 PowerPivot for SharePoint 加载项&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
-   要下载 .msi，请参阅 [Microsoft SQL Server 2014 PowerPivot for Microsoft SharePoint 2013](https://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [&#40;SharePoint 2013&#41;配置 PowerPivot 和部署解决方案](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
 **冗余性和服务器负荷：** 在 SharePoint 模式下安装第二台或更多的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器将提供 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器功能的冗余性。 附加的服务器还将在各服务器上分散负荷。 有关详细信息，请参阅以下主题：  
  
-   [配置 Analysis Services 以便在 Excel Services 中处理数据模型](https://technet.microsoft.com/library/jj614437\(v=office.15\))（https://technet.microsoft.com/library/jj614437(v=office.15))。  
  
-   [管理 Excel Services 数据模型设置（SharePoint Server 2013）](https://technet.microsoft.com/library/jj219780\(v=office.15\)) （https://technet.microsoft.com/library/jj219780(v=office.15))。  
  
 ![SharePoint 设置](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")https://connect.microsoft.com/SQLServer/Feedback)[通过 Microsoft SQL Server Connect （）提交反馈和联系信息](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另请参阅  
 [将 PowerPivot 迁移到 SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)   
 [在 SharePoint 2013 &#40;安装或卸载 PowerPivot for SharePoint 加载项&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)   
 [&#40;SharePoint 2013&#41;升级工作簿和计划的数据刷新](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)  
  
  
