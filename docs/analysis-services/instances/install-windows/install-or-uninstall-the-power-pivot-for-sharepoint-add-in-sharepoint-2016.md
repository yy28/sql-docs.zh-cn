---
title: "安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2016) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34dd07b8-d59d-49ce-bad0-74f40e4db0b8
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 712d9538d03c656a346f9e179a38abdd84aacd7e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016"></a>安装或卸载 Power Pivot for SharePoint 加载项 (SharePoint 2016)
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 是在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 场中提供 [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] 数据访问的应用程序服务器组件和后端服务的集合。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 加载项 (**spPowerpivot16.msi**) 是用于安装应用程序服务器组件的安装程序包。  
  
 **注意：** 本主题介绍如何安装 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 解决方案文件和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016 配置工具。 安装后，请参阅以下主题以了解有关配置工具和附加功能的信息：[配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
 有关如何下载 **spPowerPivot16.msi**的信息，请参阅 [Microsoft® SQL Server® 2016 Power Pivot® for Microsoft SharePoint®](https://www.microsoft.com/download/details.aspx?id=52675)。  
  
 **本主题内容：**  
  
-   [背景](#bkmk_background)  
  
-   [spPowerPivot16.msi 的安装位置在哪里？](#bkmk_where_to_install)  
  
-   [要求和先决条件](#bkmk_prereq)  
  
-   [安装 Power Pivot for SharePoint](#bkmk_install)  
  
-   [使用 Power Pivot for SharePoint 2016 配置工具部署 SharePoint 解决方案文件](#bkmk_deploy_solution)  
  
-   [卸载或修复外接程序](#bkmk_remove_addin)  
  

**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016 
  
##  <a name="bkmk_background"></a> 背景  
  
-   **应用程序服务器：** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能包括将工作簿用作数据源、计划数据刷新以及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理面板。  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] 是一个 Windows 安装程序包 (**spPowerpivot16.msi**)，用于部署 Analysis Services 客户端库和将 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 安装文件复制到计算机。 此安装程序不会在 SharePoint 中部署或配置 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能。 默认情况下将安装下列组件：  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]。 此组件包括 PowerShell 脚本（.ps1 文件）、SharePoint 解决方案包 (.wsp) 和 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具，用于在 SharePoint 2016 场中部署 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Analysis Services OLE DB 访问接口 (MSOLAP)。  
  
    -   ADOMD.NET 数据访问接口。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析管理对象。  
  
-   **后端服务：** 如果你使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 来创建包含分析数据的工作簿，则必须为 Office Online Server 配置在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式下运行 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的 BI 服务器才能访问服务器环境中的这些数据。 你可以在安装了 SharePoint Server 2016 的计算机上或没有 SharePoint 软件的其他计算机上运行 SQL Server 安装程序。 Analysis Services 对 SharePoint 没有任何依赖关系。  
  
     有关安装、卸载和配置后端服务的详细信息，请参阅以下文章：  
  
    -   [在 Power Pivot 模式下安装 Analysis Services。](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [卸载 Power Pivot for SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> spPowerPivot16.msi 的安装位置在哪里？  
 建议的最佳做法是在 SharePoint 场中的所有服务器上安装 **spPowerPivot16.msi** 以实现配置一致性，包括应用程序服务器和 Web 前端服务器。 此安装程序包包含 Analysis Services 数据访问接口以及 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具。 安装 **spPowerPivot16.msi** 时，你可通过排除个别组件来自定义安装。  
  
 **数据提供程序：** 一些 SharePoint 和 SQL Server 技术使用 Analysis Services 数据提供程序，这些技术包括 PerformancePoint Services 和 Power View。 在所有 SharePoint 服务器上安装 **spPowerPivot16.msi** 将确保全套 Analysis Services 数据提供程序和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 连接在服务器场中一致可用。  
  
> [!NOTE]  
>  你必须使用 **spPowerPivot16.msi**在 SharePoint 2016 服务器上安装 Analysis Services 数据提供程序。 不支持 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能包中提供的其他安装程序包，因为这些包中未包含数据提供程序在此环境中所需的 SharePoint 2016 支持文件。  
  
 **配置工具：** 仅 SharePoint 服务器之一需要 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具。 但是，在多服务器场中，建议的最佳做法是在至少两台服务器上安装此配置工具，以便两台服务器中的一台脱机时，您具有访问此配置工具的权限。  
  
##  <a name="bkmk_prereq"></a> 要求和先决条件  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016。  
  
-   **spPowerPivot16.msi** 只有 64 位版，以符合 SharePoint 产品和技术的要求。  
  
-   中的服务器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式。 Office Online Server 将使用 SQL Server Analysis Services 实例作为 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务器。 Analysis Services 可在本地 SharePoint 服务器或远程计算机上运行。 不能在 Office Online Server 上安装它。  
  
-   **权限：** 若要安装 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]，当前用户需要是计算机上的管理员和 SharePoint 场 Administrators 组中的成员。  
  
-   有关 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 的要求和先决条件的详细信息，请转到 [SharePoint 模式下的 Analysis Services 服务器的硬件和软件要求](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)。  
  
##  <a name="bkmk_install"></a> 安装 Power Pivot for SharePoint  
 **spPowerpivot16.msi** 安装程序包同时支持图形用户界面和命令行模式。 这两种安装方法都要求您使用管理员特权运行 .msi。 安装后，请参阅以下主题以了解有关配置工具和附加功能的信息：[配置 Power Pivot 和部署解决方案 (SharePoint 2013)](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
### <a name="user-interface-installation"></a>用户界面安装  
 若要使用图形用户界面安装 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ，请完成下列步骤：  
  
1.  运行 **spPowerPivot16.msi**。  
  
2.  在“欢迎”页上，选择“下一步”  。  
  
3.  阅读并接受许可协议，然后选择“下一步” 。  
  
4.  在 **“功能选择”** 页上，默认情况下将选择所有功能。  
  
5.  选择“下一步” 。  
  
6.  选择“安装”  以进行安装直至完成安装。  
  
### <a name="command-line-installation"></a>命令行安装  
 对于命令行安装，请使用管理权限打开命令提示符，然后运行 **spPowerPivot16.msi**。 例如：  
  
 `Msiexec.exe /i spPowerPivot16.msi`。  
  
 若要创建安装日志，请使用标准 MsiExec 日志记录开关。 以下示例使用“v”详细日志记录开关创建日志文件“Install_Log.txt”。  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>用于脚本编写的静默命令行安装  
 你可以使用 **/q** 或 **/quiet** 开关，进行不显示任何对话框或警告的“静默”安装。 如果您想要编写外接程序安装的脚本，静默安装将很有用。  
  
> [!IMPORTANT]  
>  如果你将 **/q** 开关用于无提示命令行安装，将不显示最终用户许可协议。 对此软件的使用受到许可协议控制并且由您负责遵守该许可协议，而与安装方法无关。  
  
 **执行静默安装：**  
  
1.  使用 **管理员权限**打开命令提示符。  
  
2.  运行以下命令：  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>包含特定组件的命令行安装  
 并不是所有 SharePoint 服务器上都需要 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具，但建议在至少两台服务器上安装此配置工具，以便在需要时可以使用它。  
  
 在安装 spPowerPivot16.msi 时，可使用命令行选项来安装特定项目（如数据提供程序）而不安装 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具。 下面的命令行是安装该配置工具之外的所有组件的示例：  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|选项|说明|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置|  
|SQL_OLAPDM|SQL Server 2016 的 Analysis Services OLE DB 提供程序|  
|SQL_ADOMD|ADOMD.NET 提供程序|  
|SQL_AMO|SQL Server 2016 分析管理对象 (AMO) 提供程序|  
|SQLAS_SP16_Common|SharePoint 2016 的 Analysis Services 常用组件|  
  
##  <a name="bkmk_deploy_solution"></a> 使用 Power Pivot for SharePoint 2016 配置工具部署 SharePoint 解决方案文件  
 spPowerPivot16.msi 复制到硬盘的三个文件均是 SharePoint 解决方案文件。 一个解决方案文件的作用域是 Web 应用程序级别，而其他文件的作用域是场级别。 这三个文件分别是：  
  
-   `PowerPivot16FarmSolution.wsp`  

-   `PowerPivot16WebApplicationSolution.wsp`  
  
 解决方案文件将复制到以下文件夹：  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 在 .msi 安装之后，运行 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具以在 SharePoint 场中配置和部署解决方案。  
  
 **要启动配置工具：**  
  
 在 Windows“开始”屏幕上，键入“power”，然后在“应用程序”搜索结果中，选择“[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置”。 请注意，搜索结果可能包含两个链接，因为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序为 SharePoint 2013 和 SharePoint 2016 安装单独的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 配置工具。 请确保你启动了 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置工具。  
  
 ![PowerPivot for SharePoint 2016 配置](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "PowerPivot for SharePoint 2016 配置")  
  
 **Or**  
  
1.  转到 **“开始”**、 **“所有程序”**。  
  
2.  选择 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]。  
  
3.  选择“配置工具” 。  
  
4.  在“欢迎”页上，选择“下一步” **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 配置**。  
  
 有关配置工具的详细信息，请参阅 [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
##  <a name="bkmk_remove_addin"></a> 卸载或修复外接程序  
  
> [!CAUTION]  
>  如果卸载 **spPowerPivot16.msi** ，则将卸载数据提供程序和配置工具。 卸载数据提供程序将导致服务器无法连接到 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
 您可通过下列方式之一卸载或修复 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ：  
  
1.  **Windows 控制面板**：选择 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**。 单击“卸载”  或“修复” 。  
  
2.  运行 spPowerPivot16.msi 并选择“删除”  选项或“修复”  选项。  
  
 **命令行：** 若要使用命令行修复或卸载 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ，请 **使用管理员权限** 打开命令提示符，然后运行下列命令之一：  
  
-   若要修复，请运行以下命令：  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 或  
  
-   若要卸载，请运行以下命令：  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  
