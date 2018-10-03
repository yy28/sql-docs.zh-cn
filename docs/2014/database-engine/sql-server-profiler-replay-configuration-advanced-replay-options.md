---
title: SQL Server Profiler-重播配置 （高级的重播选项） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fff89f4be7953e2eb0cec3ed9a04883052ed6d1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192477"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server Profiler - 重播配置（高级重播选项）
  在 **“重播配置”** 对话框中，使用 **“高级重播选项”** 选项卡可以指定如何重播跟踪文件。  
  
 若要查看此窗口，请使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]打开包含相应重播事件的跟踪文件或表。 有关详细信息，请参阅 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)。 打开跟踪文件或表后，在 **“重播”** 菜单上，单击 **“启动”**，连接到要重播跟踪的 SQL Server 实例，再单击 **“高级重播选项”** 选项卡。  
  
## <a name="options"></a>选项  
 **重播系统 SPID**  
 指定 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]是否重播系统进程标识符 (SPID)。  
  
 **仅重播一个 SPID**  
 仅重播与所选 SPID 相关的源跟踪文件中的活动。  
  
 **要重播的 SPID**  
 指定要重播的 SPID。  
  
 **按日期和时间限制重播**  
 选中此选项可以仅重播部分源跟踪文件。  
  
 **开始时间**  
 源跟踪文件中重播开始的日期和时间。  
  
 **结束时间**  
 源跟踪文件中重播结束的日期和时间。  
  
 **Health Monitor 等待间隔(秒)**  
 指定重播的等待间隔（秒）。 默认值为 3600 秒（1 小时）。 此设置影响进程在被 health monitor 终止前所允许运行的时间。  
  
 **Health Monitor 轮询间隔(秒)**  
 指定重播过程中的 Health Monitor 轮询间隔（秒）。 默认值为 60 秒。 使用此值，用户可以配置 Health Monitor 对终止候选项的轮询频率。  
  
 **启用 SQL Server 阻塞的进程监视器**  
 启用一个进程，搜索已阻塞或正在阻塞的进程。  
  
 **阻塞的进程监视器等待间隔(秒)**  
 配置阻塞的进程监视器搜索已阻塞的或正在阻塞的进程的频率。  
  
## <a name="see-also"></a>请参阅  
 [重播跟踪表&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重播跟踪文件 (SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重播跟踪](../tools/sql-server-profiler/replay-traces.md)  
  
  
