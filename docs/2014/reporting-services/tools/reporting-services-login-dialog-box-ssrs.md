---
title: “Reporting Services 登录”对话框 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 232ee51614a668b07263c3e3a4182f23652135bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099871"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>“Reporting Services 登录”对话框 (SSRS)
  使用 **“Reporting Services 登录”** 对话框可以提供向报表服务器发布报表时要使用的凭据。  
  
-   **注意**如果这是你首次将报表发布到 Report Server，因为设置了为项目设置**TargetServerURL**部署属性，请验证你指定的服务器名称是否类似于`http://localhost/reportserver`，而不`http://localhost/reports`是。 在本地服务器上指定 `reports` 目录而不是 `reportserver` 目录将间接打开此对话框。 有关设置 TargetServerURL 的详细信息，请参阅[设置部署属性 (Reporting Services)](set-deployment-properties-reporting-services.md)****。  
  
## <a name="options"></a>选项  
 **服务器**  
 显示报表服务器的名称。 例如，`http://localhost/reportserver` 。 如果报表服务器使用的不是默认端口 80，则需要包含端口号。 例如，`http://localhost:81/reportserver` 。  
  
 **用户名**  
 键入登录 Web 服务时要使用的用户名。  
  
 **密码**  
 键入登录 Web 服务时要使用的密码。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [为报表数据源指定凭据和连接信息](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)[报表设计器 F1 帮助](report-designer-f1-help.md)  
  
  
