---
title: 使用 SOAP 集成 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b6fffd65b22900d7c505c4b50ec290b95fe9ab4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126171"
---
# <a name="integrating-reporting-services-using-soap"></a>使用 SOAP 集成 Reporting Services
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API 提供了多个 Web 服务端点，用于开发自定义报表解决方案。 这些端点目前分为两个类别：管理和执行。 管理功能通过 <xref:ReportService2005>、<xref:ReportService2006> 和 <xref:ReportService2010> 端点公开。 <xref:ReportService2005> 端点用于管理配置为本机模式的报表服务器，而 <xref:ReportService2006> 端点用于管理配置为 SharePoint 集成模式的报表服务器。 <xref:ReportService2010> 合并了 <xref:ReportService2005> 和 <xref:ReportService2006> 的功能，可以管理配置为本机模式或 SharePoint 集成模式的报表服务器。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中不推荐使用 <xref:ReportService2005> 和 <xref:ReportService2006> 端点。 <xref:ReportService2010> 端点包含两个端点的功能和其他管理功能。  
  
 执行功能通过 <xref:ReportExecution2005> 端点公开，当将报表服务器配置为本机模式或 SharePoint 集成模式时使用它。 以下主题说明如何使用这些端点在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows、SharePoint 和 Web 应用程序中开发报表解决方案。  
  
## <a name="in-this-section"></a>本节内容  
 [在 Windows 应用程序中使用 SOAP API](integrating-reporting-services-using-soap-windows-application.md)  
 介绍如何使用 SOAP API 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到 Windows 环境中。  
  
 [在 Web 应用程序中使用 SOAP API](integrating-reporting-services-using-soap-web-application.md)  
 介绍如何使用 SOAP API 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到 Web 环境中。  
  
## <a name="see-also"></a>请参阅  
 [将 Reporting Services 集成到应用程序中](../application-integration/integrating-reporting-services-into-applications.md)   
 [报表服务器 Web 服务](../report-server-web-service/report-server-web-service.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
