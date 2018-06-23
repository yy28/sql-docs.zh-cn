---
title: 呈现和执行方法 | Microsoft Docs
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
- rendered reports [Reporting Services]
- reports [Reporting Services], execution options
- methods [Reporting Services], execution options
- methods [Reporting Services], rendering
ms.assetid: 12626aad-f0be-4653-87d0-60eb3a3fff78
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: bd1745f845cda954c0e447a8a1d035646fd298dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124480"
---
# <a name="rendering-and-execution-methods"></a>呈现和执行方法
  可以使用这些方法来管理项执行和缓存以及报表呈现。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.FlushCache%2A>|使项的缓存无效。|  
|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|返回项的缓存配置以及说明项的缓存副本何时到期的设置。|  
|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|返回单个项的执行选项和相关设置。|  
|<xref:ReportService2010.ReportingService2010.ListExecutionSettings%2A>|返回支持的执行设置的列表。|  
|<xref:ReportExecution2005.ReportExecutionService.Render%2A>|处理指定报表并以指定格式呈现报表。|  
|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|配置要缓存的项并提供指定项的缓存副本何时到期的设置。|  
|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|为指定的项设置执行选项和相关的执行属性。|  
|<xref:ReportService2010.ReportingService2010.UpdateItemExecutionSnapshot%2A>|生成指定项的项执行快照。|  
  
## <a name="see-also"></a>请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [报表服务器 Web 服务方法](report-server-web-service-methods.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  