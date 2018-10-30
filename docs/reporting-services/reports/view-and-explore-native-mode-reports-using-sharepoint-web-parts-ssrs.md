---
title: 使用 SharePoint Web 部件查看和浏览本机模式下的报表 (SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cef5578bc23c7ac49dceedaac6dfb18049600ca5
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50032136"
---
# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>使用 SharePoint Web 部件查看和浏览本机模式下的报表 (SSRS)

> [!IMPORTANT]  
>  SQL Server Reporting Services 不再支持从本机模式报表服务器上使用本机模式 (RSWebParts.cab) Web 部件访问 SharePoint 站点上的报表服务器内容。 而是使用 [SharePoint 站点上的报表查看器 Web 部件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md) 。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了多个 Web 部件，可用于特定版本的报表服务器，特别是部署模式。  
  
-   **本机模式：** 如果希望从本机模式报表服务器访问 SharePoint 站点上的报表服务器内容，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]附带的 SharePoint 2.0 Web 部件报表资源管理器和报表查看器。 本主题提供了有关安装和使用 2.0 Web 部件的说明。  
  
-   **SharePoint 模式：** 如果希望访问在 SharePoint 模式下运行的报表服务器，请使用用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序安装的 Web 部件。 有关外接程序的详细信息，请参阅 [在何处查找用于 SharePoint 产品的 Reporting Services 外接程序](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
> [!NOTE]  
>  用于本机模式的报表查看器 Web 部件 (SPViewer.dwp) 是一种与用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序安装的 Web 部件 (ReportViewer.dwp) 不同的 Web 部件。 这两种 Web 部件具有不同的架构和实现方式，但它们可以一起安装在同一个 SharePoint 场中。 可以通过以下特征直观地区分这两种 Web 部件：通过加载项安装的报表查看器 Web 部件在工具栏上有一个“操作”菜单。  
  
 有关报表服务器模式的详细信息，请参阅 [Reporting Services 报表服务器](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)。  
  
 本主题内容：  
  
-   [关于报表资源管理器和报表查看器](#bkmk_aboutwebparts)  
  
-   [使用 Web 部件的要求](#bkmk_requirements)  
  
-   [安装 Web 部件](#bkmk_installingwebparts)  
  
-   [添加和配置 Web 部件](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> 关于报表资源管理器和报表查看器  
 报表资源管理器和报表查看器是 SharePoint 2.0 Web 部件；它们是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service Pack 2 (SP2) 中引入的，并在当前版本中仍然可用。  
  
 Web 部件提供了一种从 SharePoint 站点查看报表和浏览报表服务器文件夹层次结构的方法。  
  
 请注意，不支持自定义 Web 部件。 Web 部件只能原样使用，不能进行扩展或修改。  
  
-   **报表资源管理器** (SPExplorer.dwp) 连接到报表服务器计算机上的报表管理器。 您可以浏览报表服务器上的可用报表并订阅各个报表。 如果启用了报表生成器且拥有足够的权限，则可以从报表资源管理器 Web 部件中启动报表生成器。  
  
     报表资源管理器使用报表管理器中的页面显示文件夹的内容。 对整个报表服务器文件夹层次结构中各个项和文件夹的访问通过报表服务器上的角色分配控制。 选择报表时，将在新的浏览器窗口中打开报表。 报表服务器上的 HTML 查看器可以显示报表并提供报表工具栏，而不是报表查看器 Web 部件。 如果希望自定义工具栏设置，请确保指定报表服务器上的 URL 访问参数。 有关说明，请参阅 [URL 访问参数引用](../../reporting-services/url-access-parameter-reference.md)。  
  
-   **报表查看器** (SPViewer.dwp) 可以显示报表并提供可用来导航页面、搜索内容或导出报表的工具栏。 您可以向 Web 部件页中添加报表查看器 Web 部件以始终在该页中显示特定报表， **也可以将其连接到报表资源管理器** 以显示通过该 Web 部件打开的报表。  
  
##  <a name="bkmk_requirements"></a> 使用 Web 部件的要求  
 使用报表查看器和报表资源管理器 Web 部件具有如下要求：  
  
-   支持的 SharePoint 产品和技术版本包括：  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 和 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。  
  
-   本机模式报表服务器版本必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或更高版本。  
  
-   报表服务器必须在本机模式下运行。 您 **不能** 使用报表资源管理器和报表查看器 Web 部件连接或查看在 SharePoint 集成模式下运行的报表服务器上的报表。  
  
-   必须安装报表管理器。  
  
 报表资源管理器和报表查看器 Web 部件通过 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]附带的 CAB (.cab) 文件分发。 本主题以下各部分提供了有关安装、配置和使用 Web 部件的说明。  
  
##  <a name="bkmk_installingwebparts"></a> 安装 Web 部件  
 Web 部件作为 CAB (.cab) 文件传递到 SharePoint 服务器。 从命令行针对 .cab 文件运行 SharePoint Stsadm.exe 工具以安装 Web 部件。 若要了解有关该工具和 Web 部件部署的详细信息，请参阅您的 SharePoint 文档。  
  
#### <a name="install-web-parts-using-powershell"></a>使用 PowerShell 安装 Web 部件  
  
1.  将 **RSWebParts.cab** 复制到 SharePoint 服务器上的某个文件夹。 您可以将该文件复制到 SharePoint 服务器上的任意文件夹，然后在安装 Web 部件后将其删除。 默认情况下 SQL Server 2014 Reporting Services 和更早版本将 RSWebParts.cab 文件安装到以下文件夹：  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  在安装有 SharePoint 产品的计算机上，以 **管理权限** 打开 **SharePoint 2010 Management Shell**。  
  
3.  运行以下 PowerShell 命令：  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  您应该看到如下消息，指示 Web 部件已部署。  
  
    > Name               SolutionId                                             Deployed  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     有关使用 PowerShell 的详细信息，请参阅[Install-SPWebPartPack (https://technet.microsoft.com/library/ff607840.aspx)](https://technet.microsoft.com/library/ff607840.aspx)。  
  
#### <a name="install-web-parts-using-stsadmexe"></a>使用 STSADM.exe 安装 Web 部件  
  
1.  将 **RSWebParts.cab** 文件复制到与本文的 PowerShell 部分中所述 SharePoint 服务器上的相同位置。  
  
2.  在安装了 SharePoint 产品的计算机上，使用管理权限打开命令提示符窗口并导航到包含 **Stsadm.exe** 工具的文件夹。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 的默认路径如下：  
  
    > C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\BIN。  
  
3.  使用以下语法针对 .cab 运行 Stsadm.exe：  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  您应该看到“操作已成功完成”的消息。  
  
     指定 `-globalinstall` 会将 Web 部件添加到全局程序集缓存 (GAC) 中。 如果希望连接 Web 部件，则此步骤是必需的。  
  
##  <a name="bkmk_configurewebparts"></a> 添加和配置 Web 部件  
 安装 Web 部件后，可以将其添加到 SharePoint 站点上的一个或多个网页中。 您必须具有创建网站和添加内容的权限。  
  
 下面的过程将向一个网页中添加这两种 Web 部件，然后一起连接报表资源管理器和报表查看器，这样，当您在报表资源管理器中单击某一报表时，该报表将显示在报表查看器内。  
  
#### <a name="add-report-viewer"></a>添加报表查看器  
  
1.  在“站点操作”中，单击 **“编辑页面”**。  
  
2.  在页面上的某个区域中，单击 **“添加 Web 部件”**。  
  
3.  在 **“添加 Web 部件”** 对话框中，向下滚动到 **“杂项”** 类别。  
  
4.  选择 **“报表查看器”**。  
  
    > [!WARNING]  
    >  不要选择“SQL Server Reporting Services 报表查看器”。安装用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加载项时会注册该 Web 部件，此部件用于在 SharePoint 模式下运行报表服务器。 它不能用于查看在本机模式下运行的报表服务器上的报表。  
  
5.  单击 **“添加”**。  
  
6.  当页面处于编辑模式时，在报表查看器 Web 部件中单击 **“编辑 Web 部件”** 。  
  
7.  在 **“报表管理器 URL”** 中，键入与要访问的本机模式报表服务器相关联的报表管理器实例的 URL。 默认情况下，报表管理器 URL 具有以下语法： http://\<servername>/reports。  
  
8.  在 **“报表路径”** 中，指定一个正斜杠后接文件夹路径和报表名。 请 **不要** 包括服务器名称或报表管理器虚拟目录。 例如，若要打开 Adventure Works 文件夹中的“Company Sales”报表，请指定 **/Adventure Works/Company Sales**。 下面是另一个示例，其中，报表“Products”位于报表服务器根文件夹 **/Products**中。  
  
9. 单击“确定” 。  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>添加报表资源管理器和连接到报表查看器  
  
1.  在该页的另一个区域中，单击 **“添加 Web 部件”** ，从杂项文件夹中单击 **“报表资源管理器”** ，然后单击 **“添加”**。  
  
2.  在报表资源管理器 Web 部件上下文菜单中，单击 **“编辑 Web 部件”**。  
  
3.  在 **“报表管理器 URL”** 中，键入与要访问的本机模式报表服务器相关联的报表管理器实例的 URL。  
  
4.  （可选）设置 **“开始路径”**。 开始路径是报表服务器文件夹层次结构中的文件夹。 如果希望默认页面是深入文件夹层次结构的某个文件夹，则可以指定开始路径。 该路径必须以正斜杠开头。 您必须指定从报表服务器文件夹层次结构根节点开始的完整路径，但不包含服务器名称或报表管理器虚拟目录。 例如，若要打开紧邻根节点下名为 Adventure Works 的文件夹，请在“开始路径”中指定 **/Adventure Works** 。  
  
5.  单击“确定” 。  
  
6.  报表资源管理器将显示报表服务器中报表项的列表。 默认情况下，如果您单击某一报表的名称，则会在新窗口中打开该报表。 如果您想要将报表资源管理器连接到报表查看器，以便当您在报表资源管理器中单击某一报表名称时该名称显示在报表查看器中，请完成以下步骤。  
  
    1.  在报表资源管理器上下文菜单中，单击 **“连接”**。  
  
    2.  单击 **“在以下位置显示报表”**。  
  
    3.  单击 **“报表查看器”**。  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
