---
title: "Reporting Services 安全性和保护 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
caps.latest.revision: "21"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 827bc656d6bdd4dc5b955a83c01cb8e072db3772
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 安全性和保护
  你可使用本节中的信息来了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的安全功能。 本节还将说明 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中支持的授权模型和身份验证提供程序。  
  
## <a name="extended-protection-for-authentication"></a>身份验证的扩展保护  
 自 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]开始，提供了对针对验证的扩展保护的支持。 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能支持使用渠道绑定和服务绑定来加强对身份验证的保护。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能需要用于支持扩展保护的操作系统。 有关详细信息，请参阅 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。  
  
## <a name="authentication-and-authorization"></a>身份验证和授权  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供不同的身份验证类型以便用户和客户端应用程序对报表服务器进行身份验证。 通过为您的报表服务器使用正确的身份验证类型，您的组织可以实现所需的适当安全级别。 有关详细信息，请参阅 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 还采用角色和权限来控制用户对报表服务器目录中的内容的访问（换言之，可以控制访问的人员、访问的内容以及访问的方式）。 有关详细信息，请参阅[角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
|任务说明|链接|  
|-----------------------|-----------|  
|配置安全套接字层 (SSL) 以便确保与报表服务器的客户端连接的安全。|[配置本机模式报表服务器上的 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
