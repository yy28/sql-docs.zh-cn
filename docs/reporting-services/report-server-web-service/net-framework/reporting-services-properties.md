---
title: Reporting Services 属性 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 36a105d3220755dd03ff05a50dd403d4bac25d3a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "62703831"
---
# <a name="reporting-services-properties"></a>Reporting Services 属性
  报表服务器定义对于报表服务器而言为全局的一组系统属性，并定义与报表服务器数据库中存储的单独项关联的一组项属性。 不能删除由报表服务器定义的属性，在某些情况下，它们是只读的。 应用程序可以通过将其他用户定义属性添加到系统以及添加项属性来扩展系统属性和项属性。  
  
 以下 Web 服务方法检索并设置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 属性。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|对于报表服务器数据库中的项返回一个或多个属性的值。|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|返回一个或多个系统属性。|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|为报表服务器数据库中的项设置一个或多个属性。|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|设置一个或多个系统属性。|  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[报表服务器项属性](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-item-properties.md)|介绍 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中特定于项的属性。|  
|[报表服务器系统属性](../../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)|介绍 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中特定于系统的属性。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
