---
title: "配置本机模式报表服务器进行本地管理 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a0d47b170b22f25ff8c9752a5b7a4aa9034f6284
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>为本地管理配置本机模式报表服务器 (SSRS)
  如果您想要在本地管理报表服务器实例，则将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器部署到以下操作系统之一要求更多的赋值步骤。 本主题说明如何配置报表服务器以进行本地管理。 如果尚未安装或配置报表服务器，请参阅[从安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)和[管理 Reporting Services 本机模式报表服务器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 因为上述操作系统限制了权限，所以本地 Administrators 组的成员运行大多数应用程序时就像使用标准用户帐户时一样。  
  
 虽然该方法可提高系统的整体安全性，但会阻止用户使用 Reporting Services 为本地管理员创建的预定义内置角色分配。  
  
-   [配置更改概述](#bkmk_configuraiton_overview)  
  
-   [配置本地报表服务器和报表管理器管理](#bkmk_configure_local_server)  
  
-   [为本地报表服务器管理配置 SQL Server Management Studio (SSMS)](#bkmk_configure_ssms)  
  
-   [配置 SQL Server Data Tools (SSDT) 以便发布到本地报表服务器](#bkmk_configure_ssdt)  
  
-   [其他信息](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> 配置更改概述  
 下面的配置更改对服务器进行配置，以便您可以使用标准用户权限管理报表服务器内容和操作：  
  
-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 添加到受信任站点。 默认情况下，在上列操作系统上运行的 Internet Explorer 是以 **“保护模式”**运行的，此功能可阻止浏览器请求到达运行在同一计算机上的高级别进程。 通过将报表服务器应用程序添加为受信任站点，可以禁用这些应用程序的保护模式。  
  
-   创建角色分配，授予您（报表服务器管理员）管理内容和操作的权限而无需使用 Internet Explorer 中的 **“以管理员的身份运行”** 功能。 通过为您的 Windows 用户帐户创建角色分配，并通过显式角色分配替换 Reporting Services 创建的预定义的内置角色分配，您将获得对报表服务器的访问权限（包括内容管理员和系统管理员权限）。  
  
##  <a name="bkmk_configure_local_server"></a> 配置本地报表服务器和报表管理器管理  
 如果您浏览到本地报表服务器并且看到如下错误，请完成本节中的配置步骤：  
  
-   用户 `'Domain\[user name]`' 没有必需的权限。 请验证授予了足够的权限并且解决了 Windows 用户帐户控制(UAC)限制问题。  
  
###  <a name="bkmk_site_settings"></a> 浏览器中“受信任的站点”设置  
  
1.  使用“以管理员的身份运行”权限打开一个浏览器窗口。 从 **“开始”** 菜单上，单击 **“所有程序”**，右键单击 **Internet Explorer**，然后选择 **“以管理员的身份运行”**。  
  
2.  单击 **“允许”** 以继续。  
  
3.  在 URL 地址中，输入报表管理器 URL。 有关说明，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
4.  单击 **“工具”**。  
  
5.  单击 **“Internet 选项”**。  
  
6.  单击 **“安全性”**。  
  
7.  单击 **“受信任的站点”**。  
  
8.  单击 **“站点”**。  
  
9. 添加 `http://<your-server-name>`。  
  
10. 如果不将 HTTPS 用于默认站点，请清除 **“对该区域中的所有站点要求服务器验证(https:)”** 复选框。  
  
11. 单击 **“添加”**。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_folder_settings"></a> 报表管理器文件夹设置  
  
1.  在报表管理器的主页上，单击 **“文件夹设置”**。  
  
2.  在“文件夹设置”页中，单击 **“安全性”**。  
  
3.  单击 **“新建角色分配”**。  
  
4.  在“组或用户名”  字段中，按以下格式键入 Windows 用户帐户： `<domain>\<user>`。  
  
5.  选择 **“内容管理员”**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_site_settings"></a> 报表管理器站点设置  
  
1.  使用管理权限打开浏览器并浏览到报表管理器 `http://<server name>/reports`。  
  
2.  单击主页上角的 **“站点设置”** 。  
  
    > [!TIP]  
    >  注意： 如果没有看到“站点设置”选项，请关闭后再重新打开浏览器，然后使用管理权限浏览到报表管理器。  
  
3.  单击 **“安全性”**。  
  
4.  单击 **“新建角色分配”**。  
  
5.  在“组或用户名”  字段中，按以下格式键入 Windows 用户帐户： `<domain>\<user>`。  
  
6.  选择 **“系统管理员”**。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  关闭报表管理器。  
  
9. 重新在 Internet Explorer 中打开报表管理器，但不使用 **“以管理员的身份运行”**。  
  
##  <a name="bkmk_configure_ssms"></a> 为本地报表服务器管理配置 SQL Server Management Studio (SSMS)  
 默认情况下，您不能访问在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的所有报表服务器属性，除非您使用管理权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
 **配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** 角色属性和角色分配，以便您无需每次都使用提升的权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ：  
  
-   在“开始”菜单，依次单击“所有程序”和“SQL Server 2014”，右键单击 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，然后单击“以管理员身份运行”。  
  
-   连接到您的本地 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器。  
  
-   在 **“安全性”** 节点中，单击 **“系统角色”**。  
  
-   右键单击 **“系统管理员”** ，然后单击 **“属性”**。  
  
-   在 **“系统角色属性”** 页中，选择 **“查看报表服务器属性”**。 选择您要与系统管理员角色的成员相关联的任何其他属性。  
  
-   单击 **“确定”**。  
  
-   关闭 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   若要将某一用户添加到系统角色“系统管理员”，请参阅本主题中前面的 [报表管理器站点设置](#bkmk_configure_site_settings) 部分。  
  
 现在，在您打开 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 并且没有明确选择 **“以管理员身份运行”** 时，您有权访问报表服务器属性。  
  
##  <a name="bkmk_configure_ssdt"></a> 配置 SQL Server Data Tools (SSDT) 以便发布到本地报表服务器  
 如果您在本主题的第一节中列出的操作系统之一上安装了 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ，并且希望 SSDT 与本地本机模式报表服务器交互，您将会遇到权限错误，除非您使用提升的权限打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或者配置报表服务角色。 例如，如果您没有足够的权限，将遇到如下问题：  
  
-   在您尝试将报表项部署到本地报表服务器时，您将在 **“错误列表”** 窗口中看到如下错误消息：  
  
    -   为用户“域\\<用户名\>”授予的权限不足，无法执行此操作。  
  
 **在每次打开 SSDT 时使用提升的权限运行：**  
  
1.  在开始屏幕中，键入 **sql server**，然后右键单击“SQL Server Data Tools”。 单击 **“以管理员身份运行”**。  
  
2.  单击 **“继续”**。  
  
3.  单击 **“运行程序”**。  
  
 现在，您应该能够将报表和其他项部署到本地报表服务器上了。  
  
 **配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 角色分配，以便您无需每次都使用提升的权限启动 SSDT：**  
  
-   请参阅本主题中前面的 [报表管理器文件夹设置](#bkmk_configure_folder_settings) 和 [报表管理器站点设置](#bkmk_configure_site_settings) 部分。  
  
##  <a name="bkmk_addiitonal_informaiton"></a> 其他信息  
 与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理相关的一个附加的常见配置步骤是在 Windows 防火墙中打开端口 80，以便允许访问报表服务器计算机。 有关说明，请参阅 [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
## <a name="see-also"></a>另请参阅  
 [管理 Reporting Services 本机模式报表服务器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
