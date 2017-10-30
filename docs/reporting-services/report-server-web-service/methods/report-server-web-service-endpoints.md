---
title: "报表服务器 Web 服务终结点 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
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
- management endpoints [Reporting Services]
- Web service [Reporting Services], endpoints
- endpoints [Reporting Services]
- execution endpoints [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: f3f5d85f-9359-4508-bc5a-7f78a3cf7421
caps.latest.revision: 26
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2a0c98cd0c45fc7121a93a51e623dcd2bf36d8bf
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="report-server-web-service-endpoints"></a>报表服务器 Web 服务端点
  报表服务器 Web 服务提供了几个端点，用于管理报表服务器以及执行和导航报表。  
  
## <a name="the-management-endpoints"></a>管理端点  
 有三个端点可用于管理报表服务器上的对象，即：<xref:ReportService2005>、<xref:ReportService2006> 和 <xref:ReportService2010>。 <xref:ReportService2005> 端点用于管理配置为本机模式的报表服务器上的对象。 <xref:ReportService2006> 端点用于管理配置为 SharePoint 集成模式的报表服务器上的对象。 <xref:ReportService2010> 端点合并了 <xref:ReportService2005> 和 <xref:ReportService2006> 的功能，可以管理为本机或 SharePoint 集成模式配置的报表服务器上的对象。  
  
> [!IMPORTANT]  
>  当报表服务器配置为 SharePoint 集成模式， <xref:ReportService2005> Api 将返回**rsOperationNotSupportedSharePointMode**错误。 如果报表服务器配置为纯模式， <xref:ReportService2006> Api 将返回**rsOperationNotSupportedNativeMode**错误。 同样，在非预期模式中使用 <xref:ReportService2010> 中的模式特定 API 时，API 将返回相应的错误。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 中不推荐使用 <xref:ReportService2005> 和 <xref:ReportService2006> 端点。 <xref:ReportService2010> 端点包含两个端点的功能和其他管理功能。  
  
 如果将报表服务器配置为本机模式或 SharePoint 集成模式，则可以使用以下 URL 之一访问管理端点的 WSDL：  
  
```  
http://<Server Name>/ReportServer/ReportService2010.asmx?wsdl  
```  
  
 有关详细信息，请参阅[访问 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="the-execution-endpoint"></a>执行端点  
 通过 <xref:ReportExecution2005> 端点，开发人员可以轻松地从处于本机模式和 SharePoint 集成模式下的报表服务器自定义报表处理和呈现。 此端点包含报表服务器 Web 服务的先前版本中提供的类和方法。 此外，还向报表服务器 Web 服务添加了许多通过执行端点公开的新类和新方法。  
  
 可以使用以下 URL 访问管理端点的 WSDL：  
  
```  
http://<Server Name>/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 如果将报表服务器配置为 SharePoint 集成模式，则可以使用以下 URL 访问 WSDL：  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx?wsdl  
```  
  
 有关详细信息，请参阅[访问 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="sharepoint-proxy-endpoints"></a>SharePoint 代理端点  
 当报表服务器配置为 SharePoint 集成模式且已安装 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 外接程序时，将在 SharePoint 服务器上安装一组代理端点。 当将报表服务器配置为 SharePoint 集成模式时，代理端点是用于开发报表解决方案的主要 API。 当针对代理端点进行开发时，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 外接程序在可信帐户身份验证模式下管理 SharePoint 服务器与报表服务器之间的凭据交换。 当针对报表服务器端点进行开发时，调用应用程序必须在可信帐户身份验证模式下管理凭据交换。 下表列出随 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 外接程序安装的端点。  
  
|代理端点|Description|  
|--------------------|-----------------|  
|<xref:ReportService2006>|为管理配置为 SharePoint 集成模式的报表服务器提供 API。<br /><br /> 注意： 此终结点中已弃用[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。|  
|<xref:ReportService2010>|为管理配置为本机模式或 SharePoint 集成模式的报表服务器提供 API。|  
|<xref:ReportExecution2005>|提供用于运行和导航报表的 API。|  
|<xref:ReportServiceAuthentication>|提供用于 SharePoint Web 应用程序配置用于表单身份验证时，对报表服务器的用户进行身份验证 Api。|  
  
 以下是引用 SharePoint 站点上代理端点的示例 URL。  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportService2010.asmx  
```  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportExecution2005.asmx  
```  
  
```  
http://<Server Name>/<Site Name>/_vti_bin/ReportServer/ReportServiceAuthentication.asmx  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  

