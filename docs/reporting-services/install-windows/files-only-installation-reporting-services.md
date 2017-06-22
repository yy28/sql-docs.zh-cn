---
title: "仅文件安装 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f9548290288b30b5a25d57083a7a2c4813a6609c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="files-only-installation-reporting-services"></a>“仅文件”安装 (Reporting Services)
  “仅文件安装”指的是一种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装模式，在该安装模式中，安装程序为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 程序文件创建文件夹结构、将文件复制到磁盘、在本地计算机上注册报表服务器服务、配置服务帐户、向服务帐户授予文件权限以及注册 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 提供程序。  
  
 “仅文件”安装包括以下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]功能：报表服务器 Web 服务（它承载报表服务器 Web 服务、后台处理应用程序和报表管理器）、报表生成器、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令行实用工具（rsconfig.exe、rskeymgmt.exe 和 rs.exe）。 此模式不适用于诸如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]之类的共享功能。如果要安装此类功能，就必须将其指定为独立的项。  
  
 与其他安装模式不同，“仅文件”模式下安装的报表服务器在安装程序完成后不能正常工作。 若要使用 [Reporting Services 配置管理器（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)来使报表服务器联机，则需要进行其他配置。  
  
## <a name="when-to-select-files-only-installation-mode"></a>何时选择“仅文件”安装模式  
 在以下情况下必须执行“仅文件”安装：  
  
-   想要将报表服务器连接到远程报表服务器数据库。  
  
-   想要将报表服务器作为命名实例安装。  
  
-   您的部署要求包括使用自定义设置或功能，并且想要完全控制服务器配置的时间和方式。  
  
-   安装包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]故障转移群集。  
  
## <a name="how-to-perform-a-files-only-installation"></a>如何执行“仅文件”安装  
 “仅文件”安装是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的默认安装模式。  
  
 可通过命令行或在安装向导中指定“仅文件”安装。 以下主题提供了分步说明：  
  
-   [使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
-   [从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
#### <a name="example-command-line-script"></a>命令行脚本示例  
 为清楚起见，该示例包括了 /RSINSTALLMODE="FilesOnlyMode"。 但是，由于“仅文件”模式是默认模式，因此可将其省略且仍可进行“仅文件”模式安装。  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>安装向导  
 在“功能选择”页中选择 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 时，安装程序将提供可用于指定安装模式的“[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置”页。 若要指定仅文件安装，请在“[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置”页上选择“安装但不配置报表服务器”。  
  
## <a name="see-also"></a>另请参阅  
 [验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [配置报表服务器数据库连接（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [安装 Reporting Services SharePoint 模式](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [安装 Reporting Services 本机模式报表服务器](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)  
  
  


