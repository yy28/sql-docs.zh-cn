---
title: Microsoft SQL 数据库中的自适应查询处理 | Microsoft Docs | Microsoft Docs
description: 自适应查询处理功能，用于提高 SQL Server（2017 及更高版本）和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 05/08/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 464696823e99e81a763fbbc4a2835c86ef9bea5c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="adaptive-query-processing-in-sql-databases"></a>SQL 数据库中的自适应查询处理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文将介绍以下自适应查询处理功能，这些功能可用于提高 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 开始）和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中的查询性能：
- 批处理模式内存授予反馈。
- 批处理模式自适应联接。
- 交错执行。 

一般而言，SQL Server 执行查询的过程如下所示：
1. 查询优化过程为特定查询生成一组可行的执行计划。 在此期间，估计计划选项的成本并使用估价最低的计划。
1. 查询执行过程采用查询优化器所选的计划，并将它用于执行。
    
有时，出于各种原因，查询优化器所选计划不是最优计划。 例如，预计流经查询计划的行数可能不正确。 估计成本有助于确定选择用于执行的计划。 如果基数估计不正确，不管最初的假设有多差劲，仍会使用原计划。

![自适应查询处理功能](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>如何启用自适应查询处理
可以通过对数据库启用兼容性级别 140 使工作负荷自动符合自适应查询处理条件。  可使用 Transact-SQL 进行此设置。 例如：  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```

## <a name="batch-mode-memory-grant-feedback"></a>批处理模式内存授予反馈
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中查询执行后的计划包括执行所需的最小内存和能将所有行纳入内存的理想内存授予大小。 如果内存授予大小不正确，性能将受到影响。 如果授予过量，则会导致内存浪费，减少并发执行。 如果内存授予不足，则会导致到磁盘的昂贵溢出。 通过解决重复工作负荷，批处理模式内存授予反馈可重新计算查询所需的实际内存，并更新缓存计划的授予值。  执行相同的查询语句时，查询将使用修改后的内存授予大小，减少影响并发的过量内存授予，并修复造成到磁盘的昂贵溢出的估计不足的内存授予。
下图是使用批处理模式自适应内存授予反馈的一个示例。 对于首次执行查询，由于高溢出，持续时间为 88 秒：   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![高溢出](./media/2_AQPGraphHighSpills.png)

启用内存授予反馈后，对于第二次执行，持续时间为 1 秒（从 88 秒减少），完全消除溢出，且授予内存更高： 

![无溢出](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>内存授予反馈大小调整
对于内存授予过量的情况，如果授予的内存是实际使用内存大小的两倍，内存授予反馈将重新计算内存授予并更新缓存的计划。 内存授予不足 1 MB 的计划将不会针对超额重新进行计算。
对于内存授予大小不足，造成批处理模式运算符溢出到磁盘的情况，内存授予反馈将触发内存授予的重新计算。 将向内存授予反馈报告溢出事件，并可通过 spilling_report_to_memory_grant_feedback xEvent 显露。 此事件将返回计划的节点 ID 和该节点溢出的数据大小。

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>内存授予反馈和参数敏感型方案
为保持最优，不同的参数值可能还需要不同的查询计划。 此类查询被定义为“参数敏感型”。 对于参数敏感型计划，如果查询具有不稳定的内存要求，则内存授予反馈对该查询禁用。 在重复运行查询后禁用计划，并且可以通过监视 memory_grant_feedback_loop_disabled xEvent 观察到这一切。 有关参数截取和参数敏感度的详细信息，请参阅[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。

### <a name="memory-grant-feedback-caching"></a>内存授予反馈缓存
反馈可以存储在单个执行的缓存计划中。 它是该语句的连续执行，但受益于内存授予反馈调整。 此功能适用于重复执行语句。 内存授予反馈将只更改缓存的计划。 当前未在查询存储中捕获更改。
如果从缓存中逐出计划，则不会保存反馈。 如果存在故障转移，则反馈也将丢失。 使用 `OPTION (RECOMPILE)` 的语句可创建新的计划，但不会缓存它。 由于它未被缓存，因此不会产生内存授予反馈，也不会针对编译和执行存储。  但是，如果已缓存未使用 `OPTION (RECOMPILE)` 的等效语句（即包含相同的查询哈希）并重新执行，连续语句可从内存授予反馈中受益。

### <a name="tracking-memory-grant-feedback-activity"></a>跟踪内存授予反馈活动
可以使用 memory_grant_updated_by_feedback xEvent 跟踪内存授予反馈事件。 此事件可跟踪当前执行计数历史记录，内存授予反馈更新计划的次数，修改前理想的额外内存授予，以及内存授予反馈修改缓存计划后理想的额外内存授予。

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>内存授予反馈、资源调控器和查询提示
实际内存授予服从资源调控器或查询提示确定的查询内存限制。

### <a name="disabling-memory-grant-feedback-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用内存授予反馈
可在数据库或语句范围内禁用内存授予反馈，同时将数据库兼容级别维持在 140 或更高。 若要对源自数据库的所有查询执行禁用批处理模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

禁用后，此设置在 sys.database_scoped_configurations 将显示为已启用。

若要对源自数据库的所有查询执行重新启用批处理模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

此外，将 DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK 指定为 USE HINT 查询提示也可对特定查询禁用批处理模式内存授予反馈。  例如：

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT 查询提示的优先级高于数据库范围的配置或跟踪标志设置。

## <a name="batch-mode-adaptive-joins"></a>批处理模式自适应联接
通过批处理模式自适应联接功能，可延迟选择[哈希联接或嵌套循环联接](../../relational-databases/performance/joins.md)方法，直到扫描第一个输入后。 自适应联接运算符可定义用于决定何时切换到嵌套循环计划的阈值。 因此，计划可在执行期间动态切换到较好的联接策略。
工作原理如下：
-  如果生成联接输入的行计数足够小，以致于嵌套循环联接优于哈希联接，则计划将切换到嵌套循环算法。
-  如果生成联接输入超过特定行计数阈值，则不会进行切换并且计划将通过哈希联接继续。

以下查询用于说明自适应联接示例：

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

查询将返回 336 行。 启用[实时查询统计信息](../../relational-databases/performance/live-query-statistics.MD)后，将看到以下计划：

![查询生成 336 行](./media/4_AQPStats336Rows.png)

在计划中，将看到以下信息：
1. 我们具有用于为哈希联接生成阶段提供行的列存储索引扫描。
1. 我们拥有新的自适应联接运算符。 此运算符可定义用于决定何时切换到嵌套循环计划的阈值。 对于该示例，阈值为 78 行。 包含 &gt;= 78 行的任何示例均将使用哈希联接。 如果小于阈值，将使用嵌套循环联接。
1. 由于我们将返回 336 行，超过了阈值，因此第二个分支表示标准哈希联接操作的探测阶段。 请注意，实时查询统计信息将显示流经运算符的行，在本示例中为“672 行，共 672 行”。
1. 并且，最后一个分支是供未超出阈值的嵌套循环联接使用的聚集索引查找。 请注意，我们将看到显示“0 行，共 336 行”（未使用分支）。
 现将计划与同一查询进行对比，但此次针对表格中只有一行的的 Quantity 值：
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
查询将返回一行。 启用实时查询统计信息后，将看到以下计划：

![查询生成一行](./media/5_AQPStatsOneRow.png)

在计划中，将看到以下信息：
- 返回一行后，聚集索引搜索现已有行流经它。
- 并且，由于哈希联接生成阶段未继续进行，因此没有行流经第二个分支。

### <a name="adaptive-join-benefits"></a>自适应联接优点
小型和大型联接输入扫描之间频繁振荡的工作负荷将从此功能获益最大。

### <a name="adaptive-join-overhead"></a>自适应联接开销
自适应联接引入了比索引嵌套循环联接等效计划更高的内存要求。 它会请求额外的内存，就像嵌套循环属于哈希联接一样。 此外还有作为断断续续操作而不是嵌套循环流式处理等效联接的生成阶段的开销。 这笔额外成本产生的同时也实现了行计数可在生成输入中波动的方案灵活性。

### <a name="adaptive-join-caching-and-re-use"></a>自适应联接缓存和重复使用
批处理模式自适应联接适用于语句的初始执行，编译后，根据编译的自适应联结阈值和流经外部输入生成阶段的运行时行，连续执行将保持自适应状态。

### <a name="tracking-adaptive-join-activity"></a>跟踪自适应联接活动
自适应联接运算符具有以下计划运算符属性：

| 计划属性 | 描述 |
|--- |--- |
| AdaptiveThresholdRows | 显示用于从哈希联接切换到嵌套循环联接的阈值。 |
| EstimatedJoinType | 可能的联接类型。 |
| ActualJoinType | 在实际计划中，显示根据阈值最终选择的联接算法。 |

估计的计划显示自适应联接计划形状，以及定义的自适应联接阈值和估计的联接类型。

### <a name="adaptive-join-and-query-store-interoperability"></a>自适应联接和查询存储互操作性
查询存储可捕获并强制执行批处理模式自适应联接计划。

### <a name="adaptive-join-eligible-statements"></a>符合自适应联接条件的语句
以下多个条件可使逻辑联接符合批处理模式自适应联接的条件：
- 数据库兼容级别为 140。
- 查询是 SELECT 语句（数据修改语句当前不符合条件）。
- 联接符合同时由索引嵌套循环联接或哈希联接物理算法执行的条件。
- 哈希联接将通过整体查询中的列存储索引状态或联接正在直接引用的列存储索引表使用批处理模式。
- 嵌套循环联接和哈希联接生成的替代解决方案的第一个子级（外部引用）应相同。

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>自适应联接和嵌套循环效率
如果自适应联接切换到嵌套循环操作，它将使用哈希联接生成已经读取的行。 运算符不会再次重新读取外部引用行。

### <a name="adaptive-threshold-rows"></a>自适应阈值行
下图显示了哈希联接的成本与嵌套循环联接替代的成本之间的示例交集。  在这个交点处，确定了阈值，该阈值将反过来确定将实际用于联接操作的算法。

![联接阈值](./media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用自适应联接

可在数据库或语句范围内禁用自适应联接，同时将数据库兼容性级别维持在 140 或更高。  
若要对源自数据库的所有查询执行禁用自适应联接，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;
```

禁用后，此设置在 sys.database_scoped_configurations 将显示为已启用。
若要对源自数据库的所有查询执行重新启用自适应联接，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

此外，将 DISABLE_BATCH_MODE_ADAPTIVE_JOINS 指定为 USE HINT 查询提示也可对特定查询禁用自适应联接。  例如：

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

USE HINT 查询提示的优先级高于数据库范围的配置或跟踪标志设置。

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>多语句表值函数的交错执行
交错执行可更改单一查询执行的优化和执行阶段之间的单向边界，并使计划能够根据修订后的基数估值进行调整。 如果遇到交错执行的候选项，该项当前为多语句表值函数 (MSTVF)，将暂停优化，执行适用的子树，捕获准确的基数估值，然后针对下游操作继续优化。
在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中，MSTVF 具有固定的基数猜测“100”，而早期版本为“1”。 交错执行有助于解决由于与多语句表值函数相关联的这些固定基数估值而产生的工作负荷性能问题。

下图描绘了实时查询统计信息输出，一个显示 MSTVF 的固定基数估值影响的整体执行计划的子集。 可查看实际行流与估计行数。 有三个值得注意的计划区域（从右到左显示）：
1. MSTVF 表扫描具有 100 行的固定估值。 然而，对于此示例，有 527,597 行流经此 MSTVF 表扫描，如通过“527597 行，共 100 行”的实际与估值的实时查询统计信息中所示，因此固定估值偏差显著。
1. 对于嵌套循环操作，仅假定联接的外侧将返回 100 行。 如果 MSTVF 实际返回惊人的行数，最好将另一联接算法一起使用。
1. 对于哈希匹配操作，请注意小型警告符号，在本示例中指示到磁盘的溢出。

![行流与估计行数](./media/7_AQPFlowThreeAreas.png)

将之前的计划与通过启用交替执行生成的实际计划进行对比：

![交错的计划](./media/8_AQPInterleavedEnabledPlan.png)

1. 请注意，MSTVF 表扫描现可反映准确的基数估值。 另请注意此表扫描的重新排序和其他操作。
1. 而关于联接算法，我们已改为从嵌套循环操作切换到哈希匹配操作，后者在涉及大量行时更优。
1. 另请注意，我们不再发出溢出警告，因为我们将基于从 MSTVF 表扫描流出的真实行数授予更多内存。

### <a name="interleaved-execution-eligible-statements"></a>交错执行符合条件的语句
交错执行中的 MSTVF 引用语句当前必须处于只读，且不为数据修改操作的一部分。 此外，如果 MSTVF 不使用运行时常数，则其不适合用于交错执行。

### <a name="interleaved-execution-benefits"></a>交错执行的优点
一般情况下，估计行数与实际行数之间的偏差越大，下游计划操作数翻倍，则性能影响越大。
一般来说，交错执行有益于以下情况中的查询：
1. 对于中间结果集（本例中为 MSTVF），估计行数和实际行数之间存在巨大偏差。
1. 整体查询对中间结果的大小更改十分敏感。 这通常发生在查询计划中的该子树上存在复杂树的情况。
MSTVF 中简单的“SELECT*”不会获益于交错执行。

### <a name="interleaved-execution-overhead"></a>交错执行的开销
开销应为最少-到-无。 MSTVF 已在引入交错执行前具体化，但区别是现在已允许延迟优化，并可利用具体化行集的基数估值。
与任何影响计划的更改一样，某些计划更改后虽可获得更好的子树基数，但同时也会使整体查询计划变得更糟。 缓解可包括还原兼容级别或使用查询存储来强制计划的非回归版本。

### <a name="interleaved-execution-and-consecutive-executions"></a>交错执行和连续执行
缓存交错执行计划后，包含首次执行的修订后的估值的计划将用于连续执行，无需重新实例化交错执行。

### <a name="tracking-interleaved-execution-activity"></a>跟踪交错执行活动
可在实际查询执行计划中查看使用情况属性：

| 执行计划属性 | 描述 |
| --- | --- |
| ContainsInterleavedExecutionCandidates | 适用于 QueryPlan 节点。 如果为“true”，表示计划包含交错执行候选项。 |
| IsInterleavedExecuted | TVF 节点的 RelOp 下的 RuntimeInformation 元素的属性。 如果为“true”，表示该操作已具体化为交错执行操作的一部分。 |

还可以通过以下 xEvent 跟踪交错执行匹配项：

| XEvent | 描述 |
| ---- | --- |
| interleaved_exec_status | 发生交错执行时将引发此事件。 |
| interleaved_exec_stats_update | 此事件介绍交错执行更新的基数估值。 |
| Interleaved_exec_disabled_reason | 包含交错执行可能的候选项的查询实际未获取交错执行时，将引发此事件。 |

必须执行查询才能允许交错执行修改 MSTVF 基数估值。 但是，如果通过 `ContainsInterleavedExecutionCandidates` 显示计划属性存在交错执行候选项，则估计的执行计划仍将显示。    

### <a name="interleaved-execution-caching"></a>交错执行缓存
如果已从缓存中逐出或清除计划，则在执行查询时将出现使用交错执行的全新编译。
使用 `OPTION (RECOMPILE)` 的语句将创建使用交错执行的新计划，但不会进行缓存。     

### <a name="interleaved-execution-and-query-store-interoperability"></a>交错执行和查询存储互操作性
无法强制使用交错执行的计划。 该计划是具有基于初始执行的正确基数估值的版本。    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用交错执行

可在数据库或语句范围内禁用交错执行，同时将数据库兼容性级别维持在 140 或更高。  若要对源自数据库的所有查询执行禁用交错执行，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;
```

禁用后，此设置在 sys.database_scoped_configurations 将显示为已启用。
若要对源自数据库的所有查询执行重新启用交错执行，请在适用的数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;
```

此外，将 DISABLE_INTERLEAVED_EXECUTION_TVF 指定为 USE HINT 查询提示也可对特定查询禁用交错执行。  例如：

```sql
SELECT  [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

USE HINT 查询提示的优先级高于数据库范围的配置或跟踪标志设置。

## <a name="see-also"></a>另请参阅
[SQL Server 数据库引擎和 Azure SQL 数据库的性能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)    
[Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[联接](../../relational-databases/performance/joins.md)    
[演示自适应查询处理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)          

