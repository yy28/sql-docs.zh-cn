---
title: "监视 Analysis Services 使用 SQL Server Profiler 简介 |Microsoft 文档"
ms.custom: 
ms.date: 01/23/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 568ec549-5ddc-493a-b9f8-3bdc548b562e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 193b7d2907fe41c35560f23e204a3f56e209802d
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>通过 SQL Server Profiler 监视 Analysis Services 简介
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 监视 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例生成的事件。 通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，可以执行以下操作：  
  
-   监视 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的性能。  
  
-   调试多维表达式 (MDX) 语句  
  
-   标识运行缓慢的 MDX 语句。  
  
-   在项目开发阶段，通过逐步执行语句来测试 MDX 语句，以确认代码按预期运行。  
  
-   通过捕获生产系统中的事件并在测试系统中重播这些事件来解决 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的问题。 这种方法对测试或调试很有用，并使得用户可以不受干扰地继续使用生产系统。  
  
-   审核和检查在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例中发生的活动。 安全管理员可以检查任何一个审核的事件。 这类事件包括登录尝试成功或失败，用于访问语句和对象的权限的成功或失败。  
  
-   将有关已捕获事件的数据显示到屏幕，或将有关每个事件的数据捕获和保存到文件或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，供将来分析或重放。 重播数据时，可以使保存的事件按原来发生的情况重新运行，可以是实时运行，也可以是逐步运行。  
  
## <a name="using-sql-server-profiler"></a>使用 SQL Server Profiler  
 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 创建或重播跟踪，您必须是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器角色的成员。 如果你是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器角色的成员，则可以从“开始”菜单中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程序组启动 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]时，请注意以下事项：  
  
-   跟踪定义与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库存储在一起（通过使用 CREATE 语句）。  
  
-   可以同时运行多个跟踪。  
  
-   多个连接可以从同一个跟踪接收事件。  
  
-   当 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 停止或重新启动时，跟踪可以继续。  
  
    > [!NOTE]  
    >  密码不会暴露在跟踪事件中，在事件中由 ****** 替代。  
  
 为实现最佳性能，请仅使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 监视您最关注的那些事件。 如果监视太多的事件，会增加开销，并且可能导致跟踪文件或表变得很大，尤其是在很长时期内进行监视时。 此外，可通过筛选来限制收集的数据量，防止跟踪变得太大。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [为重播 &#40; 创建事件探查器跟踪Analysis Services &#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)  
  
  
