---
title: "性能计数器 (SSAS) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: edaf6abe5becb215a58f8ae229562c774d1f0fd1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="performance-counters-ssas"></a>性能计数器 (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]使用性能监视器，你可以使用性能计数器来监视 Microsoft SQL Server Analysis Services (SSAS) 实例的性能。  
  
 性能监视器是用于跟踪资源使用情况的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制 (MMC) 管理单元。 您可以通过以下方式启动此 MMC 管理单元：在命令提示符下键入 **PerfMon** ，或从“控制面板”依次单击 **“管理工具”**和 **“性能监视器”**。 性能监视器使您可以通过使用预定义对象和计数器来跟踪服务器和进程的性能和活动，以及通过使用用户定义的计数器来监视事件。 性能监视器收集有关事件的计数而非数据，例如，内存使用量、活动事务数或 CPU 活动。 您还可以对特定计数器设置阈值以生成通知操作员的警报。  
  
 性能监视器可以监视 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的远程和本地实例。 有关详细信息，请参阅 [使用性能监视器](http://technet.microsoft.com/library/cc749115.aspx)。  
  
 若要查看可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的任何计数器的说明，请在性能监视器中打开 **“添加计数器”** 对话框，选择一个性能对象，然后单击 **“显示说明”**。 最重要的计数器是 CPU 使用率、内存使用量、磁盘 IO 率。 建议先从这些重要计数器开始，当您更了解监视其他哪些计数器对改善性能有所帮助时，再转至更具体的计数器。 有关要包含哪些计数器的详细信息，请参阅 [SQL Server 2008 R2 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 计数器分为若干组，以便您可以更轻松地找到相关计数器。  
  
## <a name="counters-by-groups"></a>按组划分的计数器  
  
|分组|Description|  
|-----------|-----------------|  
|[高速缓存](#bkmk_Cache)|与 Analysis Services 聚合缓存相关的统计信息。|  
|[连接](#bkmk_Connection)|与 Microsoft Analysis Services 连接相关的统计信息。|  
|[数据挖掘预测](#bkmk_DataMiningPrediction)|与处理数据挖掘模型相关的统计信息。|  
|[数据挖掘模型处理](#bkmk_DataMiningModelProcessing)|与根据数据挖掘模型创建预测相关的统计信息。|  
|[锁](#bkmk_Locks)|与 Microsoft Analysis Services 内部服务器锁相关的统计信息。|  
|[MDX](#bkmk_MDX)|与 Microsoft Analysis Services MDX 计算相关的统计信息。|  
|[内存](#bkmk_Memory)|与 Microsoft Analysis Services 内部服务器内存相关的统计信息。|  
|[主动缓存](#bkmk_ProactiveCaching)|与 Microsoft Analysis Services 主动缓存相关的统计信息。|  
|[处理聚合](#bkmk_ProcAggregations)|与处理 MOLAP 数据文件中的聚合相关的统计信息。|  
|[处理索引](#bkmk_ProcIndexes)|与处理 MOLAP 数据文件的索引相关的统计信息。|  
|[处理](#bkmk_Processing)|与数据处理相关的统计信息。|  
|[存储引擎查询](#bkmk_StorageEngineQuery)|与 Microsoft Analysis Services 存储引擎查询相关的统计信息。|  
|[线程](#bkmk_Threads)|与 Microsoft Analysis Services 线程相关的统计信息。|  
  
###  <a name="bkmk_Cache"></a> 高速缓存  
 与 Microsoft Analysis Services 聚合缓存相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current KB|聚合缓存使用的当前内存量 (KB)。|  
|KB added/sec|添加到缓存的内存速率（KB/秒）。|  
|Current entries|缓存条目的当前数目。|  
|Inserts/sec|插入缓存的速率。  按每个数据库的每个多维数据集的每个分区跟踪该速率。|  
|Evictions/sec|从缓存逐出的速率。  此速率基于每个数据库的每个多维数据集的每个分区。  逐出通常是由于后台清除器导致的。|  
|Total inserts|插入缓存的数目。  按每个数据库的每个多维数据集的每个分区跟踪该速率。|  
|Total evictions|从缓存逐出的数目。  按每个数据库的每个多维数据集的每个分区跟踪逐出数目。  逐出通常是由于后台清除器导致的。|  
|Direct hits/sec|缓存直接命中的速率。 缓存命中指示根据现有缓存条目响应了查询。|  
|Misses/sec|缓存未命中的速率。|  
|Lookups/sec|缓存查找的速率。|  
|Total direct hits|直接缓存命中的总数。  直接缓存命中指示根据现有缓存条目响应了查询。|  
|Total misses|缓存未命中的总数。|  
|Total lookups|在缓存中进行查找的总数。|  
|Direct hit ratio|对于计数器值之间的期间，缓存直接命中缓存查找的速率。|  
|Total filtered iterator cache hits|在筛选结果的基础上返回一个索引迭代器的缓存命中总次数。|  
|Total filtered iterator cache misses|因无法在筛选结果的基础上生成索引迭代器而不得不使用筛选结果生成新缓存的缓存命中总次数。|  
  
###  <a name="bkmk_Connection"></a> 连接  
 与 Microsoft Analysis Services 连接相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current connections|当前已建立的客户端连接数。|  
|Requests/sec|连接请求的速率。  这些请求是到达的请求。|  
|Total requests|连接请求总数。  这些请求是到达的请求。|  
|Successes/sec|连接成功完成速率。|  
|Total successes|成功连接总数。|  
|Failures/sec|连接失败速率。|  
|Total failures|失败的连接尝试总数。|  
|Current user sessions|当前已建立的用户会话数。|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a> 数据挖掘模型处理  
 与 Microsoft Analysis Services 数据挖掘模型处理相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Cases/sec|处理事例的速率。|  
|Current models processing|当前正在处理的模型数。|  
  
###  <a name="bkmk_DataMiningPrediction"></a> 数据挖掘预测  
 与 Microsoft Analysis Services 数据挖掘预测相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Concurrent DM queries|当前正在处理的数据挖掘查询数。|  
|Predictions/sec|在数据挖掘查询中生成的预测的数目。|  
|Rows/sec|在数据挖掘预测查询过程中已处理的行数。|  
|Queries/sec|已处理的数据挖掘查询数。|  
|Total Queries|服务器收到的数据挖掘查询总数。|  
|总计行|数据挖掘查询返回的行总数。|  
|Total Predictions|服务器收到的数据挖掘预测查询总数。|  
  
###  <a name="bkmk_Locks"></a> 锁  
 与 Microsoft Analysis Services 内部服务器锁相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current latch waits|当前等待闩锁的线程数。  这些闩锁请求未能立即获得闩锁，因而处于等待状态。|  
|Latch waits/sec|未能立即获得闩锁因而不得不等待的闩锁请求速率。|  
|Current locks|当前锁定的对象数。|  
|Current lock waits|当前正在等待锁的客户端数。|  
|Lock requests/sec|每秒的锁请求数。|  
|Lock grants/sec|每秒的锁授予数。|  
|Lock waits/sec|每秒的锁等待数。  这些是未能立即获得锁因而处于等待状态的锁请求。|  
|Lock denials/sec|锁拒绝速率。|  
|Unlock requests/sec|每秒的解锁请求数。|  
|Total deadlocks detected|检测到的死锁总数。|  
  
###  <a name="bkmk_MDX"></a> MDX  
 与 Microsoft Analysis Services MDX 计算相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Number of calculation covers|由 MDX 执行计划生成的求值节点的总数（包括活动求值节点和缓存求值节点）。|  
|Current number of evaluation nodes|由 MDX 执行计划生成的求值节点（包括活动求值节点和缓存求值节点）的当前（近似）数量。|  
|Number of Storage Engine evaluation nodes|由 MDX 执行计划生成的存储引擎求值节点的总数。|  
|单元格逐单元求值节点的数目|由 MDX 执行计划生成的逐单元求值节点的总数。|  
|Number of bulk-mode evaluation nodes|由 MDX 执行计划生成的批量模式求值节点的总数。|  
|Number of evaluation nodes that covered a single cell|由 MDX 执行计划生成的仅涵盖一个单元的求值节点的总数。|  
|与计算位于同一粒度的求值节点的数目|由 MDX 执行计划生成的、其计算与该求值节点位于同一粒度的求值节点的总数。|  
|Current number of cached evaluation nodes|由 MDX 执行计划生成的缓存求值节点的当前（近似）数量。|  
|Number of cached Storage Engine evaluation nodes|由 MDX 执行计划生成的缓存的存储引擎求值节点的总数。|  
|Number of cached bulk-mode evaluation nodes|由 MDX 执行计划生成的缓存的批量模式求值节点的总数。|  
|Number of cached 'other' evaluation nodes|由 MDX 执行计划生成的、既不是存储引擎求值节点也不是批量模式求值节点的缓存的求值节点的总数。|  
|Number of evictions of evaluation nodes|由于冲突而产生的求值节点的缓存逐出总数。|  
|求值节点缓存中的哈希索引命中次数|该哈希索引满足的求值节点缓存中的命中总次数。|  
|求值节点缓存中的单元格逐单元命中次数|求值节点缓存中逐单元命中总次数。|  
|求值节点缓存中逐单元格未命中数|求值节点缓存中逐单元未命中总次数。|  
|求值节点缓存中的子多维数据集命中次数|求值节点缓存中子多维数据集命中总次数。|  
|求值节点缓存中的子多维数据集未命中次数|求值节点缓存中子多维数据集未命中总次数。|  
|Total Sonar subcubes|查询优化器所生成的子多维数据集的总数。|  
|Total cells calculated|所计算单元属性的总数。|  
|Total recomputes|由于错误而重新计算的单元总数。|  
|Total flat cache inserts|插入平面计算缓存中的单元值的总数。|  
|Total calculation cache registered|已注册的计算缓存的总数。|  
|Total NON EMPTY|NON EMPTY 算法的使用总次数。|  
|Total NON EMPTY unoptimized|未优化的 NON EMPTY 算法的使用总次数。|  
|Total NON EMPTY for calculated members|NON EMPTY 算法在计算成员之间循环的总次数。|  
|Total Autoexist|执行 autoexist 的总次数。|  
|Total EXISTING|执行 EXISTING 集操作的总次数。|  
  
###  <a name="bkmk_Memory"></a> 内存  
 与 Microsoft Analysis Services 内部服务器内存相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Page Pool 64 Alloc KB|从系统借用的内存大小 (KB)。  将此内存提供给服务器的其他部分。|  
|Page Pool 64 Lookaside KB|64KB 后备链表中的当前内存大小 (KB)。  (内存页已准备就绪。)|  
|Page Pool 8 Alloc KB|从 64KB 页池借用的内存大小 (KB)。  将此内存提供给服务器的其他部分。|  
|Page Pool 8 Lookaside KB|8KB 后备链表中的当前内存大小 (KB)。  (内存页已准备就绪。)|  
|Page Pool 1 Alloc KB|从 64KB 页池借用的内存大小 (KB)。  将此内存提供给服务器的其他部分。|  
|Page Pool 1 Lookaside KB|8KB 后备链表中的当前内存大小 (KB)。  (内存页已准备就绪。)|  
|Cleaner Current Price|当前内存价格（美元/字节/时间），已被规范化为 1000。|  
|Cleaner Balance/sec|balance+shrink 操作的速率。|  
|Cleaner Memory shrunk KB/sec|收缩速率 (KB/秒)。|  
|Cleaner Memory shrinkable KB|由后台清除器清除的内存量 (KB)。|  
|Cleaner Memory nonshrinkable KB|不由后台清除器清除的内存量 (KB)。|  
|Cleaner Memory KB|后台清除器所知道的内存量 (KB)。  (可通过清除器收缩的内存 + 无法通过清除器收缩的内存。)|  
|Memory Usage KB|服务器进程在计算清除器内存价格期间的内存使用量。  等于计数器 Process\PrivateBytes 加上内存映射数据的大小，但忽略 xVelocity 内存中分析引擎 (VertiPaq) 映射或分配的超出 xVelocity 引擎内存限制的任何内存。|  
|Memory Limit Low KB|内存下限，来自配置文件。|  
|Memory Limit High KB|内存上限，来自配置文件。|  
|AggCacheKB|当前分配给聚合缓存的内存大小 (KB)。|  
|Quota KB|当前内存配额 (KB)。  内存配额也称作内存授予或内存预留。|  
|Quota Blocked|在释放其他内存配额之前将一直保持阻塞状态的当前配额请求数。|  
|Filestore KB|当前分配给文件存储（即文件缓存）的内存大小 (KB)。|  
|Filestore Page Faults/sec|文件存储页错误率。|  
|Filestore Reads/sec|每秒读取的文件存储页数。|  
|Filestore KB Reads/sec|每秒读取的文件存储 KB。|  
|Filestore Writes/sec|每秒写入的文件存储页数。写入是异步的。|  
|Filestore KB Write/sec|每秒写入的文件存储 KB。写入是异步的。|  
|Filestore IO Errors/sec|文件存储 IO 错误率。|  
|Filestore IO Errors|文件存储 IO 错误总计。|  
|Filestore Clock Pages Examined/sec|后台清除器出于逐出目的而检查页的速率。|  
|Filestore Clock Pages HaveRef/sec|后台清除器对具有当前引用计数（当前正在使用）的页的检查速率。|  
|Filestore Clock Pages Valid/sec|后台清除器对有效的逐出候选页的检查速率。|  
|Filestore Memory Pinned KB|当前文件存储驻留内存量 (KB)。|  
|In-memory Dimension Property File KB|当前内存中的维度属性文件大小 (KB)。|  
|In-memory Dimension Property File KB/sec|写入内存中维度属性文件的速率 (KB)。|  
|Potential In-memory Dimension Property File KB|内存中维度属性文件的潜在大小 (KB)。|  
|Dimension Property Files|维度属性文件的数量。|  
|In-memory Dimension Index (Hash) File KB|当前内存中的维度索引（哈希）文件大小 (KB)。|  
|In-memory Dimension Index (Hash) File KB/sec|写入内存中维度索引（哈希）文件的速率 (KB)。|  
|Potential In-memory Dimension Index (Hash) File KB|内存中的维度索引（哈希）文件的潜在大小 (KB)。|  
|Dimension Index (Hash) Files|维度索引（哈希）文件的数量。|  
|In-memory Dimension String File KB|当前内存中的维度字符串文件大小 (KB)。|  
|In-memory Dimension String File KB/sec|写入内存中维度字符串文件的速率 (KB)。|  
|Potential In-memory Dimension String File KB|内存中维度字符串文件的潜在大小 (KB)。|  
|Dimension String Files|维度字符串文件的数量。|  
|In-memory Map File KB|当前内存中的映射文件大小 (KB)。|  
|In-memory Map File KB/sec|写入内存中映射文件的速率 (KB)。|  
|Potential In-memory Map File KB|内存中映射文件的潜在大小 (KB)。|  
|Map Files|映射文件的数量。|  
|In-memory Aggregation Map File KB|当前内存中的聚合映射文件大小 (KB)。|  
|In-memory Aggregation Map File KB/sec|写入内存中聚合映射文件的速率 (KB)。|  
|Potential In-memory Aggregation Map File KB|潜在内存中聚合映射文件的大小 (KB)。|  
|Aggregation Map Files|聚合映射文件的数量。|  
|In-memory Fact Data File KB|当前内存中事实数据文件的大小 (KB)。|  
|In-memory Fact Data File KB/sec|写入内存中事实数据文件的速率 (KB)。|  
|Potential In-memory Fact Data File KB|潜在内存中事实数据文件的大小 (KB)。|  
|Fact Data Files|事实数据文件的数量。|  
|In-memory Fact String File KB|当前内存中事实字符串文件的大小 (KB)。|  
|In-memory Fact String File KB/sec|写入内存中事实字符串文件的速率 (KB)。|  
|Potential In-memory Fact String File KB|潜在内存中事实字符串文件的大小 (KB)。|  
|Fact String Files|事实字符串文件的数量。|  
|In-memory Fact Aggregation File KB|当前内存中事实聚合文件的大小 (KB)。|  
|In-memory Fact Aggregation File KB/sec|写入内存中事实聚合文件的速率 (KB)。|  
|Potential In-memory Fact Aggregation File KB|潜在内存中事实聚合文件的大小 (KB)。|  
|Fact Aggregation Files|事实聚合文件的数量。|  
|In-memory Other File KB|当前内存中其他文件的大小 (KB)。|  
|In-memory Other File KB/sec|写入内存中其他文件的速率 (KB)。|  
|Potential In-memory Other File KB|潜在内存中其他文件的大小 (KB)。|  
|Other Files|其他文件的数量。|  
|VertiPaq Paged KB|用于内存中数据的分页内存量 (KB)。|  
|VertiPaq Nonpaged KB|工作集中锁定供内存中引擎使用的内存量 (KB)。|  
|VertiPaq Memory-Mapped KB|用于内存中数据的可分页内存量 (KB)。|  
|Memory Limit Hard KB|配置文件中的硬内存限制。|  
|Memory Limit VertiPaq KB|配置文件中的内存中限制。|  
  
###  <a name="bkmk_ProactiveCaching"></a> 主动缓存  
 与 Microsoft Analysis Services 主动缓存相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Notifications/sec|从关系数据库发出通知的速率。|  
|Processing Cancellations/sec|对通知所引发的取消操作的处理速度。|  
|Proactive Caching Begin/sec|主动缓存的开始速率。|  
|Proactive Caching Completion/sec|主动缓存的完成速率。|  
  
###  <a name="bkmk_ProcAggregations"></a> 处理聚合  
 与 Microsoft Analysis Services 处理 MOLAP 数据文件中的聚合相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current partitions|当前正在处理的分区数。|  
|Total partitions|已处理的分区总数（成功或失败）。|  
|Memory size rows|内存中当前聚合的大小。  此计数为估计值。|  
|Memory size bytes|内存中当前聚合的大小。  此计数为估计值。|  
|Rows merged/sec|行合并或插入到聚合中的速率。|  
|Rows created/sec|聚合行的创建速率。|  
|Temp file rows written/sec|将行写入临时文件的速率。  聚合超过内存限制时会写入临时文件。|  
|Temp file bytes written/sec|将字节写入临时文件的速率。  聚合超过内存限制时会写入临时文件。|  
  
###  <a name="bkmk_ProcIndexes"></a> 处理索引  
 与 Microsoft Analysis Services 处理 MOLAP 数据文件的索引相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current partitions|当前正在处理的分区数。|  
|Total partitions|已处理的分区总数（成功或失败）。|  
|Rows/sec|使用 MOLAP 文件中的行创建索引的速率。|  
|总计行|使用 MOLAP 文件中的行创建索引的总行数。|  
  
###  <a name="bkmk_Processing"></a> 处理  
 与 Microsoft Analysis Services 数据处理相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Rows read/sec|从所有关系数据库中读取行的速率。|  
|Total rows read|从所有关系数据库中读取的行数。|  
|Rows converted/sec|处理过程中转换的行的速率。|  
|Total rows converted|处理过程中转换的行数。|  
|Rows written/sec|处理过程中写入的行的速率。|  
|Total rows written|处理过程中写入的行数。|  
  
###  <a name="bkmk_StorageEngineQuery"></a> 存储引擎查询  
 与 Microsoft Analysis Services 存储引擎查询相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Current measure group queries|当前正在处理的度量值组查询数。|  
|Measure group queries/sec|度量值组查询速率。|  
|Total measure group queries|度量值组查询总数。|  
|Current dimension queries|当前正在处理的维度查询数。|  
|Dimension queries/sec|维度查询速率。|  
|Total dimension queries|维度查询的总数。|  
|Queries answered/sec|应答查询的速率。|  
|Total queries answered|所应答的查询总数。|  
|Bytes sent/sec|服务器为响应查询而向客户端发送字节的速率。|  
|Total bytes sent|服务器为响应查询而发送到客户端的字节总数。|  
|Rows sent/sec|服务器向客户端发送行的速率。|  
|Total rows sent|服务器向客户端发送的行总数。|  
|Queries from cache direct/sec|直接从缓存应答查询的速率。|  
|Queries from cache filtered/sec|通过筛选现有缓存条目来应答查询的速率。|  
|Queries from file/sec|从文件应答查询的速率。|  
|Total queries from cache direct|直接从缓存中派生的查询总数。  请注意，此数目是以分区作为统计单位的。|  
|Total queries from cache filtered|通过筛选现有缓存条目而应答的查询总数。|  
|Total queries from file|从文件应答的查询总数。|  
|Map reads/sec|使用“映射”文件进行的逻辑读取操作数。|  
|Map bytes/sec|从“映射”文件读取的字节数。|  
|Data reads/sec|使用“数据”文件进行的逻辑读取操作数。|  
|Data bytes/sec|从“数据”文件读取的字节数。|  
|Avg time/query|每个查询的平均时间（毫秒）。  基于上一次计数器统计以来所应答查询的响应时间。|  
|Network round trips/sec|网络往返的速率。  这包括客户端/服务器的所有通信。|  
|Total network round trips|网络往返总计。  这包括客户端/服务器的所有通信。|  
|Flat cache lookups/sec|平面缓存查找速率。  这包括全局、会话和查询范围的平面缓存。|  
|Flat cache hits/sec|平面缓存命中率。  这包括全局、会话和查询范围的平面缓存。|  
|Calculation cache lookups/sec|计算缓存查找的速率。  这包括全局、会话和查询范围的计算缓存。|  
|Calculation cache hits/sec|计算缓存命中率。  这包括全局、会话和查询范围的计算缓存。|  
|Persisted cache lookups/sec|持久缓存查找速率。  持久缓存由 MDX 脚本的 CACHE 语句创建。|  
|Persisted cache hits/sec|持久缓存命中率。  持久缓存由 MDX 脚本的 CACHE 语句创建。|  
|Dimension cache lookups/sec|维度缓存查找速率。|  
|Dimension cache hits/sec|维度缓存命中率。|  
|Measure group cache lookups/sec|度量值组缓存查找速率。|  
|Measure group cache hits/sec|度量值组缓存命中率。|  
|Aggregation lookups/sec|聚合查找速率。|  
|Aggregation hits/sec|聚合命中率。|  
  
###  <a name="bkmk_Threads"></a> 线程  
 与 Microsoft Analysis Services 线程相关的统计信息。  
  
|计数器|Description|  
|-------------|-----------------|  
|Short parsing idle threads|短分析线程池中的空闲线程数。|  
|Short parsing busy threads|短分析线程池中的忙线程数。|  
|Short parsing job queue length|短分析线程池队列中的作业数。|  
|Short parsing job rate|作业通过短分析线程池的速率。|  
|Long parsing idle threads|长分析线程池中的空闲线程数。|  
|Long parsing busy threads|长分析线程池中的忙线程数。|  
|Long parsing job queue length|长分析线程池队列中的作业数。|  
|Long parsing job rate|作业通过长分析线程池的速率。|  
|Query pool idle threads|查询线程池中的空闲线程数。|  
|Query pool busy threads|查询线程池中的忙线程数。|  
|Query pool job queue length|查询线程池队列中的作业数。|  
|Query pool job rate|作业通过查询线程池的速率。|  
|Processing pool idle non-I/O threads|专用于非 I/O 作业的处理线程池中空闲线程的数目。|  
|Processing pool busy non-I/O threads|处理线程池中正在运行非 I/O 作业的线程的数目。|  
|Processing pool job queue length|处理线程池队列中的非 I/O 作业数。|  
|Processing pool job rate|通过处理线程池的非 I/O 作业的速率。|  
|Processing pool idle I/O job threads|处理线程池中用于 I/O 作业的空闲线程的数目。|  
|Processing pool busy I/O job threads|处理线程池中正在运行 I/O 作业的线程的数目。|  
|Processing pool I/O job queue length|处理线程池队列中的 I/O 作业数。|  
|Processing pool I/O job completion rate|通过处理线程池的 I/O 作业的速率。|  
  
  
