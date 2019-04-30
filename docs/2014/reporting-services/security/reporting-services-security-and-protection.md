---
title: Reporting Services 安全性和保护 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca88c252e37362f2a5b64bb8d41ebac27f0e24dd
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63461237"
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 安全性和保护
  你可使用本节中的信息来了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的安全功能。 本节还将说明 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中支持的授权模型和身份验证提供程序。  
  
## <a name="extended-protection-for-authentication"></a>身份验证的扩展保护  
 自 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]开始，提供了对针对验证的扩展保护的支持。 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能支持使用渠道绑定和服务绑定来加强对身份验证的保护。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能需要用于支持扩展保护的操作系统。 有关详细信息，请参阅 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)。  
  
## <a name="authentication-and-authorization"></a>身份验证和授权  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供不同的身份验证类型以便用户和客户端应用程序对报表服务器进行身份验证。 通过为您的报表服务器使用正确的身份验证类型，您的组织可以实现所需的适当安全级别。 有关详细信息，请参阅 [Authentication with the Report Server](authentication-with-the-report-server.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 还采用角色和权限来控制用户对报表服务器目录中的内容的访问（换言之，可以控制访问的人员、访问的内容以及访问的方式）。 有关详细信息，请参阅[角色和权限 (Reporting Services)](roles-and-permissions-reporting-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|链接|  
|-----------------------|-----------|  
|配置安全套接字层 (SSL) 以便确保与报表服务器的客户端连接的安全。|[配置本机模式报表服务器上的 SSL 连接](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
