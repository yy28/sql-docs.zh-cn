---
title: "Reporting Services 安全和保护 |Microsoft 文档"
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
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 217bd93631e96dae0b75532d73c14ade4355be6d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 安全性和保护
  可以使用此部分中的信息以了解有关的安全功能的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 本节还将说明 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中支持的授权模型和身份验证提供程序。  
  
## <a name="extended-protection-for-authentication"></a>身份验证的扩展保护  
 自 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]开始，提供了对针对验证的扩展保护的支持。 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能支持使用渠道绑定和服务绑定来加强对身份验证的保护。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能需要用于支持扩展保护的操作系统。 有关详细信息，请参阅 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。  
  
## <a name="authentication-and-authorization"></a>身份验证和授权  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供有关用户和客户端应用程序，报表服务器进行身份验证的不同的身份验证类型。 通过为您的报表服务器使用正确的身份验证类型，您的组织可以实现所需的适当安全级别。 有关详细信息，请参阅 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]此外使用了角色和权限以控制用户访问报表服务器目录 （换而言之，谁可以访问内容，以及如何他/她可以访问它） 中的内容。 有关详细信息，请参阅[角色和权限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
|任务说明|链接|  
|-----------------------|-----------|  
|配置安全套接字层 (SSL) 以便确保与报表服务器的客户端连接的安全。|[在本机模式报表服务器上配置 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  

