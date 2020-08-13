---
title: “Reporting Services 登录”对话框 | Microsoft Docs
description: 了解如何使用“Reporting Services 登录”对话框提供向报表服务器发布报表时要使用的凭据。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4d3e34d7ff9f92506f1225aea173521ee7d30e79
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919613"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>“Reporting Services 登录”对话框 (SSRS)
  使用 **“Reporting Services 登录”** 对话框可以提供向报表服务器发布报表时要使用的凭据。  
  
-   **注意** ：如果这是你为项目设置 **TargetServerURL** 部署属性以后首次向报表服务器发布报表，请确保你指定的服务器名类似于 **server** ，而不是 **reports**。 例如， `https://localhost/reportserver`，而不是 `https://localhost/reports`。 在本地服务器上指定 `reports` 目录而不是 `reportserver` 目录将间接打开此对话框。 有关设置 TargetServerURL 的详细信息，请参阅[设置部署属性 (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
## <a name="options"></a>选项  
 **Server**  
 显示报表服务器的名称。 例如，`https://localhost/reportserver`。 如果报表服务器使用的不是默认端口 80，则需要包含端口号。 例如，`https://localhost:81/reportserver`。  
  
 **用户名**  
 键入登录 Web 服务时要使用的用户名。  
  
 **密码**  
 键入登录 Web 服务时要使用的密码。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据连接字符串 - 报表生成器和 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [报表设计器的 F1 帮助](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
