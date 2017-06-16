---
title: "访问 SOAP API |Microsoft 文档"
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
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f05225e97ef14f06444562d0f5c45291d2e6c030
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="accessing-the-soap-api"></a>访问 SOAP API
  报表服务器 Web 服务使用通过 HTTP 的简单对象访问协议 (SOAP)，并充当客户端程序和报表服务器之间的通信接口。 该 Web 服务提供两个端点（一个用于报表执行，一个用于报表管理），并且由您可用于访问 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的完整功能的方法和一组复杂类型对象构成。 若要调用该服务，必须引用 Reporting Services Web 服务描述语言 (WSDL)。  
  
## <a name="referencing-the-reporting-services-wsdl"></a>引用 Reporting Services WSDL  
 若要成功调用某一 Web 服务，您必须知道如何访问该服务、该服务支持的操作、该服务预期的参数以及该服务返回的内容。 WSDL 在可由计算机读取或处理的 XML 文档中提供这些信息。  
  
 该报表服务器 Web 服务在三个不同的端点中公开。 该 WSDL 文件的名称对于每个端点并不相同。 <xref:ReportService2010> 端点包含一些方法，用于管理本机模式或 SharePoint 集成模式下报表服务器中的对象。 用于此端点的 WSDL 通过 `ReportService2010.asmx?wsdl.` 访问。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中不推荐使用 <xref:ReportService2005> 和 <xref:ReportService2006> 端点。 <xref:ReportService2010> 端点包含两个端点的功能和其他管理功能。  
  
-   <xref:ReportExecution2005> 端点允许开发人员以编程方式在报表服务器中处理和呈现报表。 通过访问此终结点的 WSDL `ReportExecution2005.asmx?wsdl`。  
  
 WSDL 可供开发工具包支持 SOAP 和 Web 服务，如[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
 以下示例显示指向 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理 WSDL 文件的 URL 的格式：  
  
```  
http://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 下表介绍 URL 中的各元素。  
  
|URL 元素|Description|  
|-----------------|-----------------|  
|*服务器*|报表服务器部署到的服务器的名称。|  
|*reportserver*|包含 XML Web 服务的文件夹的名称。 此名称在设置期间配置。|  
|*\<终结点名称 >.asmx*|Web 服务端点的名称。|  
  
 有关 WSDL 格式的详细信息，请参阅万维网联合会 (W3C) WSDL 规范，网址为 http://www.w3.org/TR/wsdl。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
