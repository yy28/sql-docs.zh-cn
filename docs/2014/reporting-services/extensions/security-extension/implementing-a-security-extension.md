---
title: 实现安全扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
- forms-based authentication [Reporting Services]
- custom authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: d2327e7c-0d48-49e3-bcd9-3bba4e67a68b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e5cf1fa6ce0e0a02a52e6a27f693c152d1f97152
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211539"
---
# <a name="implementing-a-security-extension"></a>实现安全扩展插件
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 身份验证是用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中保护报表安全性的主要系统。 然而，在某些情况下，您可能需要扩展 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全系统以适应企业中的自定义安全性。 为此，可以使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] API 提供的开发平台。 本节概述 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的安全扩展插件。  
  
 有关实现、部署和删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全扩展插件的完整详细信息，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。  
  
## <a name="in-this-section"></a>本节内容  
 [安全扩展插件概述](security-extensions-overview.md)  
 提供有关 Reporting Services 安全扩展插件的概述。  
  
 [Reporting Services 中的身份验证](authentication-in-reporting-services.md)  
 讨论 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的身份验证。  
  
 [Reporting Services 中的授权](authorization-in-reporting-services.md)  
 介绍 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的授权。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
