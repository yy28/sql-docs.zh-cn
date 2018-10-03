---
title: 重播跟踪文件 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22b0fb207a837407752a6356c452e215980bea24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171007"
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>重播跟踪文件 (SQL Server Profiler)
  重播是指打开已保存的跟踪并对其重播的功能。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 具有多线程播放引擎，能模拟用户连接和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 重播对于解决应用程序或进程问题是很有用的。 在您确定问题并进行更正后，请对更正后的应用程序或进程运行发现该潜在问题的跟踪。 然后，重播原始跟踪并比较结果。  
  
 除了要监视的任何其他事件类之外，还必须捕获特定的事件类才能启用重播。 如果使用 **TSQL_Replay** 跟踪模板，则在默认情况下将捕获这些事件。 有关详细信息，请参阅 [Replay Requirements](replay-requirements.md)。  
  
### <a name="to-replay-a-trace-file"></a>重播跟踪文件  
  
1.  在 **“文件”** 菜单上，指向 **“打开”**，然后单击 **“跟踪文件”**。 选择包含需要重播的事件类的跟踪文件。  
  
2.  在 **“重播”** 菜单上，单击 **“开始”**，然后连接到要重播跟踪的服务器实例。  
  
3.  在 **“重播配置”** 对话框的 **“基本重播选项”** 选项卡上，指定 **“重播服务器”**。 单击 **“更改”** 以更改 **“重播服务器”** 框中显示的服务器。  
  
4.  根据需要，选择下列目标位置之一以在其中保存重播：  
  
    -   **保存到文件**，指定用于保存重播的文件。  
  
    -   **保存到表**，该选项指定保存重播的数据库表。  
  
5.  选择“按跟踪的顺序重播事件”或“使用多个线程重播事件”。 下表列出了这些设置之间的差异。  
  
    |选项|Description|  
    |------------|-----------------|  
    |**按跟踪事件的顺序重播事件**|按记录事件的顺序重播事件。 此选项启用调试。|  
    |**使用多个线程重播事件**|此选项使用多个线程重播各个事件，而不考虑其顺序。 此选项用于优化性能。|  
  
6.  选择 **“显示重播结果”** 以在重播时查看结果。  
  
7.  还可以单击“高级重播选项”选项卡以配置以下选项：  
  
    -   若要重播所有服务器进程 ID (SPID)，请选择“重播系统 SPID”。  
  
    -   若要仅重播属于特定 SPID 的进程，请选择 **“仅重播一个 SPID”**。 在 **“要重播的 SPID”** 框中，键入 SPID。  
  
    -   若要重播特定时间段内发生的事件，请选择 **“按日期和时间限制重播”**。 为“开始时间”和“结束时间”选择日期和时间，以指定要在重播中包括的时间段。  
  
    -   若要控制重播期间 SQL Server 管理进程的方法，请配置 **“Health Monitor 选项”**。  
  
## <a name="see-also"></a>请参阅  
 [运行 SQL Server Profiler 所需的权限](sql-server-profiler.md)   
 [重播跟踪](replay-traces.md)   
 [打开跟踪文件 (SQL Server Profiler)](open-a-trace-file-sql-server-profiler.md)   
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  
