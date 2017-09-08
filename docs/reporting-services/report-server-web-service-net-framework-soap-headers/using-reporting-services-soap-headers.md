---
title: "使用 Reporting Services SOAP 标头 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 08aec184077b69d05939fe493bf677043beb99d3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="using-reporting-services-soap-headers"></a>使用 Reporting Services SOAP 标头
  使用 SOAP 与 Web 服务方法的通信遵循标准的格式。 此格式中的部分内容为在 XML 文档中编码的数据。 XML 文档包含的根**信封**元素，这反过来又包括的所需**正文**元素和可选**标头**元素。 **正文**元素包含特定于消息数据。 可选**标头**元素可以包含与特定的消息不直接相关的其他信息。 每个子元素**标头**元素称为 SOAP 标头。  
  
 尽管 SOAP 标头可以包含与相应消息相关的数据，但是一般而言， SOAP 标头包含的是 Web 服务器基础结构所处理的信息。  
  
 报表服务器 Web 服务定义几个可在 SOAP 标头中使用的类：<xref:ReportService2005.BatchHeader>、<xref:ReportService2010.ItemNamespaceHeader>、<xref:ReportService2010.ServerInfoHeader>、<xref:ReportService2010.TrustedUserHeader> 和 <xref:ReportExecution2005.ExecutionHeader>。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[批处理方法](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|介绍如何使用 <xref:ReportService2005.BatchHeader> 将多个操作纳入一个事务中进行批处理。|  
|[标识执行状态](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|描述如何管理中的会话状态[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]使用**SessionHeader**。|  
|[设置项 Namespace GetProperties 方法](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|介绍如何通过使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法和 <xref:ReportService2010.ItemNamespaceHeader> SOAP 标头来根据项的路径或 ID 检索属性。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和.NET Framework 构建应用程序](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技术参考 &#40;SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
