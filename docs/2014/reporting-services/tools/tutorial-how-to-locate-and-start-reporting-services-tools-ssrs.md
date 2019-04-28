---
title: 教程：如何查找并启动 Reporting Services 工具 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 03fb1d70046fe784fecafd8d9b3092ce21962498
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657978"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>教程：如何查找并启动 Reporting Services 工具 (SSRS)
  该教程介绍了用于配置报表服务器、管理报表服务器内容和操作以及创建与发布报表的工具。 本教程旨在于帮助新用户了解如何查找和打开各个工具。 如果您已经熟悉了这些工具，您可以转到其他教程学习有关使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]的重要技能。 有关其他教程的详细信息，请参阅[Reporting Services 教程&#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)。  
  
 本主题内容：  
  
-   [Reporting Services 配置管理器（本机节点）](#bkmk_configuration_manager)  
  
-   [报表管理器 （本机模式）](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [具有报表设计器和报表向导的 SQL Server Data Tools](#bkmk_ssdt)  
  
-   [报表生成器](#bkmk_report_builder)  
  
##  <a name="bkmk_configuration_manager"></a> Reporting Services 配置管理器（本机节点）  
 使用本机模式配置管理器完成以下任务： 、 、 、 、 和 。  
  
-   指定服务帐户。  
  
-   创建或升级报表服务器数据库。  
  
-   修改连接属性。  
  
-   指定 URL。  
  
-   管理加密密钥。  
  
-   配置无人参与的报表处理和电子邮件报表传递。  
  
 **安装：** 安装 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式时，会安装 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Configuration Manager。 有关详细信息，请参阅 [安装 Reporting Services 本机模式报表服务器](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>启动 Reporting Services 配置管理器  
  
1.  在 Windows 开始屏幕上，键入`reporting`然后在**应用程序**搜索结果中，单击**Reporting Services 配置管理器**。  
  
     ![正在启动的 Reporting Services 配置管理器](../media/bi-ssrs-configmanager-win8-startscreen.gif "正在启动的 Reporting Services 配置管理器")  
  
     **Or**  
  
     单击 **“开始”**，然后依次单击 **“程序”**、“ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]”、 **“配置工具”**、 **“Reporting Services 配置管理器”**。  
  
     此时将出现 **“选择报表服务器安装实例”** 对话框，可以选择要配置的报表服务器实例。  
  
2.  在 **“服务器名称”** 中，指定安装报表服务器实例的计算机的名称。 指定的默认值是本地计算机名称，但也可以键入远程 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
     如果指定远程计算机，请单击 **“查找”** 以建立一个连接。 必须事先配置报表服务器，以便进行远程管理。 有关详细信息，请参阅 [配置报表服务器以进行远程管理](../report-server/configure-a-report-server-for-remote-administration.md)。  
  
3.  在 **在stance Name**中，选择要配置的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 实例。 列表中只显示 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器实例。 不能配置较早版本的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。  
  
4.  单击 **“连接”**。  
  
5.  若要验证是否已启动工具，请将您的结果与下图进行比较：  
  
     ![Reporting Services 配置工具](../media/rs-ui-reportserverconfigkatmai.gif "Reporting Services 配置工具")  
  
 **后续步骤：**[配置和管理报表服务器（SSRS 本机模式）](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)和 [Reporting Services 配置管理器（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
##  <a name="bkmk_report_manager"></a> 报表管理器 （本机模式）  
 使用[报表管理器&#40;SSRS 本机模式&#41;](../report-manager-ssrs-native-mode.md)可设置权限、 管理订阅和计划，以及处理报表。 也可以使用报表管理器来查看报表。  
  
 **安装：** 在安装时安装报表管理器[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]本机模式：[安装 Reporting Services 本机模式报表服务器](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 必须拥有足够的权限才能打开报表管理器（最初，只有本地 Administrators 组的成员拥有访问报表管理器功能的权限）。 报表管理器根据当前用户的角色分配提供不同的页和选项。 没有权限的用户将得到一个空页。 拥有查看报表权限的用户将获得链接，用户点击这些链接可以打开报表。 若要了解有关权限的详细信息，请参阅[角色和权限 (Reporting Services)](../security/roles-and-permissions-reporting-services.md)。  
  
#### <a name="to-start-report-manager"></a>启动报表管理器  
  
1.  打开浏览器。 有关支持的浏览器和浏览器版本的信息，请参阅[规划 Reporting Services 和 Power View 浏览器支持&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)。  
  
2.  在 Web 浏览器的地址栏中，键入报表管理器 URL。 默认情况下，URL 是**http://\<服务器名 > / 报表**。 可以使用 Reporting Services 配置工具确认服务器名称和 URL。 有关 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中使用的 URL 的详细信息，请参阅[配置报表服务器 URL（SSRS 配置管理器）](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)。  
  
3.  报表管理器将在浏览器窗口中打开。 引导页为主文件夹。 根据权限，您可能看到引导页中的其他文件夹、指向报表的超链接和资源文件。 也可能在工具栏上看到其他按钮和命令。  
  
4.  如果本地报表服务器上运行报表管理器，请参阅[为本地管理配置本机模式报表服务器&#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
 **后续步骤：**[配置报表管理器&#40;本机模式&#41;](../report-server/configure-web-portal.md)。  
  
##  <a name="bkmk_managements_studio"></a> Management Studio  
 报表服务器管理员可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来管理报表服务器及其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 组件服务器。 有关详细信息，请参阅 [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)。  
  
#### <a name="to-start-sql-server-management-studio"></a>启动 SQL Server Management Studio  
  
1.  从 Windows 开始屏幕上，键入`sql server`然后在**应用程序**搜索结果中，单击**SQL Server Management Studio**。  
  
     ![Windows“开始”屏幕中的 Managment Studio](../media/bi-ssms-win8-startscreen.gif "Windows“开始”屏幕中的 Managment Studio")  
  
     **Or**  
  
     依次单击“开始” 、“所有程序” 、“ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]”和“SQL Server Management Studio” 。 此时，将显示 **“连接到服务器”** 对话框。  
  
2.  如果没有出现 **“连接到服务器”** 对话框，请在 **“对象资源管理器”** 中单击 **“连接”** ，然后选择 **Reporting Services**。  
  
3.  在 **“服务器类型”** 列表中，选择 **Reporting Services**。 如果 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 不在列表中，则说明没有安装它。  
  
4.  在 **“服务器名称”** 列表中，选择一个报表服务器实例。 本地实例将显示在列表中。 您还可以键入远程 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
5.  单击 **“连接”**。 可以扩展根节点以设置服务器属性，修改角色定义或关闭报表服务器功能。  
  
##  <a name="bkmk_ssdt"></a> 具有报表设计器和报表向导的 SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 提供了报表设计器 - Business Intelligence for Visual Studio 2012。 该工具中的设计图面包括用于访问报表创作功能的选项卡式窗口、向导和菜单。 选择报表服务器项目或者报表服务器向导模板后，该报表设计器工具即可用。 若要了解详细信息，请参阅 [SQL Server Data Tools 中的 Reporting Services (SSDT)](reporting-services-in-sql-server-data-tools-ssdt.md)。  
  
#### <a name="to-start-report-designer"></a>启动报表设计器  
  
1.  从 Windows“开始”屏幕，键入 **“data”** ，然后在 **“应用程序”** 搜索结果中，单击 **“SQL Server Data Tools for Visual Studio 2012”**。  
  
     **Or**  
  
     单击**启动**，依次指向**所有程序**，指向[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]，然后单击**SQL Server Data Tools (SSDT)**。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，再单击 **“项目”**。  
  
3.  在 **“项目类型”** 列表中，单击 **“商业智能项目”**。  
  
4.  在 **“模板”** 列表中，单击 **“报表服务器项目”**。 下图显示了对话框中显示的项目模板的外观：  
  
     ![“新建项目模板”对话框](../media/rs-ui-newrsproject.gif "“新建项目模板”对话框")  
  
5.  为项目键入名称和位置，或单击 **“浏览”** 并选择位置。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] ，并显示 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 起始页。 解决方案资源管理器提供用来创建报表和数据源的类别。 可以使用这些类别来创建新的报表和数据源。 创建报表定义时将显示选项卡式窗口。 选项卡式窗口包括“数据”、“布局”和“预览”。  
  
 若要掌握有关创建报表的入门知识，请参阅[创建基本表报表（SSRS 教程）](../create-a-basic-table-report-ssrs-tutorial.md)。 若要了解有关您可以使用报表设计器中的查询设计器的详细信息，请参阅[报表设计器 SQL Server Data Tools 中的查询设计工具&#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)。  
  
##  <a name="bkmk_report_builder"></a> 报表生成器  
 使用[报表生成器&#40;SSRS&#41; ](report-builder-authoring-environment-ssrs.md)中创建报表[!INCLUDE[msCoName](../../includes/msconame-md.md)]类似 Office 的创作环境。 您可以自定义和更新所有的现有报表，无论这些报表是在报表设计器中还是在早期版本的报表生成器中创建的。 请与管理员联系，以获得在本地计算机上安装报表生成器所要运行的 ReportBuilder3.msi 文件的位置。  
  
 **安装：** 单击-后版本的报表生成器安装通过[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]本机模式或 SharePoint 模式。 报表生成器的独立版是一个单独的下载包。  请参阅[安装报表生成器的独立版本&#40;报表生成器&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>从报表管理器启动 ClickOnce 版报表生成器（本机模式）  
  
1.  在 Web 浏览器中，键入报表服务器的报表管理器 URL。 默认情况下，该 URL 为 http://\<*servername*>/reports。 报表管理器随之打开。  
  
2.  单击 **“报表生成器”**。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>使用 URL 启动报表生成器 ClickOnce  
  
1.  在 Web 浏览器的地址栏中，键入以下 URL：  
  
     **http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application**  
  
2.  按 Enter。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>在 Reporting Services SharePoint 模式下启动 ClickOnce 版报表生成器  
  
1.  导航到包含要创建新报表的库的站点。  
  
2.  打开库。  
  
3.  在 **“新建”** 菜单中单击 **“报表生成器报表”**。  
  
     报表生成器将打开，您随后可以在报表服务器上创建报表或打开报表。  
  
#### <a name="to-start-report-builder-stand-alone"></a>启动独立版报表生成器  
  
1.  在 Windows“开始”屏幕上，键入 **“report builder”** ，然后单击 **“Report Builder 3.0”**。  
  
     **Or**  
  
     在“开始”菜单上，依次单击 **“所有程序”** 和 **“Microsoft SQL Server 2014 报表生成器”**。  
  
2.  单击 **“报表生成器”**。  
  
     报表生成器将打开，您可以创建或打开报表了。  
  
3.  单击 **“报表生成器帮助”** 可打开报表生成器的文档。  
  
## <a name="see-also"></a>请参阅  
 [安装、 卸载和报表生成器支持](../install-uninstall-and-report-builder-support.md)   
 [Reporting Services SharePoint 模式下安装&#40;SharePoint 2010 和 SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services 报表服务器](../reporting-services-report-server.md)   
 [查询设计工具在报表设计器的 SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)  
  
  
