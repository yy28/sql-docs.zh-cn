---
title: “Reporting Services 登录”对话框 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: e4a3feeca737e1d4db6627af5ece9fa9d36c6b7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123828"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>“Reporting Services 登录”对话框 (SSRS)
  使用 **“Reporting Services 登录”** 对话框可以提供向报表服务器发布报表时要使用的凭据。  
  
-   **请注意**如果这是已自集报表发布到报表服务器的第一个时间设置的部署属性**TargetServerURL**对于一个项目，请验证你指定的服务器名称是否类似于`http://localhost/reportserver`，而不`http://localhost/reports`。 在本地服务器上指定 `reports` 目录而不是 `reportserver` 目录将间接打开此对话框。 有关设置 TargetServerURL 的详细信息，请参阅[设置部署属性 (Reporting Services)](set-deployment-properties-reporting-services.md)。  
  
## <a name="options"></a>“常规”  
 **Server**  
 显示报表服务器的名称。 例如， `http://localhost/reportserver`。 如果报表服务器使用的不是默认端口 80，则需要包含端口号。 例如， `http://localhost:81/reportserver`。  
  
 **用户名**  
 键入登录 Web 服务时要使用的用户名。  
  
 **密码**  
 键入登录 Web 服务时要使用的密码。  
  
## <a name="see-also"></a>请参阅  
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [指定凭据和报表数据源的连接信息](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)[报表设计器的 F1 帮助](report-designer-f1-help.md)  
  
  