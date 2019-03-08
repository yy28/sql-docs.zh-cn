---
title: Microsoft SQL 数据库中的智能查询处理 | Microsoft Docs
description: 智能查询处理功能，用于提高 SQL Server 和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b92bc15079fcc85212ea3d1b51be64a3348a4b1
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305365"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 数据库中的智能查询处理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

智能查询处理 (QP) 功能系列包括可产生广泛影响的功能。 它们最大限度地减少实现工作量，以提升现有工作负载的性能。 为了能够自动受益于此功能系列，请迁移到适用的数据库兼容性级别。

| **IQP 功能** | **在 Azure SQL 数据库中是否受支持** | **在 SQL Server 中是否受支持** |
| --- | --- | --- |
| [自适应联接（批处理模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|
| [非重复近似计数](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | 是，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，公共预览版|
| [行存储上的批处理模式](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|
| [交错执行](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|
| [内存授予反馈（批处理模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|
| [内存授予反馈（行模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|
| [标量 UDF 内联](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | 否，但计划今后推出更新 | 是，自 SQL Server 2019 CTP 2.1 起，兼容性级别为 150，公共预览版|
| [表变量延迟编译](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|



## <a name="adaptive-query-processing"></a>自适应查询处理

自适应查询处理功能系列进行了以下查询处理改进。 这些改进将优化策略调整为适应应用程序工作负载的运行时条件： 
- 批处理模式自适应联接
- 内存授予反馈
- 多语句表值函数 (MSTVF) 交错执行

### <a name="batch-mode-adaptive-joins"></a>批处理模式自适应联接

借助此功能，可以在执行期间使用一个缓存计划，将计划动态切换为采用更优质的联接策略。

有关批处理模式自适应联接的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>行模式和批处理模式内存授予反馈

> [!NOTE]
> 行模式内存授予反馈是一项公共预览版功能。  

此功能重新计算查询所需的实际内存。 然后，它更新缓存计划的授予值。 它减少了影响并发的过多内存授予。 此功能还修复了低估的内存授予，此问题导致代价大的溢出到磁盘。

有关内存授予反馈的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="interleaved-execution-for-mstvfs"></a>适用于 MSTVF 的交错执行

通过交错执行，函数中的实际行计数可用于做出更明智的下游查询计划决策。 若要详细了解多语句表值函数 (MSTVF)，请参阅[表值函数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

有关交错执行的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="table-variable-deferred-compilation"></a>表变量延迟编译

> [!NOTE]
> 表变量延迟编译是公共预览功能。  

表变量延迟编译功能提升了引用表变量的查询的计划质量和整体性能。 在优化和初始编译期间，此功能传播基于实际表变量行计数的基数估计。 这种准确的行计数信息可优化下游计划操作。

表变量延迟编译会延迟编译引用表变量的语句，直到首次实际运行语句为止。 此延迟编译行为与临时表的相同。 此更改导致使用实际基数，而不是原始单行猜测。 

可以在 Azure SQL 数据库中启用表变量延迟编译的公共预览版。 为此，请为要在运行查询时连接到的数据库启用兼容性级别 150。

有关详细信息，请参阅[表变量延迟编译](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation)。

## <a name="scalar-udf-inlining"></a>标量 UDF 内联

> [!NOTE]
> 标量用户定义函数 (UDF) 内联是一项公共预览版功能。  

标量 UDF 内联会自动将[标量 UDF](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) 转换为关系表达式， 并将它们嵌入正在调用的 SQL 查询中。 此转换提升了利用标量 UDF 的工作负载的性能。 标量 UDF 内联可便于实现 UDF 内部基于成本的操作优化。 生成的是高效、面向集、并行的（而不是低效、迭代、串行的）执行计划。 在数据库兼容性级别 150 下默认启用此功能。

有关详细信息，请参阅[标量 UDF 内联](../user-defined-functions/scalar-udf-inlining.md)。

## <a name="approximate-query-processing"></a>近似查询处理

> [!NOTE]
> APPROX_COUNT_DISTINCT 是一项公共预览版功能。  

近似查询处理是新的功能系列。 它可以跨响应速度比绝对精度更为关键的大型数据集进行聚合。 例如，要跨 100 亿行计算 COUNT(DISTINCT())，以供显示在仪表板上。 在这种情况下，绝对精度并不重要，而响应速度则至关重要。 新增的 APPROX_COUNT_DISTINCT 聚合函数返回组中唯一非 NULL 值的近似数。

有关详细信息，请参阅 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="batch-mode-on-rowstore"></a>行存储上的批处理模式 

> [!NOTE]
> 行存储上的批处理模式是一项公共预览版功能。  

行存储上的批处理模式可实现分析工作负载的批处理模式执行，而无需列存储索引。  此功能支持用于磁盘上堆和 B 树索引的批处理模式执行和位图筛选器。 行存储上的批处理模式可实现对所有现有支持批处理模式的运算符的支持。

### <a name="background"></a>背景

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引入了一项可加速分析工作负载的新功能，即列存储索引。 我们扩展了用例，并改进了每个后续版本中列存储索引的性能。 到目前为止，我们已将所有这些功能作为单一功能进行了表述和记录。 可以在表上创建列存储索引。 分析工作负载的速度会变快。 不过，有两套相关但不同的技术：
- 使用列存储索引，分析查询仅访问所需列中的数据。 与传统行存储索引中的压缩相比，列存储格式的页压缩更高效。 
- 使用批处理模式处理，查询运算符可以更高效地处理数据。 它们一次处理一批行，而不是一行。 许多其他可伸缩性改进都与批处理模式处理相关。 若要详细了解批处理模式，请参阅[执行模式](../../relational-databases/query-processing-architecture-guide.md#execution-modes)。

两组功能协同工作，以改进输入/输出 (I/O) 和 CPU 利用率：
- 通过使用列存储索引，更多数据适合内存。 这可以减少 I/O 需求。
- 批处理模式处理可更有效地使用 CPU。

这两种技术尽可能利用彼此。 例如，批处理模式聚合可以计算为列存储索引扫描的一部分。 我们还使用批处理模式联接和批处理模式聚合，更高效地处理使用运行长度编码压缩的列存储数据。 
 
这两种功能可独立使用：
* 获取使用列存储索引的行模式计划。
* 获取仅使用行存储索引的批处理模式计划。 

结合使用这两种功能时，通常效果最佳。 因此，到目前为止，SQL Server 查询优化器仅对涉及至少一个有列存储索引的表的查询考虑使用批处理模式处理。

对于一些应用程序，列存储索引并不是理想选择。 应用程序可能会使用列存储索引不支持的其他一些功能。 例如，就地修改与列存储压缩不兼容。 因此，有聚集列存储索引的表不支持触发器。 更重要的是，列存储索引会增加 DELETE 和 UPDATE 语句的开销。 

对于一些混合事务分析工作负载，工作负载的事务方面开销远比列存储索引的优势重要。 此类方案只能通过批处理模式处理来改进 CPU 利用率。 正因如此，“行存储上的批处理模式”功能对所有查询考虑使用批处理模式。 涉及哪些索引并不重要。

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>可能会受益于行存储上的批处理模式的工作负载

以下工作负载可能会受益于行存储上的批处理模式：
* 工作负载的很大一部分由分析查询组成。 通常情况下，这些查询有联接或聚合等运算符，可处理数十万行或更多行。
* 工作负载受 CPU 限制。 如果瓶颈是 I/O，仍建议尽量考虑使用列存储索引。
* 创建列存储索引会增加太多的工作负载事务部分开销。 或者，创建列存储索引不可行，因为应用程序依赖列存储索引尚不支持的功能。

> [!NOTE]
> 只有通过减少 CPU 利用率，行存储上的批处理模式才能起到帮助作用。 如果瓶颈与 I/O 相关，且数据尚未缓存（“冷”缓存），那么行存储上的批处理模式不会改善运行时间。 同样，如果计算机上没有足够的内存可用来缓存所有数据，性能也不太可能得到提升。

### <a name="what-changes-with-batch-mode-on-rowstore"></a>行存储上的批处理模式带来哪些变化？

除了迁移到兼容性级别 150 之外，无需自行更改任何内容，即可为候选工作负载启用行存储上的批处理模式。

即使查询不涉及任何有列存储索引的表，查询处理器现在也使用启发式方法来决定是否考虑使用批处理模式。 启发式方法包括以下检查：
1. 初始检查输入查询中的表大小、使用的运算符和估计的基数。
2. 其他检查点，因为优化器会发现新的、成本更低的查询计划。 如果这些替代计划没有大量使用批处理模式，优化器会停止探索批处理模式替代方案。

如果使用行存储上的批处理模式，则会发现在查询计划中实际运行模式为批处理模式。 扫描运算符对磁盘堆和 B 树索引使用批处理模式。 此批处理模式扫描可以评估批处理模式位图筛选器。 还可以在计划中看到其他批处理模式运算符。 例如，哈希联接、基于哈希的聚合、排序、窗口聚合、筛选器、串联和计算标量运算符。

### <a name="remarks"></a>Remarks

* 查询计划并不总是使用批处理模式。 查询优化器可能会认为批处理模式对查询没有益处。 
* 查询优化器的搜索空间正在发生变化。 因此，如果获取行模式计划，它可能与在较低兼容性级别获取的计划不同。 另外，如果获取批处理模式计划，它可能与通过列存储索引获取的计划不同。 
* 鉴于新增的行存储上的批处理模式扫描，计划也可能会对混合列存储索引和行存储索引的查询发生变化。
* 新增的行存储上的批处理模式扫描当前存在以下限制： 
    * 它不会为内存中 OLTP 表，或除磁盘堆和 B 树以外的任何索引启动。 
    * 如果提取或筛选大型对象 (LOB) 列，它也不会启动。 此限制包括稀疏列集和 XML 列。
* 有些查询即使使用列存储索引，也无法使用批处理模式。 例如，涉及游标的查询。 这些相同的排除项也扩展到行存储上的批处理模式。

### <a name="configure-batch-mode-on-rowstore"></a>配置行存储上的批处理模式

BATCH_MODE_ON_ROWSTORE 数据库范围内配置默认处于启用状态。 无需更改数据库兼容性级别，即可禁用行存储上的批处理模式：

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

可以通过数据库范围内配置来禁用行存储上的批处理模式。 但仍可使用 ALLOW_BATCH_MODE 查询提示，在查询一级替代设置。 以下示例启用行存储的批处理模式，即使通过数据库作用域配置禁用了该功能：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

还可以使用 DISALLOW_BATCH_MODE 查询提示，对特定查询禁用行存储上的批处理模式。 请参阅以下示例：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>另请参阅

[SQL Server 数据库引擎和 Azure SQL 数据库的性能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)    
[显示计划逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[联接](../../relational-databases/performance/joins.md)    
[演示自适应查询处理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[演示智能 QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
