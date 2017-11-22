---
title: "内存管理体系结构指南 | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e3dd8e87facc46305c7a3f86e9f7507fa29cd6b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="memory-management-architecture-guide"></a>内存管理体系结构指南
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

## <a name="memory-architecture"></a>内存体系结构

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将根据需要动态获取并释放内存。 虽然该选项仍然存在且在有些环境下需要用到，但通常情况下管理员不必指定为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]分配多少内存。

所有数据库软件的主要设计目标之一是尽量减少磁盘 I/O，因为磁盘的读取和写入操作占用大量资源。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在内存中生成缓冲池，用于保存从数据库读取的页。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的大量代码专门用于尽可能减少磁盘与缓冲池之间的物理读写次数。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 设法在以下两个目标之间达到平衡：

* 防止缓冲池变得过大，从而导致整个系统内存不足。
* 尽量增加缓冲池达的大小，以便尽量减少数据库文件的物理 I/O。


> [!NOTE]
> 在负载过重的系统中，某些在运行时需要大量内存的大型查询不能获取所需的最小内存量，并在等待内存资源时收到超时错误。 若要解决此问题，请增大 [query wait 选项](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)。 对于并行查询，请考虑减小 [最大并行度选项](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。
 
> [!NOTE]
> 在负载过重而内存不足的系统中，对于查询计划中带有合并联接、排序和位图的查询，如果无法获得位图所需的最小内存量，可以删除位图。 这会影响查询性能，并且如果排序过程无法容纳在内存中，就会增加 tempdb 数据库中工作表的使用量，从而导致 tempdb 增大。 若要解决此问题，可添加物理内存或优化查询以使用其他更迅速的查询计划。
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供最大内存量

通过使用 AWE 和“锁定内存中的页”权限，可为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎提供下列内存量。 （下表包含一个 32 位版本的列，这些版本不再可用。）

| |32 位 <sup>1</sup> |64 位
|-------|-------|-------| 
|常规内存 |所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 最大处理虚拟地址空间限制： <br>- 2 GB<br>- 3 GB，带有 /3gb 引导参数 <sup>2</sup> <br>- 4 GB，在 WOW64 <sup>3</sup>上 |所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 最大处理虚拟地址空间限制： <br>- 7 TB，带有 IA64 体系结构（ [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 及更高版本中不支持 IA64）<br>- 操作系统支持的最大值，带有 x64 体系结构 <sup>4</sup>
|AWE 机制（允许 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 32 位平台上超过处理虚拟地址空间限制。） |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition、Enterprise Edition 和 Developer Edition：缓冲池最多可以访问 64 GB 内存。|不适用 <sup>5</sup> |
|“锁定内存中的页”操作系统 (OS) 权限（允许锁定物理内存，防止 OS 对锁定的内存进行分页。）<sup>6</sup> |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition、Enterprise Edition 和 Developer Edition：[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 进程使用 AWE 机制所必需的。 通过 AWE 机制分配的内存不能出页。 <br> 授予此权限但未启用 AWE 不会对服务器产生影响。 |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition 和 Developer Edition：建议，以避免操作系统分页。 是否具有性能优势取决于工作负荷。 可访问的内存量类似于常规内存的情况。 |

<sup>1</sup> 32 位版本不可用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]作为开头。  
<sup>2</sup> /3gb 是一个操作系统启动参数。 有关详细信息，请访问 MSDN 库。  
<sup>3</sup> WOW64 (Windows on Windows 64) 是 32 位 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 64 位操作系统上运行的一种模式。  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition 最大支持 128 GB。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition 支持操作系统的最大值。  
<sup>5</sup> 请注意，sp_configure awe enabled 选项存在于 64 位 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上，但将被忽略。    
<sup>6</sup> 如果授予“锁定内存中的页”权限 (LPIM)（在支持 AWE 的 32 位系统上或单独在 64 位系统上），建议也要设置最大服务器内存。

> [!NOTE]
> 旧版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可在 32 位操作系统上运行。 在 32 位操作系统上访问超过 4 GB 的内存需要地址窗口化扩展插件 (AWE) 对内存进行管理。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 64 位操作系统上运行，则不需要。 有关 AWE 的详细信息，请参阅 [2008 文档中的](https://msdn.microsoft.com/library/ms189334) 进程地址空间 [和](https://msdn.microsoft.com/library/ms191481) 管理大型数据库的内存 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。   


## <a name="dynamic-memory-management"></a>动态内存管理

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎的默认内存管理行为是获取尽可能多的内存而不会造成系统内存短缺。 数据库引擎通过使用 Microsoft Windows 中的内存通知 API 来实现这一点。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的虚拟地址空间可分为两个不同的区域：缓冲池占用的空间和其余空间。 如果启用了 AWE 机制，缓冲池就可以驻留在 AWE 映射内存中，为数据库页提供更多的空间。 

缓冲池用作 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的主内存分配源。 驻留在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 进程中且没有使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 内存管理设备的外部组件（例如 COM 对象），将使用缓冲池占用的虚拟地址空间以外的内存。

启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 时，它将基于多个参数（例如系统的物理内存量、服务器线程数和各个引导参数）计算缓冲池的虚拟地址空间的大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将为缓冲池保留计算得到的进程虚拟地址空间量，但它仅为当前负荷获取（提交）所需的物理内存量。

然后实例将继续获取支持工作负荷所需的内存。 随着用户连接和运行查询的逐步增多， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将按需获取更多的物理内存。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例将继续获取物理内存直到达到自己的最大服务器内存分配目标或 Windows 指示不再有可用剩余内存；如果该实例获取的内存超过最小服务器内存设置并且 Windows 指示可用内存短缺，将释放内存。

随着在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的计算机上启动其他应用程序，这些应用程序将会占用内存，从而使可用物理内存量降到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目标以下。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例将调整其内存使用量。 如果另一个应用程序已停止，并且可用内存增多， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例会增加其内存分配的大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 每秒可释放和获取几 MB 的内存，从而根据内存分配变化快速做出调整。


## <a name="effects-of-min-and-max-server-memory"></a>min server memory 和 max server memory 的影响

“最小服务器内存”和“最大服务器内存”配置选项建立 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎缓冲池使用的内存量的上限和下限。 缓冲池并不立即获取最小服务器内存中指定的内存量。 缓冲池启动时只使用初始化所需的内存。 随着数据库引擎工作负荷的增加，它将继续获取支持工作负荷所需的内存。 在达到最小服务器内存中指定的内存量之前，缓冲池不会释放它获取的任何内存。 达到最小服务器内存后，缓冲池将使用标准算法，根据需要来获取和释放内存。 唯一的区别是缓冲池从不将内存分配降到最小服务器内存所指定的水平下，也从不获取超过最大服务器内存所指定水平的内存。

> [!NOTE]
> 作为进程的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将获取超过最大服务器内存选项所指定的内存。 内部和外部组件都可以分配缓冲池以外的内存，这将占用额外内存，但是分配给缓冲池的内存通常表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]占用的内存的最大部分。


数据库引擎获取的内存量完全取决于放置在实例上的工作负荷。 不处理很多请求的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例可能永远不会达到最小服务器内存。

如果为最小服务器内存和最大服务器内存指定相同的值，则一旦分配给数据库引擎的内存达到该值，数据库引擎将停止为缓冲池动态释放和获取内存。

如果在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的计算机上频繁启动或停止其他应用程序，启动这些应用程序所需的时间可能会因 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例分配和释放内存而延长。 另外，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 是几个在一台计算机上运行的服务器应用程序中的一个，系统管理员可能需要控制分配给 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的内存量。 在这些情况下，可以使用最小服务器内存和最大服务器内存选项控制 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可使用的内存量。 有关详细信息，请参阅 [服务器内存配置选项](../database-engine/configure-windows/server-memory-server-configuration-options.md)。

最小服务器内存和最大服务器内存选项以 MB 为单位指定。

## <a name="memory-used-by-includessnoversionincludesssnoversion-mdmd-objects-specifications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象规范使用的内存

以下列表介绍了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中不同对象所用内存量的近似值。 列出的数值为估计值，根据环境以及创建对象的方式可能有所不同。

* 锁定：每个所有者 64 字节 + 32 字节   
* 用户连接：约为 (3* *network_packet_size + 94 kb)    

网络数据包大小是表格数据模式 (TDS) 数据包的大小，该数据包用于应用程序和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎之间的通信。 默认的数据包大小为 4 KB，由“网络数据包大小”配置选项控制。

启用多个活动的结果集 (MARS) 时，用户连接约为 (3 + 3 * num_logical_connections) * network_packet_size + 94 KB

## <a name="buffer-management"></a>缓冲区管理

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的主要用途是存储和检索数据，因此，大量磁盘 I/O 是该数据库引擎的一个核心特点。 此外，完成磁盘 I/O 操作要消耗许多资源并且耗时较长，所以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 侧重于提高 I/O 效率。 缓冲区管理是实现高效 I/O 操作的关键环节。 缓冲区管理组件由下列两种机制组成：用于访问及更新数据库页的缓冲区管理器和用于减少数据库文件 I/O 的缓冲区高速缓存（又称为“缓冲池”）。 

### <a name="how-buffer-management-works"></a>缓冲区管理的工作原理

一个缓冲区就是一个 8KB 大小的内存页，其大小与一个数据页或索引页相当。 因此，缓冲区缓存被划分为多个 8-KB 页。 缓冲区管理器负责将数据页或索引页从数据库磁盘文件读入缓冲区高速缓存中，并将修改后的页写回磁盘。 缓冲区缓存中会保留一页，直到缓冲区管理器需要该缓冲区读入更多数据。 数据只有在被修改后才重新写入磁盘。 在将缓冲区缓存中的数据写回磁盘之前，可对其进行多次修改。 有关详细信息，请参阅 [读取页](../relational-databases/reading-pages.md) 和 [写入页](../relational-databases/writing-pages.md)。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 启动时，它将基于大量参数（例如系统的物理内存量、配置的最大服务器线程数和各个启动参数）计算缓冲区缓存的虚拟地址空间的大小。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将为缓冲区缓存保留此计算得到的进程虚拟地址空间量（称为“内存目标”），但它仅为当前负荷获取（提交）所需的物理内存量。 可查询 **sys.dm_os_sys_info** 目录视图中的 **bpool_commit_target** 和 [bpool_committed columns](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 列，分别返回保留为内存目标的页数以及缓冲区缓存中当前提交的页数。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 启动与缓冲区缓存获得其内存目标之间的间隔称为“增长期”。 在此期间，读取请求将根据需要填充缓冲区。 例如，单页读取请求将填充一个缓冲区页。 也就是说，增长期取决于客户端请求的数量和类型。 通过将单页读取请求转换为对齐的八页请求加快增长。 这样可更快地完成增长，尤其是那些内存容量很大的机器。

因为缓冲区管理器将多数内存用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 进程，所以它会与内存管理器协作以使其他组件能使用其缓冲区。 缓冲区管理器主要与下列组件交互：

* 资源管理器。此交互用于控制内存的整体使用情况以及 32 位平台中的地址空间使用情况。  
* 数据库管理器和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 操作系统 (SQLOS)。此交互用于低级文件 I/O 操作。  
* 日志管理器。此交互用于预写日志记录。  

### <a name="supported-features"></a>支持的功能

缓冲区管理器支持以下功能：

* 缓冲区管理器可识别非一致性内存访问 (NUMA)。 缓冲区高速缓存页将跨硬件 NUMA 节点进行分布，它允许线程访问分配到本地 NUMA 节点上的缓冲区页，而不是从外部内存访问。 
* 缓冲区管理器支持热添加内存，用户无需重新启动服务器即可添加物理内存。 
* 缓冲区管理器在 64 位平台上支持大型页。 页大小因 Windows 版本不同而异。 
* 缓冲区管理器提供通过动态管理视图显示的其他诊断信息。 您可以使用这些视图来监视 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]特有的各种操作系统资源。 例如，您可以使用 sys.dm_os_buffer_descriptors 视图来监视缓冲区缓存中的页。   

### <a name="disk-io"></a>磁盘 I/O
缓冲区管理器仅对数据库执行读写操作。 其他文件和数据库操作（如打开、关闭、扩展和收缩）则由数据库管理器和文件管理器组件执行。 

缓冲区管理器的磁盘 I/O 操作具有以下特点：

* 所有 I/O 操作均异步执行。这样，在后台进行 I/O 操作的同时，即可调用线程继续处理。
* 所有 I/O 操作均在调用线程中发出，除非 affinity I/O 选项处于使用状态。 Affinity I/O mask 选项将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 磁盘 I/O 绑定到指定的 CPU 子集。 在高端 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机事务处理 (OLTP) 环境中，此扩展可以提高 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 线程执行 I/O 的性能。
* 可通过散播-聚集 I/O 实现多页 I/O，散播-聚集 I/O 允许数据传入或传出非连续内存区域。 这意味着 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以快速填充或刷新缓冲区高速缓存，同时避免多个物理 I/O 请求。 

#### <a name="long-io-requests"></a>长时 I/O 请求  
缓冲区管理器报告任何经过 15 秒或更长时间仍未完成的 I/O 请求。 这可以帮助系统管理员区分 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 问题和 I/O 子系统问题。 将报告错误消息 833 并且该消息在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 错误日志中显示如下：

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

长时 I/O 可以是读或写，不过当前消息并未指明。 长时 I/O 消息是警告而不是错误。 它们不指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]存在问题。 报告这些消息是为了帮助系统管理员更快地找到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 响应缓慢的原因，并找出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无法控制的问题。 因此，不需要为它们执行任何操作，但系统管理员应调查 I/O 请求耗时很长的原因以及耗时是否合理。

#### <a name="causes-of-long-io-requests"></a>长时 I/O 请求的原因  
长时 I/O 消息可能指示 I/O 永久阻塞并且永远无法完成（称为“I/O 丢失”），或者只是它尚未完成。 虽然 I/O 丢失往往会导致闩锁超时，但无法根据消息确定是哪种情况。

长时 I/O 往往指示磁盘子系统的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作负荷过于密集。 以下情况可能会指示磁盘子系统不足：

* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作负荷很大时，错误日志中出现多个长时 I/O 消息。
* Perfmon 计数器显示磁盘长时间滞后、磁盘队列长或无磁盘空闲时间。  

长时 I/O 还可能因以下原因所致：I/O 路径中的某个组件（如驱动程序、控制器或固件）不断延迟为早期 I/O 请求提供服务，而为距离当前磁头位置较近的新请求提供服务。 这种对距离读/写磁头当前位置最近的请求进行优先处理的常见技术称为“电梯式查找”。 它可能很难与 Windows 系统监视器 (PERFMON.EXE) 工具配合使用，因为多数 I/O 是立即获得服务的。 执行大量连续 I/O 的工作负荷可能会使长时 I/O 请求情况更严重，如备份和还原、表扫描、排序、创建索引、大容量加载以及清零文件。

单独出现的长时 I/O 如果与上述情况无关，则可能是由硬件或驱动程序问题所致。 系统事件日志可能会包含有助于进行问题诊断的相关事件。

#### <a name="error-detection"></a>错误检测  
数据库页可使用下面两种可选机制之一来保证页在从写入磁盘到再次读取期间的完整性：残缺页保护和校验和保护。 这些机制允许采用独立方法验证数据存储以及诸如控制器、驱动程序、电缆等硬件组件甚至操作系统的正确性。 在即将把页写入磁盘之前将向页添加保护，并在从磁盘读取页后对它进行验证。

#### <a name="torn-page-protection"></a>残缺页保护  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 中引入的“残缺页保护”其实是一种对电源故障导致的页损坏进行检测的方法。 例如，意外电源故障可能导致只有部分页写入磁盘。 使用残缺页保护时，页的每个 512 字节扇区末尾会放置一个 2 位签名（在将原来的 2 位复制到页头之后）。 每次进行写操作时，这个签名在二进制数 01 和 10 之间交替，这样始终可以确定是否只有部分扇区写到磁盘：如果稍后读取页时发现某个位的状态不正确，则说明该页没有被正确写入并会因此检测到残缺页。 残缺页检测使用的资源最少，但是它无法检测到磁盘硬件故障导致的所有错误。

#### <a name="checksum-protection"></a>校验和保护  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 中引入的“校验和保护”提供了更强大的数据完整性检查。 此方法将对写入每一页中的数据进行校验和计算并将其值存储在页头中。 每次从磁盘读取存储了校验和的页时，数据库引擎将重新计算页中数据的校验和。如果新的校验和不同于已存储的校验和，则引发错误 824。 校验和保护比残缺页保护能捕获到更多的错误，因为它受到页中每个字节的影响，但它对资源的消耗较多。 启用校验和后，当缓冲区管理器从磁盘读取页时均可以检测到因电源故障以及硬件或固件故障导致的错误。

页保护类型是包含此页的数据库的属性之一。 校验和保护是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 和更高版本中创建的数据库的默认保护。 页保护机制是在创建数据库时指定的，并且可以使用 ALTER DATABASE 进行更改。 可通过查询 [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目录视图中的 page_verify_option 列或 [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md) 函数的 IsTornPageDetectionEnabled 属性来确定当前的页保护设置。 如果页保护设置发生变化，新设置不会立即影响到整个数据库。 相反，每当下一次写入时，这些页才会采用数据库的当前保护级别。 这意味着数据库可能包含带有不同保护的页。 

## <a name="understanding-non-uniform-memory-access"></a>了解非一致性内存访问

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 能识别非一致性内存访问 (NUMA)，无需特殊配置便可在 NUMA 硬件上顺利地执行。 随着处理器时钟速度的提高和处理器数量的增加，使用这种额外处理能力所需的内存滞后时间越来越难以减少。 为了避开这一问题，硬件供应商提供了大型的 L3 缓存，但这只是一种有限的解决方案。 NUMA 体系结构为此问题提供了可缩放的解决方案。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 已设计为利用基于 NUMA 的计算机而无需更改任何应用程序。 有关详细信息，请参阅 [如何：将 SQL Server 配置为使用软件 NUMA](../database-engine/configure-windows/soft-numa-sql-server.md)。

## <a name="see-also"></a>另请参阅
[读取页](../relational-databases/reading-pages.md)   
 [写入页](../relational-databases/writing-pages.md)

