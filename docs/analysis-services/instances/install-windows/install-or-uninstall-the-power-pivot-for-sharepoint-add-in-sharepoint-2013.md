---
title: "安装或卸载 Power Pivot 有关 SharePoint 外接程序 (SharePoint 2013) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ea599e36ce4926881d77a3164acfbd2035f1fba
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013"></a>安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 是在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 场中提供 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] 数据访问的应用程序服务器组件和后端服务的集合。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 外接程序 (**spPowerpivot.msi**) 是用于安装应用程序服务器组件的安装程序包。  
  
-   该外接程序对于 SharePoint 2010 部署不是必需的。  
  
-   在包含 SharePoint 2013 和 SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的单一服务器部署中，此外接程序不是必需的。 在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器时，将包括由此外接程序安装的组件。 有关具有该外接程序的示例部署的关系图，请参阅 [SharePoint 中 SQL Server BI 功能的部署拓扑](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)。  
  
 **注意：** 本主题介绍如何安装 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 解决方案文件和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具。 安装后，请参阅以下主题以了解有关配置工具和附加功能的信息：[配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
 有关如何下载 **spPowerPivot.msi**的信息，请参阅 [Microsoft® SQL Server® 2014 Power Pivot® for Microsoft SharePoint®](http://go.microsoft.com/fwlink/?LinkID=324854)。  
  
 **本主题内容：**  
  
-   [背景](#bkmk_background)  
  
-   [spPowerPivot.msi 的安装位置](#bkmk_where_to_install)  
  
-   [要求和先决条件](#bkmk_prereq)  
  
-   [安装 Power Pivot for SharePoint](#bkmk_install)  
  
-   [使用 Power Pivot for SharePoint 2013 配置工具部署 SharePoint 解决方案文件](#bkmk_deploy_solution)  
  
-   [卸载或修复外接程序](#bkmk_remove_addin)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
##  <a name="bkmk_background"></a> 背景  
  
-   **应用程序服务器：** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能包括将工作簿用作数据源、计划数据刷新以及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理仪表板。  
  
     [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 是一个 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 安装程序包 (**spPowerpivot.msi**)，用于部署 Analysis Services 客户端库和将 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 安装文件复制到计算机。 此安装程序不会在 SharePoint 中部署或配置 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能。 默认情况下将安装下列组件：  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013.此组件包括 PowerShell 脚本（.ps1 文件）、SharePoint 解决方案包 (.wsp) 和 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 配置工具，用于在 SharePoint 2013 服务器场中部署 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Analysis Services OLE DB 访问接口 (MSOLAP)。  
  
    -   ADOMD.NET 数据访问接口。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析管理对象。  
  
-   **后端服务：** 如果您使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 来创建包含分析数据的工作簿，则必须为 Excel Services 配置在 SharePoint 模式下运行 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的 BI 服务器才能访问服务器环境中的这些数据。 您可在安装了 SharePoint Server 2013 的计算机上或没有 SharePoint 软件的其他计算机上运行 SQL Server 安装程序。 Analysis Services 对 SharePoint 没有任何依赖关系。  
  
     有关安装、卸载和配置后端服务的详细信息，请参阅以下文章：  
  
    -   [在 Power Pivot 模式下安装 Analysis Services。](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [卸载 Power Pivot for SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> spPowerPivot.msi 的安装位置  
 建议的最佳做法是在 SharePoint 场中的所有服务器上安装 **spPowerPivot.msi** 以实现配置一致性，包括应用程序服务器和 Web 前端服务器。 此安装程序包包含 Analysis Services 数据访问接口以及 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 配置工具。 安装 **spPowerPivot.msi** 时，您可通过排除个别组件来自定义安装。  
  
 **数据访问接口：** 一些 SharePoint 和 SQL Server 技术使用 Analysis Services 数据访问接口，这些技术包括 Excel Services、PerformancePoint Services 和 Power View。 在所有 SharePoint 服务器上安装 **spPowerPivot.msi** 将确保全套 Analysis Services 数据访问接口和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 连接在服务器场中一致可用。  
  
> [!NOTE]  
>  您必须使用 **spPowerPivot.msi**在 SharePoint 2013 服务器上安装 Analysis Services 数据访问接口。 不支持 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能包中提供的其他安装程序包，因为这些包中未包含数据访问接口在此环境中所需的 SharePoint 2013 支持文件。  
  
 **配置工具：** 仅 SharePoint 服务器之一需要 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具。 但是，在多服务器场中，建议的最佳做法是在至少两台服务器上安装此配置工具，以便两台服务器中的一台脱机时，您具有访问此配置工具的权限。  
  
##  <a name="bkmk_prereq"></a> 要求和先决条件  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013。  
  
-   **spPowerPivot.msi** 只有 64 位版，以符合 SharePoint 产品和技术的要求。  
  
-   中的服务器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式。 Excel Services 将使用 SQL Server Analysis Services 实例作为 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务器。 Analysis Services 可在本地或远程计算机上运行。  
  
-   **权限：** 若要安装 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)]，当前用户需要是计算机上的管理员和 SharePoint 场 Administrators 组的成员。  
  
-   有关 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 的要求和先决条件的详细信息，请转到 [SharePoint 模式下的 Analysis Services 服务器的硬件和软件要求](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)。  
  
##  <a name="bkmk_install"></a> 安装 Power Pivot for SharePoint  
 **spPowerpivot.msi** 安装程序包同时支持图形用户界面和命令行模式。 这两种安装方法都要求您使用管理员特权运行 .msi。 安装后，请参阅以下主题以了解有关配置工具和附加功能的信息：[配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
### <a name="user-interface-installation"></a>用户界面安装  
 若要使用图形用户界面安装 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] ，请完成下列步骤：  
  
1.  运行 **SpPowerPivot.msi**。  
  
2.  在“欢迎”页上，单击 **“下一步”** 。  
  
3.  阅读并接受许可协议，然后单击 **“下一步”**。  
  
4.  在 **“功能选择”** 页上，默认情况下将选择所有功能。  
  
5.  在“欢迎”页上，单击 **“下一步”**。  
  
6.  单击 **“安装”** 以进行安装直至完成安装。  
  
### <a name="command-line-installation"></a>命令行安装  
 对于命令行安装，请使用管理权限打开命令提示符，然后运行 **spPowerPivot.msi**。 例如：  
  
 `Msiexec.exe /i SpPowerPivot.msi`。  
  
 若要创建安装日志，请使用标准 MsiExec 日志记录开关。 以下示例使用“v”详细日志记录开关创建日志文件“Install_Log.txt”。  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>用于脚本编写的静默命令行安装  
 你可以使用 **/q** 或 **/quiet** 开关，进行不显示任何对话框或警告的“静默”安装。 如果您想要编写外接程序安装的脚本，静默安装将很有用。  
  
> [!IMPORTANT]  
>  如果你将 **/q** 开关用于无提示命令行安装，将不显示最终用户许可协议。 对此软件的使用受到许可协议控制并且由您负责遵守该许可协议，而与安装方法无关。  
  
 **执行静默安装：**  
  
1.  使用 **管理员权限**打开命令提示符。  
  
2.  运行以下命令：  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>包含特定组件的命令行安装  
 并不是所有 SharePoint 服务器上都需要 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 配置工具，但建议在至少两台服务器上安装此配置工具，以便在需要时可以使用它。  
  
 在安装 spPowerPivot.msi 时，可使用命令行选项来安装特定项目（如数据访问接口）而不安装 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 配置工具。 下面的命令行是安装该配置工具之外的所有组件的示例：  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|选项|说明|  
|------------|-----------------|  
|Analysis_Server_SP_addin|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 配置|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|ADOMD.net 提供程序|  
|SQL_AMO|AMO 提供程序|  
|SQLAS_SP_Common|SharePoint 2013 的 Analysis Services 常用组件|  
  
##  <a name="bkmk_deploy_solution"></a> 使用 Power Pivot for SharePoint 2013 配置工具部署 SharePoint 解决方案文件  
 spPowerPivot.msi 复制到硬盘的三个文件均是 SharePoint 解决方案文件。 一个解决方案文件的作用域是 Web 应用程序级别，而其他文件的作用域是场级别。 这三个文件分别是：  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 解决方案文件将复制到以下文件夹：  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 在 .msi 安装之后，运行 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 配置工具以在 SharePoint 场中配置和部署解决方案。  
  
 **要启动配置工具：**  
  
 在 Windows“开始”屏幕上，键入“power”，然后在“应用程序”搜索结果中，单击“[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 配置”。 请注意，搜索结果可能包含两个链接，因为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序为 SharePoint 2010 和 SharePoint 2013 安装单独的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 配置工具。 确保您启动了 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具。  
  
 ![两个 powerpivot 配置工具](../../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "two powerpivot configuratoin tools")  
  
 **Or**  
  
1.  转到 **“开始”**、 **“所有程序”**。  
  
2.  单击 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]。  
  
3.  单击 **“配置工具”**。  
  
4.  单击“[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 配置”。  
  
 有关配置工具的详细信息，请参阅 [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
##  <a name="bkmk_remove_addin"></a> 卸载或修复外接程序  
  
> [!CAUTION]  
>  如果卸载 **spPowerPivot.msi** ，则将卸载数据访问接口和配置工具。 卸载数据提供程序将导致服务器无法连接到 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
 您可通过下列方式之一卸载或修复 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] ：  
  
1.  **Windows 控制面板：** 选择 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013**。 单击 **“卸载”** 或 **“修复”**。  
  
2.  运行 spPowerPivot.msi 并选择 **“删除”** 选项或 **“修复”** 选项。  
  
 **命令行：** 若要使用命令行修复或卸载 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013，请 **使用管理员权限** 打开命令提示符，然后运行下列命令之一：  
  
-   若要修复，请运行以下命令：  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 或  
  
-   若要卸载，请运行以下命令：  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  

