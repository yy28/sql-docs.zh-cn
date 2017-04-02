---
title: "改进全文索引的性能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "性能 [SQL Server]，全文搜索"
  - "全文查询 [SQL Server]，性能"
  - "爬网 [全文搜索]"
  - "全文检索 [SQL Server]，性能"
  - "全文搜索 [SQL Server]，性能"
  - "批处理 [SQL Server]，全文搜索"
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
caps.latest.revision: 68
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 67
---
# 改进全文索引的性能
  硬件资源（例如内存、磁盘速度、CPU 速度和计算机体系结构）会影响全文索引和全文查询的性能。  
  
##  <a name="causes"></a> 性能问题的常见原因  
 导致全文索引性能降低的主要原因是硬件资源的限制：  
  
-   如果筛选器后台程序主机进程 (fdhost.exe) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程 (sqlservr.exe) 的 CPU 使用率接近 100%，则 CPU 会成为瓶颈。  
  
-   如果平均磁盘等待队列长度是磁盘头数量的两倍以上，则磁盘将成为瓶颈。 主要的解决方法是创建独立于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库文件和日志的全文目录。 将日志、数据库文件和全文目录分别放在不同的磁盘上。 购买运行速度更快的磁盘和使用 RAID 也能帮助改善索引性能。  
  
-   如果物理内存不足，则可能是遇到了内存瓶颈。  
  
    > [!NOTE]  
    >  从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，全文引擎可以使用 AWE 内存，因为全文引擎是 sqlservr.exe 的一部分。  
  
 如果系统没有硬件瓶颈，则全文搜索的索引性能主要取决于以下因素：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建全文批次花费的时间。  
  
-   筛选器后台程序能以多快的速度处理这些批次。  
  
> [!NOTE]  
>  与完全填充不同，增量、手动和自动更改跟踪填充的设计目的并不是为了最大程度地利用硬件资源以获得更高速度。 因此，这些优化建议可能不会增强全文索引的性能。  
  
 填充完成后，将触发最终的合并过程，以便将索引碎片合并为一个主全文索引。 由于只需要查询主索引而不需要查询大量索引碎片，因此这将提高查询性能，并且可以使用更好的计分统计信息来得出相关性排名。 请注意，由于合并索引碎片时必须读取和写入大量数据，所以主合并可能会耗费大量 I/O，但它不会阻塞传入的查询。  
  
> [!IMPORTANT]  
>  对大量数据进行主合并会创建一个长时间运行的事务，在检查点期间延迟事务日志的截断。 在这种情况下，事务日志可能会在完整恢复模式下显著增长。 作为最佳做法，在使用完整恢复模式的数据库中重新组织较大的全文索引之前，应确保事务日志中包含足够的空间用于长时间运行的事务。 有关详细信息，请参阅[管理事务日志文件的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)。  
  
##  <a name="tuning"></a> 优化全文索引的性能  
 若要最大限度地提高全文索引的性能，请实施下列最佳做法：  
  
-   若要最大程度地使用所有处理器或内核，请将 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)‘**max full-text crawl ranges**’ 设置为系统的 CPU 数。 有关此配置选项的信息，请参阅 [max full-text crawl range 服务器配置选项](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)。  
  
-   请确保基表具有聚集索引。 对聚集索引的第一列使用整数数据类型。 避免在聚集索引的第一列使用 GUID。 对聚集索引执行多范围填充可以产生最高的填充速度。 我们建议充当全文键的列采用整数数据类型。  
  
-   使用 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 语句更新基表的统计信息。 更重要的是，更新聚集索引或全文键的统计信息以进行完全填充。 这有助于多范围填充在表上生成良好的分区。  
  
-   如果要提高增量填充的性能，请对 **timestamp** 列生成辅助索引。  
  
-   在大型多 CPU 计算机上执行完全填充之前，建议你通过设置**最大服务器内存**值来暂时限制缓冲池的大小，从而留出足够的内存供 fdhost.exe 进程及操作系统使用。 有关详细信息，请参阅本主题后面的“估计筛选器后台程序宿主进程 (fdhost.exe) 的内存需求量”。  
  
##  <a name="full"></a> 解决完全填充性能问题  
 若要诊断性能问题，请查看全文爬网日志。 有关爬网日志的信息，请参阅[填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
 如果对完全填充的性能不满意，则建议按顺序执行以下故障排除步骤。  
  
### 物理内存使用量  
 在全文填充期间，fdhost.exe 或 sqlservr.exe 的内存有可能不足。 如果全文爬网日志显示 fdhost.exe 正在反复重新启动，或系统返回错误代码 8007008，则意味着这些进程中的某一个进程内存不足。 如果 fdhost.exe 在生成转储（特别是在大型多 CPU 计算机上），则该进程的内存可能不足。  
  
> [!NOTE]  
>  若要获得有关全文爬网所用的内存缓冲区的信息，请参阅 [sys.dm_fts_memory_buffers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)。  
  
 可能的原因如下：  
  
-   如果在完全填充期间可用的物理内存数量是零，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 缓冲池可能正占用系统的大部分物理内存。  
  
     sqlservr.exe 进程试图侵占缓冲池的所有可用内存（最大为配置的最大服务器内存）。 如果分配的**最大服务器内存**过大，fdhost.exe 进程可能会遇到内存不足的状况和无法分配共享内存的问题。  
  
    > [!NOTE]  
    >  在多 CPU 计算机上进行全文填充期间，fdhost.exe 或 sqlservr.exe 之间可能出现缓冲池内存争用。 由此造成的共享内存不足会导致批次重试、内存抖动并让 fdhost.exe 进程进行转储。  
  
     可以通过正确设置 **缓冲池的** 最大服务器内存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 值来解决此问题。 有关详细信息，请参阅本主题后面的“估计筛选器后台程序宿主进程 (fdhost.exe) 的内存需求量”。 减小用于全文索引的批次大小可能也会有用。  
  
-   分页问题  
  
     页文件大小不足也会导致 fdhost.exe 或 sqlservr.exe 的内存不足，例如在具有增长受限的较小页文件的系统上。  
  
     如果爬网日志未指示存在任何与内存相关的故障，则很可能是因为过度分页导致性能下降。  
  
### 估计筛选器后台程序宿主进程 (fdhost.exe) 的内存需求量  
 进行填充时 fdhost.exe 进程需要的内存量主要取决于它使用的全文爬网范围数、入站共享内存 (ISM) 的大小以及最大 ISM 实例数。  
  
 可以使用下面的公式粗略估算筛选器后台程序宿主占用的内存量（以字节为单位）：  
  
 *number_of_crawl_ranges* \**ism_size***max_outstanding_isms*\* 2  
  
 上面公式中的变量的默认值如下所示：  
  
|**变量**|**默认值**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|CPU 的数目|  
|*ism_size*|x86 计算机为 1 MB<br /><br /> x64 计算机为 4 MB、8 MB 或 16MB，具体取决于物理内存总量|  
|*max_outstanding_isms*|x86 计算机为 25<br /><br /> x64 计算机为 5|  
  
 下表列出了有关如何估算 fdhost.exe 的内存需求量的准则。 此表中的公式使用以下值：  
  
-   *F*，它是 fdhost.exe 所需内存的估计值（以 MB 为单位）。  
  
-   *T*，它是系统中可用物理内存的总量（以 MB 为单位）。  
  
-   *M*，它是 **最大服务器内存** 最优设置。  
  
> [!IMPORTANT]  
>  有关公式的基本信息，请参阅下面的 (1)、(2) 和 (3)。  
  
|平台|估计 fdhost.exe 的内存需求量 (MB) -*F*^1|用于计算最大服务器内存的公式 -*M*^2|  
|--------------|-----------------------------------------------------------|-----------------------------------------------------|  
|x86|*F* **=** *爬网范围数* **\*** 50|*M* **=最小值(** *T* **,** 2000**)–***F***–** 500|  
|x64|*F* **=** *爬网范围数* **\*** 10 **\*** 8|*M* **=** *T* **–** *F* **–** 500|  
  
 (1) 如果正在进行多个完全填充，则分别计算每个完全填充的 fdhost.exe 内存需求量，如 *F1*、*F2* 等。 然后计算 *M* 为 *T***–** sigma**(***F*i**)**。  
  
 (2) 500 MB 是系统中其他进程所需内存的估计值。 如果系统正在执行其他工作，请相应地增加此值。  
  
 (3) 对于 x64 平台，*ism_size* 假定为 8 MB。  
  
 **示例：估计 fdhost.exe 的内存需求量**  
  
 此示例针对具有 8GM RAM 和 4 个双核处理器的 AMD64 计算机。 首先计算出 fdhost.exe 所需内存的估计值*F*。 爬网范围数是 `8`。  
  
 `F = 8*10*8=640`  
  
 然后，计算出 **最大服务器内存**的最佳值*M*。 该系统的可用物理内存总量（以 MB 为单位）—*T*—是 `8192`。  
  
 `M = 8192-640-500=7052`  
  
 **示例：设置最大服务器内存**  
  
 此示例使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 和 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句将**最大服务器内存**设置为上一个示例中计算得到的 *M* 的值，`7052`：  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
 **设置最大服务器内存配置选项**  
  
-   [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
### 可以降低 CPU 占用率的因素  
 我们希望当平均 CPU 占用率低于大约 30% 时完全填充的性能不是最佳的。 本节讨论影响 CPU 占用率的一些因素。  
  
-   长时间等待页面  
  
     若要了解等待页面的时间是否太长，请执行下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    Execute SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     下表描述了这里需要了解的等待类型。  
  
    |等待类型|说明|可能的解决方法|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH（_EX 或 _UP）|这可能表明存在 IO 瓶颈，在此情况下通常还会发现平均磁盘队列长度很高。|将全文索引移动到其他磁盘上的其他文件组可能有助于减少 IO 瓶颈。|  
    |PAGELATCH_EX（或 _UP）|这可能表明多个正在试图写入相同数据库文件的线程之间存在大量争用现象。|将文件添加到全文索引所在的文件组可能有助于减轻此类争用。|  
  
     有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。  
  
-   扫描基表的效率很低  
  
     完全填充将扫描基表，以生成批次。 在下列情况下，这样的表扫描可能很低效：  
  
    -   如果基表有很高百分比的行外列正在建立全文索引，则扫描基表以生成批次可能成为瓶颈。 在这种情况下，使用 **varchar(max)** 或 **nvarchar(max)** 对较小的数据进行行内移动可能有用。  
  
    -   如果基表非常零碎，扫描可能很低效。 有关计算行外数据和索引碎片的信息，请参阅 [sys.dm_db_partition_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 和 [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)。  
  
         若要减少碎片，可以重新组织或重新生成聚集索引。 有关详细信息，请参阅[重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
##  <a name="filters"></a> 解决索引性能由于筛选器而变慢的问题  
 在填充全文索引时，全文引擎使用以下两种类型的筛选器：多线程筛选器和单线程筛选器。 有些文档（如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文档）使用多线程筛选器进行筛选。 另外一些文档使用单线程筛选器进行筛选，如 Adobe Acrobat 可移植文档格式 (PDF) 文档。  
  
 为了安全起见，筛选器是由筛选器后台程序主机进程加载的。 服务器实例对所有多线程筛选器使用多线程进程，并对所有单线程筛选器使用单线程进程。 如果使用多线程筛选器的文档包含使用单线程筛选器的嵌入文档，全文引擎将启动单线程进程以处理嵌入文档。 例如，在遇到包含 PDF 文档的 Word 文档时，全文引擎使用多线程进程来处理 Word 内容，并启动单线程进程以处理 PDF 内容。 但是，单线程筛选器可能无法在此环境中正常工作，并且可能会破坏筛选进程的稳定性。 在某些频繁出现此类嵌入的环境中，它可能会导致筛选进程崩溃。 如果发生这种情况，全文引擎会将任何失败的文档（如包含嵌入 PDF 内容的 Word 文档）重新传送到单线程筛选进程。 如果频繁进行重新传送，将会导致全文索引进程性能下降。  
  
 若要解决该问题，必须将容器文档（此处为 Word 文档）的筛选器标记为单线程筛选器。 可以更改筛选器注册表值，以便将给定筛选器标记为单线程筛选器。 若要将筛选器标记为单线程筛选器，你需要将筛选器的 **ThreadingModel** 注册表值设置为 **Apartment Threaded**。 有关单线程单元的信息，请参阅白皮书[了解和使用 COM 线程模型](http://go.microsoft.com/fwlink/?LinkId=209159)。  
  
## 另请参阅  
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [max full-text crawl range 服务器配置选项](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)   
 [创建和管理全文索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)   
 [排除全文索引故障](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
  