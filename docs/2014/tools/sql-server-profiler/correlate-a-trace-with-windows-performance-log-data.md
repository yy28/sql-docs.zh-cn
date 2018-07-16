---
title: 将跟踪与 Windows 性能日志数据关联 | Microsoft Docs
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
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e17eddc2b6ff02968709b6f1bb7c8de5557211fa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317487"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>将跟踪与 Windows 性能日志数据关联
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以打开 Microsoft Windows 性能日志、选择要与跟踪关联的计数器，并在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 图形用户界面中将所选性能计数器与跟踪一起显示。 选择跟踪窗口中的事件时， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的系统监视器数据窗口窗格中的红色竖线用于指示与所选跟踪事件关联的性能日志数据。  
  
 若要将跟踪与性能计数器关联，请打开包含 **StartTime** 和 **EndTime** data columns, 和 then click **的** “文件” [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **“导入性能数据”** 。 然后您就可以打开性能日志，选择要与跟踪关联的系统监视器对象和计数器。  
  
## <a name="see-also"></a>请参阅  
 [将跟踪与 Windows 性能日志数据关联 (SQL Server Profiler)](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
