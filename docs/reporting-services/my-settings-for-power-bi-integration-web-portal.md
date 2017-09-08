---
title: "我的设置以便 Power BI 集成 （web 门户） |Microsoft 文档"
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 8e627f20918a4d6ee5f882677ccc7b2c26616e2f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/17/2017

---

# <a name="my-settings-for-power-bi-integration-web-portal"></a>我的 Power BI 集成（Web 门户）设置

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

单个用户使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 中的“我的设置”页来管理其 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 登录。 当执行步骤以将报表项固定时，将自动提示你登录。  但是，你可以使用**我的设置**页上，如果需要进行手动登录或者需要注销。  如果**我的设置**菜单选项不可见，请不与集成报表服务器[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。  有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>为什么登录

 当登录时，你可以在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 用户帐户和 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 帐户之间建立关系。  登录创建有效期为 90 天的安全令牌。 如果令牌过期，并且你具有固定到 Power BI 的项，将看到一条通知。  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
在磁贴[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]直到通过再次登录，将不会刷新仪表板**MySettings**。  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
登录后，将会立即创建一个新的安全令牌。  仪表板磁贴将开始更新它们以前配置的计划。  

## <a name="next-steps"></a>后续步骤

[Power BI 报表服务器集成](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[将 Reporting Services 项目固定到 Power BI 仪表板](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Power BI 中的仪表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Web 门户](../reporting-services/web-portal-ssrs-native-mode.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
