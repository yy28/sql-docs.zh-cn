---
title: 监视 Analysis Services 实例概述 |Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39cc5a22165d07aafce29e4216548c4e8d226892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62709462"
---
# <a name="monitoring-overview"></a>监视概述
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 具有许多不同的工具来帮助你监视和优化服务器的性能。 工具的选择取决于要执行的监视或优化类型和要监视的具体事件。

有关监视 SQL Server Analysis Services 的详细信息，请参阅[SQL Server 2008 R2 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
## <a name="monitoring-tools"></a>监视工具  

|Tool  |Description  |
|---------|---------|
|[SQL Server 事件探查器](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   跟踪引擎进程事件。 它还会捕获有关这些事件，使您能够监视服务器和数据库活动的数据。      |
| [扩展事件](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   轻量跟踪和性能监视系统，它使用系统资源非常少，因此诊断生产和测试服务器上的问题的理想工具。       |
| [动态管理视图&#40;Dmv&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   返回有关模型对象、 服务器操作和服务器运行状况信息的查询。 基于 SQL 的查询是架构行集的接口。      |
| [跟踪事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  按照通过捕获然后分析实例生成的跟踪事件的活动实例。 跟踪事件将会划分为若干组，以便您可以更轻松地找到相关跟踪事件。        |
|   [性能计数器](../../analysis-services/instances/performance-counters-ssas.md)\*    |    使用性能监视器，您可以通过性能计数器监视 Microsoft SQL Server Analysis Services (SSAS) 实例的性能。     |
|[日志操作](../../analysis-services/instances/performance-counters-ssas.md)\*|SQL Server Analysis Services 实例中，到 msmdsrv.log 文件-一个用于在安装每个实例都将记录服务器通知、 错误和警告。 |

\* 适用于 SQL Server Analysis Services 仅。

## <a name="see-also"></a>另请参阅

[监视 Azure Analysis Services 服务器指标](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[设置 Azure Analysis services 的诊断日志记录](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)
