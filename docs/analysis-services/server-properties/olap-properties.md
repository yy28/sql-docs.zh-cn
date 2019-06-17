---
title: Analysis Services OLAP 属性 |Microsoft Docs
ms.date: 03/15/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e2643488710548b3a773730e9b9898125783dc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714584"
---
# <a name="olap-properties"></a>OLAP 属性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的 OLAP 服务器属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **适用范围：** 仅限多维服务器模式  
  
## <a name="memory"></a>内存  
 **DefaultPageSizeForData**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForDataHeader**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForIndex**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForIndexHeader**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForString**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForHash**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultPageSizeForProp**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 **已启用**  
 一个布尔值属性，指定是否启用迟缓聚合处理。  
  
 **SleepIntervalSecs**  
 一个有符号 32 位整数属性，它定义服务器检查是否存在挂起的迟缓处理作业的时间间隔（秒）。  
  
 **MaxCPUUsage**  
 一个有符号 64 位双精度浮点数属性，它定义迟缓处理的最大 CPU 使用率（以百分比表示）。 服务器基于快照监视 CPU 的平均使用率。 CPU 使用率的峰值高于此阈值属于正常行为。  
  
 此属性的默认值为 0.5，指示迟缓处理的最大 CPU 使用率为 50%。  
  
 **MaxObjectsInParallel**  
 一个有符号 32 位整数属性，它指定可并行迟缓处理的最大分区数。  
  
 **MaxRetries**  
 一个有符号 32 位整数属性，它定义在迟缓处理失败的事件中重试多少次后引发错误。  
  
## <a name="processplan"></a>ProcessPlan  
 **CacheRowsetRows**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CacheRowsetToDisk**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DistinctBuffer**  
 一个有符号 32 位整数属性，它定义用于非重复计数的内部缓冲区的大小。 如果增大此值，则可提高非重复计数处理速度，但同时会增加内存使用开销。  
  
 **EnableRolapDimQueryTableGrouping**  
 一个布尔值属性，指定是否为 ROLAP 维度启用表分组。 如果为 True，则在运行时查询 ROLAP 维度时，也同时查询整个 ROLAP 维度表，这与每个属性的单独查询正好相反。  
  
 **EnableTableGrouping**  
 一个布尔值属性，指定是否启用表分组。 如果为 True，则在处理维度时，也同时查询整个维度表，这与每个属性的单独查询正好相反。  
  
 **ForceMultiPass**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MaxTableDepth**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryAdjustConst**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryAdjustFactor**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryLimit**  
 一个有符号 64 位双精度浮点数属性，它定义用于处理的最大内存量（以物理内存的百分比表示）。  
  
 此属性的默认值为 65，指示可将 65% 的物理内存用于多维数据集和维度处理。  
  
 **MemoryLimitErrorEnabled**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **OptimizeSchema**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 **DefaultRefreshInterval**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DimensionLatencyAccuracy**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PartitionLatencyAccuracy**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="process"></a>Process  
 **AggregationMemoryLimitMax**  
 一个有符号 64 位双精度浮点数属性，它定义可用于聚合处理的最大内存量（以物理内存的百分比表示）。  
  
 此属性的默认值为 80，指示可将 80% 的物理内存用于聚合处理。  
  
 **AggregationMemoryLimitMin**  
 一个有符号 64 位双精度浮点数属性，它定义可用于聚合处理的最小内存量（以物理内存的百分比表示）。 如果增大此值，则可提高聚合处理速度，但同时会增加内存使用开销。  
  
 此属性的默认值为 10，指示最少要将 10% 的物理内存用于聚合处理。  
  
 **AggregationNewAlgo**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **AggregationPerfLog2**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **AggregationsBuildEnabled**  
 一个布尔值属性，指定是否启用聚合生成。 这是一种在不更改聚合设计的情况下确定聚合生成基准的机制。  
  
 **BufferMemoryLimit**  
 一个有符号 64 位双精度浮点数属性，它定义处理缓冲区内存限制值（以物理内存的百分比表示）。  
  
 此属性的默认值为 60，指示最多可将 60% 的物理内存用于缓冲区内存。  
  
 **BufferRecordLimit**  
 一个有符号 32 位整数属性，它定义在处理期间可缓冲的记录数。  
  
 此属性的默认值为 1048576（记录）。  
  
 **CacheRecordLimit**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CheckDistinctRecordSortOrder**  
 一个布尔值属性，它定义在处理分区时非重复计数查询的结果的排序顺序是否有意义。 如果为 True，指示排序顺序没有意义，必须由服务器进行“检查”。 处理具有非重复计数度量值的分区时，查询按排序依据发送到 SQL。 设置为 false 可加速处理。  
  
 此属性的默认值为 True，指示排序顺序没有意义，必须对其进行检查。  
  
 **DatabaseConnectionPoolConnectTimeout**  
 一个有符号 32 位整数属性，它指定打开新连接时的超时值（秒）。  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 一个有符号 32 位整数属性，它指定使用外部 OLEDB 连接时的数据库连接超时值（秒）。  
  
 **DatabaseConnectionPoolMax**  
 一个有符号 32 位整数属性，它指定入池数据库连接的最大数。  
  
 此属性的默认值为 50（连接）。  
  
 **DatabaseConnectionPoolTimeout**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataFileInitEnabled**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataPlacementOptimization**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataSliceInitEnabled**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DeepCompressValue**  
 一个布尔值属性，它应用于 Double 数据类型的度量值，指定是否可以压缩数字（导致数值精度损失）。 如果值为 False，指示无压缩，无精度损失。  
  
 此属性的默认值为 True，指示启用压缩，将引发精度损失。  
  
 **DimensionPropertyKeyCache**  
 一个布尔值属性，它指定是否缓存维度属性键。 如果键不唯一，则必须设为 True。  
  
 **IndexBuildEnabled**  
 一个布尔值属性，它指定是否在处理后生成索引。 此属性用于基准确定，可供参考。  
  
 **IndexBuildThreshold**  
 一个有符号 32 位整数属性，它指定行计数阈值，低于该阈值时，将不为分区生成索引。  
  
 此属性的默认值为 4096（行）。  
  
 **IndexFileInitEnabled**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MapFormatMask**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **RecordsReportGranularity**  
 一个有符号 32 位整数属性，它指定在处理期间服务器记录跟踪事件的频率（行）。  
  
 此属性的默认值为 1000，指示每 1000 行后记录一个跟踪事件。  
  
 **ROLAPDimensionProcessingEffort**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="query"></a>查询  
 **AggregationsUseEnabled**  
 一个布尔值属性，定义在运行时是否使用存储聚合。 此属性允许在不更改聚合设计或不重新处理的情况下禁用聚合，用于基准确定，可供参考。  
  
 此属性的默认值为 True，指示启用聚合。  
  
 **AllowSEFiltering**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CalculationCacheRegistryMaxIterations**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CalculationEvaluationPolicy**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ConvertDeletedToUnknown**  
 一个布尔值属性，它指定是否将已删除的维度成员转换为未知成员。  
  
 **CopyLinkedDataCacheAndRegistry**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCacheRegistryMaxIterations**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DefaultDrillthroughMaxRows**  
 一个有符号 32 位整数属性，指定将从钻取查询中返回的最大行数。  
  
 此属性的默认值为 10000（行）。  
  
 **DimensionPropertyCacheSize**  
 一个带符号的 32 位整数属性，可指定用于缓存查询中使用的维度成员的内存量（字节）。  
  
 默认值为每个属性层次结构的每个有效查询 4,000,000 字节（或 4 MB）。 该默认值为具有典型层次结构的解决方法提供了均衡的缓存大小。 但是，如果增加此值，则具有大量（数百万）成员或多层层次结构的维度的执行效果更好。  
  
 增加缓存大小的涵义：  
  
-   在允许维度缓存使用更多内存时，内存利用率开销将增加。 实际使用率取决于查询执行情况。 并非所有查询都将使用允许的最大值。  
  
     请注意，这些缓存使用的内存被认为是不可收缩的，将在考虑 **TotalMemoryLimit**时包括这些内存。  
  
-   影响服务器上的所有数据库。 **DimensionPropertyCachesize** 是服务器范围内的属性。 更改此属性会影响当前实例上运行的所有数据库。  
  
用于估计维度缓存要求的方法：  
  
1.  首先通过显著增加大小来确定增加维度缓存大小是否有好处。 例如，您可能需要在执行初始步骤时将默认值扩大一倍。  
  
2.  如果性能显著提高，则以递增方式减小该值，直至在性能和内存利用率之间找到平衡点。  


 **ExpressNonEmptyUseEnabled**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **IgnoreNullRolapRows**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **IndexUseEnabled**  
 一个布尔值属性，它定义在运行时是否使用索引。 此属性用于基准确定，可供参考。  
  
 **MapHandleAlgorithm**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MaxRolapOrConditions**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
 
 **RowsetSerializationLimit**   
 适用于 Azure Analysis Services。 在行集返回到客户端的行数的限制。 默认值为-1，这意味着无限制应用。 适用于 DAX 和 MDX 查询。 它可以用于保护从广泛的数据导出的服务器资源。 查询提交到服务器超出该限制的连接将被取消并且返回错误。  

 **UseCalculationCacheRegistry**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseDataCacheFreeLastPageMemory**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseDataCacheRegistry**  
 一个布尔值属性，它指定是否启用数据缓存注册表（其中缓存查询结果，但不是计算结果）。  
  
 **UseDataCacheRegistryHashTable**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseDataCacheRegistryMultiplyKey**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseDataSlice**  
 一个布尔值属性，它定义在运行时是否使用分区数据切片进行查询优化。 此属性用于基准确定，可供参考。  
  
 **UseMaterializedIterators**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseSinglePassForDimSecurityAutoExist**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **UseVBANet**  
 一个布尔值属性，它定义是否将 VBA .net 程序集用于用户定义函数。  
  
 **CalculationPrefetchLocality\ ApplyIntersect**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CalculationPrefetchLocality\ ApplySubtract**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **CalculationPrefetchLocality\ PrefetchLowerGranularities**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\  CachedPageAlloc\ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\  CachedPageAlloc\ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\  CachedPageAlloc\ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\  CachedPageAlloc\ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\  CachedPageAlloc\ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\CellStore\ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\CellStore\ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\CellStore\ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\CellStore\ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\CellStore\ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\ MemoryModel \ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\ MemoryModel \ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\ MemoryModel \ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\ MemoryModel \ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **DataCache\ MemoryModel\ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="jobs"></a>中执行计划的管理任务，即“作业”  
 **ProcessAggregation\ MemoryModel\ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ MemoryModel\ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ MemoryModel\ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ MemoryModel\ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ MemoryModel\ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessPartition\ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessPartition \ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessPartition \ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessPartition \ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessPartition \ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessProperty\ Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessProperty\ InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessProperty\ MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessProperty\ MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **ProcessAggregation\ ProcessProperty\ Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
