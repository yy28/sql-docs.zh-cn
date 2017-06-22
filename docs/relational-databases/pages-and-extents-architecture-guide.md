---
title: "页和区体系结构指南 | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- page and extent architecture guide
- guide, page and extent architecture
ms.assetid: 83a4aa90-1c10-4de6-956b-7c3cd464c2d2
caps.latest.revision: 2
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 970981a0f8db1baa802a68ea1186211f031488e6
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="pages-and-extents-architecture-guide"></a>页和区体系结构指南
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

页是 SQL Server 中数据存储的基本单位。 区是由八个物理上连续的页构成的集合。 区有助于有效管理页。 本指南介绍用于管理所有版本的 SQL Server 中的页和区的数据结构。 要设计和开发高效执行的数据库，了解页和区的体系结构是很重要的。

## <a name="pages-and-extents"></a>页和区

SQL Server 中数据存储的基本单位是页。 为数据库中的数据文件（.mdf 或 .ndf）分配的磁盘空间可以从逻辑上划分成页（从 0 到 n 连续编号）。 磁盘 I/O 操作在页级执行。 也就是说，SQL Server 读取或写入所有数据页。

区是八个物理上连续的页的集合，用来有效地管理页。 所有页都存储在区中。

### <a name="pages"></a>页

在 SQL Server 中，页的大小为 8 KB。 这意味着 SQL Server 数据库中每兆字节有 128 页。 每页的开头是 96 字节的标头，用于存储有关页的系统信息。 此信息包括页码、页类型、页的可用空间以及拥有该页的对象的分配单元 ID。

下表说明了 SQL Server 数据库的数据文件中所使用的页类型。

|页类型 | 目录 |
|-------|-------|
|Data |当行中的文本设置为 ON 时，具有除 text、ntext、image、nvarchar(max)、varchar(max)、varbinary(max) 和 xml 数据以外的所有数据的数据行。 |
|索引 |索引条目。 |
|测试/图像 |大型对象数据类型：（text、ntext、image、nvarchar(max)、varchar(max)、varbinary(max) 和 xml 数据） <br> 数据行超过 8 KB 时为可变长度数据类型列：（varchar、nvarchar、varbinary 和 sql_variant） |
|Global Allocation Map、Shared Global Allocation Map |有关区是否分配的信息。 |
|页可用空间 (PFS) |有关页分配和页的可用空间的信息。 |
|索引分配映射 (Index Allocation Map) |有关每个分配单元中表或索引所使用的区的信息。 |
|大容量更改映射表 |有关每个分配单元中自最后一条 BACKUP LOG 语句之后的大容量操作所修改的区的信息。 |
|差异更改映射表 |有关每个分配单元中自最后一条 BACKUP DATABASE 语句之后更改的区的信息。 |

> [!NOTE]
> 日志文件不包含页，而是包含一系列日志记录。

在数据页上，数据行紧接着标头按顺序放置。 页的末尾是行偏移表，对于页中的每一行，每个行偏移表都包含一个条目。 每个条目记录对应行的第一个字节与页首的距离。 行偏移表中的条目的顺序与页中行的顺序相反。

![page_architecture](../relational-databases/media/page-architecture.gif)

**大型行支持**  

行不能跨页，但是行的部分可以移出行所在的页，因此行实际可能非常大。 页的单个行中的最大数据量和开销是 8,060 字节 (8 KB)。 但是，这不包括用 Text/Image 页类型存储的数据。 对于包含 varchar、nvarchar、varbinary 或 sql_variant 列的表，可以放宽此限制。 当表中的所有固定列和可变列的行的总大小超过限制的 8,060 字节时，SQL Server 将从最大宽度的列开始动态将一个或多个可变长度列移动到 ROW_OVERFLOW_DATA 分配单元中的页。 每当插入或更新操作将行的总大小增大到超过限制的 8,060 字节时，将会执行此操作。 将列移动到 ROW_OVERFLOW_DATA 分配单元中的页后，将在 IN_ROW_DATA 分配单元中的原始页上维护 24 字节的指针。 如果后续操作减小了行的大小，SQL Server 会动态将列移回到原始数据页。 


### <a name="extents"></a>Extents 

区是管理空间的基本单位。 一个区是八个物理上连续的页（即 64 KB）。 这意味着 SQL Server 数据库中每兆字节有 16 个区。

为了使空间分配有效，SQL Server 不会将所有区分配给包含少量数据的表。 SQL Server 有两种类型的区： 

* 统一区，由单个对象所有。区中的所有 8 页只能由所属对象使用。
* 混合区，最多可由八个对象共享。 区中八页的每页可由不同的对象所有。


通常从混合区向新表或索引分配页。 当表或索引增长到 8 页时，将变成使用统一区进行后续分配。 如果对现有表创建索引，并且该表包含的行足以在索引中生成 8 页，则对该索引的所有分配都使用统一区进行。

![Extents](../relational-databases/media/extents.gif)

## <a name="managing-extent-allocations-and-free-space"></a>管理区分配和可用空间 

管理区分配情况并跟踪可用空间的 SQL Server 数据结构有一个相对简单的结构。 这有下列好处： 

* 可用空间信息被紧密压缩，因此包含此信息的页相对较少。   
  这样，可提高速度，因为它减少了检索分配信息时所需的磁盘读取量。 同时还可增加分配页保留在内存中的机会并且不需要更多的读操作。 

* 大多数分配信息不是链在一起的。 这就简化了对分配信息的维护。    
  可以快速执行每个页的分配或释放。 这将减少需要分配页或释放页的并发任务之间的争用。 

### <a name="managing-extent-allocations"></a>管理区分配

SQL Server 使用两种类型的分配映射表来记录区的分配： 

* 全局分配映射表 (GAM)   
  GAM 页记录已分配的区。 每个 GAM 包含 64,000 个区，相当于近 4 GB 的数据。 GAM 用一个位来表示所涵盖区间内的每个区的状态。 如果位为 1，则区可用；如果位为 0，则区已分配。 

* 共享全局分配映射表 (SGAM)   
  SGAM 页记录当前用作混合区且至少有一个未使用的页的区。 每个 SGAM 包含 64,000 个区，相当于近 4 GB 的数据。 SGAM 用一个位来表示所涵盖区间内的每个区的状态。 如果位为 1，则区正用作混合区且有可用页。 如果位为 0，则区未用作混合区，或者虽然用作混合区但其所有页均在使用中。 

根据区当前的使用情况，GAM 和 SGAM 中每个区具有以下位模式。 

|区的当前使用情况 | GAM 位设置 | SGAM 位设置 |
|---------|----------|------| 
|可用，未使用 |1 |0 |
|统一区或已满的混合区 |0 |0 |
|具有可用页的混合区 |0 |1 |
 
这将简化区管理算法。 为了分配统一区，数据库引擎将在 GAM 中搜索为 1 的位，并将其设置为 0。 为了查找具有可用页的混合区，数据库引擎将在 SGAM 中搜索为 1 的位。 为了分配混合区，数据库引擎将在 GAM 中搜索为 1 的位，并将其设置为 0；然后也将 SGAM 中相应的位设置为 1。 若取消分配某个区，数据库引擎确保 GAM 位设置为 1，而 SGAM 位设置为 0。 数据库引擎在内部实际使用的算法比本主题中介绍的更复杂，因为数据库引擎在数据库中平均分布数据。 但是，由于无需管理区分配信息链，因此即使是实际算法也会被简化。

### <a name="tracking-free-space"></a>跟踪可用空间

页可用空间 (PFS) 页记录每页的分配状态，是否已分配单个页以及每页的可用空间量。 PFS 对每页都有一个字节，记录该页是否已分配。如果已分配，则记录该页是为空、已满 1% 到 50%、已满 51% 到 80%、已满 81% 到 95% 还是已满 96% 到 100%。

将区分配给对象后，数据库引擎将使用 PFS 页来记录区中的哪些页已分配或哪些页可用。 当数据库引擎必须分配新页时，将使用此信息。 保留的页中的可用空间量仅用于堆和 Text/Image 页。 当数据库引擎必须找到一个具有可用空间的页来保存新插入的行时，将使用此信息。 索引不要求跟踪页的可用空间，因为插入新行的点是由索引键值设置的。

在数据文件中，PFS 页是文件头页之后的第一页（页码为 1）。 接着是 GAM 页（页码为 2），然后是 SGAM 页（页码为 3）。 第一个 PFS 页之后是一个大小大约为 8,000 页的 PFS 页。 在第 2 页的第一个 GAM 页之后还有另一个 GAM 页（包含 64,000 个区），在第 3 页的第一个 SGAM 页之后也有另一个 SGAM 页（包含 64,000 个区）。 下图显示了数据库引擎用来分配和管理区的页顺序。

![manage_extents](../relational-databases/media/manage-extents.gif)

## <a name="managing-space-used-by-objects"></a>管理对象使用的空间 

“索引分配映射 (IAM)”页将映射分配单元使用的数据库文件中 4 GB 部分中的区。 分配单元有下列三种类型：

* IN_ROW_DATA   
    用于存储堆分区或索引分区。

* LOB_DATA   
   包含大型对象 (LOB) 数据类型，如 xml、varbinary(max) 和 varchar(max)。

* ROW_OVERFLOW_DATA   
   包含超过 8,060 字节行大小限制的 varchar、nvarchar、varbinary 或 sql_variant 列中存储的可变长度数据。 

堆或索引的每个分区至少包含一个 IN_ROW_DATA 分配单元。 根据堆或索引的架构，可能还包含一个 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元。 有关分配单元的详细信息，请参阅表和索引组织。

一个 IAM 页在文件中的范围为 4 GB，与 GAM 或 SGAM 页的范围相同。 如果分配单元包含来自多个文件的区，或者超过一个文件的 4 GB 范围，那么一个 IAM 链中将链接多个 IAM 页。 因此，每个分配单元在有区的每个文件中至少有一个 IAM 页。 如果分配给分配单元的文件中的区的范围超过了一个 IAM 页能够记录的范围，一个文件中也可能会有多个 IAM 页。 

![iam_pages](../relational-databases/media/iam-pages.gif)

IAM 页根据需要分配给每个分配单元，在文件中的位置也是随机的。 系统视图 (sys.system_internals_allocation_units) 指向分配单元的第一个 IAM 页。 该分配单元的所有 IAM 页都链接到一个链中。

> [!IMPORTANT]
> sys.system_internals_allocation_units 系统视图仅供内部使用，随时可能更改。 不保证兼容性。

![iam_chain](../relational-databases/media/iam-chain.gif)
 
每个分配单元的链中所链接的 IAM 页 IAM 页有一个标头，指明 IAM 页所映射的区范围的起始区。 IAM 页中还有一个大位图，其中每个位代表一个区。 位图中的第一个位代表范围内的第一个区，第二个位代表第二个区，依此类推。 如果某个位是 0，它所代表的区将不会分配给拥有该 IAM 页的分配单元。 如果这个位是 1，它所代表的区将被分配给拥有该 IAM 页的分配单元。

当 SQL Server 数据库引擎必须在当前页中插入新行，而当前页中没有可用空间时，它将使用 IAM 和 PFS 页查找要将该行分配到的页，或者（对于堆或 Text/Image 页）查找具有足够空间容纳该行的页。 数据库引擎使用 IAM 页查找分配给分配单元的区。 对于每个区，数据库引擎将搜索 PFS 页，以查看是否有可用的页。 每个 IAM 和 PFS 页覆盖大量数据页，因此一个数据库内只有很少的 IAM 和 PFS 页。 这意味着 IAM 和 PFS 页通常位于内存中的 SQL Server 缓冲池中，以便可以快速搜索它们。 对于索引，新行的插入点由索引键设置。 在这种情况下，不会出现上述搜索过程。

仅当数据库引擎不能在现有的区中快速找到空间足够容纳插入行的页时，才将新区分配给分配单元。 数据库引擎使用比例分配算法从文件组的可用区中分配区。 如果文件组内有两个文件，而一个文件的可用空间是另一个文件的两倍，那么每从后一个文件分配一页，就从前一个文件分配两页。 这意味着文件组内的每个文件应该有近似的空间使用百分比。 

 
## <a name="tracking-modified-extents"></a>跟踪已修改的区 

SQL Server 使用两个内部数据结构跟踪被大容量复制操作修改的区，以及自上次完整备份后修改的区。 这些数据结构极大地加快了差异备份的速度。 当数据库使用大容量日志恢复模式时，这些数据结构也可以加快将大容量复制操作记录至日志的速度。 与全局分配图 (GAM) 和共享全局分配图 (SGAM) 页相同，这些结构也是位图，其中的每一位代表一个单独的区。 

* 差异更改映射表 (DCM)   
   这样便可以跟踪自上次执行 BACKUP DATABASE 语句后更改过的区。 如果扩展盘区的位是 1，则自上次执行 BACKUP DATABASE 语句后扩展盘区已被修改。 如果位是 0，则扩展盘区没有被修改。 差异备份只读取 DCM 页便可以确定已修改的区。 这样大大减少了差异备份必须扫描的页数。 运行差异备份所需的时间与自上次执行 BACKUP DATABASE 语句之后修改的区数成正比，而不是与整个数据库的大小成正比。 

* 大容量更改映射表 (BCM)   
   跟踪自上次执行 BACKUP LOG 语句后，被大容量日志记录操作修改的区。 如果某个扩展盘区的位是 1，表明自上次执行 BACKUP LOG 语句后，该扩展盘区已经被有日志记录的大容量复制操作修改。 如果位是 0，则该扩展盘区未被有日志记录的大容量复制操作修改。 尽管所有数据库中都显示 BCM 页，但只有在数据库使用大容量日志记录恢复模式时，才会与 BCM 页有关。 在此恢复模式中，当执行 BACKUP LOG 时，备份进程将扫描 BCM 查找已经修改的区。 然后，将那些区包括在日志备份中。 如果数据库从数据库备份和一系列事务日志备份恢复，便可以恢复大容量日志记录操作。 在使用简单恢复模式的数据库中，BCM 页是不相关的，因为大容量日志记录操作不记入日志。 在使用完整恢复模式的数据库中，BCM 页同样不相关，因为该恢复模式将大容量日志记录操作视为有完整日志记录的操作。 

DCM 页和 BCM 页的间隔与 GAM 和 SGAM 页的间隔相同，都是 64,000 个区。 在物理文件中，DCM 和 BCM 页位于 GAM 和 SGAM 页之后。

![special_page_order](../relational-databases/media/special-page-order.gif)
 

