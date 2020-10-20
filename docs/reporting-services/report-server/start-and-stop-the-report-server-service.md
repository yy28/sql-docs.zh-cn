---
title: 启动和停止报表服务器服务 | Microsoft Docs
description: 了解如何启动和停止包含报表服务器 Web 服务、Web 门户和后台处理应用程序的 Windows 服务。
ms.date: 05/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b7f60e735ecd2483f8f105666ee181cb48eaa98b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987503"
---
# <a name="start-and-stop-the-report-server-service"></a>启动和停止报表服务器服务

  报表服务器是作为包含报表服务器 Web 服务、Web 门户和后台处理应用程序的 Windows 服务来实现的。 若要使用任何报表服务器功能，必须运行该服务。 停止该服务将停止所有报表服务器操作。  
  
 如果停止该服务，则对服务运行时应发生的计划报表和订阅处理的请求将添加到队列中。 这是因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理运行的作业会创建该事件。 如果想要在关闭服务时避免积压操作，请注意要同时停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
 可以使用多种工具来启动或停止报表服务器服务，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 中提供的服务工具。  
  
 如果要执行的操作不只是启动或停止服务（例如，更改服务帐户），则必须使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。 如果使用其他工具更改服务帐户，可能会破坏 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装。 有关详细信息，请参阅[配置报表服务器服务帐户（报表服务器配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
 不能暂停和恢复服务。 没有引导参数。 虽然没有显式依赖关系，但若要在报表服务器上支持任何订阅或计划报表操作，则必须运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
## <a name="use-the-reporting-services-configuration-tool"></a>使用 Reporting Services 配置工具  
  
1. 启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并连接到报表服务器。  
  
2. 在“报表服务器状态”页上，选择“停止”或“启动”。   
  
## <a name="use-administrative-tools"></a>使用管理工具  

- 在“管理工具”中，打开“服务”，右键单击 SQL Server Reporting Services (MSSQLSERVER)，再选择“停止”或“重新启动”。    
  
- 如果正在运行多个实例或报表服务器正在作为命名实例运行，请验证圆括号中的实例名称是否对应于你希望停止或重新启动的报表服务器实例。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器配置管理器（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [启动、停止或暂停 SQL Server 代理服务](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
