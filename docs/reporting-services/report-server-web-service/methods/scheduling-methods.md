---
title: 计划方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 20695ab30ea26c72b607fd217fc7fcaefab270fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="scheduling-methods"></a>计划方法
  可以使用这些方法来创建和管理用于报表执行和传递的共享计划，还可以使用这些方法来缓存报表服务器使用的刷新计划。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|创建项的缓存刷新计划。|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|创建新的共享计划。|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|删除缓存刷新计划。|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|基于特定的计划 ID 删除共享计划。|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|返回指定的缓存刷新计划的属性。|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|返回共享计划的属性值。|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|返回与目录项关联的缓存刷新计划的列表。|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|返回与共享计划关联的项的列表。|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|返回报表服务器或 SharePoint 网站上的所有共享计划列表。|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|返回支持的计划状态的列表。|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|暂停给定计划的执行。|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|恢复已暂停的共享计划。|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|设置缓存刷新计划的属性。|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|设置共享计划的属性值。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [报表服务器 Web 服务方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [技术参考 (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
