---
title: Microsoft SQL 数据库中的智能查询处理 | Microsoft Docs
description: 智能查询处理功能，用于提高 SQL Server 和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 01/11/2019
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
ms.openlocfilehash: 768f9d00e1eea9b97c32d35c240befdaf555122f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254922"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 数据库中的智能查询处理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

“智能查询处理”功能系列包含有广泛影响的功能，以提升现有工作负载的性能，同时最大限度地减少实现工作量。

![“智能查询处理”功能](./media/3_IQPFeatureFamily2.png)

## <a name="adaptive-query-processing"></a>自适应查询处理

“自适应查询处理”功能系列包含查询处理改进，以对应用程序工作负荷的运行时状况采用优化策略。 这些改进功能包括： 
- 批处理模式自适应联接
- 内存授予反馈
- 多语句表值函数 (MSTVF) 交错执行

### <a name="batch-mode-adaptive-joins"></a>批处理模式自适应联接

此功能可让你的计划在使用单个缓存计划执行期间动态切换到更好的连接策略。

有关批处理模式自适应联接的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>行模式和批处理模式内存授予反馈

> [!NOTE]
> 行模式内存授予反馈是一项公共预览版功能。  

此功能会重新计算查询所需的实际内存，然后更新缓存计划的授予值，从而减少影响并发的过度内存授予并修复导致磁盘大量溢出的低估内存授予。

有关内存授予反馈的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>多语句表值函数 (MSTVF) 交错执行

通过交错执行，函数中的实际行计数可用于做出更明智的下游查询计划决策。 有关多语句表值函数 (MSTVF) 的详细信息，请参阅[表值函数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

有关交错执行的详细信息，请参阅 [SQL 数据库中的自适应查询处理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="table-variable-deferred-compilation"></a>表变量延迟编译

> [!NOTE]
> 表变量延迟编译是公共预览功能。  

“表变量延迟编译”功能提升了计划质量和引用表变量的查询的整体性能。 在优化和初始编译期间，此功能会传播基于实际表变量行计数的基数估计。  这种准确的行计数信息将用于优化下游计划操作。

使用“表变量延迟编译”，引用表变量的语句会延迟编译，直到首次实际执行语句后。 此延迟编译行为等同于临时表行为，这一变化会导致使用实际基数，而不是原始的一行猜测。 若要在 Azure SQL 数据库中启用“表变量延迟编译”的公共预览版，请为执行查询时连接到的数据库启用数据库兼容性级别 150。

有关详细信息，请参阅[表变量延迟编译](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation )。

## <a name="scalar-udf-inlining"></a>标量 UDF 内联

> [!NOTE]
> 标量 UDF 内联是公共预览版功能。  

标量 UDF 内联自动将[标量用户定义函数 (UDF)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) 转换为关系表达式，并将其嵌入调用 SQL 查询，从而提高利用标量 UDF 的工作负荷性能。 标量 UDF 内联有助于实现基于成本的 UDF 内部操作优化，并产生面向集合的并行高效计划，而不是低效、迭代、串行执行计划。 在数据库兼容性级别 150 下默认启用此功能。

有关详细信息，请参阅[标量 UDF 内联](../user-defined-functions/scalar-udf-inlining.md)。

## <a name="approximate-query-processing"></a>近似查询处理

> [!NOTE]
> APPROX_COUNT_DISTINCT 是公共预览版功能。  

“近似查询处理”是新功能系列，旨在跨响应速度比绝对精度更为关键的大型数据集进行聚合。  例如，跨 100 亿行计算 COUNT(DISTINCT())，以供显示在仪表板上。  在这种情况下，绝对精度并不重要，关键在于响应速度。 新增的 APPROX_COUNT_DISTINCT 聚合函数返回组中唯一非空值的近似数。

有关详细信息，请参阅 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="batch-mode-on-rowstore"></a>行存储的批处理模式 

> [!NOTE]
> 行存储的批处理模式是公共预览功能。  

### <a name="background"></a>背景

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引入了一项可加速分析工作负荷的新功能：列存储索引。 我们扩展了用例并改进了每个后续版本中列存储索引的性能。 到目前为止，我们已将所有这些功能作为单一功能进行了表述和记录：可以在表上创建列存储索引，这样分析工作负载“会更快”。 然而，事实上，有两套相关但不同的技术：
- 列存储索引允许分析查询仅访问所需列中的数据。 与传统“行存储”索引中的页压缩相比，列存储格式还允许更有效的压缩。 
- **批处理模式**处理允许查询运算符更有效地处理数据，方法是一次处理一批行，而不是一次一行。 许多其他可伸缩性改进都与批处理模式处理相关。 有关批处理模式的详细信息，请参阅[执行模式](../../relational-databases/query-processing-architecture-guide.md#execution-modes)。

两组功能协同工作以提高 I/O 和 CPU 利用率：
- 列存储索引允许更多数据适应内存，从而减少对 I/O 的需求。
- 批处理模式处理可更有效地使用 CPU。

这两种技术尽可能利用彼此。 例如，批处理模式聚合可以计算为列存储索引扫描的一部分。 通过批处理模式联接和批处理模式聚合，我们还可更有效地处理使用运行长度编码压缩的列存储数据。 
 
这两项功能已单独可用：可以获取使用列存储索引的行模式计划，并可获取仅使用行存储索引的批处理模式计划。 但是由于在大多数情况下这两项功能一起使用时可获得最佳结果，因此 SQL 的查询优化器直到现在仅对涉及至少一个具有列存储索引的表的查询考虑批处理模式处理。

对于某些应用程序，列存储索引并非可行的选项，因为应用程序使用列存储索引不支持的一些其他功能（例如，具有群集列存储索引的表不支持触发器）。 更重要的是，列存储索引会增加 DELETE 和 UPDATE 语句的开销，因为就地修改与列存储压缩不兼容。 对于某些混合事务分析工作负载，列存储索引将为分析查询带来的优势会被工作负载的事务方面的开销所抵消。 此类方案仅能从批处理模式处理中提高 CPU 利用率，这就是为什么**行存储的批处理模式**功能将为所有查询考虑批处理模式，而不管所涉及的索引如何。

### <a name="what-workloads-may-benefit-from-batch-mode-on-rowstore"></a>哪些工作负载可能会受益于行存储的批处理模式

以下工作负载可能会受益于行存储的批处理模式：
1. 工作负载的重要部分包括分析查询（根据经验，是带有运算符的查询，例如处理数十万行或更多行的联接或聚合），并且
2. 工作负载受 CPU 约束（如果瓶颈是 IO，在可能的情况下仍建议考虑列存储索引），并且
3. 创建列存储索引会给工作负载的事务部分增加过多开销，或者创建列存储索引不可行，因为应用程序依赖于列存储索引尚不支持的功能。

> [!NOTE]
> 行存储的批处理模式只能通过减少 CPU 使用来提供帮助。 如果瓶颈与 IO 相关，并且数据尚未缓存（“冷”缓存），则行存储的批处理模式不会改善运行时间。 同样，如果计算机上没有足够的内存来缓存所有数据，性能也不可能得到提高。

### <a name="what-changes-with-batch-mode-on-rowstore"></a>行存储的批处理模式有哪些更改

除了迁移到兼容性级别 150 之外，无需更改任何内容，即可为候选工作负载启用行存储的批处理模式。

即使查询不涉及任何具有列存储索引的表，查询处理器现在也使用启发式方法来决定是否考虑批处理模式。 启发式方法包括：
1. 初始检查输入查询中的表大小、使用的运算符和估计的基数。
2. 其他检查点，因为优化器会发现新的、成本更低的查询计划。 如果这些替代计划没有大量使用批处理模式，优化器将停止探索批处理模式替代方案。

如果使用行存储的批处理模式，则在查询执行计划中将看到实际的执行模式为扫描运算符用于磁盘堆和 B 树索引的“批处理模式”。  此批处理模式扫描可以评估批处理模式位图筛选器。  还可以在计划中看到其他批处理模式运算符，例如哈希联接、基于哈希的聚合、排序、窗口聚合、筛选器、串联和计算标量运算符。

### <a name="remarks"></a>Remarks

1. 无法保证查询计划将使用批处理模式。 查询优化器可能会认为批处理模式对查询没有益处。 
2. 由于查询优化器的搜索空间在不断变化，并不能保证如果获取行模式计划，它将与在较低兼容性级别中获取的计划相同。 同样无法保证，如果获取批处理模式计划，它将与在列存储索引中获取的计划相同。 
3. 由于新的批处理模式行存储扫描，计划也可能针对混合列存储和行存储索引的查询以微妙的方式更改。
4. 行存储扫描上新批处理模式的当前限制：它不会为内存中 OLTP 表，或者磁盘堆和 B 树以外的任何索引启动。 如果提取或筛选出 LOB 列，它也不会启动。 此限制包括稀疏列集和 XML 列。
5. 有些查询即使具有列存储索引（例如涉及游标的查询），也不会使用批处理模式，并且这些相同的排除也扩展到行存储的批处理模式。

### <a name="configuring-batch-mode-on-rowstore"></a>配置行存储的批处理模式

BATCH_MODE_ON_ROWSTORE 数据库作用域配置默认情况下处于启用状态，并且可用于禁用行存储的批处理模式，而无需更改数据库兼容性级别：

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

可以通过数据库作用域配置禁用行存储的批处理模式，但仍使用 ALLOW_BATCH_MODE 查询提示替代查询级别的设置。 以下示例启用行存储的批处理模式，即使通过数据库作用域配置禁用了该功能：

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

还可以通过使用 DISALLOW_BATCH_MODE 查询提示为特定查询禁用行存储的批处理模式。 例如：

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
[Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[联接](../../relational-databases/performance/joins.md)    
[演示自适应查询处理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[演示智能 QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
