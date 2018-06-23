---
title: SQL Server 事件探查器的源表数据库引擎优化顾问-选择工作负荷表 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8b5ccfddb032fb3833e517632290cfdf7d82e643
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016181"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>SQL Server 事件探查器的源表数据库引擎优化顾问-选择工作负荷表
  Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]和 [!INCLUDE[ssDE](../includes/ssde-md.md)]优化顾问使用此对话框来选择表。  
  
 在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 中，使用“源表”对话框为跟踪表指定源表。 This is a table from which a trace is loaded, and the contents of which are viewed or used for replaying the trace.  
  
 在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 优化顾问中，使用“选择工作负荷表”对话框选择包含 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 跟踪信息的数据库表，以用作优化工作负荷或在开始优化分析前预览表的内容。  
  
## <a name="options"></a>“常规”  
 **SQL Server**  
 指定当前连接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例。 此字段将自动填充，并且无法更新。  
  
 **“数据库”**  
 指定跟踪表所在的数据库。  
  
 **“所有者”**  
 Specifies the owner of the trace table. 此字段将自动填充为 **dbo**。  
  
 **表**  
 指定将从中读取跟踪的跟踪表的名称。  
  
## <a name="see-also"></a>请参阅  
 [将跟踪结果保存到表&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [数据库引擎优化顾问](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  