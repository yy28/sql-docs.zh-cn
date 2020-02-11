---
title: 服务器性能和活动监视 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7289c18fac421bbdb5ccc0e00a3bea60b7a22d9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150619"
---
# <a name="server-performance-and-activity-monitoring"></a>服务器性能和活动监视
  监视数据库的目的是评估服务器的性能。 有效监视包括定期拍摄当前性能的快照来隔离导致问题的进程，以及连续收集数据来跟踪性能趋势。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统提供实用工具，使您可以查看数据库的当前状态并在条件更改时跟踪性能。  
  
 下一节包含的主题说明了如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 性能以及活动监视工具。 本节包含以下主题：  
  
## <a name="in-this-section"></a>本节内容  
 **使用 Windows 工具执行监视任务**  
  
-   [启动系统监视器 &#40;Windows&#41;](start-system-monitor-windows.md)  
  
-   [查看 Windows 应用程序日志 (Windows)](view-the-windows-application-log-windows-10.md)  
  
 **用 Windows 工具创建 SQL Server 数据库警报**  
  
-   [设置 SQL Server 数据库警报 &#40;Windows&#41;](set-up-a-sql-server-database-alert-windows.md)  
  
 **使用 SQL Server Management Studio 执行监视任务**  
  
-   [查看 SQL Server 错误日志 &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [打开活动监视器 (SQL Server Management Studio)](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **使用 Transact-SQL 存储过程并通过 SQL 跟踪执行监视任务**  
  
-   [创建跟踪 (Transact-SQL)](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [将跟踪筛选器设置 &#40;Transact-sql&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [&#40;Transact-sql&#41;修改现有跟踪](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [&#40;Transact-sql&#41;查看保存的跟踪](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [&#40;Transact-sql&#41;查看筛选器信息](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [&#40;Transact-sql&#41;删除跟踪](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **使用 SQL Server Profiler 创建和修改跟踪**  
  
-   [创建跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [设置全局跟踪选项 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [指定跟踪文件的事件和数据列 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [创建用于运行跟踪 &#40;SQL Server Profiler 的 Transact-sql 脚本&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [将跟踪结果保存到文件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [设置跟踪文件的最大文件大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [将跟踪结果保存到表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [设置跟踪表的最大表大小 (SQL Server Profiler)](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [在跟踪中筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [查看筛选器信息 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [修改筛选器 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [根据事件开始时间 &#40;SQL Server Profiler 来筛选事件&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [基于事件结束时间筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [筛选服务器进程 Id &#40;Spid&#41; 在跟踪 &#40;SQL Server Profiler 中&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [组织跟踪中显示的列 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 启动、暂停和停止跟踪**  
  
-   [连接到服务器后自动启动跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [暂停跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [停止跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [在跟踪暂停或停止之后运行跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 打开跟踪并配置如何显示跟踪**  
  
-   [打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [打开跟踪表 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [清除跟踪窗口 (SQL Server Profiler)](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [关闭跟踪窗口 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [设置跟踪定义默认值 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [设置跟踪显示默认值 (SQL Server Profiler)](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 重播跟踪**  
  
-   [重播跟踪文件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [重播跟踪表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [每次重播一个事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [重播到断点 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [重播至光标处 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [重播 Transact-sql 脚本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 创建、修改和使用跟踪模板**  
  
-   [创建跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [修改跟踪模板 (SQL Server Profiler)](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [从正在运行的跟踪中派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [从跟踪文件或跟踪表派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [导出跟踪模板 (SQL Server Profiler)](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [导入跟踪模板 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **使用 SQL Server Profiler 跟踪来收集和监视服务器性能**  
  
-   [在跟踪 &#40;SQL Server Profiler 时查找值或数据列&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [保存死锁图形 &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [单独保存显示计划 XML 事件 &#40;SQL Server Profiler&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [单独保存显示计划 XML 统计信息事件 &#40;SQL Server Profiler&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [从跟踪 &#40;SQL Server Profiler 中提取脚本&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [将跟踪与 Windows 性能日志数据关联 &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
