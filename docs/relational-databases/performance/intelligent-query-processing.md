---
title: Microsoft SQL 数据库中的智能查询处理 | Microsoft Docs
description: 智能查询处理功能，用于提高 SQL Server 和 Azure SQL 数据库中的查询性能。
ms.custom: ''
ms.date: 03/05/2019
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
ms.openlocfilehash: 6bc44d24631454e792b150750508647019411631
ms.sourcegitcommit: ae333686549dda5993fa9273ddf7603adbbaf452
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59533355"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 数据库中的智能查询处理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

智能查询处理 (QP) 功能系列包含有广泛影响的功能，既能提升现有工作负荷的性能，还能最大限度地减少实现工作量。 

![智能查询处理](./media/3_iqpfeaturefamily.png)

可以通过对数据库启用适当的数据库兼容性级别使工作负荷自动符合只能查询处理条件。 可使用 Transact-SQL 进行此设置。 例如：  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

下表详细列出了所有智能查询处理功能，以及针对数据库兼容性级别必须具备的任何要求。

| **IQP 功能** | **在 Azure SQL 数据库中是否受支持** | **在 SQL Server 中是否受支持** |**Description** |
| --- | --- | --- |--- |
| [自适应联接（批处理模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|自适应联接在运行时期间根据实际输入行自动选择联接类型。|
| [非重复近似计数](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | 是，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，公共预览版|由于高性能和低内存占用量，可针对大数据方案提供近似的 COUNT DISTINCT。 |
| [行存储上的批处理模式](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|可为 CPU 绑定关系的 DW 工作负载提供批处理模式，无需列存储索引。  | 
| [交错执行](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#interleaved-execution-for-mstvfs) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|请使用在首次编译时遇到的多语句表值函数的实际基数，而不是一个固定猜测值。|
| [内存授予反馈（批处理模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | 是，兼容性级别为 140| 是，自 SQL Server 2017 起，兼容性级别为 140|如果批处理模式查询有溢出到磁盘的操作，则需为以后的执行添加更多内存。 如果查询浪费分配给它的超过 50% 内存，请对连续的执行减少内存授予。|
| [内存授予反馈（行模式）](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|如果行模式查询有溢出到磁盘的操作，则需为以后的执行添加更多内存。 如果查询浪费分配给它的超过 50% 内存，请对连续的执行减少内存授予。|
| [标量 UDF 内联](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | 否 | 是，自 SQL Server 2019 CTP 2.1 起，兼容性级别为 150，公共预览版|标量 UDF 将转换为内联在调用查询中的等效关系表达式，这通常会使性能显著提升。|
| [表变量延迟编译](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | 是，兼容性级别为 150，公共预览版| 是，自 SQL Server 2019 CTP 2.0 起，兼容性级别为 150，公共预览版|请使用在首次编译时遇到的表变量的实际基数，而不是一个固定猜测值。|

## <a name="batch-mode-adaptive-joins"></a>批处理模式自适应联接

借助此功能，可以在执行期间使用一个缓存计划，将计划动态切换为采用更优质的联接策略。

通过批处理模式自适应联接功能，可延迟选择[哈希联接或嵌套循环联接](../../relational-databases/performance/joins.md)方法，直到扫描第一个输入后。 自适应联接运算符可定义用于决定何时切换到嵌套循环计划的阈值。 因此，计划可在执行期间动态切换到较好的联接策略。
工作原理如下：
-  如果生成联接输入的行计数足够小，以致于嵌套循环联接优于哈希联接，则计划将切换到嵌套循环算法。
-  如果生成联接输入超过特定行计数阈值，则不会进行切换并且计划将通过哈希联接继续。

以下查询用于说明自适应联接示例：

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

查询将返回 336 行。 启用[实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)后，将看到以下计划：

![查询生成 336 行](./media/4_AQPStats336Rows.png)

在计划中，将看到以下信息：
1. 我们具有用于为哈希联接生成阶段提供行的列存储索引扫描。
1. 我们拥有新的自适应联接运算符。 此运算符可定义用于决定何时切换到嵌套循环计划的阈值。 对于该示例，阈值为 78 行。 包含 &gt;= 78 行的任何示例均将使用哈希联接。 如果小于阈值，将使用嵌套循环联接。
1. 由于我们将返回 336 行，超过了阈值，因此第二个分支表示标准哈希联接操作的探测阶段。 请注意，实时查询统计信息将显示流经运算符的行，在本示例中为“672 行，共 672 行”。
1. 并且，最后一个分支是供未超出阈值的嵌套循环联接使用的聚集索引查找。 请注意，我们将看到显示“0 行，共 336 行”（未使用分支）。
 现将计划与同一查询进行对比，但此次针对表格中只有一行的的 Quantity 值：
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
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
下图显示了哈希联接的成本与嵌套循环联接替代的成本之间的示例交集。  在这个交点处，确定了阈值，该阈值将反过来确定将实际用于联接操作的算法。

![联接阈值](./media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用自适应联接

可在数据库或语句范围内禁用自适应联接，同时将数据库兼容性级别维持在 140 或更高。  
若要对源自数据库的所有查询执行禁用自适应联接，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;
```

启用后，此设置在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 将显示为已启用。
若要对源自数据库的所有查询执行重新启用自适应联接，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

此外，将 `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` 指定为 [USE HINT 查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)也可为特定查询禁用自适应联接。 例如：

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

## <a name="batch-mode-memory-grant-feedback"></a>批处理模式内存授予反馈
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中查询执行后的计划包括执行所需的最小内存和能将所有行纳入内存的理想内存授予大小。 如果内存授予大小不正确，性能将受到影响。 如果授予过量，则会导致内存浪费，减少并发执行。 如果内存授予不足，则会导致到磁盘的昂贵溢出。 通过解决重复工作负荷，批处理模式内存授予反馈可重新计算查询所需的实际内存，并更新缓存计划的授予值。 执行相同的查询语句时，查询将使用修改后的内存授予大小，减少影响并发的过量内存授予，并修复造成到磁盘的昂贵溢出的估计不足的内存授予。
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
如果从缓存中逐出计划，则不会保存反馈。 如果存在故障转移，则反馈也将丢失。 使用 `OPTION (RECOMPILE)` 的语句可创建新的计划，但不会缓存它。 由于它未被缓存，因此不会产生内存授予反馈，也不会针对编译和执行存储。 但是，如果已缓存未使用 `OPTION (RECOMPILE)` 的等效语句（即包含相同的查询哈希）并重新执行，连续语句可从内存授予反馈中受益。

### <a name="tracking-memory-grant-feedback-activity"></a>跟踪内存授予反馈活动
可以使用 memory_grant_updated_by_feedback xEvent 跟踪内存授予反馈事件。 此事件可跟踪当前执行计数历史记录，内存授予反馈更新计划的次数，修改前理想的额外内存授予，以及内存授予反馈修改缓存计划后理想的额外内存授予。

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>内存授予反馈、资源调控器和查询提示
实际内存授予服从资源调控器或查询提示确定的查询内存限制。

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用批处理模式内存授予反馈
可在数据库或语句范围内禁用内存授予反馈，同时将数据库兼容级别维持在 140 或更高。 若要对源自数据库的所有查询执行禁用批处理模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

启用后，此设置在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 将显示为已启用。

若要对源自数据库的所有查询执行重新启用批处理模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

此外，将 `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` 指定为 [USE HINT 查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)也可为特定查询禁用批处理模式内存授予反馈。 例如：

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT 查询提示的优先级高于数据库范围的配置或跟踪标志设置。

## <a name="row-mode-memory-grant-feedback"></a>行模式内存授予反馈
适用对象：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 为公开预览版功能

> [!NOTE]
> 行模式内存授予反馈是一项公共预览版功能。  

通过调整批处理模式和行模式运算符的内存授予大小，行模式内存授予反馈扩展了批处理模式内存授予反馈功能。  

若要在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中启用行模式内存授予反馈的公共预览版，请为执行查询时连接到的数据库启用数据库兼容性级别 150。

通过 memory_grant_updated_by_feedback XEvent，可以查看行模式内存授予反馈活动。 

从行模式内存授予反馈开始，将显示两个新的查询计划属性，用于实际执行后计划：IsMemoryGrantFeedbackAdjusted 和 LastRequestedMemory，它们将添加到 MemoryGrantInfo 查询计划 XML 元素。 

LastRequestedMemory 显示上一次查询执行中的授予内存（以千字节 (KB) 为单位）。 使用 IsMemoryGrantFeedbackAdjusted 属性，可以查看实际查询执行计划内语句的内存授予反馈状态。 下面列出了此属性的可取值：

| IsMemoryGrantFeedbackAdjusted 值 | 描述 |
|---|---|
| No:First Execution | 内存授予反馈不调整用于首次编译和相关执行的内存。  |
| No:Accurate Grant | 如果没有溢出到磁盘，且语句使用至少 50% 的授予内存，就不会触发内存授予反馈。 |
| No:Feedback disabled | 如果内存授予反馈不断触发，且在内存增加和内存减少操作之间波动，就会对语句禁用内存授予反馈。 |
| Yes:Adjusting | 内存授予反馈已应用，并且可能会针对下一次执行进行进一步调整。 |
| Yes:Stable | 内存授予反馈已应用，并且授予内存现在处于稳定状态。也就是说，为上一次执行最后授予的内存是为当前执行授予的内存。 |

> [!NOTE]
> 公共预览版行模式内存授予反馈计划特性在版本 17.9 及更高版本中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 图形查询执行计划内可见。 

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>在不更改兼容级别的情况下禁用行模式内存授予反馈
可在数据库或语句范围内禁用行模式内存授予反馈，同时将数据库兼容级别维持在 150 或更高。 若要对源自数据库的所有查询执行禁用行模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

若要对源自数据库的所有查询重新启用行模式内存授予反馈，请在对应数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

此外，将 `DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK` 指定为 [USE HINT 查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)也可对特定查询禁用行模式内存授予反馈。 例如：

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT 查询提示的优先级高于数据库范围的配置或跟踪标志设置。

## <a name="interleaved-execution-for-mstvfs"></a>适用于 MSTVF 的交错执行

通过交错执行，函数中的实际行计数可用于做出更明智的下游查询计划决策。 若要详细了解多语句表值函数 (MSTVF)，请参阅[表值函数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

交错执行可更改单一查询执行的优化和执行阶段之间的单向边界，并使计划能够根据修订后的基数估值进行调整。 如果遇到交错执行的候选项，该项当前为“多语句表值函数 (MSTVF)”，将暂停优化，执行适用的子树，捕获准确的基数估值，然后针对下游操作继续优化。   

自 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 起，MSTVF 的固定基数猜测为“100”，而早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本为“1”。 交错执行有助于解决由于与 MSTVF 关联的这些固定基数估值而导致的工作负荷性能问题。 有关 MSTVF 的详细信息，请参阅[创建用户定义函数（数据库引擎）](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)。

下图描绘了[实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)输出，一个显示 MSTVF 的固定基数估值影响的整体执行计划的子集。 可查看实际行流与估计行数。 有三个值得注意的计划区域（从右到左显示）：
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
MSTVF 中简单的 `SELECT *` 不会获益于交错执行。

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

启用后，此设置在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 将显示为已启用。
若要对源自数据库的所有查询执行重新启用交错执行，请在适用的数据库的上下文中执行以下命令：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;
```

此外，将 `DISABLE_INTERLEAVED_EXECUTION_TVF` 指定为 [USE HINT 查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)也可对特定查询禁用交错执行。 例如：

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
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
[演示智能 QP](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)   
