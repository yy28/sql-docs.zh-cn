---
title: "配置 web 门户 |Microsoft 文档"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c0c6cc27711140e96bbf4420e8de596af53ddfcd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal"></a>配置 web 门户

web 门户是用于查看报表、 管理报表服务器内容，以及授予对本机模式报表服务器的用户访问权限的 Web 前端应用程序。 安装与同一个报表服务器实例中的报表服务器 Web 服务和有选择地配置如果您选择 web 门户**安装在默认本机模式配置**安装程序中的选项。 作为安装后任务，你还可以配置 web 门户。 本主题提供有关以下信息的 web 门户配置方案：

## <a name="prerequisites"></a>必要條件

若要使用 web 门户，必须满足以下先决条件：

- 必须拥有最小配置的报表服务器。 有关按最小方式配置报表服务器的详细信息，请参阅[配置报表服务器](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)。

- 报表服务器必须在本机模式下运行。 为 SharePoint 集成模式，无法与配置的报表服务器使用 web 门户。 在 SQL Server 2012 中，不能将报表服务器从一个模式切换到另一个模式。 如果要更改您环境使用的报表服务器类型，必须安装所需的报表服务器模式，然后将报表项复制或移到新报表服务器。 此过程通常称为“迁移”。 迁移所需的步骤取决于您要迁移到的模式和迁移前所在的版本。 有关详细信息，请参阅 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。

- 你还必须具有 Internet Explorer 11 或更高版本的脚本启用。 有关详细信息，请参阅 [Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。

## <a name="configure-the-web-portal-to-use-the-default-url"></a>配置 web 门户以使用默认 URL

Web 门户网站是在 Web 浏览器中的用户访问的 Web 应用。 因此必须至少定义用于在浏览器窗口中打开该应用程序的 URL。 该 URL 由主机名、端口和虚拟目录组成。 此 URL 的默认值包括为报表服务器 Web 服务 URL 定义的主机名和端口值，再加上 **reports** 虚拟目录名。 如果有命名实例，则虚拟目录为 **reports_instance**，其中 **instance** 是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例的名称。

默认情况下，web 门户 URL 组成的唯一的虚拟目录名称，以及为同一实例中运行的报表服务器 Web 服务定义的端口和主机名称。 在大多数情况下，主机名是报表服务器计算机的网络名称，但也可以是解析该计算机的 IP 地址或主机标头。 若要配置 web 门户来使用默认 URL，使用**Web 门户 URL**页面[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置工具。

> [!TIP]
> 如果你尝试访问远程计算机上的 web 门户，在浏览器中收到连接错误消息，一个常见原因是由于防火墙设置。 有关详细信息，请参阅 [将防火墙配置为允许报表服务器访问](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>配置默认 web 门户 URL 和虚拟目录

1. 启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并连接到报表服务器实例。

2. 在[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置工具中，选择**Web 门户 URL**以打开配置 URL 页。

3. 输入 web 门户网站的唯一的虚拟目录名称。

4. 单击 **“应用”**。

5. 如果你使用[!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]或 Windows Server 2008 中，需要执行其他步骤可能才可以使用 web 门户。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>配置 web 门户以使用特定的报表服务器 URL

默认情况下，web 门户连接到同一报表服务器服务中运行的报表服务器 Web 服务。 Web 门户使用报表服务器 Web 服务 URL 来建立连接。 如果定义多个报表服务器 Web 服务 Url，web 门户将使用你定义的最后一个。 但是，对于某些部署，你可能希望在 web 门户中始终连接到 Web 服务通过静态 URL。 这样做的一种情况是：您对特定端口或 IP 地址配置了数据包筛选，并且希望所有到报表服务器的连接都通过您所定义的筛选规则。

配置中的 Url 时[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置工具中，web 门户会自动检测并在相同的服务器实例中运行的报表服务器使用的任何新的和更新 Url。 如果部署要求对所有报表服务器请求使用单个静态 URL，您可以在 RSReportServer.config 文件中指定该 URL。

#### <a name="to-configure-a-static-report-server-url"></a>配置静态报表服务器 URL

1. 在文本编辑器中打开 **RSReportServer.config** 文件。 默认情况下，它是位于 files\microsoft SQL Server\MSRS12。\< *instancename*> \Reporting Services\ReportServer。  

2. 查找 **ReportServerURL**。

3. 将其替换为相应报表服务器实例的 URL。

4. 保存所做的更改，并关闭该文件。

有关配置文件的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 和 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。

## <a name="customize-styles-or-application-title"></a>自定义样式或应用程序标题

你可以创建自定义品牌包更改的 web 门户网站使用的颜色。 有关详细信息，请参阅[web 门户的品牌](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>修改应用程序标题

1. 使用分配有报表服务器 **“系统管理员”** 权限的帐户登录。

2. 打开 Internet Explorer。

3. 输入 web 门户 URL。 默认情况下，它是 http://\<**你的服务器名称**> / 报表，但如果你安装 Reporting Services 作为命名实例，则默认 URL 将为 http://\<**你的服务器名称**> / 报表\<**_instancename**>。

4. 选择“站点设置” 。

5. 在 **“常规”** 选项卡上的 **“名称”**中，将 **SQL Server Reporting Services** 替换为其他名称。

6. 选择“应用” 。

## <a name="next-steps"></a>后续步骤

[Web 门户](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Reporting Services 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[配置 URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[打开或关闭 Reporting Services 功能](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[管理 Reporting Services 本机模式报表服务器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[为本地管理配置本机模式报表服务器](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
