---
title: 计划方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
caps.latest.revision: 34
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 10513c14e2d9c65a210eee837ce3c23b21ff77aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014726"
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
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [报表服务器 Web 服务方法](report-server-web-service-methods.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  