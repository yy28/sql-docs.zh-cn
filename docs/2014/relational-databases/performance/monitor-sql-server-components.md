---
title: 监视 SQL Server 组件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c0534bf3a12aa81a9fc84d0e2c4f82a189748a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150753"
---
# <a name="monitor-sql-server-components"></a>监视 SQL Server 组件
  监视操作非常重要，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在动态环境中提供服务。 应用程序中的数据在变化。 用户需要的访问类型在变化。 用户连接的方式在变化。 甚至，访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的应用程序的类型也可能在变化，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动管理系统级资源（如内存和磁盘空间），以便最小化对广泛系统级手动优化的需要。 管理员可以通过监视来标识性能趋势以确定是否有必要进行更改。  
  
 有效地监视任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件：  
  
1.  确定监视目标。  
  
2.  选择相应工具。  
  
3.  标识要监视的组件。  
  
4.  选择那些组件的度量。  
  
5.  监视服务器。  
  
6.  分析数据。  
  
 下面将依次介绍这些步骤。  
  
## <a name="determine-your-monitoring-goals"></a>确定监视目标  
 若要有效监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，必须清楚地确定监视原因。 下面列出了可能的原因：  
  
-   建立性能基线。  
  
-   标识一段时间内的性能变化。  
  
-   诊断特定性能问题。  
  
-   标识要优化的组件或进程。  
  
-   比较对不同客户端应用程序性能的影响。  
  
-   审核用户活动。  
  
-   在不同负荷下测试服务器。  
  
-   测试数据库体系结构。  
  
-   测试维护计划。  
  
-   测试备份和还原计划。  
  
-   确定何时修改硬件配置。  
  
## <a name="select-the-appropriate-tool"></a>选择相应工具  
 确定监视原因后，应该为该监视类型选择相应的工具。 Windows 操作系统和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一整套用于在大型事务环境中监视服务器的工具。 这些工具清楚地显示 SQL Server 数据库引擎实例或 SQL Server Analysis Services 实例的状态。  
  
 Windows 提供下列工具来监视在服务器上运行的应用程序：  
  
-   系统监视器，使您可以收集和查看有关活动（如内存、磁盘和处理器使用）的实时数据  
  
-   性能日志和警报  
  
-   任务管理器  
  
 有关 Windows Server 或 Windows 工具的详细信息，请参阅 Windows 文档。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供下列工具来监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的组件：  
  
-   SQL 跟踪  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
-   分布式重播实用工具  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 活动监视器  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 图形显示计划  
  
-   存储过程  
  
-   数据库控制台命令 (DBCC)  
  
-   内置函数  
  
-   跟踪标志  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 监视工具的信息，请参阅 [性能监视和优化工具](performance-monitoring-and-tuning-tools.md)。  
  
## <a name="identify-the-components-to-monitor"></a>标识要监视的组件  
 监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的第三步是标识监视组件。 例如，如果使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪服务器，则可以定义该跟踪来收集有关特定事件的数据。 还可以排除不适合您的情况的事件。  
  
## <a name="select-metrics-for-monitored-components"></a>选择监视组件的度量指标  
 确定监视组件后，就需要确定监视组件的度量。 例如，选择跟踪中包括的事件后，可以选择只包括有关事件的特定数据。 限制只跟踪与该跟踪有关的数据可最大限度减少执行跟踪所需的系统资源。  
  
## <a name="monitor-the-server"></a>监视服务器  
 若要监视服务器，请运行已配置为收集数据的监视工具。 例如，定义跟踪后，可以运行该跟踪以收集有关服务器中生成的事件的数据。  
  
## <a name="analyze-the-data"></a>分析数据  
 跟踪结束后，分析数据以查看是否实现了监视目标。 如果没有，请修改用于监视服务器的组件或度量。  
  
 下面概述了捕获事件数据并使用这些数据的过程。  
  
1.  使用筛选器限制收集的事件数据。  
  
     限制事件数据使系统可以集中在与监视方案有关的事件上。 例如，若要监视执行速度慢的查询，可使用筛选器只监视那些在特定数据库中运行 30 秒以上的应用程序发出的查询。 有关详细信息，请参阅[设置跟踪筛选器 (Transact-SQL)](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md) 和 [在跟踪中筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)。  
  
2.  监视（捕获）事件。  
  
     一旦启用，活动监视就从指定的应用程序、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例或操作系统捕获数据。 例如，当使用系统监视器监视磁盘活动时，监视将捕获事件数据（如磁盘读取和写入）并在屏幕上显示该数据。 有关详细信息，请参阅[监视资源使用情况（系统监视器）](../performance-monitor/monitor-resource-usage-system-monitor.md)。  
  
3.  保存捕获的事件数据。  
  
     保存捕获的事件数据使您可以在以后对其进行分析，甚至使用分布式重播实用工具或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]重播该数据。 捕获的事件数据将保存到文件，该文件可以加载回最初创建它的工具中以进行分析。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 允许将事件数据保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 保存捕获的事件数据对创建性能基线非常重要。 在比较最近捕获的事件数据来确定是否已获得最佳性能时，将保存并使用性能基线数据。 有关详细信息，请参阅 [SQL Server Profiler 模板和权限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)。  
  
4.  创建包含为捕获事件所指定设置的跟踪模板。  
  
     跟踪模板包括有关事件本身、事件数据和用于捕获数据的筛选器的规范。 这些模板可用于以后监视特定事件集，而无需重新定义事件、事件数据和筛选器。 例如，若要频繁监视死锁数以及那些死锁所涉及的用户，您可以创建一个模板来定义那些事件、事件数据和事件筛选器；保存此模板；并在下次监视死锁时重新应用此筛选器。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 使用跟踪模板。 有关详细信息，请参阅[设置跟踪定义默认值 (SQL Server Profiler)](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md) 和[创建跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)。  
  
5.  分析捕获的事件数据。  
  
     为了进行分析，将捕获的事件数据加载到捕获该数据的应用程序中。 例如，可以将通过 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 捕获的跟踪重新加载到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中进行查看和分析。 有关详细信息，请参阅 [使用 SQL Server Profiler 查看和分析跟踪](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)。  
  
     对事件数据的分析包括确定所发生的事件和发生原因。 利用这些信息可以做一些更改（如根据所执行的分析类型添加更多内存、更改索引、更正使用 Transact-SQL 语句或存储过程的编码问题等）来提高性能。 例如，可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问分析通过 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 捕获的跟踪并根据结果生成索引建议。  
  
6.  重播捕获的事件数据。  
  
     事件重播使您可以建立捕获数据时的数据库环境的测试副本，然后可以重复捕获的事件，就像最初在真实系统上捕获事件一样。 此功能仅适用于分布式重播实用工具或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。 可以按事件最初发生时的速度重播它们，尽可能快地重播（增加系统的压力），或者尽可能一次重播一步（每个事件发生后对系统进行分析）。 通过在测试环境中分析确切事件，可以防止对生产系统产生有害影响。 有关详细信息，请参阅 [重播跟踪](../../tools/sql-server-profiler/replay-traces.md)。  
  
  
