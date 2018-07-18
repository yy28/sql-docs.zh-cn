---
title: 实时查询统计信息 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1ea9f40ecda2d22e9117ae9156282e42b5101cd9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34331228"
---
# <a name="live-query-statistics"></a>实时查询统计信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 能够查看活动查询的实时执行计划。 此实时查询计划作为控制流，能够实时了解从一个[查询计划操作员](../../relational-databases/showplan-logical-and-physical-operators-reference.md)到另一个操作员的查询执行过程。 实时查询计划显示总体查询进度和操作员级运行时执行统计信息（例如处理的行数、经过的时间、操作员进度等）。由于此数据是实时可用的，无需等待完成查询，因此这些执行统计信息对于调试查询性能问题非常有用。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]开始支持此功能，但它可以与 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]配合使用。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
  
> [!WARNING]  
> 此功能主要用于故障排除。 使用此功能会明显降低整体查询性能。 此功能可与 [Transact-SQL 调试器](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)配合使用。  
  
#### <a name="to-view-live-query-statistics"></a>查看实时查询统计信息  
  
1.  若要查看实时查询执行计划，请在工具菜单上单击“实时查询统计信息”  图标。  
  
     ![工具栏上的“实时查询统计信息”按钮](../../relational-databases/performance/media/livequerystatstoolbar.png "工具栏上的“实时查询统计信息”按钮")  
  
     还可以查看实时查询执行计划，方法是在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中右键单击所选查询，然后单击“包含实时查询统计信息”。  
  
     ![弹出菜单上的“实时查询统计信息”按钮](../../relational-databases/performance/media/livequerystatsmenu.png "弹出菜单上的“实时查询统计信息”按钮")  
  
2.  现在执行查询。 实时查询计划显示查询计划操作员的总体查询进度和运行时执行统计信息（例如，经过的时间、进度等）。 查询进度信息和执行统计信息会在查询执行的同时定期更新。 使用此信息可了解整个查询执行过程，以及调试长时间运行的查询、无限期运行的查询、导致 tempdb 溢出和超时问题的查询。  
  
     ![显示计划中的“实时查询统计信息”按钮](../../relational-databases/performance/media/livequerystatsplan.png "显示计划中的“实时查询统计信息”按钮")  
  
 此外，可以通过右键单击“消耗资源的活动查询”  表中的查询，从“活动监视器”  中访问实时执行计划。  
  
 ![活动监视器中的“实时查询统计信息”按钮](../../relational-databases/performance/media/livequerystatsactmon.png "活动监视器中的“实时查询统计信息”按钮")  
  
## <a name="remarks"></a>Remarks  
 必须启用统计信息配置文件基础结构，实时查询统计信息才能捕获查询进度的相关信息。 在 **中指定“包含实时查询统计信息”**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可以启用当前查询会话的统计信息基础结构。 
 
从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 起，可通过另外两种方法启用统计信息基础结构，从而查看其他会话（如活动监视器）中的实时查询统计信息：  
  
-   在目标会话中执行 `SET STATISTICS XML ON;` 或 `SET STATISTICS PROFILE ON;` 。  
  
 或多个  
  
-   启用 **query_post_execution_showplan** 扩展事件。 这是一个服务器级设置，用于启用所有会话中的实时查询统计信息。 若要启用扩展事件，请参阅 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  

从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含统计信息配置文件基础结构的轻型版本。 可通过两种方法启用轻型统计信息基础结构，从而查看其他会话（如活动监视器）中的实时查询统计信息：

-   使用全局跟踪标志 7412。  
  
 或多个  
  
-   启用 **query_thread_profile** 扩展事件。 这是一个服务器级设置，用于启用所有会话中的实时查询统计信息。 若要启用扩展事件，请参阅 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。
  
 > [!NOTE]
 > 不支持本机编译的存储过程。  
  
## <a name="permissions"></a>权限  
 需要数据库级别 **SHOWPLAN** 权限来填充“实时查询统计信息”  结果页，需要服务器级别 **VIEW SERVER STATE** 权限来查看实时统计信息，还需要执行查询所需的所有权限。  
  
## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [性能监视和优化工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [打开活动监视器 (SQL Server Management Studio)](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [活动监视器](../../relational-databases/performance-monitor/activity-monitor.md)     
 [使用查询存储监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
