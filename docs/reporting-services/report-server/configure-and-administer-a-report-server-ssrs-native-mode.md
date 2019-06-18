---
title: 配置和管理报表服务器（SSRS 本机模式）| Microsoft Docs
ms.date: 05/15/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, components
- deploying [Reporting Services], component options
- report servers [Reporting Services], component options
- configuration options [Reporting Services]
- administering Reporting Services
- components [Reporting Services], configuring
- configuring servers [Reporting Services]
ms.assetid: cfec012b-56f1-4346-9814-247acf22351c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f605121be80ecef94f5a4412d23869cfd17c6ca6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500311"
---
# <a name="configure-and-administer-a-report-server-ssrs-native-mode"></a>配置和管理报表服务器（SSRS 本机模式）
  本文总结了可用于配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的方法。 它还包含一个主题列表，其中所列的主题说明了如何配置特定的组件、功能或服务器功能。 若要配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，您可以：  
  
-   使用 Reporting Services 配置管理器。 本节中的许多主题均包含有关如何通过该工具配置特定功能的信息。  
  
-   使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可自定义服务器属性，启用“我的报表”，启用跟踪日志和设置站点范围的默认值。 有关站点设置的详细信息，请参阅 Management studio 的 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md) 。 请注意，可以创建并运行通过编程方式设置服务器属性的脚本。 有关详细信息，请参阅 [为部署和管理任务编写脚本](../../reporting-services/tools/script-deployment-and-administrative-tasks.md) 和 [报表服务器系统属性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)。  
  
-   使用 Web 门户授予访问报表服务器的权限。 权限通过为每个用户帐户或组帐户定义的角色分配进行传送。 有关详细信息，请参阅[角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)。  
  
-   也可以修改配置文件以更改应用程序设置。 有关每个文件的详细信息以及这些文件的修改指南，请参阅 [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="in-this-section"></a>在本节中  
 [配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 介绍如何定义用来访问报表服务器和 Web 门户的 URL。  
  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 为如何修改服务帐户和密码提供建议和步骤。  
  
 [创建报表服务器数据库（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
 介绍如何创建存储服务器元数据和对象所必需的报表服务器数据库。  
  
 [配置报表服务器数据库连接（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 介绍如何修改报表服务器用于连接到报表服务器数据库的连接字符串。  
  
 [Reporting Services 中的电子邮件传递](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
 介绍如何配置报表服务器，以便通过电子邮件来分发报表。  
  
 [配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 介绍如何配置用户帐户以便以无人参与的方式处理报表。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 安全性和保护](../../reporting-services/security/reporting-services-security-and-protection.md)   
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  
