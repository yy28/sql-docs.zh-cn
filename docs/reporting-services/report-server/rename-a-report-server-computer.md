---
title: "重命名报表服务器计算机 |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 349180bb3cfe2b03bee076dfc2dbb90265118fa4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="rename-a-report-server-computer"></a>重命名报表服务器计算机
  重命名计算机将导致相应地更改 Web 服务器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称（如果是在同一台计算机上）。 在某些情况下，在计算机名称发生更改之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可能无法访问。 请使用本主题中提供的步骤在计算机名称更改之后重新配置报表服务器。  
  
## <a name="renaming-a-sql-server-database-engine"></a>重命名 SQL Server 数据库引擎  
 如果要重命名运行报表服务器数据库的  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例，请执行下列操作：  
  
1.  启动 Reporting Services 配置工具，并连接到使用重命名的服务器中的报表服务器数据库的报表服务器。  
  
2.  打开“数据库安装”页。  
  
3.  在 **“服务器名称”**中，键入或选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名称，再单击 **“连接”**。  
  
4.  单击 **“应用”**。  
  
 如果报表服务器使用的是本地 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，则可以使用 *(local)* 或 *(local)\instancename* 来指定服务器。 如果使用 *(local)* 表示服务器，则可以重命名服务器，同时连接将继续工作。 如果使用的是远程服务器，或使用服务器名称配置了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则每次更改服务器名称时都必须更新数据库连接信息。  
  
## <a name="renaming-a-report-server-computer"></a>重命名报表服务器计算机  
 如果要重命名运行报表服务器的计算机，请执行下列操作：  
  
1.  在文本编辑器中打开 RSReportServer.config，并修改 **UrlRoot** 设置以反映新的服务器名称。 传递扩展插件使用 **UrlRoot** 设置来编写在访问存储于报表服务器中的项时所使用的 URL。 更改报表服务器 URL 地址时需要更新 **UrlRoot** 设置，以便订阅可以继续按预期方式传递报表。  
  
2.  在同一个文件中，修改 **ReportServerUrl** 设置（如果对其进行了配置），使其反映新服务器名称。 注意，并非每次安装时都会使用此设置。 如果此设置为空，则无需执行任何操作。  
  
    > [!NOTE]  
    >  如果在企业网络中使用的是 Windows Internet 名称服务 (WINS)，则在一段时间内仍可以通过以前的名称使用报表服务器和报表管理器。 WINS 向它所服务的每一台计算机映射一个 IP 地址。 WINS 为重命名的计算机刷新 IP 地址之后，将无法再使用旧的计算机名称访问报表服务器或报表管理器。  
  
## <a name="see-also"></a>另请参阅  
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 配置管理器 &#40;本机模式 &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 报表服务器 &#40;本机模式 &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [rsconfig 实用工具 &#40;SSRS &#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  
  
