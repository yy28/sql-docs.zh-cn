---
title: 配置报表管理器 （本机模式） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 7af188d6f1adf097de20bf08ef8343c9e075c073
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025650"
---
# <a name="configure-report-manager-native-mode"></a>配置报表管理器（本机模式）
  报表管理器是一种用于查看报表、管理报表服务器内容以及向用户授予本机模式报表服务器访问权限的 Web 前端应用程序。 如果在安装程序中选择 **“以默认的本机模式配置安装”** 选项，则可以将报表管理器与报表服务器 Web 服务一起安装在同一个报表服务器实例中，并有选择地进行配置。 还可以在安装完成后配置报表管理器。 本主题提供有关以下报表管理器配置方案的信息：  
  
-   [将报表管理器配置为使用默认 URL](#ConfigureRMURL)  
  
     报表管理器是用户在 Web 浏览器中访问的 Web 应用程序。 因此必须至少定义用于在浏览器窗口中打开该应用程序的 URL。 该 URL 由主机名、端口和虚拟目录组成。 此 URL 的默认值包括为报表服务器 Web 服务 URL 定义的主机名和端口值，再加上 **reports** 虚拟目录名。 如果有命名实例，则虚拟目录为 **reports_instance**，其中 **instance** 是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例的名称。  
  
-   **从远程计算机运行报表管理器**。 根据您的网络设置，您可能需要在计算机上启用端口 80 以允许报表管理器的请求。  
  
    > [!TIP]  
    >  如果尝试访问远程计算机上的报表管理器，但在浏览器中收到连接错误消息，这通常是由于防火墙设置造成的。 有关详细信息，请参阅 [将防火墙配置为允许报表服务器访问](configure-a-firewall-for-report-server-access.md)。  
  
     如有必要，启用两台计算机上的端口 80 以允许通过该端口的请求。 有关详细信息，请参阅 [将防火墙配置为允许报表服务器访问](configure-a-firewall-for-report-server-access.md)。  
  
-   [将报表管理器配置为使用特定的报表服务器 URL](#ConfigureSpecificURL)  
  
     默认情况下，报表管理器连接到在同一报表服务器服务中运行的报表服务器 Web 服务。 报表管理器使用报表服务器 Web 服务 URL 进行连接。 如果为报表服务器 Web 服务定义了多个 URL，则报表管理器将使用所定义的最后一个 URL。 但是，对于某些部署来说，您可能希望报表管理器始终通过静态 URL 连接到 Web 服务。 这样做的一种情况是：您对特定端口或 IP 地址配置了数据包筛选，并且希望所有到报表服务器的连接都通过您所定义的筛选规则。  
  
-   [将报表管理器指向远程报表服务器](#ConfigureRemoteRS)  
  
     默认情况下，报表管理器提供对在同一服务器实例中运行的报表服务器 Web 服务的前端访问，但是如果希望在不同的进程中运行 Web 服务和报表管理器，或要为每个服务器配置不同的服务器访问（例如，如果通过 Extranet 或 Internet 连接向用户部署报表管理器并且希望在报表服务器和报表管理器之间部署防火墙），则可以将报表管理器配置为连接到远程报表服务器 Web 服务。  
  
-   [自定义样式和应用程序标题](#ModifyTitle)  
  
     您可以通过有限的方式更改样式和编辑显示在报表管理器中的应用程序标题，从而自定义报表管理器、HTML 报表查看器和报表工具栏。  
  
-   [关闭报表管理器](#DisableRM)  
  
     安装使用本机模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例时，报表管理器默认为启用状态。 但是在以下情况下可以关闭报表管理器：如果有提供等效功能的自定义前端应用程序，如果仅希望使用 SOAP 或 URL 访问接口访问报表服务器，或者如果正在从其他报表服务器实例使用报表管理器。  
  
## <a name="prerequisites"></a>必要條件  
 若要使用报表管理器，必须满足下列前提条件：  
  
-   必须拥有最小配置的报表服务器。 有关对报表服务器进行最小配置的详细信息，请参阅[配置报表服务器（Reporting Services 本机模式）](configure-a-report-server-reporting-services-native-mode.md)。  
  
-   报表服务器必须在本机模式下运行。 在报表服务器配置为 SharePoint 集成模式的情况下无法使用报表管理器。 在 SQL Server 2012 中，不能将报表服务器从一个模式切换到另一个模式。 如果要更改您环境使用的报表服务器类型，必须安装所需的报表服务器模式，然后将报表项复制或移到新报表服务器。 此过程通常称为“迁移”。 迁移所需的步骤取决于您要迁移到的模式和迁移前所在的版本。 有关详细信息，请参阅 [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)。  
  
-   还必须装有启用了脚本功能的 Internet Explorer 7.0 或更高版本。 有关详细信息，请参阅[规划 Reporting Services 和 Power View 浏览器支持&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)。  
  
##  <a name="ConfigureRMURL"></a> 将报表管理器配置为使用默认 URL  
 默认情况下，报表管理器 URL 由唯一的虚拟目录名和为在同一实例中运行的报表服务器 Web 服务定义的端口和主机名组成。 在大多数情况下，主机名是报表服务器计算机的网络名称，但也可以是解析该计算机的 IP 地址或主机标头。 若要将报表管理器配置为使用默认 URL，请使用 **配置工具中的** “报表管理器 URL” [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 页。  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>配置默认报表管理器 URL 和虚拟目录  
  
1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并连接到报表服务器实例。  
  
2.  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中，单击 **“报表管理器 URL”** 以打开配置 URL 的页面。  
  
3.  为报表管理器输入唯一的虚拟目录名。  
  
4.  单击 **“应用”**。  
  
5.  如果使用的是 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 或 Windows Server 2008，则可能还需要执行其他步骤才能使用报表管理器。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
##  <a name="ConfigureSpecificURL"></a> 将报表管理器配置为使用特定的报表服务器 URL  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中配置 URL 时，报表管理器将自动检测并使用在同一服务器实例中运行的报表服务器的任何新的或更新的 URL。 如果部署要求对所有报表服务器请求使用单个静态 URL，您可以在 RSReportServer.config 文件中指定该 URL。  
  
#### <a name="to-configure-a-static-report-server-url"></a>配置静态报表服务器 URL  
  
1.  在文本编辑器中打开 **RSReportServer.config** 文件。 默认情况下，该文件位于 \Program Files\Microsoft SQL Server\MSRS12.\<实例名>\Reporting Services\ReportServer。  
  
2.  查找`ReportServerURL`。  
  
3.  将其替换为相应报表服务器实例的 URL。  
  
4.  保存所做的更改，并关闭该文件。  
  
 有关配置文件的详细信息，请参阅[修改 Reporting Services 配置文件&#40;RSreportserver.config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md)和[RSReportServer Configuration File](rsreportserver-config-configuration-file.md)。  
  
##  <a name="ConfigureRemoteRS"></a> 将报表管理器配置为使用远程报表服务器  
 对于将报表管理器和报表服务器置于不同计算机上的部署配置，必须有两个单独的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安装。 报表管理器嵌入在报表服务器服务中，无法自行安装。 如果希望报表管理器在另一台计算机上以自身进程运行，则必须安装第二个报表服务器。 这两个服务器实例都必须是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器。  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>将报表管理器连接到远程报表服务器实例  
  
1.  安装两个报表服务器实例。  
  
2.  对承载报表服务器的第一个安装进行配置：  
  
    1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。  
  
    2.  单击 **“Web 服务 URL”** ，为报表服务器配置主机名、端口和虚拟目录。  
  
    3.  单击 **“数据库”** ，配置报表服务器数据库。  
  
3.  对承载报表管理器的第二个安装进行配置：  
  
    1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。  
  
    2.  单击 **“报表管理器 URL”** ，为报表管理器输入虚拟目录名。  
  
     不要配置该数据库。 不要测试 URL。  
  
4.  在报表管理器计算机上，修改 RSReportServer.config 中的配置设置以指向远程报表服务器实例。 在启动时，报表管理器将读取该配置文件以获取指向报表服务器的 URL：  
  
    1.  在文本编辑器中打开 RSReportServer.config。 默认情况下，它是位于 files\microsoft SQL Server\MSRS11。\< *instancename*> \Reporting Services\ReportServer。  
  
    2.  查找`ReportServerURL`。  
  
    3.  将其替换为远程报表服务器实例的 URL。  
  
    4.  保存所做的更改，并关闭该文件。  
  
5.  > [!TIP]  
    >  如有必要，启用两台计算机上的端口 80 以允许通过该端口的请求。 有关详细信息，请参阅 [将防火墙配置为允许报表服务器访问](configure-a-firewall-for-report-server-access.md)。  
  
6.  重新启动报表服务器。  
  
7.  在浏览器窗口中打开报表管理器。 如果已打开，请刷新浏览器以验证报表管理器已连接到远程服务器。 应可看到目标服务器的内容。  
  
8.  关闭不使用的服务器功能：  
  
    -   在报表管理器计算机上，关闭`WebServiceAndHTTPAccessEnabled`和`ScheduleEventsAndReportDeliveryEnabled`。  
  
    -   在报表服务器计算机上关闭`ReportManagerEnabled`。  
  
 关于关闭功能的详细信息，请参阅 [打开或关闭 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)。  
  
##  <a name="ModifyTitle"></a> 自定义样式或应用程序标题  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不支持自定义报表管理器样式表。 但是，如果您具备 Web 开发的专业知识，则可以修改样式，但需自行承担相应的风险。 有关哪些文件包含样式信息的详细信息，请参阅 [自定义 HTML 查看器和报表管理器的样式表](../customize-style-sheets-for-html-viewer-and-report-manager.md)。  
  
 报表管理器具有显示在页面顶部的应用程序标题。 默认情况下，该标题为 **SQL Server Reporting Services**。 可以自定义此标题。 若要更改此标题，可使用报表管理器中的“站点设置”页。 若要修改报表管理器中的应用程序设置，您必须分配有 **“系统管理员”** 角色才能在“站点设置”页上设置属性。 若要查看应用程序标题，用户必须分配有 **“系统用户”** 角色。  
  
#### <a name="to-modify-application-title"></a>修改应用程序标题  
  
1.  使用分配有报表服务器 **“系统管理员”** 权限的帐户登录。  
  
2.  打开 Internet Explorer。  
  
3.  输入报表管理器 URL。 默认情况下，该 URL 为 http://\<your-server-name>/reports，但如果已将 Reporting Services 作为命名实例安装，则默认 URL 将为 http://\<your-server-name>/reports\<_instancename>。  
  
4.  单击 **“网站设置”**。  
  
5.  在 **“常规”** 选项卡上的 **“名称”** 中，将 **SQL Server Reporting Services** 替换为其他名称。  
  
6.  单击 **“应用”**。  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 在以下情况下可以关闭报表管理器：如果有可提供等效功能的自定义应用程序，或正在使用其他服务实例的报表管理器应用程序。 若要关闭报表管理器，可以修改 RSReportServer.config 文件。  
  
#### <a name="to-turn-off-report-manager"></a>关闭报表管理器  
  
1.  在文本编辑器中打开 RSReportServer.config 文件。 默认情况下，它是位于 files\microsoft SQL Server\MSRS11。\< *instancename*> \Reporting Services\ReportServer。  
  
2.  查找 **IsReportManagerEnabled**。  
  
3.  将其值设为 **False**。  
  
4.  保存所做的更改，并关闭该文件。  
  
 有关如何修改配置文件的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](modify-a-reporting-services-configuration-file-rsreportserver-config.md)。 关于禁用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的功能的详细信息，请参阅[打开或关闭 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../report-manager-ssrs-native-mode.md)   
 [Planning for Reporting Services 和 Power View 浏览器支持&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [配置 URL &#40;SSRS 配置管理器&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [验证 Reporting Services 安装](../install-windows/verify-a-reporting-services-installation.md)   
 [为 HTML 查看器和报表管理器自定义样式表](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [打开或关闭 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)   
 [管理 Reporting Services 本机模式报表服务器](manage-a-reporting-services-native-mode-report-server.md)   
 [RSReportServer 配置文件](rsreportserver-config-configuration-file.md)   
 [为本地管理配置本机模式报表服务器&#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  