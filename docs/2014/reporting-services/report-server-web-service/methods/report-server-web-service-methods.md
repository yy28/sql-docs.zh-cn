---
title: 报表服务器 Web 服务方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: df2849f2aabfd7d69645d5fd82dbec8195df27b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059037"
---
# <a name="report-server-web-service-methods"></a>报表服务器 Web 服务方法
  根据不同的组件功能，报表服务器 Web 服务方法包含不同的类别。 这些方法通过作为 <xref:ReportService2010.ReportingService2010> 和 <xref:ReportExecution2005.ReportExecutionService> 类的成员公开的若干 Web 服务端点（三个用于报表管理，一个用于报表执行）提供。 这些类可使用代理类工具（如 wsdl.exe）生成，[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 中包含此工具。 有关使用报表服务器 Web 服务和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的详细信息，请参阅[使用 Web 服务和 .NET Framework 生成应用程序](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
## <a name="endpoints-and-methods"></a>端点和方法  
 下表列出了报表服务器 Web 服务的端点以及 <xref:ReportService2010.ReportingService2010> 端点提供的方法的类别。 有关其他终结点中可用方法的信息，请参阅[技术参考 (SSRS)](../../technical-reference-ssrs.md)。  
  
|主题|Description|  
|-----------|-----------------|  
|[报表服务器 Web 服务终结点](report-server-web-service-endpoints.md)|介绍如何管理和执行报表服务器 Web 服务的端点。|  
|[报表服务器命名空间管理方法](report-server-namespace-management-methods.md)|介绍可用来管理报表服务器数据库的方法。 特别值得一提的是，您可以管理文件夹和资源，并设置项属性。|  
|[授权方法](authorization-methods.md)|介绍可用来管理任务、角色和策略的方法。|  
|[数据源和连接方法](data-sources-and-connection-methods.md)|介绍可用来设置和管理报表的数据源连接和凭据信息的方法。|  
|[报表参数方法](report-parameters-methods.md)|介绍可用来设置和检索报表的参数的方法。|  
|[模型方法](../report-server-web-service.md)|介绍可用来管理模型的方法。|  
|[呈现和执行方法](rendering-and-execution-methods.md)|介绍可用来管理报表执行、呈现和缓存的方法。|  
|[报表历史记录方法](report-history-methods.md)|介绍可用来创建和管理报表历史记录快照的方法。|  
|[计划方法](scheduling-methods.md)|介绍可用来创建和管理报表服务器采用的共享计划和缓存刷新计划的方法。|  
|[订阅和传递方法](subscription-and-delivery-methods.md)|介绍可用来创建和管理订阅和报表传递的方法。|  
|[链接报表方法](linked-reports-methods.md)|介绍可用来创建和管理链接报表的方法。|  
  
## <a name="see-also"></a>请参阅  
 [访问 SOAP API](../accessing-the-soap-api.md)   
 [使用 Web 服务和 .NET Framework 生成应用程序](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
