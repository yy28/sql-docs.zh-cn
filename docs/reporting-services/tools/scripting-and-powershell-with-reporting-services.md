---
title: "脚本编写和带 Reporting Services 的 PowerShell |Microsoft 文档"
ms.custom: 
ms.date: 09/14/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2bb429f6b2f7ffb876887714a1eea64d97d76773
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="scripting-and-powershell-with-reporting-services"></a>脚本编写和带 Reporting Services 的 PowerShell
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支持范围广泛的开发和管理方案通过脚本，包括 rs.exe 命令行实用工具、 适用于 SharePoint 模式报表服务器，PowerShell cmdlet 和利用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]从 PowerShell 为本机模式和 SharePoint 模式的对象模型。  
  
-   管理员可以用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 编写脚本来自动控制如何部署和管理所安装的报表服务器， 可以生成和运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本来创建、配置和更新报表服务器数据库， 还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的记录和播放脚本功能来自动执行日常维护任务。  
  
-   开发人员可以创建包括脚本的自定义应用程序。 您可以运行调用 Report Server Web 服务的脚本。 几乎所有可以用托管代码编写的操作都可以用脚本编写。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]支持[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 脚本作为可通过 RS.exe 实用工具在报表服务器运行的脚本主机处理的脚本语言。  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Reporting Services SharePoint 模式 PowerShell cmdlet 和示例  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式包括[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用于报表服务器管理的 cmdlet。  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) 包括以下示例：  
  
    -   创建服务应用程序和代理  
  
    -   查看和更新传递扩展插件  
  
    -   获取和设置 Reporting Service 应用程序数据库的属性，例如数据库超时  
  
    -   列表数据扩展插件  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Reporting Service 对象模型和 Powershell 示例  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")  
  
 PowerShell 调用核心对象模型，对于 SharePoint 模式和本机模式大部分有效，例如迁移工作、订阅工作以及 SQL15 中的订阅工作的更多相关示例。  
  
-   [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)。  
  
-   [使用 PowerShell 来创建带有本机模式报表服务器的 Azure VM](http://msdn.microsoft.com/library/azure/dn449661.aspx)。  
  
-   请参阅 [Access the Reporting Services WMI Provider](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)中的“使用 PowerShell 访问 WMI 类”一节。  
  

## <a name="rsexe-scripting-samples"></a>RS.exe 脚本示例  
  
-   [Sample Reporting Services rs.exe Script to Copy Content between Report Servers](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)。  
  
-   有关其他脚本、应用程序和扩展插件的示例，请参阅 [SQL Server Reporting Service 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另请参阅  
 [RS.exe 实用工具 &#40;SSRS &#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [脚本部署和管理任务](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [使用 rs.exe 实用工具和 Web 服务的脚本](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  

