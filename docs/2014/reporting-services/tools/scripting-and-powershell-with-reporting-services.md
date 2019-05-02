---
title: 脚本编写和带 Reporting Services 的 PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 005d1e580f64adc3687886a1562598ac575183fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158826"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>脚本编写和带 Reporting Services 的 PowerShell
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 支持广泛的开发和管理方案（通过脚本进行），包括 rs.exe 命令行实用工具、适用于 SharePoint 模式报告服务器的 PowerShell cmdlet 以及利用 PowerShell 中的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 对象模式实现本机模式和 SharePoint 模式。  
  
-   管理员可以用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 编写脚本来自动控制如何部署和管理所安装的报表服务器， 可以生成和运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本来创建、配置和更新报表服务器数据库， 还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的记录和播放脚本功能来自动执行日常维护任务。  
  
-   开发人员可以创建包括脚本的自定义应用程序。 您可以运行调用 Report Server Web 服务的脚本。 几乎所有可以用托管代码编写的操作都可以用脚本编写。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 支持 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 脚本作为可通过 RS.exe 实用工具（可在报告服务器上运行的脚本主机）进行处理的脚本语言。  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Reporting Services SharePoint 模式 PowerShell cmdlet 和示例  
 ![与 PowerShell 相关的内容](../media/rs-powershellicon.jpg "PowerShell related content")  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式包括用于报表服务器管理的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] cmdlet。  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md) 包括以下示例：  
  
    -   创建服务应用程序和代理  
  
    -   查看和更新传递扩展插件  
  
    -   获取和设置 Reporting Service 应用程序数据库的属性，例如数据库超时  
  
    -   列表数据扩展插件  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Reporting Service 对象模型和 Powershell 示例  
 ![与 PowerShell 相关的内容](../media/rs-powershellicon.jpg "PowerShell related content")  
  
 PowerShell 调用核心对象模型，对于 SharePoint 模式和本机模式大部分有效，例如迁移工作、订阅工作以及 SQL15 中的订阅工作的更多相关示例。  
  
-   [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](../subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)。  
  
-   [使用 PowerShell 来创建带有本机模式报表服务器的 Azure VM](https://msdn.microsoft.com/library/azure/dn449661.aspx)。  
  
-   请参阅[访问 Reporting Services WMI 提供程序](access-the-reporting-services-wmi-provider.md)中的“使用 PowerShell 访问 WMI 类”一节。  
  
-   [如何使用 PowerShell 管理 SSRS](https://www.sqlshack.com/how-to-administer-sql-server-reporting-services-ssrs-subscriptions-using-powershell/).scriptin  
  
## <a name="rsexe-scripting-samples"></a>RS.exe 脚本示例  
  
-   [用于在报表服务器之间复制内容的示例 Reporting Services rs.exe 脚本](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。列中的一个值匹配。  
  
-   有关其他脚本、应用程序和扩展插件的示例，请参阅 [SQL Server Reporting Service 产品示例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>请参阅  
 [RS.exe 实用工具 (SSRS)](rs-exe-utility-ssrs.md)   
 [为部署和管理任务编写脚本](script-deployment-and-administrative-tasks.md)   
 [使用 rs.exe 实用工具和 Web 服务编写脚本](script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
