---
title: 将 PowerPivot 解决方案部署到 SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b568790f9a61c01054d4a7225e4a2dbf9a39887
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071509"
---
# <a name="deploy-powerpivot-solutions-to-sharepoint"></a>将 PowerPivot 解决方案部署到 SharePoint
  使用以下说明可手动部署两个解决方案包，这两个解决方案包将 PowerPivot 功能添加到 SharePoint Server 2010 环境。 部署解决方案是在 SharePoint 2010 服务器上配置 PowerPivot for SharePoint 所必需的步骤。 若要查看所需步骤的完整列表，请参阅[PowerPivot 服务器管理和配置在管理中心内](power-pivot-server-administration-and-configuration-in-central-administration.md)。  
  
 或者，您可以使用 PowerPivot 配置工具来部署解决方案。 对于单服务器部署来说，使用配置工具更为容易且效率更高，但如果您喜欢使用熟悉的工具或者同时配置多个功能，则最好使用管理中心和 PowerShell。 有关使用配置工具的详细信息，请参阅[PowerPivot 配置工具](power-pivot-configuration-tools.md)。  
  
 在部署解决方案之前，必须首先使用 SQL Server 2012 安装介质安装 PowerPivot for SharePoint。 SQL Server 安装程序将会安装您要部署的解决方案包。  
  
 本主题包含以下各节：  
  
 [先决条件：确认 Web 应用程序使用经典模式身份验证](#bkmk_classic)  
  
 [步骤 1：部署场解决方案](#bkmk_farm)  
  
 [步骤 2：将 PowerPivot Web 应用程序解决方案部署到管理中心](#deployCA)  
  
 [步骤 3：将 PowerPivot Web 应用程序解决方案部署到其他 Web 应用程序](#deployUI)  
  
 [重新部署或收回解决方案](#retract)  
  
 [关于 PowerPivot 解决方案](#intro)  
  
##  <a name="bkmk_classic"></a>先决条件：确认 Web 应用程序使用经典模式身份验证  
 只有使用 Windows 经典模式身份验证的 Web 应用程序才支持 PowerPivot for SharePoint。 若要检查应用程序是否使用经典模式，请运行以下 PowerShell cmdlet 从**SharePoint 2010 Management Shell**，并替换`http://<top-level site name>`与您的 SharePoint 站点的名称：  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 返回值应为 **false**。 如果它是 **，则返回 true**，不能访问此 web 应用程序与 PowerPivot 数据。  
  
##  <a name="bkmk_farm"></a> 步骤 1：部署场解决方案  
 本节向您演示如何使用 PowerShell 部署解决方案，但您也可以使用 PowerPivot 配置工具完成此任务。 有关详细信息，请参阅[配置或修复 PowerPivot for SharePoint 2010 &#40;PowerPivot 配置工具&#41;](../configure-repair-powerpivot-sharepoint-2010.md)。  
  
 在您 PowerPivot for SharePoint 安装后，此任务只需要执行一次。  
  
1.  在服务器上具有安装了 PowerPivot for SharePoint，打开 SharePoint 2010 Management Shell 使用**以管理员身份运行**选项。  
  
2.  运行以下 cmdlet 以便添加场解决方案。  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     该 cmdlet 返回解决方案的名称、其解决方案 ID 和 Deployed=False。 在下一步骤中，您将部署解决方案。  
  
3.  运行下一个 cmdlet 以便部署场解决方案：  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> 步骤 2：将 PowerPivot Web 应用程序解决方案部署到管理中心  
 在您部署了场解决方案后，必须将 Web 应用程序解决方案部署到管理中心。 此步骤将 PowerPivot 管理面板添加到管理中心。  
  
1.  使用 **“以管理员身份运行”** 选项打开 SharePoint 2010 Management Shell。  
  
2.  运行以下 cmdlet 以创建对管理中心的引用：  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  运行以下 cmdlet 以便添加场解决方案。  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp"  
    ```  
  
     该 cmdlet 返回解决方案的名称、其解决方案 ID 和 Deployed=False。 在下一步骤中，您将部署解决方案。  
  
4.  运行下一个 cmdlet 以将 Web 应用程序解决方案部署到管理中心。  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 现在，Web 应用程序解决方案已部署到管理中心，您可以使用管理中心完成所有其余配置步骤。  
  
##  <a name="deployUI"></a> 步骤 3：将 PowerPivot Web 应用程序解决方案部署到其他 Web 应用程序  
 在上一个任务中，您将 Powerpivotwebapp.wsp 部署到了管理中心。 在本节中，您可以在支持 PowerPivot 数据访问的每个现有 Web 应用程序上都部署 powerpivotwebapp.wsp。 如果您在以后添加更多的 Web 应用程序，请确保对于这些附加的 Web 应用程序都重复执行此步骤。  
  
1.  在管理中心的“系统设置”中，单击 **“管理场解决方案”** 。  
  
2.  单击 **“powerpivotwebapp.wsp”** 。  
  
3.  单击 **“部署解决方案”** 。  
  
4.  在中**部署到？** ，选择你想要添加 PowerPivot 功能支持的 SharePoint web 应用程序。  
  
5.  单击“确定”  。  
  
6.  对也要支持 PowerPivot 数据访问的其他 SharePoint Web 应用程序重复此过程。  
  
##  <a name="retract"></a> 重新部署或收回解决方案  
 尽管 SharePoint 管理中心提供解决方案收回，但您无需收回 powerpivotwebapp.wsp 文件，除非您在系统地排除安装或修补程序部署问题。  
  
1.  在 SharePoint 2010 管理中心的“系统设置”中，单击 **“管理场解决方案”** 。  
  
2.  单击 **Powerpivotwebapp.wsp**。  
  
3.  单击 **“收回解决方案”** 。  
  
 如果遇到回溯场解决方案的服务器部署问题，您可以通过运行重新部署**修复**PowerPivot 配置工具中的选项。 应优先通过工具进行修复操作，因为这样只需执行较少的步骤。 有关详细信息，请参阅[配置或修复 PowerPivot for SharePoint 2010 &#40;PowerPivot 配置工具&#41;](../configure-repair-powerpivot-sharepoint-2010.md)。  
  
 如果您仍想要重新部署所有解决方案，则请确保按照下面的顺序进行重新部署：  
  
1.  从使用它的所有 SharePoint Web 应用程序中收回 PowerPivot Web 应用程序解决方案。  
  
2.  收回 PowerPivot 场解决方案。  
  
3.  重新部署 PowerPivot 场解决方案。  
  
4.  将 PowerPivot Web 应用程序解决方案重新部署到所有 SharePoint Web 应用程序中。  
  
##  <a name="intro"></a> 关于 PowerPivot 解决方案  
 PowerPivot for SharePoint 使用两个解决方案包将其应用程序页和程序文件部署到场中和单独的 Web 应用程序中。  
  
-   场解决方案是全局的。 该解决方案仅需部署一次就会变得自动可用于您以后添加到场中的任何新的 PowerPivot for SharePoint 服务器。  
  
-   Web 应用程序解决方案是特定于应用程序的，且必须部署到场中的每个 Web 应用程序，包括管理中心 Web 应用程序。  
  
 每个解决方案的部署方式都是不同的。  场解决方案会在第一个 PowerPivot for SharePoint 实例安装后部署一次。 若要部署场解决方案，可使用 PowerPivot 配置工具或 PowerShell cmdlet。  
  
 首先，会将 Web 应用程序部署到管理中心，然后会将后续解决方案部署到支持对 PowerPivot 数据的请求的任何其他 Web 应用程序。 若要将 web 应用程序解决方案部署到管理中心，必须使用 PowerPivot 配置工具或 PowerShell cmdlet。 对于所有其他 Web 应用程序，您可以使用管理中心或 PowerShell 手动部署 Web 应用程序解决方案。  
  
|解决方案|Description|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|将 Microsoft.AnalysisServices.SharePoint.Integration.dll 添加到全局程序集中。<br /><br /> 将 Microsoft.AnalysisServices.ChannelTransport.dll 添加到全局程序集中。<br /><br /> 安装功能和资源文件，并且注册内容类型。<br /><br /> 为 PowerPivot 库和数据馈送库添加库模板。<br /><br /> 为服务应用程序配置、PowerPivot 管理面板、数据刷新和 PowerPivot 库添加应用程序页。|  
|“powerpivotwebapp.wsp”|将 Microsoft.AnalysisServices.SharePoint.Integration.dll 资源文件添加到 Web 前端上的 Web 服务器扩展插件文件夹中。<br /><br /> 将 PowerPivot Web 服务添加到 Web 前端。<br /><br /> 为 PowerPivot 库添加缩略图生成。|  
  
## <a name="see-also"></a>请参阅  
 [升级 PowerPivot for SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [在管理中心的 PowerPivot 服务器管理和配置](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [使用 Windows PowerShell 配置 Power Pivot](power-pivot-configuration-using-windows-powershell.md)  
  
  
