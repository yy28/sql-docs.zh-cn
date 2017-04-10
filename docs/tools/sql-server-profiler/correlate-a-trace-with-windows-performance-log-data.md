---
title: "将跟踪与 Windows 性能日志数据关联 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "将跟踪与日志数据关联"
  - "日志 [SQL Server], 跟踪"
  - "Profiler [SQL Server Profiler], 将跟踪与日志数据关联"
  - "跟踪 [SQL Server], 日志"
  - "SQL Server Profiler, 将跟踪与日志数据关联"
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 将跟踪与 Windows 性能日志数据关联
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以打开 Microsoft Windows 性能日志、选择要与跟踪关联的计数器，并在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 图形用户界面中将所选性能计数器与跟踪一起显示。 选择跟踪窗口中的事件时， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的系统监视器数据窗口窗格中的红色竖线用于指示与所选跟踪事件关联的性能日志数据。  
  
 若要将跟踪与性能计数器关联，请打开包含 **StartTime** 和 **EndTime** data columns, 和 then click **的** “文件” [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **“导入性能数据”** 。 然后您就可以打开性能日志，选择要与跟踪关联的系统监视器对象和计数器。  
  
## 另请参阅  
 [将跟踪与 Windows 性能日志数据关联 (SQL Server Profiler)](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  