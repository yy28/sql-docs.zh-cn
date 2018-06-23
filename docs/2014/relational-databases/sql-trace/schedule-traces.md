---
title: 计划跟踪 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3017f239b024bcab3d19b589be1ec189187a5d09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024286"
---
# <a name="schedule-traces"></a>安排跟踪
  在 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中有两种计划跟踪的方法。 您可以：  
  
-   启用跟踪停止时间。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来计划跟踪。  
  
## <a name="specifying-a-stop-time"></a>指定停止时间  
 如果您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，则可以指定跟踪停止时间。 停止时间必须在最初配置跟踪时设置。  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>使用 SQL Server 代理来计划跟踪  
 计划跟踪的最佳方法是先使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动跟踪，再使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程 **sp_trace_setstatus**或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]来指定跟踪停止时间。  
  
 **设置跟踪的结束时间筛选器**  
  
 [基于事件结束时间筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [自动执行管理任务（SQL Server 代理）](../../ssms/agent/sql-server-agent.md)  
  
  
