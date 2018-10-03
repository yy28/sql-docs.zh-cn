---
title: 重播跟踪 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1d10e70c86f98933a2b7081767f6f0362075ca3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47768267"
---
# <a name="replay-traces"></a>重播跟踪
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  重播是重现在跟踪内捕获的活动的功能。 在创建或编辑跟踪时，可以将跟踪保存到文件中并在以后重播。 可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 从一台计算机重播跟踪活动。 对于大型工作负荷，可使用分布式重播实用工具从多台计算机重播跟踪数据。  
  
 本节描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]的重播功能。 有关分布式重播实用工具的详细信息，请参阅 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 具有多线程播放引擎，能模拟用户连接和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 重播对于解决应用程序或进程问题是很有用的。 当标识出问题并进行了纠正后，请对纠正后的应用程序或进程运行找出潜在问题的跟踪。 然后，重播原始跟踪并比较结果。  
  
 跟踪重播支持通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]“重播”菜单上的“切换断点”和“运行至光标处”选项来进行调试。 由于这些选项可以将跟踪重播打断为较短的段以便进行增量分析，因此尤其改善了对长脚本的分析。  
  
 有关重播跟踪所需权限的信息，请参阅 [运行 SQL Server Profiler 所需的权限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[重播要求](../../tools/sql-server-profiler/replay-requirements.md)|说明跟踪定义必须包含的事件，以便它能使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]进行重播。|  
|[重播选项 (SQL Server Profiler)](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|说明在 **的** “重播配置” [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]对话框中可以设置的选项。|  
|[重播跟踪的注意事项 (SQL Server Profiler)](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|说明不能使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 重播的跟踪事件以及重播跟踪对服务器性能的影响。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
