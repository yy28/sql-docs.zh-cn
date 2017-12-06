---
title: "数据源和连接方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- data sources [Reporting Services], methods
ms.assetid: 50999b52-fc7c-4333-9fb0-d04c37a4c90f
caps.latest.revision: "38"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2e8039303a6d21a3979a76d1a37aa0e041ba8eaa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="data-sources-and-connection-methods"></a>数据源和连接方法
  可以使用以下方法设置和管理数据源连接和凭据。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateDataSource%2A>|在报表服务器数据库或 SharePoint 库中创建新数据源。|  
|<xref:ReportService2010.ReportingService2010.DisableDataSource%2A>|禁用已启用的数据源。|  
|<xref:ReportService2010.ReportingService2010.EnableDataSource%2A>|启用已禁用的数据源。|  
|<xref:ReportService2010.ReportingService2010.GetDataSourceContents%2A>|返回数据源的内容。|  
|<xref:ReportService2010.ReportingService2010.GetItemDataSourcePrompts%2A>|获取指定项的数据源提示。|  
|<xref:ReportService2010.ReportingService2010.GetItemDataSources%2A>|返回目录中项的数据源。|  
|<xref:ReportService2010.ReportingService2010.ListDependentItems%2A>|返回引用指定目录项的目录项列表。|  
|<xref:ReportService2010.ReportingService2010.ListSubscriptionsUsingDataSource%2A>|返回与给定数据源关联的订阅列表。|  
|<xref:ReportService2010.ReportingService2010.SetDataSourceContents%2A>|设置与数据源关联的连接属性。|  
|<xref:ReportService2010.ReportingService2010.SetItemDataSources%2A>|为报表服务器数据库或 SharePoint 库中的项设置数据源。|  
|<xref:ReportService2010.ReportingService2010.TestConnectForDataSourceDefinition%2A>|测试数据源的连接。 此方法支持数据源的直接测试。|  
|<xref:ReportService2010.ReportingService2010.TestConnectForItemDataSource%2A>|测试数据源的连接。 此方法支持已发布的数据源的测试，这些数据源由报表或模型和共享数据源使用。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [报表服务器 Web 服务方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
