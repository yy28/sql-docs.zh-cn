---
title: "Web 门户（SSRS 本机模式） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 13
---
# Web 门户（SSRS 本机模式）
Reporting Services [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 是一种基于 Web 的体验，它允许你查看报表、移动报表、KPI 并在报表服务器实例中的各元素间导航。 还可以使用 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 来管理单个报表服务器实例。  
  
![ssRSPortal](../reporting-services/media/ssrsportal.png)  
  
本主题内容：  
  
-   [什么是 Web 门户？](#whatisportal)  
  
-   [启动和使用 Web 门户](#startanduse)  
  
-   [按类别分组](#categories)  
  
-   [搜索项目](#search)  
  
-   [Web 门户任务](#tasks)  
  
<a name="whatisportal"/>  
## 什么是 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]？  
  
可以使用 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 来执行以下任务：  
  
-   查看、搜索、打印和订阅报表。  
  
-   创建、保护和维护文件夹层次结构，以便组织服务器上的项。  
  
-   配置基于角色的安全性，确定对项和操作的访问权限。  
  
-   配置报表执行属性、报表历史记录和报表参数。  
  
-   创建共享计划和共享数据源，以提高计划和数据源连接的可管理性。  
  
-   创建可以将报表展开为大型收件人列表的数据驱动订阅。  
  
-   创建链接报表，以便按不同方式重用现有报表和重新确定其用途。  
  
-   下载常用工具，如报表生成器和移动报表发布服务器。  
  
-   [创建 KPI](../reporting-services/working-with-kpis-in-reporting-services.md)。  
  
-   发送反馈或提出功能请求。  
  
使用 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 可以浏览报表服务器文件夹或搜索特定报表。 可以查看报表、报表的常规属性以及在报表历史记录中捕获的报表以前的副本。 根据权限，可能还可以订阅报表，以便将其传递到电子邮件收件箱或文件系统中的共享文件夹。  
  
> [!NOTE] 有关支持的浏览器和版本的信息，请参阅 [Reporting Services 浏览器支持计划](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 只能供在本机模式下运行的报表服务器使用。 配置为 SharePoint 集成模式的报表服务器不支持报表管理器。  
  
仅在特定的 [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)] 版本中才提供某些 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 功能。 有关详细信息，请参阅 [SQL Server 2016 各个版本支持的功能](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.xml)。  
  
如果是全新安装，则只有本地管理员有足够的权限来处理内容和设置。 若要对其他用户授予权限，本地管理员必须创建角色分配，以便提供对报表服务器的访问权限。 用户随后可以访问的应用程序页和任务将取决于该用户的角色分配。 有关详细信息，请参阅“如何：将用户添加到报表服务器”。  
  
> [!NOTE] 如果浏览至服务器正在其上运行的本地计算机上的 Web 门户，你可能会看到一条消息指示你不能查看此文件夹。 这是由于通用访问控制 (UAC) 以及你未以管理员身份运行浏览器的原因造成的。 你不能以管理员身份运行 Edge。 你将需要使用 Internet Explorer。 你可以远程浏览至服务器，或以管理员身份启动 Internet Explorer 并浏览至 Web 门户。 如果想要远程使用 Web 门户，则需要给为你的帐户授予文件夹的内容管理者权限。  
  
<a name="startanduse"/>  
## 启动和使用 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]  
  
[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 是一种 Web 应用程序，你可通过在浏览器窗口的地址栏中键入 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] URL 的方式来将其打开。 启动 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 时，基于你在报表服务器中拥有的权限，所看到的页面、链接和选项会有所不同。 若要执行某项任务，必须为自己分配包括该任务的角色。  如果为某用户分配了具有完整权限的角色，则该用户可以访问用来管理报表服务器的所有应用程序菜单和页。 如果为某用户分配的角色具有查看和运行报表的权限，则该用户只能看到支持这些活动的菜单和页。 对于不同的报表服务器，甚至对于存储在单个报表服务器上的不同报表和文件夹，每个用户可以具有不同的角色分配。  
  
有关角色的详细信息，请参阅 [授予对本机模式报表服务器的权限](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)。  
  
### 启动 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]  
要从浏览器启动 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] ，请执行以下操作：  
  
1.  打开 Web 浏览器。 有关支持的 Web 浏览器的列表，请参阅 [Reporting Services 浏览器支持计划](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
2.  在 Web 浏览器的地址栏中，键入 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] URL。  
  
    默认情况下，该 URL 为 *http://[ComputerName]/reports*。  
  
    报表服务器可能已配置为使用特定的端口。 例如，*http://[ComputerName]:80/reports* 或 *http://[ComputerName]:8080/reports*  
  
<a name="categories">  
## 按类别分组  
  
[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 将项按不同的类别分组。 可用类别如下。  
  
-   KPI  
-   移动报表  
-   分页报表  
-   Power BI 桌面报表  
-   Excel 工作薄  
-   数据集  
-   数据源  
-   Resources  
  
通过选择右上方的“视图”可以控制显示的内容。 如果在指定文件夹中有可用的项，将显示选中的项。 若要隐藏项，可以取消选中。  
  
![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)  
   
如果选择“显示隐藏项”，这些项将以较浅的颜色显示出来。  
  
![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)  
   
### Power BI 桌面报表和 Excel 工作薄  
  
可以上传、组织和管理 Power BI 桌面报表和 Excel 工作薄的权限。 它们会在 Web 门户中被分组到一起。  
  
![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)  
   
与其他资源文件类似，文件将存储在 Reporting Services 内。 选择其中一项会将它们下载到本地桌面。 可以通过将它们上传到报表服务器来保存已做的更改。  
  
<a name="search">  
## 搜索项目  
  
可以输入搜索术语，然后你将看到你可以访问的所有内容。 结果分为 KPI、报表、数据集和其他项。 然后可以对结果进行交互并将它们添加到你的收藏夹。  
  
![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)  
  
<a name="tasks">  
## Web 门户任务  
  
[设置 Web 门户的品牌](../reporting-services/branding-the-web-portal.md)  

[处理 KPI](../reporting-services/working-with-kpis-in-reporting-services.md)
  
[使用共享数据集](../reporting-services/working-with-shared-datasets-web-portal.md)  
  
## 另请参阅

[使用 SQL Server 移动报表发布服务器创建移动报表](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
[配置 URL（SSRS 配置管理器）](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
[Reporting Services 工具](../reporting-services/tools/reporting-services-tools.md)  
  
[Reporting Services 浏览器支持计划](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
[SQL Server 2016 各个版本支持的功能](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.xml)  
  
  
