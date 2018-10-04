---
title: 性能、快照、缓存 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c578e5e56d575f3d324d8585f73a9891b2ad00ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091677"
---
# <a name="performance-snapshots-caching-reporting-services"></a>性能、快照、缓存 (Reporting Services)
  报表服务器性能受各种组合因素的影响，这些因素包括硬件、访问报表的并发用户的数量、报表中的数据量和输出格式。 若要了解影响您的安装的具体性能因素以及哪个补救办法将生成所需的结果，您将需要获得基准数据并运行测试。 有关工具和指南的详细信息，请参阅 MSDN 上的以下发布内容： [Reporting Services 性能优化](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) 和 [使用 Visual Studio 2005 在 SQL Server 2005 Reporting Services 报表服务器上执行负载测试](http://go.microsoft.com/fwlink/?LinkID=77519)。  
  
 下面是需要考虑的总原则：  
  
-   报表的处理和呈现操作会占用大量内存。 如有可能，请选择具有大量内存的计算机。  
  
-   将报表服务器和报表服务器数据库承载到单独的计算机上往往比将二者同时承载到单台高端计算机上能取得更好的性能。  
  
-   如果所有报表的处理速度都慢，请考虑使用一个扩展部署，其中的多个报表服务器实例都支持单个报表服务器数据库。 为了获得最佳效果，请使用负载平衡软件来将请求平均分布到部署中。  
  
-   如果只是单个报表的处理速度慢，而且该报表必须按需运行，请对报表数据集查询进行优化。 您还可以考虑使用可高速缓存的共享数据集、高速缓存报表或将报表作为快照运行。  
  
-   如果所有报表在以特定格式处理（例如，以 PDF 格式呈现）时都慢，请考虑使用文件共享传递、添加更多的内存或者选择其他格式。  
  
-   若要确定处理报表所需的时间以及其他使用情况指标，请检查报表服务器的执行日志。 有关详细信息，请参阅[报表服务器执行日志和 ExecutionLog3 视图](report-server-executionlog-and-the-executionlog3-view.md)。  
  
-   有关如何通过优化内存管理配置设置来缓解性能问题的详细信息，请参阅[为报表服务器应用程序配置可用内存](../report-server/configure-available-memory-for-report-server-applications.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [监视报表服务器性能](monitoring-report-server-performance.md)  
 介绍可用来跟踪服务器上的处理负载的性能对象。  
  
 [设置报表处理属性](set-report-processing-properties.md)  
 介绍如何将报表配置为按需运行、从高速缓存运行或按计划作为报表快照运行。  
  
 [为报表服务器应用程序配置可用内存](../report-server/configure-available-memory-for-report-server-applications.md)  
 说明如何覆盖默认内存管理行为。  
  
 [缓存报表&#40;SSRS&#41;](caching-reports-ssrs.md)  
 介绍报表服务器上的报表高速缓存行为。  
  
 [缓存共享数据集&#40;SSRS&#41;](cache-shared-datasets-ssrs.md)  
 介绍报表服务器上的共享数据集高速缓存行为。  
  
 [处理大型报表](process-large-reports.md)  
 为如何配置和分发大型报表提供建议。  
  
 [为报表和共享数据集处理设置超时值&#40;SSRS&#41;](setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 介绍如何针对查询和报表处理设置超时值。  
  
## <a name="see-also"></a>请参阅  
 [管理正在运行的进程](../subscriptions/manage-a-running-process.md)   
 [验证报表运行情况](verifying-a-report-run.md)  
  
  
