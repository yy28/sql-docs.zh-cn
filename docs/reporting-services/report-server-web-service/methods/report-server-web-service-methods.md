---
title: "报表服务器 Web 服务方法 |Microsoft 文档"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: f99a0c09bfbe96062b078c07f86295b34069d9cf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="report-server-web-service-methods"></a>报表服务器 Web 服务方法
  根据不同的组件功能，报表服务器 Web 服务方法包含不同的类别。 这些方法通过作为 <xref:ReportService2010.ReportingService2010> 和 <xref:ReportExecution2005.ReportExecutionService> 类的成员公开的若干 Web 服务端点（三个用于报表管理，一个用于报表执行）提供。 可以通过 wsdl.exe，它又包括在之类的代理类工具生成这些类[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK。 有关报表服务器 Web 服务的详细信息和[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]，请参阅[生成应用程序使用 Web 服务和.NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
## <a name="endpoints-and-methods"></a>端点和方法  
 下表列出了报表服务器 Web 服务的端点以及 <xref:ReportService2010.ReportingService2010> 端点提供的方法的类别。 其他终结点中可用的方法上的信息，请参阅[技术参考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md).  
  
|主题|Description|  
|-----------|-----------------|  
|[报表服务器 Web 服务终结点](../../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)|介绍如何管理和执行报表服务器 Web 服务的端点。|  
|[报表服务器命名空间管理方法](../../../reporting-services/report-server-web-service/methods/report-server-namespace-management-methods.md)|介绍可用来管理报表服务器数据库的方法。 特别值得一提的是，您可以管理文件夹和资源，并设置项属性。|  
|[授权方法](../../../reporting-services/report-server-web-service/methods/authorization-methods.md)|介绍可用来管理任务、角色和策略的方法。|  
|[数据源和连接方法](../../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)|介绍可用来设置和管理报表的数据源连接和凭据信息的方法。|  
|[报表参数方法](../../../reporting-services/report-server-web-service/methods/report-parameters-methods.md)|介绍可用来设置和检索报表的参数的方法。|  
|[模型方法 - 报表服务器 Web 服务](../../../reporting-services/report-server-web-service/methods/model-methods-report-server-web-service.md)|介绍可用来管理模型的方法。|  
|[呈现和执行方法](../../../reporting-services/report-server-web-service/methods/rendering-and-execution-methods.md)|介绍可用来管理报表执行、呈现和缓存的方法。|  
|[报表历史记录方法](../../../reporting-services/report-server-web-service/methods/report-history-methods.md)|介绍可用来创建和管理报表历史记录快照的方法。|  
|[计划方法](../../../reporting-services/report-server-web-service/methods/scheduling-methods.md)|介绍可用来创建和管理报表服务器采用的共享计划和缓存刷新计划的方法。|  
|[订阅和传递方法](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|介绍可用来创建和管理订阅和报表传递的方法。|  
|[链接报表方法](../../../reporting-services/report-server-web-service/methods/linked-reports-methods.md)|介绍可用来创建和管理链接报表的方法。|  
  
## <a name="see-also"></a>另请参阅  
 [访问 SOAP API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [使用 Web 服务和.NET Framework 构建应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技术参考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

