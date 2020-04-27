---
title: SQL Server Profiler 源表-数据库引擎优化顾问-选择工作负荷表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 973680d07c3bd6a304e63f4b3fde0e228f0f7bff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088883"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>SQL Server Profiler 源表-数据库引擎优化顾问-选择工作负荷表
  Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]和 [!INCLUDE[ssDE](../includes/ssde-md.md)]优化顾问使用此对话框来选择表。  
  
 在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 中，使用****“源表”对话框为跟踪表指定源表。 源表是一个加载跟踪的表，重播跟踪时需要查看或使用其内容。  
  
 在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 优化顾问中，使用****“选择工作负荷表”对话框选择包含 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 跟踪信息的数据库表，以用作优化工作负荷或在开始优化分析前预览表的内容。  
  
## <a name="options"></a>选项  
 **SQL Server**  
 指定当前连接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例。 此字段将自动填充，并且无法更新。  
  
 **Database**  
 指定跟踪表所在的数据库。  
  
 **所有者**  
 Specifies the owner of the trace table. 此字段将自动填充为 **dbo**。  
  
 **表**  
 指定将从中读取跟踪的跟踪表的名称。  
  
## <a name="see-also"></a>另请参阅  
 [将跟踪结果保存到表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
