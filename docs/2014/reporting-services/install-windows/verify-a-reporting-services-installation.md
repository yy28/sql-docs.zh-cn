---
title: 验证 Reporting Services 安装 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9e57883c7b6119499135fede5ad9c398350e587a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272524"
---
# <a name="verify-a-reporting-services-installation"></a>Verify a Reporting Services Installation
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。 验证安装时应遵循的步骤取决于报表服务器的模式。  
  
 本主题包含以下信息：  
  
-   [验证 SharePoint 模式安装](#bkmk_sharepointmode)  
  
-   [验证本机模式安装](#bkmk_nativemode)  
  
##  <a name="bkmk_sharepointmode"></a> 验证 SharePoint 模式安装  
  
#### <a name="to-verify-the-reporting-services-service"></a>验证 Reporting Services 服务  
  
1.  在 SharePoint 管理中心中，单击 **“系统设置”** 组中的 **“管理服务器上的服务”** 。  
  
2.  验证是否已经安装了 **“SQL Server Reporting Services 服务”** 且该服务处于 **“运行”** 状态。  
  
     如果您在列表中看不到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务，则验证是否已安装该服务。 有关详细信息，请参阅的"安装并启动 Reporting Services SharePoint 服务"部分[安装 Reporting Services SharePoint 模式适用于 SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。  
  
#### <a name="to-verify-the-service-application"></a>验证服务应用程序  
  
1.  若要验证您在管理中心中至少有一种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序，请单击 **“应用程序管理”** 组中的 **“管理服务应用程序”** 。  
  
2.  验证是否有 **“SQL Server Reporting Services 服务应用程序”** 类型的服务应用程序和相应的应用程序代理。  
  
3.  单击服务应用程序名称 **旁边** ，然后单击 SharePoint 工具栏中的 **“属性”** 。  如果单击服务应用程序的名称，将打开服务应用程序的“管理”页，而非属性页。  
  
4.  验证是否将 **“Web 应用程序关联”** 配置为指向所需的 Web 应用程序。  
  
#### <a name="to-verify-the-site-collection-feature"></a>验证网站集功能  
  
1.  在网站设置中，单击 **“网站集管理”** 组中的 **“网站集功能”** 。  
  
2.  验证是否激活了 **“报表服务器集成功能”** 。  
  
#### <a name="to-verify-reporting-server-content-types"></a>验证报表服务器内容类型  
  
1.  若要验证或添加[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表服务器内容类型，请参阅[将报表服务器内容类型添加到库&#40;SharePoint 集成模式下的 Reporting Services&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
#### <a name="to-verify-you-can-launch-report-builder"></a>验证是否可以启动报表生成器  
  
1.  从文档库中，单击 SharePoint 功能区中的 **“文档”** 。  
  
2.  单击 **“新建文档”** ，然后单击 **“报表生成器报表”**。 如果看不到此选项，请回顾以前向库中添加报表服务器内容类型的过程。  
  
#### <a name="create-a-basic-report"></a>创建基本报表  
  
1.  在 SharePoint 文档库中，创建一个仅包含文本框的基本 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表，例如标题。 该报表不包含任何数据源或数据集。 目的是验证能否打开报表生成器和预览基本报表。  
  
2.  将报表保存到文档库并从库中运行该报表。 有关使用报表生成器创建报表的详细信息，请参阅 [启动报表生成器（报表生成器）](http://technet.microsoft.com/library/ms159221.aspx)。  
  
#### <a name="reporting-services-samples"></a>Reporting Services 示例  
  
1.  完成 Reporting Services 教程之一。 有关详细信息，请参阅 [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)。  
  
2.  从 CodePlex 下载 Adventure Works 示例数据库和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 示例报告。 有关详细信息，请参阅 [AdventureWorks 报表示例](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home)。  
  
##  <a name="bkmk_nativemode"></a> 验证本机模式安装  
 如果使用默认配置安装本机模式的报表服务器，安装程序将安装并部署该服务器。 可以执行几个简单的测试来验证安装程序是否部署了报表服务器。 只有本地管理员才能执行这些步骤。 若要让其他用户执行测试，必须为这些用户配置报表服务器访问权限。  
  
#### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>验证报表服务器已安装并正常运行  
  
1.  运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具，然后连接到您刚安装的报表服务器实例。 “Web 服务 URL”页包括指向报表服务器 Web 服务的链接。 单击该链接可验证您是否可以访问该服务器。 如果未配置报表服务器数据库，请先进行配置，再单击该链接。  
  
2.  打开“服务”控制台应用程序并验证报表服务器服务是否正在运行。 若要查看报表服务器服务的状态，请单击“开始”，指向“控制面板”，双击“管理工具”，再双击“服务”。 出现服务列表后，滚动到“报表服务器 (MSSQLSERVER)”。 该服务的状态应为 **“已启动”**。  
  
3.  打开浏览器，在地址栏中键入报表服务器的 URL。 该地址由安装过程中为报表服务器指定的服务器名称和虚拟目录名组成。 默认情况下，报表服务器虚拟目录的名称为 **ReportServer**。 可以使用以下 URL 验证报表服务器安装：http://\<计算机名称>/ReportServer\<_实例名称>。 如果将报表服务器安装为命名实例，URL 将有所不同。 有关 URL 格式的详细信息，请参阅[配置报表服务器 URL（SSRS 配置管理器）](configure-report-server-urls-ssrs-configuration-manager.md)。 如果你在 Windows Vista 或 Windows Server 2008 上是本地管理员，请参阅[为本地管理配置本机模式报表服务器 (SSRS)](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
4.  运行报表以测试报表服务器的操作。 对于此步骤，您可以从教程创建一个示例报表。 有关详细信息，请参阅[创建基本表报表（SSRS 教程）](../create-a-basic-table-report-ssrs-tutorial.md)。  
  
#### <a name="to-verify-that-report-manager-is-installed-and-running"></a>验证报表管理器已安装并正常运行  
  
1.  打开浏览器，在地址栏中键入报表服务器的 URL。 该地址由您在安装过程中或在 Reporting Services 配置工具的“报表管理器 URL”页中为报表管理器指定的服务器名称和虚拟目录名称组成。 默认情况下，报表管理器虚拟目录的名称为 **Reports**。 可以使用以下 URL 验证报表管理器安装：  
  
     http://\<计算机名称>/Reports\<_实例名称>。  
  
2.  使用报表管理器创建新文件夹或上载文件，以测试定义是否传回报表服务器数据库。 如果上述操作成功，则表明连接正常。  
  
     有关详细信息，请参阅[报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
#### <a name="to-verify-that-report-designer-is-installed-and-running"></a>验证报表设计器已安装并正常运行  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，然后创建基于报表服务器项目类型的新项目。 有关使用报表服务器项目向导的详细信息，请参阅 SQL Server 联机丛书中的 [SQL Server Data Tools 中的 Reporting Services (SSDT)](../tools/reporting-services-in-sql-server-data-tools-ssdt.md)。  
  
2.  如果安装了报表示例，请打开示例报表项目文件并将报表发布到报表服务器。  
  
## <a name="see-also"></a>请参阅  
 [排除 Reporting Services 安装故障](troubleshoot-a-reporting-services-installation.md)   
 [Reporting Services 错误的原因和解决方法](../troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
