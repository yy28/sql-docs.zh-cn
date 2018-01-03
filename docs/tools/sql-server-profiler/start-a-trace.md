---
title: "启动跟踪 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, stopping traces
- pausing traces
- Profiler [SQL Server Profiler], stopping traces
- Profiler [SQL Server Profiler], starting traces
- traces [SQL Server], starting
- SQL Server Profiler, pausing traces
- traces [SQL Server], stopping
- Profiler [SQL Server Profiler], pausing traces
- traces [SQL Server], pausing
- SQL Server Profiler, starting traces
- stopping traces
- starting traces
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bce247fa86806a4acd40bdfefd11a167a5c614f0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="start-a-trace"></a>启动跟踪
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]定义新跟踪或通过使用创建了模板之后[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，你可以启动、 暂停或停止捕获数据使用的新的跟踪定义或模板。  
  
## <a name="starting-a-trace"></a>启动跟踪  
 当启动跟踪并且已定义的源为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将创建一个队列，为捕获的服务器事件提供临时存放位置。  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 访问 SQL 跟踪时，启动跟踪将打开一个新的跟踪窗口（如果没有窗口打开），并立即捕获数据。  
  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系统存储过程访问 SQL 跟踪时，每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都必须启动跟踪，以便捕获数据。 启动跟踪后，只能修改跟踪的名称。  
  
> [!NOTE]  
>  在使用现有跟踪时，可以查看属性，但是不能修改属性。 若要修改属性，请停止或暂停跟踪。  
  
## <a name="see-also"></a>另请参阅  
 [连接到服务器后自动启动跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [暂停跟踪 &#40;SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   
 [停止跟踪 &#40;SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   
 [清除跟踪窗口 &#40;SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   
 [在跟踪暂停或停止之后运行跟踪 (SQL Server Profiler)](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
