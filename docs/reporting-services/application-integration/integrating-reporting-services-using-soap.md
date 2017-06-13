---
title: "将集成 Reporting Services 使用 SOAP |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
caps.latest.revision: 45
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 00c18a33dc186c5724c6812451153539571cd96c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="integrating-reporting-services-using-soap"></a>使用 SOAP 集成 Reporting Services
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API 提供用于开发自定义报表解决方案的多个 Web 服务终结点。 这些端点目前分为两个类别：管理和执行。 管理功能通过 <xref:ReportService2005>、<xref:ReportService2006> 和 <xref:ReportService2010> 端点公开。 <xref:ReportService2005> 端点用于管理配置为本机模式的报表服务器，而 <xref:ReportService2006> 端点用于管理配置为 SharePoint 集成模式的报表服务器。 <xref:ReportService2010> 合并了 <xref:ReportService2005> 和 <xref:ReportService2006> 的功能，可以管理配置为本机模式或 SharePoint 集成模式的报表服务器。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中不推荐使用 <xref:ReportService2005> 和 <xref:ReportService2006> 端点。 <xref:ReportService2010> 端点包含两个端点的功能和其他管理功能。  
  
 执行功能通过 <xref:ReportExecution2005> 端点公开，当将报表服务器配置为本机模式或 SharePoint 集成模式时使用它。 以下主题说明如何使用这些端点在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows、SharePoint 和 Web 应用程序中开发报表解决方案。  
  
## <a name="in-this-section"></a>本节内容  
 [在 Windows 应用程序中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
 介绍如何使用 SOAP API 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到 Windows 环境中。  
  
 [在 Web 应用程序中使用 SOAP API](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
 介绍如何使用 SOAP API 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到 Web 环境中。  
  
## <a name="see-also"></a>另请参阅  
 [将 Reporting Services 集成到应用程序](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
