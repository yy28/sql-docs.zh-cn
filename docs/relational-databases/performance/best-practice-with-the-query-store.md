---
title: Query Store 最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4627118daa91305dc905eb5f306e6bd2fcc1b91c
ms.sourcegitcommit: 7625f78617a5b4fd0ff68b2c6de2cb2c758bb0ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71163889"
---
# <a name="best-practice-with-the-query-store"></a>Query Store 最佳实践
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本文概述使用查询存储处理工作负载的最佳实践。  
  
##  <a name="SSMS"></a>使用最新 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 设计各种用户界面的目的是方便用户对查询存储进行配置和使用收集的工作负荷数据。  
单击[此处](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)下载最新版 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
 有关如何使用查询存储进行方案故障排除的快速说明，请参阅 [@Azure博客中的查询存储](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
##  <a name="Insight"></a>在 Azure SQL 数据库中使用 Query Performance Insight  
 如果你在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中运行 Query Store，则可使用 **Query Performance Insight** 来分析一定时段内的 DTU 消耗情况。  
虽然可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来获取所有查询的详细资源消耗情况（CPU、内存、I/O 等），但使用 Query Performance Insight 可以快速且有效地确定查询对数据库总体 DTU 消耗情况的影响。  
有关详细信息，请参阅 [Azure SQL Database Query Performance Insight](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)（Azure SQL 数据库的 Query Performance Insight）。    

##  <a name="using-query-store-with-elastic-pool-databases"></a>将 Query Store 与弹性池数据库配合使用
可以毫无顾忌地在所有数据库中使用 Query Store，甚至是在密集打包的池中。 与过多资源使用（为弹性池中的大量数据库启用了 Query Store 时可能会遇到这种情况）相关的所有问题都已得到了解决。

##  <a name="Configure"></a> 始终根据工作负载调整查询存储  
 根据工作负荷和性能故障排除要求来配置 Query Store。   
默认参数是启动的理想参数，但应监视查询存储在一定时段内的行为表现，并对其配置进行相应的调整：  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 下面是设置参数值时应遵循的准则：  
  
 **最大大小 (MB)：** 为查询存储在数据库中占用的数据空间指定一个限制。 这是最重要的设置，直接影响 Query Store 的操作模式。  
  
 当 Query Store 收集查询、执行计划和统计信息时，其在数据库中的大小会一直增长，直至达到此限制。 达到此限制后，Query Store 会自动将操作模式更改为只读，并停止收集新数据，这意味着你的性能分析自此不再精确。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中的默认值为 100 MB，如果你的工作负荷会生成大量不同的查询和计划，或者你想要让查询历史记录保存较长的时间，则默认值可能不够大。 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始，默认值是 1 GB。 跟踪当前的空间使用情况，增大“最大大小(MB)”以防 Query Store 转换到只读模式。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或执行以下脚本，以便获取有关 Query Store 大小的最新信息：  
  
```sql 
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 以下脚本将设置新的“最大大小(MB)”：  
  
```sql  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  

 **数据刷新间隔：** 定义将收集的运行时统计信息保存到磁盘的频率（以秒为单位，默认为 900 秒，即 15 分钟）。 如果工作负荷不生成大量不同的查询和计划或者你能够在数据库关闭之前撑住更长时间来保留数据，请考虑使用更高的值。 
 
> [!NOTE]
> 如果出现故障转移或关闭命令，使用跟踪标志 7745 会阻止查询存储数据写入磁盘。 请查阅[在任务关键型服务器上使用跟踪标志改善灾难恢复](#Recovery)部分，了解详情。

使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 为数据刷新间隔设置不同的值：  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);  
```  

 **统计信息收集间隔：** 定义已收集的运行时统计信息的粒度级别（默认值为 60 分钟）。 如果你需要更细的粒度或更短的时间来检测问题和解决问题，则可考虑使用更低的值，但请记住，这会直接影响 Query Store 数据的大小。 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 为统计信息收集间隔设置不同的值：  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);  
```  
  
 **过时查询阈值（天）：** 基于时间的清除策略，用于控制持久化运行时统计信息和非活动查询的保持期。  
默认情况下，查询存储配置为将数据保留 30 天，这对于你的方案来说可能过长了。  
  
 避免保留你不计划使用的历史数据。 这样可以减少变为只读状态的次数。 Query Store 数据的大小以及检测问题和解决问题的时间将会变得更可预测。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或以下脚本配置基于时间的清理策略：  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));  
```  
  
 **基于大小的清除模式：** 指定在 Query Store 数据大小达到限制时，是否启用自动数据清理功能。  
  
 强烈建议你激活基于大小的清理功能，确保 Query Store 始终以读写模式运行并收集最新数据。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **查询存储捕获模式：** 指定查询存储的查询捕获策略。  
  
-   **All** - 捕获所有查询。 这是 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中的默认选项。  
  
-   **Auto** - 忽略不太频繁的查询以及编译和执行持续时间不长的查询。 执行计数、编译和运行时持续时间的阈值由内部决定。 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始，这是默认选项。  
  
-   **None** - 查询存储停止捕获新查询。  

-   **Custom** - 允许其他控件和微调数据收集策略。 新的自定义设置定义在内部捕获策略时间阈值（计算可配置条件的时间边界）内执行的操作，如果所有值为 true，则查询存储可以捕获查询。
  
 以下脚本将“查询捕获模式”设置为“Auto”：  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  

### <a name="examples"></a>示例
以下示例将“查询捕获”模式设置为“自动”，并在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中设置其他建议选项：  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```  

以下示例将“查询捕获”模式设置为“自动”，并在 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中设置其他建议选项以包括等待统计信息：  

```sql
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

下面的示例将“查询捕获”模式设置为“自动”，并在 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 中设置其他建议选项，同时视需要  使用默认值设置自定义捕获策略，而不使用新的默认捕获模式“自动”：  

```sql
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE = ON 
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100 
      )
    );
```

## <a name="how-to-start-with-query-performance-troubleshooting"></a>如何开始进行查询性能故障排除  
 Query Store 工作流的故障排除很简单，如下图所示：  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 按上一节的说明通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来启用 Query Store，或者执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
```sql  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  

Query Store 收集能够准确代表工作负荷的数据集需要一定的时间。 通常情况下，即使是很复杂的工作负荷，一天的时间也足够了。 但是，在启用此功能后，你就可以立即开始浏览数据并确定需要注意的查询。   
导航到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的对象资源管理器中数据库节点下的 Query Store 子文件夹，以便打开特定方案的故障排除视图。   
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 查询存储视图在操作时使用一组执行度量值，每个度量值都表示为下述任意统计函数：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|执行度量值|统计函数|  
|----------------------|----------------------|------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|CPU 时间、持续时间、执行计数、逻辑读取次数、逻辑写入次数、内存消耗、物理读取次数、CLR 时间、并行度 (DOP) 和行计数|平均值、最大值、最小值、标准偏差、总数|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|CPU 时间、持续时间、执行计数、逻辑读取次数、逻辑写入次数、内存消耗、物理读取次数、CLR 时间、并行度 (DOP)、行计数、日志内存、TempDB 内存和等待时间|平均值、最大值、最小值、标准偏差、总数|
  
 下图显示了如何查找 Query Store 视图：  
  
 ![查询存储视图](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "Query Store views")  
  
 下表说明了何时使用每个 Query Store 视图：  
  
|SSMS 视图|应用场景|  
|---------------|--------------|  
|回归查询|查明哪些查询的执行度量值最近进行了回归（即变得更糟）。 <br />使用此视图将应用程序中观察到的性能问题与需要进行修复或改进的实际查询关联起来。|  
|总体资源消耗|针对任意执行度量值分析数据库的总资源消耗量。<br />使用此视图可以确定资源模式（白天工作负荷与夜间工作负荷的比较），并优化数据库的总体消耗。|  
|资源使用排名靠前的查询|选择所关注的执行度量值，确定在指定的时间间隔内哪些查询的值最极端。 <br />此视图可以帮助你关注最相关的查询，这些查询对数据库资源消耗的影响最大。|  
|具有强制计划的查询|使用查询存储列出以前的强制计划。 <br />使用此视图快速访问当前的所有强制计划。|  
|变化程度高的查询|分析执行变化程度较高的查询，因为此类查询与任何可用的维度相关，例如所需时间间隔内的持续时间、CPU 时间、IO 和内存使用情况。<br />使用此视图可以标识性能有很大差异且可能会影响用户跨应用程序体验的查询。|  
|查询等待统计信息|分析数据库中最活跃的等待类别和哪些查询对所选等待类别贡献最大。<br />使用此视图分析等待统计信息并识别可能在应用程序中影响用户体验的查询。<br /><br />**适用范围：** 从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18.0 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 开始|  
|跟踪的查询|实时跟踪最重要查询的执行情况。 通常情况下，使用此视图是因为你计划强制执行相关查询，因此需确保查询性能的稳定性。|
  
> [!TIP]
> 如需详细了解如何使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来确定资源使用排名靠前的查询并修复那些因计划选择变化而导致回归的查询，请参阅 [@Azure 博客中的查询存储](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
 如果确定某个查询的性能不够理想，则可根据问题性质进行操作。  
  
-   如果所执行的查询具有多个计划，而最后一个计划明显不如前面的计划，则可通过计划强制机制来强制使用最佳计划。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试强制实施优化器中的计划。 如果计划强制实施失败，将触发 XEvent，并指示优化器正常优化。 
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  

> [!NOTE]
> 上面的图形针对特定的查询计划会显示不同的形状，以下是可能出现的每种形状的对应意义：<br />  
> 
> |形状|含义|  
> |-------------------|-------------|
> |Circle|查询完成（常规执行成功完成）|
> |Square|取消（客户端发起的执行中止）|
> |Triangle|失败（由异常引起的执行中止）|
> 
> 此外，形状大小反映指定时间间隔内的查询执行计数，执行数量较大时形状也会随之增大。  

-   你可以认为，你的查询因为缺少索引而无法达到最佳执行效果。 此信息显示在查询执行计划中。 使用 Query Store 创建缺失的索引并检查查询性能。  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     如果你在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上运行工作负荷，可注册获取 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 索引顾问，然后即可自动接收索引建议。  
  
-   在某些情况下，如果你看到执行计划中估计的行数和实际的行数存在显著差异，则可强制执行统计信息的重新编译。  
  
-   重写有问题的查询。 这样有很多好处，例如可以充分利用查询参数化或实现更优化的逻辑。  
  
##  <a name="Verify"></a>确保查询存储持续收集查询数据  
 Query Store 可通过无提示方式更改操作模式。 你应该定期监视 Query Store 的状态以确保 Query Store 正常运行，并采取相应措施，避免那些本来可以避免的因素造成故障。 执行以下查询，以便确定操作模式并查看最相关的参数：  
  
```sql
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 `actual_state_desc` 和 `desired_state_desc` 之间存在差异，这表明自动更改了操作模式。 最常见的更改是 Query Store 以无提示方式切换到只读模式。 在极罕见的情况下，Query Store 最终可能会因内部错误而处于 ERROR 状态。  
  
 当实际状态为只读时，可使用 **readonly_reason** 列来确定根本原因。 通常情况下，你会发现，Query Store 转换为只读模式是因为超出了大小配额。 这种情况下，**readonly_reason** 会被设置为 65536。 有关其他原因，请参阅 [sys.database_query_store_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)。  
  
 考虑执行以下步骤将 Query Store 切换为读写模式并激活数据收集功能：  
  
-   使用 **ALTER DATABASE** 的 **MAX_STORAGE_SIZE_MB**选项增大最大存储大小。  
  
-   使用以下语句清理 Query Store 数据：  
  
    ```sql  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
在应用这两项步骤或其中一项步骤时，可以执行以下语句，通过显式方式将操作模式改回为读写：  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 采用以下前摄性步骤：  
  
-   遵循最佳实践规范即可避免在无提示情况下更改操作模式。 如果你可以确保 Query Store 大小始终小于最大允许值，则会极大地降低转换为只读模式的几率。 根据[配置查询存储](#Configure)部分所述激活基于大小的策略，使查询存储在大小接近极限时自动清除数据。  
  
-   为了确保最新的数据能够得到保留，可将基于时间的策略配置为定期删除过时信息。  
  
-   最后，你应该考虑将“查询捕获模式”设置为“Auto”，因为这样通常可以筛选掉与工作负荷不太相关的查询。  
  
### <a name="error-state"></a>错误状态  
 若要恢复查询存储，可尝试显式设置读写模式，然后再次检查实际状态。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 如果问题仍然存在，则表明磁盘上的查询存储数据已永久损坏。
 
 从 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 开始，可通过在受影响的数据库内执行 sp_query_store_consistency_check 存储过程来恢复查询存储  。 必须先禁用查询存储，然后才能尝试恢复操作。 对于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，需要从查询存储中清除数据，如下所示。
 
 如果恢复失败，可先尝试清除查询存储，然后再设置读写模式。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-capture-mode"></a>设置最佳查询捕获模式  
 在 Query Store 中保留最相关数据。 下表描述了每个查询捕获模式的典型方案：  
  
|查询捕获模式|应用场景|  
|------------------------|--------------|  
|All|对工作负荷进行彻底的分析，分析所有查询形状及其执行频率和其他统计信息。<br /><br /> 确定工作负荷中的新查询。<br /><br /> 检测是否使用了即席查询来确定是否有机会进行用户参数化或自动参数化。<br /><br />**注意：** 这是 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中的默认捕获模式。|  
|Auto|注重相关的可操作查询，即那些定期执行的查询或资源消耗很大的查询。<br /><br />**注意：** 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始，这是默认捕获模式。|  
|None|你已经捕获了需要在运行时监视的查询集，因此需消除其他查询可能会带来的干扰。<br /><br /> “无”适用于测试和基准测试环境。<br /><br /> “无”也适用于需要提供已配置的 Query Store 配置来监视其应用程序工作负荷的软件供应商。<br /><br /> 在使用“无”时应格外小心，因为你可能无法跟踪和优化重要的新查询。 避免使用“无”，除非你的特定方案需要使用它。|  
|自定义|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 在 `ALTER DATABASE SET QUERY_STORE` 命令下引入自定义捕获模式。 启用后，在新的“查询存储捕获策略”设置下有额外可用的查询存储配置，可用于微调特定服务器中的数据收集。<br /><br />新的自定义设置定义在内部捕获策略时间阈值（计算可配置条件的时间边界）内执行的操作，如果所有值为 true，则查询存储可以捕获查询。 有关详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。|  

> [!NOTE]
> 当查询捕获模式设置为“全部”、“自动”或“自定义”时，始终捕获游标、存储过程中的查询和本机编译的查询。 若要捕获本机编译的查询，请使用 [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 启用每个查询统计信息的收集。 

## <a name="keep-the-most-relevant-data-in-query-store"></a>在 Query Store 中保留最相关数据  
 将 Query Store 配置为只包含最相关的数据，使之在持续运行的时候对你的常规工作负荷的影响最小，方便你进行故障排除。  
下表提供最佳实践：  
  
|最佳实践|设置|  
|-------------------|-------------|  
|对保留的历史数据进行限制。|配置基于时间的策略以激活自动清理功能。|  
|筛选掉不相关的查询。|将“查询捕获模式”配置为“Auto”。|  
|达到最大大小时，删除不太相关的查询。|激活基于大小的清理策略。|  
  
##  <a name="Parameterize"></a> 避免使用非参数化查询  
根据最佳做法，仅在绝对必要时（例如，临时分析时），才使用非参数化查询。  不能重复使用缓存的计划，因为这会强制查询优化器在碰到每个唯一的查询文本时都进行查询编译。 有关详细信息，请参阅[强制参数化使用指南](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide)。  
此外，Query Store 可能会很快超过大小配额，因为可能会存在大量不同的查询文本，结果会出现大量不同的执行计划，而查询形状是类似的。  
结果就是，工作负荷性能无法优化，Query Store 可能会切换为只读模式，或者可能会不断删除数据以应对传入的查询。  
  
请考虑下列选项：  

-   适用时，将查询参数化（例如，在存储过程或 sp_executesql 中包装查询）。 有关详细信息，请参阅[参数和执行计划重用](../../relational-databases/query-processing-architecture-guide.md#PlanReuse)。    
  
-   如果工作负载包含许多一次性使用的临时批处理且查询计划各不相同，请使用“[针对临时工作负载进行优化](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)”  选项。  
  
    -   将不同 query_hash 值的数目与 sys.query_store_query 中项的总数进行比较。 如果该比率接近 1，则说明你的即席工作负荷生成了不同的查询。  
  
-   如果不同查询计划的数量不多，请对数据库或部分查询应用“[强制参数化](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)”  。  
  
    -   请参阅[计划指南](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)，仅对选定查询强制执行参数化操作。  
  
    -   如果工作负载中不同查询计划的数量不多（即唯一 query_hash 数量与 sys.query_store_query 中条目总数的比 1 小得多时），将强制参数化配置为使用[参数化数据库选项](../../relational-databases/databases/database-properties-options-page.md#miscellaneous)命令。  
  
-   将“查询捕获模式”设置为“AUTO”即可自动筛选掉资源消耗小的即席查询  。  
  
##  <a name="Drop"></a> 维护查询的包含对象时，避免使用 DROP 和 CREATE 模式  
Query Store 会将查询条目与包含对象（存储过程、函数和触发器）相关联。  重新创建包含对象时，将会针对同一查询文本生成新的查询条目。 这会阻止你跟踪该查询在一定时段内的性能统计信息，并会使用计划强制机制。 若要避免这种问题，请尽可能使用 `ALTER <object>` 过程来更改包含对象定义。  
  
##  <a name="CheckForced"></a> 定期检查强制计划的状态  
可以方便地使用计划强制机制来修复关键查询的性能问题，使这些查询的结果更可预测。 但与计划提示和计划指南一样，强制实施某项计划并不能确保在今后的执行过程中会用到它。 通常情况下，如果对数据库架构的更改导致执行计划所引用的对象被更改或删除，计划强制就会失败。 在这种情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会回退到重新编译查询，而强制失败实际原因则显示在 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 中。 以下查询返回强制计划的相关信息：  
  
```sql  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 有关原因的完整列表，请参阅 [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。 你还可以使用 query_store_plan_forcing_failed  XEvent 来跟踪和故障排除计划强制失败情况。  
  
##  <a name="Renaming"></a> 避免在使用强制计划执行查询时重命名数据库  

执行计划使用由三个部分组成的名称 `database.schema.object` 来引用对象。   

如果重命名数据库，计划强制就会失败，导致在执行所有后续的查询时都需要重新编译。  

##  <a name="Recovery"></a> 在任务关键型服务器上使用跟踪标志
 
全局跟踪标志 7745 和 7752 可用于提高使用查询存储的数据库的可用性。 有关详细信息，请参阅[跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。
  
-  跟踪标志 7745 会阻止以下默认行为：在可关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前，查询存储将数据写入磁盘。 这意味着已收集但尚未保留到磁盘的查询存储数据将会丢失。 
  
-  跟踪标志 7752 启用了查询存储的异步加载。 这会使数据库变为联机状态，并且在查询存储完全恢复之前执行查询。 默认行为是同步加载查询存储。 默认行为可在恢复查询存储之前防止执行查询，但同时也可在数据集合中防止遗漏任何查询。

   > [!NOTE]
   > 从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始，此行为由引擎控制，跟踪标志 7752 不再有效。

> [!IMPORTANT]
> 如果仅对 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中正在运行的工作负载见解使用查询存储，请尽快安装 [KB 4340759](https://support.microsoft.com/help/4340759) 中的性能可伸缩性修补程序。 

## <a name="see-also"></a>另请参阅  
[ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)     
[查询存储目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)     
[查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)     
[通过内存中 OLTP 使用查询存储](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)     
[相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)      
[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)     
  
