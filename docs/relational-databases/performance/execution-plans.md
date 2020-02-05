---
title: 执行计划 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68232021"
---
# <a name="execution-plans"></a>执行计划
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

若要能够执行查询，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 必须分析语句，以确定访问所需数据的最高效方式。 由名为查询优化器的组件来处理此分析。 查询优化器的输入包括查询、数据库方案（表和索引的定义）以及数据库统计信息。 查询优化器的输出称为“查询执行计划”，有时也称为“查询计划”或直接称为“执行计划”。   

查询执行计划定义： 

* 访问源表的顺序。  
  数据库服务器一般可以按许多不同的序列访问基表以生成结果集。 例如，如果 `SELECT` 语句引用三个表，数据库服务器可以先访问 `TableA`，使用 `TableA` 中的数据从 `TableB` 中提取匹配的行，然后使用 `TableB` 中的数据从 `TableC` 中提取数据。 数据库服务器访问表的其他顺序包括：  
  `TableC`、 `TableB`、 `TableA`或  
  `TableB`、 `TableA`、 `TableC`或  
  `TableB`、 `TableC`、 `TableA`或  
  `TableC`、`TableA`、`TableB`  

* 从每个表析取数据的方法。  
  访问每个表中的数据一般也有不同的方法。 如果只需要有特定键值的几行，数据库服务器可以使用索引。 如果需要表中的所有行，数据库服务器则可以忽略索引并执行表扫描。 如果需要表中的所有行，而有一个索引的键列在 `ORDER BY`中，则执行索引扫描而非表扫描可能会省去对结果集的单独排序。 如果表很小，则对该表的几乎所有访问来说，表扫描可能都是最有效的方法。

> [!TIP]
> 有关查询进程和查询执行计划的详细信息，请参阅[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)。

## <a name="in-this-section"></a>本节内容  
  
-   [查询分析基础结构](../../relational-databases/performance/query-profiling-infrastructure.md)  
  
-   [显示和保存执行计划](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [比较和分析执行计划](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [计划指南](../../relational-databases/performance/plan-guides.md)  

## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [性能监视和优化工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)    
 [实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)     
 [活动监视器](../../relational-databases/performance-monitor/activity-monitor.md)     
 [使用查询存储来监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
