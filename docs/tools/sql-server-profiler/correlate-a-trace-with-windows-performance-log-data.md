---
title: "将跟踪与 Windows 性能日志数据关联 |Microsoft 文档"
ms.custom: 
ms.date: 07/12/2017
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
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: "10"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fc0474e0f3c823b2ca3fa16979e16ff5123f321
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>跟踪与 Windows 性能日志数据关联
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，你可以打开 Microsoft Windows 性能日志、 选择你想要与跟踪，关联的计数器和显示在跟踪旁边的所选的性能计数器[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]图形用户界面。 选择跟踪窗口中的事件时， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的系统监视器数据窗口窗格中的红色竖线用于指示与所选跟踪事件关联的性能日志数据。  
  
 若要将跟踪与性能计数器关联，请打开包含 **StartTime** 和 **EndTime** data columns, 和 then click **的** “文件” [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **“导入性能数据”** 。 然后您就可以打开性能日志，选择要与跟踪关联的系统监视器对象和计数器。  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>将跟踪与性能日志数据关联  
  
1.  在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中，打开保存的跟踪文件或跟踪表。 不能关联仍在收集事件数据的运行中的跟踪。 为实现与系统监视器数据的准确关联，跟踪必须同时包含 **StartTime** 和 **EndTime** 数据列。  
  
2.  在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **“文件”** 菜单上，单击 **“导入性能数据”**。  
  
3.  在 **“打开”** 对话框中，选择包含性能日志的文件。 必须在捕获跟踪数据的同一时间段捕获性能日志数据。  
  
4.  在 **“性能计数器限制”** 对话框中，选中与要显示在跟踪旁边的系统监视器对象和计数器相对应的复选框。 单击 **“确定”**。  
  
5.  在跟踪事件窗口中选择一个事件，或者使用箭头键在跟踪事件窗口的几个相邻行中导航。 **“系统监视器数据”** 窗口中的红色竖线指明与所选跟踪事件关联的性能日志数据。  
  
6.  在系统监视器图形中单击一个相关点。 将选中时间最接近的相应跟踪行。 若要扩大时间范围，请在系统监视器图形中按住并拖动鼠标指针。  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>创建可在 Windows 不同版本间共享的性能日志  
  
1.  在“控制面板”中，打开 **“管理工具”**，再双击 **“性能”**。  
  
2.  在“性能”对话框中，展开“性能日志和警报”，右键单击“计数器日志”，再单击“新建日志设置”。  
  
3.  键入计数器日志的名称，然后单击 **“确定”**。  
  
4.  在 **“常规”** 选项卡中，单击 **“添加计数器”**。  
  
5.  在 **“性能对象”** 列表中，选择要监视的性能对象。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能对象名称以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 开头，命名实例以 MSSQL$*instanceName*开头。  
  
6.  添加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所需的所有计数器和其他重要值（例如处理器时间和磁盘时间）。  
  
7.  添加计数器后，单击 **“关闭”**。  
  
8.  设置 **“数据抽样间隔”** 的值。 开始时使用适中的抽样间隔值（例如 5 分钟），然后在必要时调整间隔值。  
  
9. 在“日志文件”选项卡上，从“日志文件类型”列表中选择“文本文件（逗号分隔）”。 逗号分隔文本日志文件可以在不同版本的 Windows 中共享，并可以稍后在报表工具（例如 Microsoft Excel）中查看。  
  
10. 在 **“计划”** 选项卡上，指定监视计划。  
  
11. 单击 **“确定”** 创建性能日志。  
