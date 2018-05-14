---
title: 服务器性能和活动监视 | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 49c3cc0b2426f2906e11cd75ff01c02f8a5daa28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="server-performance-and-activity-monitoring"></a>服务器性能和活动监视
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  监视数据库的目的是评估服务器的性能。 有效监视包括定期拍摄当前性能的快照来隔离导致问题的进程，以及连续收集数据来跟踪性能趋势。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 操作系统提供实用工具，使您可以查看数据库的当前状态并跟踪性能的状态变化。  
  
 下一节包含的主题说明了如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 性能以及活动监视工具。 本节包含以下主题：  
  
## <a name="in-this-section"></a>本节内容  
 **使用 Windows 工具执行监视任务**  
  
-   [启动系统监视器 (Windows)](../../relational-databases/performance/start-system-monitor-windows.md)  
  
-   [查看 Windows 应用程序日志 (Windows)](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
 **使用 Windows 工具创建 SQL Server 数据库警报**  
  
-   [设置 SQL Server 数据库警报 (Windows)](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)  

 **使用扩展事件执行监视任务**  
 
 -   [扩展事件](../../relational-databases/extended-events/extended-events.md)
 
  -   [快速入门：SQL Server 中的扩展事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
   
 **使用 SQL Server Management Studio 执行监视任务**  
  
-   [查看 SQL Server 错误日志 (SQL Server Management Studio)](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
-   [打开活动监视器 (SQL Server Management Studio)](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **使用 Transact-SQL 存储过程并通过 SQL 跟踪执行监视任务**  
  
-   [创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
-   [设置跟踪筛选器 (Transact-SQL)](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
-   [修改现有跟踪 (Transact-SQL)](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [查看保存的跟踪 (Transact-SQL)](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [查看筛选器信息 (Transact-SQL)](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)  
  
-   [删除跟踪 (Transact-SQL)](../../relational-databases/sql-trace/delete-a-trace-transact-sql.md)  
  
 **使用 SQL Server Profiler 创建和修改跟踪**  
  
-   [创建跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [设置全局跟踪选项 (SQL Server Profiler)](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [指定跟踪文件的事件和数据列 (SQL Server Profiler)](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [将跟踪结果保存到文件 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [设置跟踪文件的最大文件大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [将跟踪结果保存到表 (SQL Server Profiler)](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [设置跟踪表的最大表大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [在跟踪中筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [查看筛选器信息 (SQL Server Profiler)](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [修改筛选器 (SQL Server Profiler)](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [基于事件开始时间筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [基于事件结束时间筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [在跟踪中筛选服务器进程 ID (SPID) (SQL Server Profiler)](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [组织跟踪中显示的列 (SQL Server Profiler)](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 启动、暂停和停止跟踪**  
  
-   [连接到服务器后自动启动跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [暂停跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [停止跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [在跟踪暂停或停止之后运行跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 打开跟踪并配置如何显示跟踪**  
  
-   [打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [清除跟踪窗口 (SQL Server Profiler)](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [关闭跟踪窗口 (SQL Server Profiler)](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [设置跟踪定义默认值 (SQL Server Profiler)](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [设置跟踪显示默认值 (SQL Server Profiler)](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 重播跟踪**  
  
-   [重播跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [重播跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [每次重播一个事件 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [重播到断点 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [重播至光标处 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [重播 Transact-SQL 脚本 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 创建、修改和使用跟踪模板**  
  
-   [创建跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [修改跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
-   [从正在运行的跟踪中派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [从跟踪文件或跟踪表派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [导出跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [导入跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 跟踪来收集和监视服务器性能**  
  
-   [在跟踪时查找值或数据列 (SQL Server Profiler)](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [保存死锁图形 (SQL Server Profiler)](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
-   [分别保存 Showplan XML 事件 (SQL Server Profiler)](../../relational-databases/performance/save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [分别保存 Showplan XML Statistics Profile 事件 (SQL Server Profiler)](../../relational-databases/performance/save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [从跟踪提取脚本 (SQL Server Profiler)](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [将跟踪与 Windows 性能日志数据关联 (SQL Server Profiler)](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
