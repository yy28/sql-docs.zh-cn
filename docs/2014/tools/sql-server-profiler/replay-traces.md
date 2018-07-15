---
title: 重播跟踪 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, replaying traces
- Run to Cursor option
- Toggle Breakpoint option
- traces [SQL Server], replaying
- replaying traces
- playback engine [SQL Server Profiler]
- events [SQL Server], replaying traces
- Profiler [SQL Server Profiler], replaying traces
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 76ef0ddde1f23d68e198854466a8b0abbbecc427
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325277"
---
# <a name="replay-traces"></a>重播跟踪
  重播是重现在跟踪内捕获的活动的功能。 在创建或编辑跟踪时，可以将跟踪保存到文件中并在以后重播。 可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 从一台计算机重播跟踪活动。 对于大型工作负荷，可使用分布式重播实用工具从多台计算机重播跟踪数据。  
  
 本节描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]的重播功能。 有关分布式重播实用工具的详细信息，请参阅 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 具有多线程播放引擎，能模拟用户连接和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 重播对于解决应用程序或进程问题是很有用的。 当标识出问题并进行了纠正后，请对纠正后的应用程序或进程运行找出潜在问题的跟踪。 然后，重播原始跟踪并比较结果。  
  
 跟踪重播支持通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]“重播”菜单上的“切换断点”和“运行至光标处”选项来进行调试。 由于这些选项可以将跟踪重播打断为较短的段以便进行增量分析，因此尤其改善了对长脚本的分析。  
  
 有关重播跟踪所需权限的信息，请参阅 [运行 SQL Server Profiler 所需的权限](permissions-required-to-run-sql-server-profiler.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[重播要求](replay-requirements.md)|说明跟踪定义必须包含的事件，以便它能使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]进行重播。|  
|[重播选项&#40;SQL Server Profiler&#41;](replay-options-sql-server-profiler.md)|说明在 **的** “重播配置” [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]对话框中可以设置的选项。|  
|[重播跟踪的注意事项&#40;SQL Server Profiler&#41;](considerations-for-replaying-traces-sql-server-profiler.md)|说明不能使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重播的跟踪事件以及重播跟踪对服务器性能的影响。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 分布式重播](../distributed-replay/sql-server-distributed-replay.md)  
  
  
