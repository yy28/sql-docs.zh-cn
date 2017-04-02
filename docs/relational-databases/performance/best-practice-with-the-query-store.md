---
title: "Query Store 最佳实践 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Query Store, 最佳实践"
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Query Store 最佳实践
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主题概述使用 Query Store 处理工作负荷的最佳实践。  
  
##  <a name="a-namessmsa-use-the-latest-sql-server-management-studio"></a><a name="SSMS"></a>使用最新 SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 设计各种用户界面的目的是方便用户对查询存储进行配置和使用收集的工作负荷数据。  
下载最新版 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的网址：[https://msdn.microsoft.com/library/mt238290.aspx](https://msdn.microsoft.com/library/mt238290.aspx)  
  
 有关如何使用查询存储进行方案故障排除的快速说明，请参阅 [@Azure博客中的查询存储](https://azure.microsoft.com/en-us/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
##  <a name="a-nameinsighta-use-query-performance-insight-in-azure-sql-database"></a><a name="Insight"></a>在 Azure SQL 数据库中使用 Query Performance Insight  
 如果你在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中运行 Query Store，则可使用 **Query Performance Insight** 来分析一定时段内的 DTU 消耗情况。  
虽然可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来获取所有查询的详细资源消耗情况（CPU、内存、IO 等），但使用 Query Performance Insight 可以快速且有效地确定查询对数据库总体 DTU 消耗情况的影响。  
有关详细信息，请参阅 [Azure SQL Database Query Performance Insight](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)（Azure SQL 数据库的 Query Performance Insight）。    

##  <a name="using-query-store-with-elastic-pool-databases"></a>将 Query Store 与弹性池数据库配合使用
可以毫无顾忌地在所有数据库中使用 Query Store，甚至是在密集打包的池中。 与过多资源使用（为弹性池中的大量数据库启用了 Query Store 时可能会遇到这种情况）相关的所有问题都已得到了解决。
##  <a name="a-nameconfigurea-keep-query-store-adjusted-to-your-workload"></a><a name="Configure"></a>始终按工作负荷来调整查询存储  
 根据工作负荷和性能故障排除要求来配置 Query Store。   
默认参数适用于快速启动，但你应该监视 Query Store 在一定时段内的行为表现，并对其配置进行相应的调整：  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 下面是设置参数值时应遵循的准则：  
  
 **最大大小 (MB)：**为 Query Store 在数据库中占用的数据空间指定一个限制。  这是最重要的设置，直接影响 Query Store 的操作模式。  
  
 当 Query Store 收集查询、执行计划和统计信息时，其在数据库中的大小会一直增长，直至达到此限制。 达到此限制后，Query Store 会自动将操作模式更改为只读，并停止收集新数据，这意味着你的性能分析自此不再精确。  
  
 如果你的工作负荷会生成大量不同的查询和计划，或者你想要让查询历史记录保存较长的时间，则默认值 (100 MB) 可能不够大。 跟踪当前的空间使用情况，增大“最大大小(MB)”以防 Query Store 转换到只读模式。  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或执行以下脚本，以便获取有关 Query Store 大小的最新信息：  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 以下脚本将设置新的“最大大小(MB)”：  
  
```  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  
  
 **统计信息收集间隔：**定义已收集的运行时统计信息的粒度级别（默认值为 1 小时）。 如果你需要更细的粒度或更短的时间来检测问题和解决问题，则可考虑使用更低的值，但请记住，这会直接影响 Query Store 数据的大小。 使用 SSMS 或 Transact-SQL 为“统计信息收集间隔”设置不同的值：  
  
```  
ALTER DATABASE [QueryStoreDB] SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 30);  
```  
  
 **过时查询阈值（天）：**基于时间的清除策略，用于控制持久化运行时统计信息和非活动查询的保持期。  
默认情况下，查询存储配置为将数据保留 30 天，这对于你的方案来说可能过长了。  
  
 避免保留你不计划使用的历史数据。 这样可以减少变为只读状态的次数。 Query Store 数据的大小以及检测问题和解决问题的时间将会变得更可预测。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或以下脚本配置基于时间的清理策略：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 14));  
```  
  
 **基于大小的清理模式：** 指定在 Query Store 数据大小达到限制时，是否启用自动数据清理功能。  
  
 强烈建议你激活基于大小的清理功能，确保 Query Store 始终以读写模式运行并收集最新数据。  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **Query Store 捕获模式：** 指定 Query Store 的查询捕获策略。  
  
-   **All** – 捕获所有查询。 这是默认选项。  
  
-   **Auto** – 忽略不太频繁的查询以及编译和执行持续时间不长的查询。 执行计数、编译和运行时持续时间的阈值由内部决定。  
  
-   **None** – Query Store 停止捕获新查询。  
  
 以下脚本将“查询捕获模式”设置为“Auto”：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="how-to-start-with-query-performance-troubleshooting"></a>如何开始进行查询性能故障排除  
 Query Store 工作流的故障排除很简单，如下图所示：  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 按上一节的说明通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来启用 Query Store，或者执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
```  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  
  
 Query Store 收集能够准确代表工作负荷的数据集需要一定的时间。 通常情况下，即使是很复杂的工作负荷，一天的时间也足够了。 但是，在启用此功能后，你就可以立即开始浏览数据并确定需要注意的查询。   
导航到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的对象资源管理器中数据库节点下的 Query Store 子文件夹，以便打开特定方案的故障排除视图。   
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 查询存储视图在操作时使用一组执行度量值，每个度量值都表示为下述任意统计函数：  
  
|执行度量值|统计函数|  
|----------------------|------------------------|  
|CPU 时间、持续时间、执行计数、逻辑读取次数、逻辑写入次数、内存消耗和物理读取次数|平均值、最大值、最小值、标准偏差、总数|  
  
 下图显示了如何查找 Query Store 视图：  
  
 ![query-store-views](../../relational-databases/performance/media/query-store-views.png "query-store-views")  
  
 下表说明了何时使用每个 Query Store 视图：  
  
|SSMS 视图|应用场景|  
|---------------|--------------|  
|回归查询|查明哪些查询的执行度量值最近进行了回归（即变得更糟）。 <br />使用此视图将应用程序中观察到的性能问题与需要进行修复或改进的实际查询关联起来。|  
|资源使用排名靠前的查询|选择所关注的执行度量值，确定在指定的时间间隔内哪些查询的值最极端。 <br />此视图可以帮助你关注最相关的查询，这些查询对数据库资源消耗的影响最大。|  
|跟踪的查询|实时跟踪最重要查询的执行情况。 通常情况下，使用此视图是因为你计划强制执行相关查询，因此需确保查询性能的稳定性。|  
|总体资源消耗|针对任意执行度量值分析数据库的总资源消耗量。<br />使用此视图可以确定资源模式（白天工作负荷与夜间工作负荷的比较），并优化数据库的总体消耗。|  
  
> [!TIP]  
>  如需详细了解如何使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来确定资源使用排名靠前的查询并修复那些因计划选择变化而导致回归的查询，请参阅 [@Azure 博客中的查询存储](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
 如果确定某个查询的性能不够理想，则可根据问题性质进行操作。  
  
-   如果所执行的查询具有多个计划，而最后一个计划明显不如前面的计划，则可通过计划强制机制来强制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在今后执行查询时始终使用最佳计划。  
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  
  
-   你可以认为，你的查询因为缺少索引而无法达到最佳执行效果。 此信息显示在查询执行计划中。 使用 Query Store 创建缺失的索引并检查查询性能。  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     如果你在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上运行工作负荷，可注册获取 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 索引顾问，然后即可自动接收索引建议。  
  
-   在某些情况下，如果你看到执行计划中估计的行数和实际的行数存在显著差异，则可强制执行统计信息的重新编译。  
  
-   重写有问题的查询。 这样有很多好处，例如可以充分利用查询参数化或实现更优化的逻辑。  
  
##  <a name="a-nameverifya-verify-query-store-is-collecting-query-data-continuously"></a><a name="Verify"></a>确保查询存储持续收集查询数据  
 Query Store 可通过无提示方式更改操作模式。 你应该定期监视 Query Store 的状态以确保 Query Store 正常运行，并采取相应措施，避免那些本来可以避免的因素造成故障。 执行以下查询，以便确定操作模式并查看最相关的参数：  
  
```  
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
  
-   使用 **ALTER DATABASE** 的 **MAX_STORAGE_SIZE_MB** 选项增大最大存储大小。  
  
-   使用以下语句清理 Query Store 数据：  
  
    ```  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
 在应用这两项步骤或其中一项步骤时，可以执行以下语句，通过显式方式将操作模式改回为读写：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 采用以下前摄性步骤：  
  
-   遵循最佳实践规范即可避免在无提示情况下更改操作模式。 如果你可以确保 Query Store 大小始终小于最大允许值，则会极大地降低转换为只读模式的几率。 根据 [配置 Query Store](#Configure) 部分所述激活基于大小的策略，使 Query Store 在大小接近极限时自动清除数据。  
  
-   为了确保最新的数据能够得到保留，可将基于时间的策略配置为定期删除过时信息。  
  
-   最后，你应该考虑将“查询捕获模式”设置为“Auto”，因为这样通常可以筛选掉与工作负荷不太相关的查询。  
  
### <a name="error-state"></a>错误状态  
 若要恢复 Query Store，可尝试显式设置读写模式，然后再次检查实际状态。  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 如果问题仍然存在，则表明磁盘上的 Query Store 数据已永久损坏。 在请求读写模式之前，需清除 Query Store。  
  
```  
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
|全部|对工作负荷进行彻底的分析，分析所有查询形状及其执行频率和其他统计信息。<br /><br /> 确定工作负荷中的新查询。<br /><br /> 检测是否使用了即席查询来确定是否有机会进行用户参数化或自动参数化。|  
|Auto|注重相关的可操作查询，即那些定期执行的查询或资源消耗很大的查询。|  
|无|你已经捕获了需要在运行时监视的查询集，因此需消除其他查询可能会带来的干扰。<br /><br /> “无”适用于测试和基准测试环境。<br /><br /> “无”也适用于需要提供已配置的 Query Store 配置来监视其应用程序工作负荷的软件供应商。<br /><br /> 在使用“无”时应格外小心，因为你可能无法跟踪和优化重要的新查询。 避免使用“无”，除非你的特定方案需要使用它。|  
  
## <a name="keep-the-most-relevant-data-in-query-store"></a>在 Query Store 中保留最相关数据  
 将 Query Store 配置为只包含最相关的数据，使之在持续运行的时候对你的常规工作负荷的影响最小，方便你进行故障排除。  
下表提供最佳实践：  
  
|最佳实践|设置|  
|-------------------|-------------|  
|对保留的历史数据进行限制。|配置基于时间的策略以激活自动清理功能。|  
|筛选掉不相关的查询。|将“查询捕获模式”配置为“Auto”。|  
|达到最大大小时，删除不太相关的查询。|激活基于大小的清理策略。|  
  
##  <a name="a-nameparameterizea-avoid-using-non-parameterized-queries"></a><a name="Parameterize"></a>避免使用非参数化查询  
 在不是绝对需要的情况下使用非参数化查询（例如，在即席分析时使用）不符合最佳实践规范。  不能重复使用缓存的计划，因为这会强制查询优化器在碰到每个唯一的查询文本时都进行查询编译。  
  此外，Query Store 可能会很快超过大小配额，因为可能会存在大量不同的查询文本，结果会出现大量不同的执行计划，而查询形状是类似的。  
结果就是，工作负荷性能无法优化，Query Store 可能会切换为只读模式，或者可能会不断删除数据以应对传入的查询。  
  
 请考虑下列选项：  
  
-   根据需要将查询参数化，例如，将查询包装在存储过程中。  
  
-   如果查询包含许多一次性使用的即席批处理且查询计划各不相同，则可使用“针对即席工作负荷进行优化”选项。  
  
    -   将不同 query_hash 值的数目与 sys.query_store_query 中项的总数进行比较。 如果该比率接近 1，则说明你的即席工作负荷生成了不同的查询。  
  
-   如果不同查询计划的数目不大，则可对数据库或部分查询应用 FORCED PARAMETERIZATION。  
  
    -   遵照计划指南，仅对所选查询强制实施参数化操作。  
  
    -   如果工作负荷中不同查询计划的数目很小，则为数据库配置 FORCED PARAMETERIZATION。 （当不同 query_hash 的计数与 sys.query_store_query 中项的总数之比远小于 1 时。）  
  
-   将“查询捕获模式”设置为“AUTO”即可自动筛选掉资源消耗小的即席查询。  
  
##  <a name="a-namedropa-avoid-a-drop-and-create-pattern-when-maintaining-containing-objects-for-the-queries"></a><a name="Drop"></a>对查询的包含对象进行维护时，避免使用 DROP 和 CREATE 模式  
 Query Store 会将查询条目与包含对象（存储过程、函数和触发器）相关联。  重新创建包含对象时，将会针对同一查询文本生成新的查询条目。 这会阻止你跟踪该查询在一定时段内的性能统计信息，并会使用计划强制机制。 若要避免这种问题，请尽可能使用 `ALTER <object>` 过程来更改包含对象定义。  
  
##  <a name="a-namecheckforceda-check-the-status-of-forced-plans-regularly"></a><a name="CheckForced"></a>定期检查强制计划的状态  
 可以方便地使用计划强制机制来修复关键查询的性能问题，使这些查询的结果更可预测。 但与计划提示和计划指南一样，强制实施某项计划并不能确保在今后的执行过程中会用到它。 通常情况下，如果对数据库架构的更改导致执行计划所引用的对象被更改或删除，计划强制就会失败。 这种情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会通过回退来重新编译查询，并在 [sys.query_store_plan (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 中显示实际的强制失败原因。 以下查询返回强制计划的相关信息：  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 有关原因的完整列表，请参阅 [sys.query_store_plan (Transact SQL)](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。 你还可以使用 **query_store_plan_forcing_failed** XEvent 来跟踪故障排除计划强制失败情况。  
  
##  <a name="a-namerenaminga-avoid-renaming-databases-if-you-have-queries-with-forced-plans"></a><a name="Renaming"></a>避免在使用强制计划进行查询时重命名数据库  
 执行计划通过由三个部分组成的名称 (`database.schema.object`) 来引用对象。   
如果重命名数据库，计划强制就会失败，导致在执行所有后续的查询时都需要重新编译。  
  
## <a name="see-also"></a>另请参阅  
 [查询存储目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [通过内存中 OLTP 使用查询存储](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [使用查询存储监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  