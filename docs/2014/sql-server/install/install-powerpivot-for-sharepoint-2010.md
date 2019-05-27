---
title: 安装 PowerPivot for SharePoint 2010 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8e1aa9411fbc11becf8e7b159c27ef609e38083b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094555"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>安装 PowerPivot for SharePoint
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 是在 SharePoint 2010 场中提供 PowerPivot 数据访问的中间层和后端服务的集合。 如果您的组织使用客户端应用程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 2010 来创建包含分析数据的工作簿，您必须具有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 才能访问服务器环境中的数据。 本主题演练基本安装过程，并包含可帮助您配置 PowerPivot 的其他主题链接。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 
  
 有关如何安装说明[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]并[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在同一服务器上，请参阅[部署核对清单：Reporting Services、 Power View 和 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)。  
  
## <a name="prerequisites"></a>先决条件  
  
1.  您必须是本地管理员才能运行 SQL Server 安装程序。  
  
2.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 需要 SharePoint Server 2010 Enterprise Edition。 您也可以使用评估企业版。  
  
3.  必须安装 SharePoint Server 2010 SP2。 如果没有该软件，您就无法将场配置为使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能。  
  
4.  必须将计算机加入到域中。  
  
5.  您必须具有域用户帐户才能设置 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装中，Analysis Services 服务帐户必须是域用户帐户，您才能从管理中心对其进行管理。 将上键入帐户和凭据**服务器配置**页作为此文档中的步骤的一部分。  
  
6.  必须提供 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 实例名称。 在您要安装 PowerPivot for SharePoint 的计算机上，不能具有现有的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 命名实例。  
  
7.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 实例不能是 SQL Server 故障转移群集的一部分。 使用 SharePoint 产品的高可用性功能。 例如，Excel Services 管理 PowerPivot for SharePoint 服务器的负载平衡。 有关详细信息，请参阅[管理 Excel Services 数据模型设置 (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx)。  
  
8.  如果要在现有场中安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，则必须具有为经典模式身份验证配置的一个或多个 SharePoint Web 应用程序。 只有该 Web 应用程序支持经典模式身份验证，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问才有效。 有关经典模式要求的详细信息，请参阅[PowerPivot 身份验证和授权](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)。  
  
9. 查看以下其他主题以了解系统和版本要求：  
  
    -   [使用 SharePoint 2010 场中的 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a> 步骤 1：安装 PowerPivot for SharePoint  
 在此步骤中，您将运行 SQL Server 安装程序以安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。 在后续步骤中，您将配置服务器来作为安装后任务。  
  
1.  插入安装介质或者打开包含 SQL Server 安装程序文件的文件夹，然后双击**setup.exe**。  
  
2.  单击**安装**左侧的导航窗格中。  
  
3.  单击 **“全新 SQL Server 独立安装或向现有安装添加功能”**。  
  
4.  上**产品密钥**页上，指定 evaluation edition 或输入产品密钥的 enterprise edition 的许可副本。  
  
     单击“下一步” 。  
  
5.  接受 Microsoft 软件许可协议条款，我们还希望您启用客户体验和错误报告。 单击“下一步” 。  
  
6.  如果提示您更新安装程序文件，请照做。  
  
7.  上**安装规则**页上，安装程序将标识可能会阻止安装的任何问题。 查看该列表，以确定安装程序是否在系统中检测到了潜在问题。  
  
    > [!NOTE]  
    >  因为启用了 Windows 防火墙，所以系统将警告您打开端口以便允许进行远程访问。 此警告通常不适用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 安装。 使用已为 SharePoint 服务到服务通信打开的 SharePoint 端口建立与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务和数据文件的连接。  
  
     单击“下一步” 。 等候 SQL Server 安装程序的程序文件安装到服务器上。  
  
8.  在 **“设置角色”** 页中，选择 **“SQL Server PowerPivot for SharePoint”**。  
  
9. 或者，您可以向您的安装添加数据库引擎的实例。 如果您正在设置新场且需要运行该场的配置和内容数据库的数据库服务器，则可能需要这样做。 如果添加数据库引擎，它将作为 PowerPivot 命名实例安装。 每当需要指定 （例如，在场配置向导时如果使用该项导配置场），在此实例的连接按以下格式输入数据库名称： <`servername`> \PowerPivot。  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. 单击“下一步” 。  
  
11. 上**功能选择**页上，将安装的功能的只读列表显示供您参考。 不能添加或删除为此角色预先选择的项。 单击“下一步” 。  
  
12. 上**功能规则**页上，单击**下一步**。 该页可能会被跳过。  
  
13. 在 **“实例配置”** 页中，将显示“PowerPivot”的只读实例名称供您参考。 此实例名称**POWERPIVOT**是**所需，不能修改**。 但是，您可以输入唯一的实例 ID 以便指定说明性的目录名称和注册表项。 单击“下一步” 。  
  
14. 上**服务器配置**页上，键入所需的帐户信息。  
  
     对于 SQL Server Analysis Services，您必须指定一个域用户帐户。 不要指定内置帐户。 域帐户所需的管理 Analysis Services 服务帐户作为*托管帐户*在 SharePoint 管理中心中。  
  
     ![SSAS 服务器配置](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS 服务器配置")  
  
     如果您添加了 SQL Server 数据库引擎和 SQL Server 代理，则可以将服务配置为在域用户帐户或者默认虚拟帐户下运行。  
  
     切勿使用您自己的域用户帐户来设置任何服务。 这样做会向服务器授予您在网络中对资源拥有的相同权限。 如果服务器受到恶意用户的威胁，该用户将在您的域凭据下登录，并且能够下载或使用您所能下载或使用的相同数据和应用程序。  
  
15. 单击“下一步” 。  
  
16. 如果安装数据库引擎，则将显示“数据库引擎配置”页。 在数据库引擎配置中，单击**添加当前用户**以授予您的用户帐户数据库引擎实例上的管理员权限。 单击**添加**以添加其他帐户。 单击“下一步” 。  
  
17. 在 **“Analysis Services 配置”** 页中，单击 **“添加当前用户”** 以便向您的用户帐户授予管理权限。 在完成安装程序后，您将需要管理权限以便对服务器进行配置。  
  
18. 在同一页中，添加也要求管理权限的任何人士的 Windows 用户帐户。 例如，如果用户想要在 SQL Server Management Studio 中连接到 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]实例以便排除数据库连接问题或获取版本信息，则任何此类用户都必须对服务器具有系统管理员权限。 添加可能需要立即排除服务器问题或管理服务器的任何人士的用户帐户。  
  
19. 单击“下一步” 。  
  
20. 单击**下一步**上每个剩余的页，直到你转到安装页已准备好。  
  
21. 单击 **“安装”**。  
  
> [!TIP]  
>  如果需要进行故障排除 SQL Server 安装，请参阅[查看和阅读 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
##  <a name="bkmk_config"></a> 步骤 2：配置服务器  
  
> [!IMPORTANT]  
>  必须首先安装 SharePoint 2010 SP2，然后才能配置 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 或配置使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 数据库服务器的 SharePoint 场。 如果您尚未安装 Service Pack，则应立即安装 Service Pack，然后再开始配置服务器。  
  
 在配置服务器前，安装是不完整的。 在此版本中，服务器配置始终作为安装后任务，使用以下方法之一执行：[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具、 管理中心或 PowerShell。 若要继续，请选择下列方法之一：  
  
-   [配置或修复 PowerPivot for SharePoint 2010 &#40;PowerPivot 配置工具&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [在管理中心中管理和配置 PowerPivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
-   [使用 Windows PowerShell 配置 Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 **连接到数据库引擎实例。** [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]在安装  时，SQL Server 安装程序会为您提供用于向安装中添加数据库引擎实例的选项。 您可能添加了数据库引擎实例向您的安装如果正在设置新场且需要让数据库服务器来运行该场的配置和内容数据库。 如果添加了数据库引擎，则它已安装为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 命名实例。 每当需要指定 （例如，在场配置向导时如果使用该项导配置场），在此实例的连接，请务必按以下格式输入数据库名称： <`servername`> \PowerPivot。  
  
##  <a name="bkmk_redist"></a> 步骤 3：在 Excel Services 应用程序服务器上安装 Analysis Services OLE DB 访问接口  
 如果在单独的应用程序服务器上运行 Excel Calculation Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]，则需要执行其他安装步骤。 在运行 Excel Calculation Services 的应用程序服务器上，安装适当版本的 Analysis Services OLE DB (MSOLAP) 访问接口。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 MSOLAP 包含在 SQL Server 安装程序中，因此，仅当您的应用程序服务器不是 PowerPivot 应用程序服务器的情况下，才需要显式安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 MSOLAP。  
  
    > [!NOTE]  
    >  Excel Calculation Services 应用程序服务器还需要文件的实例**Microsoft.AnalysisServices.Xmla.dll**在全局程序集。 若要在应用程序服务器上安装 .dll，请安装 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 在选择"管理工具-完整"**功能选择**SQL Server 安装程序向导的页。  
  
-   如果希望应用程序服务器支持较旧版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿，则需要安装 SQL Server 2008 R2 版本的 MSOLAP。  
  
 有关安装提供程序，包括验证步骤的详细信息请参阅[SharePoint 服务器上安装 Analysis Services OLE DB 访问接口](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
##  <a name="bkmk_verify"></a> 步骤 4:验证安装  
 在最后一步中，您将验证 SharePoint 2010 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 是否完全正常运行。 有关说明，请参阅[验证 PowerPivot for SharePoint 安装](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。  
  
## <a name="see-also"></a>请参阅  
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [部署核对清单：Reporting Services、 Power View 和 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [部署核对清单：通过向 SharePoint 2010 场添加 PowerPivot 服务器来进行扩展](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [部署核对清单：PowerPivot for SharePoint 2010 的多服务器安装](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  
