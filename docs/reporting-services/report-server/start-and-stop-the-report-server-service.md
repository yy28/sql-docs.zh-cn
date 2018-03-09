---
title: "启动和停止报表服务器服务 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: "55"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 48d0f1dddabd461401027633a70a0d51b9efa345
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="start-and-stop-the-report-server-service"></a>启动和停止报表服务器服务
  报表服务器是作为包含报表服务器 Web 服务、报表管理器和后台处理应用程序的 Windows 服务来实现的。 若要使用任何报表服务器功能，必须运行该服务。 停止该服务将停止所有报表服务器操作。  
  
 如果停止该服务，则对服务运行时应发生的计划报表和订阅处理的请求将添加到队列中。 这是因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理运行的作业会创建该事件。 如果想要在关闭服务时避免积压操作，请注意要同时停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
 可以使用多种工具来启动或停止报表服务器服务，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 中提供的服务工具。  
  
 如果要执行的操作不只是启动或停止服务（例如，更改服务帐户），则必须使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。 如果使用其他工具更改服务帐户，可能会破坏 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装。 有关详细信息，请参阅 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
 不能暂停和恢复服务。 没有引导参数。 虽然没有显式依赖关系，但若要在报表服务器上支持任何订阅或计划报表操作，则必须运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>使用 Reporting Services 配置工具启动或停止服务  
  
1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并连接到报表服务器。  
  
2.  在“报表服务器状态”页上，单击 **“停止”** 或 **“启动”**。  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>使用管理工具中的服务启动或停止服务  
  
-   在“管理工具”中，打开“服务”，右键单击 **SQL Server Reporting Services (MSSQLSERVER)**，再单击 **“停止”** 或 **“重新启动”**。  
  
 如果正在运行多个实例或报表服务器正在作为命名实例运行，请验证圆括号中的实例名称是否对应于您希望停止或重新启动的报表服务器实例。  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>使用 SQL Server 配置管理器启动或停止服务。  
  
1.  启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
2.  选择 SQL Server 服务，右键单击 **“SQL Server Reporting Services”**，再单击 **“停止”** 或 **“重新启动”**。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [启动、停止或暂停 SQL Server 代理服务](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
