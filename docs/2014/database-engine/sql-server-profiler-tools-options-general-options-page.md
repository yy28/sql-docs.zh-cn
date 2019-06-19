---
title: SQL Server Profiler-工具选项 （常规选项页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9da36f49927acd2a313bcb9f8647655731006d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089621"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler-工具选项 （常规选项页）
  使用 **“常规选项”** 对话框可以查看或指定以下选项：  
  
## <a name="options"></a>选项  
  
### <a name="display-options"></a>显示选项  
 **字体名称**  
 显示在跟踪过程中“跟踪结果”网格所使用字体的名称。  
  
 **字号**  
 显示在跟踪过程中“跟踪结果”网格所使用字体的大小。  
  
 **选择字体**  
 打开一个对话框，可以在其中更改字体设置。  
  
 **使用区域设置来显示日期和时间值**  
 使用为计算机配置的区域设置显示日期和时间值。 如果不选择此选项，日期和时间值将采用 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用的固定格式显示，在该格式中包含毫秒。  
  
> [!NOTE]  
>  切换此复选框将更改时间列的显示格式，如 **StartTime** 和 **EndTime**。 但是，此操作不会更改语言事件或远程过程调用 (RPC) 中的 **DateTime** 值参数。  
  
 **在“持续时间”列中以微秒为单位显示值**  
 在跟踪的 **“持续时间”** 数据列中以微秒为单位显示值。 默认情况下， **“持续时间”** 列以毫秒为单位显示值。  
  
### <a name="tracing-options"></a>跟踪选项  
 **建立连接后立即开始跟踪**  
 建立连接后立即使用默认模板开始跟踪。  
  
 **当提供程序版本发生更改时更新跟踪定义**  
 更新提供程序后，为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 应用最新的跟踪定义。 默认情况下不选中此项。 此选项强制 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]在服务器中查询跟踪定义，如果存在，则将在磁盘上重新创建该文件。  
  
### <a name="file-rollover-options"></a>文件滚动更新选项  
 **不作提示，依次加载所有滚动更新文件**  
 在打开跟踪文件时，自动加载滚动更新文件。 如果在跟踪时创建了多个文件，选择此选项可以自动加载所有滚动更新文件。  
  
 **加载滚动更新文件之前进行提示**  
 打开跟踪文件后，让 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 在添加滚动更新文件之前进行提示。  
  
 **从不加载后续滚动更新文件**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 从不在跟踪文件处于打开状态时加载后续滚动更新文件。  
  
### <a name="replay-options"></a>重播选项  
 **默认重播线程数**  
 指定要并发使用的重播线程数。 数目越大，重播期间消耗的资源越多，但是可增加并发的重播事件数目。  
  
 **默认 Health Monitor 等待间隔(秒)**  
 指定重播的等待间隔（秒）。 默认值为 3600 秒（1 小时）。 此设置影响线程在被 Health Monitor 终止前所允许运行的时间。  
  
 **默认 Health Monitor 轮询间隔(秒)**  
 指定重播过程中的 Health Monitor 轮询间隔（秒）。 默认值为 60 秒。 使用此值，用户可以配置 Health Monitor 对终止候选项的轮询频率。  
  
## <a name="see-also"></a>请参阅  
 [连接到服务器后自动启动跟踪 (SQL Server Profiler)](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [设置跟踪显示默认值 (SQL Server Profiler)](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [重播跟踪表 (SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重播跟踪文件 (SQL Server Profiler)](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重播跟踪](../tools/sql-server-profiler/replay-traces.md)   
 [设置全局跟踪选项&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
