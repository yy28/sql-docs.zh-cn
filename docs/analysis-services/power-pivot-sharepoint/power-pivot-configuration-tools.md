---
title: Power Pivot 配置工具 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ab3e6eb8839b87f1145501cd0b30895bf181ec60
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984469"
---
# <a name="power-pivot-configuration-tools"></a>Power Pivot Configuration Tools
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具配置、修复或删除 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导不会为 SharePoint 安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。 配置工具将在未来的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本中提供下载。  
  
 本主题说明了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工具的两种常规使用方法及它们之间的差异。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013  
  
 **本主题内容：**  
  
-   [使用配置工具的要求](#bkmk_requirements)  
  
-   [配置工具的两个版本](#bkmk_twoversions)  
  
-   [使用 Power Pivot 配置工具的概述](#bkmk_overview)  
  
-   [启动其中一个 Power Pivot 配置工具](#bmkm_start_tool)  
  
##  <a name="bkmk_requirements"></a> 使用配置工具的要求  
  
-   您必须是场管理员。  
  
-   您必须是 Analysis Services 实例的服务器管理员（仅限 SharePoint 2010）。  
  
-   您必须是场的配置数据库的 db_owner。  
  
-   这些配置工具无 TCP/IP 端口要求，因此，无需配置防火墙以适应这些配置工具。 配置工具要求在 SharePoint 平台中提供 Web 应用程序和共享服务。 可能需要针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器配置防火墙。 有关详细信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
##  <a name="bkmk_twoversions"></a> 配置工具的两个版本  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导将安装用于 SharePoint 2010 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具以及用于 SharePoint 2013 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。  
  
 这两个工具仅可用于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]实例。 不能使用它们安装 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。  
  
|“属性”|支持的 SharePoint 版本|详细配置|  
|----------|-------------------------------------|----------------------------|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置|SharePoint 2013|[配置或修复 Power Pivot for SharePoint 2013（Power Pivot 配置工具）](../../analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具|SharePoint 2010 和 SharePoint 2010|[配置或修复 Power Pivot for SharePoint 2010 （Power Pivot 配置工具）](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046)|  
  
###  <a name="bkmk_sum_differences_betweentools"></a> 这两种配置工具有何不同  
 这两个配置工具版本很相似，但运行这两种工具的配置步骤存在差异。 这些差异是由于 SharePoint 2010 与 SharePoint 2013 之间的变化，以及 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SQL Server 2012 SP1 版本与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的之前版本之间的体系结构差异而导致的。  
  
 下表描述了 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置** 工具中的新功能和更改功能。 下表还描述了 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具** 中有的，但 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具中没有的功能。 该表中的行与配置工具中的选项卡的顺序相同。  
  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具|  
|--------------------------------------------------------------|-----------------------------------------------|  
|主页提供了用于 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Server for Excel Services**的新选项。 此选项对于在 SharePoint 场外部运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持新的体系结构。 您可以将 Excel Services 配置为使用一个或多个在 SharePoint 模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。<br /><br /> ![新的配置工具中的 PowerPivot 服务器](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-configtool-differences-new-mainpage.gif "新配置工具中的 PowerPivot 服务器")||  
||2010 工具包括“在本地服务器上注册 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])”页，以配置 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本地实例。 该页面不是 2013 工具的组成部分，因为没有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的本地实例。<br /><br /> ![作为旧配置工具中的服务帐户](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-configtool-differences-old-register-as-localserver.gif "作为旧配置工具中的服务帐户")|  
||“创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序”页具有一个额外的选项，即“升级工作簿以启用数据刷新”。 此选项在 2013 工具中不可用。<br /><br /> ![升级旧配置工具中的工作簿](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-configtool-differences-old-uprgadeworkbooks.gif "升级旧配置工具中的工作簿")|  
|2013 工具具有一个新页面，即“配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器”。 此页支持在 SharePoint 场外部运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的新体系结构。 默认情况下，在主页的“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Server for Excel Services”文本框中键入的服务器名称也列在“配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器”上。<br /><br /> ![注册 PowerPivot 服务器新配置工具](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-configtool-differences-new-powerpivot-servers.gif "注册 PowerPivot 服务器新配置工具")||  
|2013 工具具有一个新页面，即“将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 加载项注册为 Excel Services 用法跟踪程序”。 SharePoint 2010 Excel Services 不跟踪 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]的使用数据。||  
||2010 工具包含“将 MSOLAP.5 作为受信任提供程序添加”  页以注册 MSOLAP，以便 SharePoint 2010 中的 Excel Services 可以加载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型。 此页不是 2013 工具的组成部分。 SharePoint 2013 Excel Services 不使用 MSOLAP 访问接口来加载模型。|  
  
##  <a name="bkmk_overview"></a> 使用 Power Pivot 配置工具的概述  
 当启动其中一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具时，该工具会评估现有安装，以确定哪些操作适用。 对于全新安装，只有配置任务可用。 配置服务器之后，会出现删除任务。 如果您是使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 实例启动的，升级也会出现在可用任务列表中。  
  
 如果您不熟悉管理中心或 Windows PowerShell，作为替代方式，您可以运行配置工具以完成 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装。  
  
 此外，该工具可以检测是否已配置场，或者是否缺少必需的功能。 如果已安装 SharePoint 程序文件但未配置场，该工具将提供用来配置场和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装的操作。  
  
 可以查看“脚本”  选项卡以了解如何使用 Windows PowerShell 配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 和 SharePoint。 有关详细信息，请参见以下内容：  
  
-   [使用 Windows PowerShell 配置 Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
-   [针对 Power Pivot for SharePoint 的 PowerShell 参考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
> [!NOTE]  
>  该工具不配置 Reporting Services。 如果要将 Reporting Services 添加到您的 SharePoint 环境，需要单独安装和配置 Reporting Services。 有关详细信息，请参见以下内容：  
>   
>  -   [在 SharePoint 模式下安装第一个报表服务器](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)。  
> -   [安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)。  
  
##  <a name="bmkm_start_tool"></a> 启动其中一个 Power Pivot 配置工具  
  
1.  在“开始”  屏幕上，键入 **powerpivot**  
  
     在“开始”屏幕上，键入 **powerpivot**，或者，在“开始”菜单上，依次单击“所有程序”、[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、“配置工具”，然后单击下列项之一：  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具**。  
  
    -   **OR**  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置**。  
  
     ![两个 powerpivot 配置工具](../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "two powerpivot configuratoin tools")  
  
     **注意：** 只有在本地服务器上安装了 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 后，这些工具才可用。  
  
2.  启动时，配置工具会检查您安装的状态，并提供适用于您的安装的任务。  
  
3.  可以执行下列一项或多项任务，具体取决于您的安装的当前状态：  
  
    1.  单击“配置或修复 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint”以完成安装后的任务或修复安装。  
  
    2.  单击 **“删除功能、服务、应用程序和解决方案”** ，从场中删除功能和解决方案。  
  
    3.  单击 **“升级功能、服务、应用程序和解决方案”** ，升级使用以前版本的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]安装的功能和解决方案。  
  
     例如，此图片显示用于 SharePoint 2013 工具的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置的启动页面。  
  
     ![PowerPivot for SharePoint 2013 配置工具](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-configtool-4-sharepoint2013-choosemode.gif "PowerPivot for SharePoint 2013 配置工具")  
  
 每个任务由用来解决服务器特定方面配置的各个操作组成。 例如，配置任务包括用于部署解决方案、创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序、激活功能和配置数据刷新的操作。 操作列表因您安装的当前状态而有所不同。 如果不需要某个操作，该工具会将其从任务列表中排除。  
  
 当您单击“运行”时，该工具以批处理模式处理所有操作。 尽管每个操作都显示为任务列表中的一个单独项，但任务中包括的所有操作将一起处理。 只处理通过验证检查的操作。 您可能需要添加或更改某些输入值以通过验证检查。  
  
## <a name="related-content"></a>相关内容  
 [Upgrade Power Pivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md) 描述升级场中现有安装的工作流。  
  
 [卸载 PowerPivot for SharePoint](../../sql-server/install/uninstall-power-pivot-for-sharepoint.md) ：描述从场中删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务、解决方案和应用程序页的工作流。  
  
 [使用 Windows PowerShell 配置 Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [在管理中心中管理和配置 Power Pivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
