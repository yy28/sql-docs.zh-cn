---
title: "计划跟踪 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d2644b34916c0263b9ae45251050da2331f7f60
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="schedule-traces"></a>安排跟踪
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中有两种计划跟踪的方法。 您可以：  
  
-   启用跟踪停止时间。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来计划跟踪。  
  
## <a name="specifying-a-stop-time"></a>指定停止时间  
 如果您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，则可以指定跟踪停止时间。 停止时间必须在最初配置跟踪时设置。  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>使用 SQL Server 代理来计划跟踪  
 计划跟踪的最佳方法是先使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动跟踪，再使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程 **sp_trace_setstatus**或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]来指定跟踪停止时间。  
  
 **设置跟踪的结束时间筛选器**  
  
 [基于事件结束时间筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [自动执行管理任务（SQL Server 代理）](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
