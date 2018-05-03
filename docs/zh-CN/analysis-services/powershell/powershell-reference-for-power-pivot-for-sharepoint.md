---
title: Power Pivot for SharePoint 的 PowerShell 参考 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8a133d55644545e9af6331653a8ec153b53abea9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>针对 PowerPivot for SharePoint 的 PowerShell 参考
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本节列出了用来配置或管理 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装的 PowerShell cmdlet。 有关启用 cmdlet 和查看内置帮助的详细信息，请参阅 [使用 Windows PowerShell 配置 PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="cmdlet-list"></a>Cmdlet 列表  
 从 PowerShell 提示符处查看 cmdlet 列表：  
  
1.  使用 **“以管理员身份运行”** 选项打开 SharePoint Management Shell。  
  
2.  输入以下命令： `Get-help *powerpivot*`  
  
|Cmdlet|支持的版本|  
|------------|------------------------|  
|[Get-PowerPivotServiceApplication cmdlet](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Get-PowerPivotSystemService cmdlet](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Get-PowerPivotSystemServiceInstance cmdlet](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[New-PowerPivotServiceApplication cmdlet](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[New-PowerPivotSystemServiceInstance cmdlet](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Remove-PowerPivotServiceApplication cmdlet](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Remove-PowerPivotSystemServiceInstance cmdlet](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Set-PowerPivotServiceApplication cmdlet](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Set-PowerPivotSystemService cmdlet](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
|[Update-PowerPivotSystemService cmdlet](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 | SharePoint 2016|  
  
 注意：以下 Cmdlet 适用于 SharePoint 2010 ，但其并不受 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 支持。  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  
