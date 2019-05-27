---
title: SQL Server Profiler-重播配置 （基本重播选项） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: 85a1dec6-9bbc-477a-86c5-b463db9ebb31
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ea9517047321f54734b3ccd8d072ba8f3f23152
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089721"
---
# <a name="sql-server-profiler---replay-configuration-basic-replay-options"></a>SQL Server Profiler - 重播配置（基本重播选项）
  在 **“重播配置”** 对话框中，使用 **“基本重播配置”** 页可以指定如何重播跟踪文件或表。  
  
 若要查看此窗口，请使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]打开包含相应重播事件的跟踪文件或表。 有关详细信息，请参阅 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)。 打开跟踪文件或表后，在 **“重播”** 菜单上，单击 **“启动”**，然后连接到要重播跟踪的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。  
  
## <a name="options"></a>选项  
 **重播服务器**  
 显示要连接用来重播的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。  
  
 **更改...**  
 启动“连接到服务器”对话框以连接到另一台服务器。  
  
 **保存到文件**  
 将重播结果保存到文件。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 将显示标准文件对话框，您可以在该对话框中指定文件的保存位置。  
  
 **保存到表**  
 将重播结果保存到表。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 将显示表选择对话框，您可以在该对话框中指定表的保存位置。  
  
 **重播线程数**  
 指定要并发使用的重播线程数。 数目越大，重播期间消耗的资源越多，但是重播速度更快，允许的并发事件更多。  
  
 **按跟踪事件的顺序重播事件**  
 按顺序重播事件。 如果重播跟踪进行调试，请使用此选项。  
  
 **使用多个线程重播事件**  
 并发重播事件。 此选项比按顺序重播事件速度快，但将禁用调试。 事件按其系统进程标识符 (SPID) 进行排序。  
  
 **显示重播结果**  
 在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]中显示重播结果。  
  
## <a name="see-also"></a>请参阅  
 [重播跟踪表 (SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重播跟踪文件 (SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重播跟踪](../tools/sql-server-profiler/replay-traces.md)  
  
  
