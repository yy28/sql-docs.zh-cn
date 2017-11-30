---
title: "报表服务器 Windows 服务 (MSSQLServer) 107 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4f7fc2af769ef83db3736b4cd82fb645b751de1c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="report-server-windows-service-mssqlserver-107"></a>报表服务器 Windows 服务 (MSSQLServer) 107
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|107|  
|事件源|报表服务器 Windows 服务|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|报表服务器 Windows 服务 (MSSQLSERVER) 无法与报表服务器数据库建立连接。|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 报表服务器服务无法连接到报表服务器数据库。 如果无法建立与报表服务器数据库的连接，在服务重新启动过程中就会出现该错误。 在下列情况下会出现此错误：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务未运行。  
  
-   由于远程连接或 TCP/IP 协议未启用，无法连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务。  
  
-   报表服务器数据库配置不正确。  
  
-   服务帐户配置不正确，或该帐户不再有权访问报表服务器数据库。 如果不使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具来设置该帐户或报表服务器数据库，就可能出现这种情况。  
  
## <a name="user-action"></a>用户操作  
 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务未运行，请启动此服务，并检查是否针对 TCP/IP 协议启用了远程连接。  
  
 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具配置报表服务器数据库和服务帐户。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>另请参阅  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager（本机模式）](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
