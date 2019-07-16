---
title: Power Pivot 配置使用 Windows PowerShell |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e290e0e15797a8b84a6d52c945a5fd78458515fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208206"
---
# <a name="power-pivot-configuration-using-windows-powershell"></a>使用 Windows PowerShell 配置 Power Pivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供 Windows PowerShell cmdlet，您可以使用这些 cmdlet 配置安装的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。 使用 PowerShell 完全配置已安装的软件需要使用 SharePoint cmdlet 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint cmdlet。 大多数配置可使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工具之一来完成。 有关这些工具的详细信息，请参阅 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
> [!IMPORTANT]  
>  对于 SharePoint 2010 场，必须首先安装 SharePoint 2010 SP1，然后才能配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或配置使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 数据库服务器的 SharePoint 场。 如果您尚未安装 Service Pack，则应首先安装 Service Pack，然后再开始配置服务器。  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-powershell"></a>使用 PowerShell 配置 Power Pivot for SharePoint 的好处  
 可以生成 Windows PowerShell 脚本 (.ps1) 文件来自动执行配置任务。 如果您需要可以在任何服务器上运行的脚本化的安装和配置步骤，则推荐使用上述做法。 您可能需要这样一个脚本，将其纳入出现硬件故障时用来重新构建服务器的灾难恢复计划。  
  
## <a name="view-a-list-of-the-power-pivot-cmdlets-on-a-server"></a>查看服务器上 Power Pivot Cmdlet 的列表  
 若要查看 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlet 的内容和示例，请参阅 [针对 PowerPivot for SharePoint 的 PowerShell 参考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)。  
  
 使用 PowerShell 查看 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlet 列表：  
  
1.  使用 **“以管理员身份运行”** 选项打开 SharePoint Management Shell。  
  
2.  输入以下命令：  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     你应该看到 cmdlet 名称中包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的 cmdlet 的列表。 例如 `Get-PowerPivotServiceApplication`。 可用的 cmdlet 数量取决于您使用的 Analysis Services 版本。  
  
    -   10 个 cmdlet 以及在 SharePoint 模式下配置的 SQL Server 2012 SP1 Analysis Services 服务器，以及 SharePoint 2013。 2012 SP1 版本利用了一个新的体系结构，允许 Analysis Server 在 SharePoint 场之外运行，所需的管理 Windows PowerShell cmdlet 更少。  
  
    -   17 个 cmdlet 以及在 SharePoint 模式下配置的 SQL Server 2012 Analysis Services 服务器，以及 SharePoint 2010。  
  
     如果在列表中未返回任何命令或者您看到类似的错误消息"`get-help could not find *powerpivot* in a help file in this session.`"，请参阅如何启用说明本主题中的下一步部分[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]在服务器上的 cmdlet。  
  
     所有 cmdlet 都有联机帮助。 下面的示例显示了如何查看 **New-PowerPivotServiceApplication** cmdlet 的联机帮助：  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     或者，若仅查看示例，使用下面的语法：  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-power-pivot-cmdlets-on-a-server"></a>在服务器上启用 Power Pivot Cmdlet  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 在安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 并部署场解决方案后，即可使用 cmdlet。 在您运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具时部署解决方案。 请按照以下步骤启用 cmdlet：  
  
1.  使用 **“以管理员身份运行”** 选项打开 SharePoint Management Shell。  
  
2.  运行第一个 cmdlet：  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     该 cmdlet 返回解决方案的名称、其解决方案 ID 和 Deployed=False。 在下一步骤中，您将部署解决方案。  
  
3.  运行第二个 cmdlet 以便部署解决方案：  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  关闭“服务” 窗口。 使用 **“以管理员身份运行”** 选项重新打开该窗口。  
  
## <a name="related-content"></a>相关内容  
 [在管理中心中管理和配置 Power Pivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [针对 PowerPivot for SharePoint 的 PowerShell 参考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
  
