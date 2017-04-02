---
title: "我的 Power BI 集成（Web 门户）设置 | Microsoft Docs"
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "pbi"
  - "power bi"
  - "power bi integration"
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# 我的 Power BI 集成（Web 门户）设置
  单个用户使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 中的“我的设置”页来管理其 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 登录。 当执行步骤以将报表项固定时，将自动提示你登录。  但是，如果需要进行手动登录或者需要注销，可以使用“我的设置”页。  如果“我的设置”  菜单选项不可见，则报表服务器未与  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]集成。  有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## 为什么登录  
 当登录时，你可以在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 用户帐户和 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 帐户之间建立关系。  登录创建有效期为 90 天的安全令牌。 如果令牌过期，并且你具有固定到 Power BI 的项，将看到一条通知。  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
通过“我的设置”页再次登录后，[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板中的磁贴才会刷新。  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
登录后，将会立即创建一个新的安全令牌。  仪表板磁贴将开始更新它们以前配置的计划。  
  
## 另请参阅  
 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [将 Reporting Services 项目固定到 Power BI 仪表板](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
 [Power BI 中的仪表板](https://support.powerbi.com/knowledgebase/articles/424868-dashboards-in-power-bi)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
