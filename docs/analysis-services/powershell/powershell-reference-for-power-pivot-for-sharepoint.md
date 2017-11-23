---
title: "Power Pivot for SharePoint 的 PowerShell 参考 |Microsoft 文档"
ms.custom: 
ms.date: 11/16/2015
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 538992c846ed5dd7bfe9fdd8ab0aaf0ec47009ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>针对 Power Pivot for SharePoint 的 PowerShell 参考

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

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
  
  
