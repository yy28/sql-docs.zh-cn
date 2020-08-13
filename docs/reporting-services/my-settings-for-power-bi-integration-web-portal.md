---
title: Power BI 集成的“我的设置”（Web 门户）| Microsoft Docs
description: 了解 Reporting Services Web 门户中的“我的设置”页面，以及各个用户如何使用它管理其对 Power BI 的登录。
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f25ab8f848c642de95f1ba62eaca15bbb8b7e7d9
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248572"
---
# <a name="my-settings-for-power-bi-integration-web-portal"></a>我的 Power BI 集成（Web 门户）设置

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

单个用户使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 中的“我的设置”页面来管理其 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 登录。 当执行步骤以将报表项固定时，将自动提示你登录。  但是，如果需要手动登录或者需要注销，可以使用“我的设置”页。如果“我的设置”菜单选项不可见，则报表服务器未与 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 集成。  有关详细信息，请参阅 [Power BI 报表服务器集成 (Configuration Manager)](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)相集成。  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>为什么登录

 当登录时，你可以在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 用户帐户和 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 帐户之间建立关系。  登录创建有效期为 90 天的安全令牌。 如果令牌过期，并且你具有固定到 Power BI 的项，将看到一条通知。  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
通过“我的设置”页再次登录后，[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 仪表板中的磁贴才会刷新。  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
登录后，将会立即创建一个新的安全令牌。  仪表板磁贴将开始更新它们以前配置的计划。  

## <a name="next-steps"></a>后续步骤

[Power BI 报表服务器集成](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[将 Reporting Services 项目固定到 Power BI 仪表板](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Power BI 中的仪表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Web 门户](../reporting-services/web-portal-ssrs-native-mode.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
