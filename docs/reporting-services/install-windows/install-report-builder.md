---
title: "安装报表生成器 | Microsoft Docs"
ms.custom: 
ms.date: 09/22/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: "20"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 395ec440e3cae0ac4013edc9c35af36e32a73d0c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="install-report-builder"></a>Install Report Builder
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 是一个独立应用，由你或管理员安装到你的电脑上。 可以从 Microsoft 下载中心、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表服务器或者与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]集成的 SharePoint 站点进行安装。  
  
 通常，由管理员安装和配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、授予从 Web 门户下载 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的权限，以及管理文件夹与对报表、报表部件和保存到报表服务器的共享数据集的权限。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理的详细信息，请参阅 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-from--a--web-portal-or-sharepoint-library"></a>从 Web 门户或 SharePoint 库安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 
  
 可以从 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] Web 门户或者与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成的 SharePoint 站点启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 有关信息，请参阅 [启动报表生成器](../../reporting-services/report-builder/start-report-builder.md)。  
  
### <a name="sharepoint-site-integrated-with-includessrsnoversionincludesssrsnoversion-mdmd"></a>与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 在与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]集成的 SharePoint 站点上，如果“新建文档”  菜单未列出“报表生成器报表” 、“报表生成器模型” 和“报表数据源” ，则需要将其内容类型添加到 SharePoint 库中。 有关详细信息，请参阅 [向 SharePoint 库添加 Reporting Services 内容类型](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
 
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 
  
 管理员还可以使用 System Center Configuration Manager 等软件将程序推送到你的计算机上。 若要了解如何使用特定软件安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]，请查阅该软件的文档。 有关详细信息，请参阅 [System Center Configuration Manager 站点](https://www.microsoft.com/en-us/cloud-platform/system-center-configuration-manager)。  
  
> [!IMPORTANT]  
>  Windows Vista 和 Windows 7 安全功能需要提升权限以运行命令行操作，并将提示您提供运行命令行的权限。 安装不是静默的。 若要进行静默安装，您需要以管理员身份运行命令行。  
  
## <a name="system-requirements"></a>系统要求
  
 请参阅 Microsoft 下载中心上 [报表生成器下载页](http://go.microsoft.com/fwlink/?LinkID=734968) 的 **“系统要求”**部分。
  
##  <a name="download"></a> 从下载站点安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  在 [Microsoft 下载中心的报表生成器页上](http://go.microsoft.com/fwlink/?LinkID=734968) ，单击“下载” 。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 下载完成后，单击“运行”。  
  
     此操作将启动 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 向导。  
  
3.  接受许可协议中的条款，然后单击“下一步” 。  
  
4.  在 **“默认的目标服务器”** 页上，如果目标报表服务器的 URL 与默认 URL 不同，则可选择提供前者。 单击“下一步” 。  
  
    > [!NOTE]  
    >  如果计划在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 连接到某个报表服务器时使用它，则此时提供该报表服务器的 URL 将会非常方便。 从 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 中的“选项”对话框也可以执行相同操作。  
  
5.  单击“安装”以完成 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的安装。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-a-share"></a>从共享安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  请与管理员联系，以获得在本地计算机上安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 所要运行的 ReportBuilder3.msi 的位置。  
  
2.  浏览找到 ReportBuilder3.msi（ [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]的 Windows 安装程序包 (MSI)），然后单击它。  
  
     此操作将启动 SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 向导。  
  
3.  完成 [To install Report Builder from the download site](#download)中的剩余步骤。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-the-command-line"></a>从命令行安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 

 还可以执行 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的命令行安装，并提供参数以自定义安装。 除了标准的 MSI 内部参数以外，还可以使用 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 提供的自定义参数：RBINSTALLDIR 和 REPORTSERVERURL。 RBINSTALLDIR 指定 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]的根安装文件夹。 REPORTSERVERURL 指定 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 用于在服务器上保存报表的默认报表服务器。  
  
 如果要进行根本没有用户界面交互的完全静默安装，请指定 **/quiet** 选项。 根据设计，quiet 选项标志会隐藏安装错误。 因此，建议在使用 quiet 选项时包括 **/l** 选项，该选项指定进行日志记录。   
  
1.  在 [Microsoft 下载中心的“报表生成器”页](http://go.microsoft.com/fwlink/?LinkID=734968)上，单击“下载”。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 下载完成后，单击“保存”。  
  
3.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
4.  在“打开”  框中，键入 **cmd.**  
  
5.  在命令提示符窗口中，导航到保存 ReportBuilder3.msi 的文件夹。  
  
6.  使用以下格式键入命令：  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 的两个特定选项为：RBINSTALLDIR 和 REPORTSERVERURL。 不需要在命令行中包含这些参数。 以下为基准命令：  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  若要运行命令，请按 ENTER。  
  
## <a name="set-includessrbnoversionincludesssrbnoversion-mdmd-defaults"></a>设置 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 默认值。  
  
-   安装 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]后，可以设置一些默认选项。 单击“文件” > “选项”。  
  
     设置默认 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户或者 SharePoint 站点最有用。 有关详细信息，请参阅 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)。  
  
-   单击“报表生成器”  。  
  
     如果未在现有服务器列表中看到报表服务器，请关闭“打开报表”对话框，并单击 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 底部的“连接” ，以连接到服务器。  
  
## <a name="see-also"></a>另请参阅  
 [启动报表生成器](../../reporting-services/report-builder/start-report-builder.md)   
 [卸载报表生成器](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
