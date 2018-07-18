---
title: 实现安全扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], extensions
- forms-based authentication [Reporting Services]
- custom authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: d2327e7c-0d48-49e3-bcd9-3bba4e67a68b
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8b6a81d2171a013af5b02684ca0e4e1f2372ac5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33015574"
---
# <a name="implementing-a-security-extension"></a>实现安全扩展插件
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 身份验证是用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中保护报表安全性的主要系统。 然而，在某些情况下，您可能需要扩展 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全系统以适应企业中的自定义安全性。 为此，可以使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] API 提供的开发平台。 本节概述 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的安全扩展插件。  
  
 有关实现、部署和删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全扩展插件的完整详细信息，请参阅 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="in-this-section"></a>本节内容  
 [安全扩展插件概述](../../../reporting-services/extensions/security-extension/security-extensions-overview.md)  
 提供有关 Reporting Services 安全扩展插件的概述。  
  
 [Reporting Services 中的身份验证](../../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)  
 讨论 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的身份验证。  
  
 [Reporting Services 中的授权](../../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)  
 介绍 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的授权。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
