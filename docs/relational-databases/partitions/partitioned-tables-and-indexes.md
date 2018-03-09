---
title: "已分区表和已分区索引 | Microsoft Docs"
ms.custom: 
ms.date: 01/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: partitions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-partition
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6e5758702f60671b64fc97d9e9e98b89a80ccd6f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="partitioned-tables-and-indexes"></a>已分区表和已分区索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持表和索引分区。 已分区表和已分区索引的数据划分为分布于一个数据库中多个文件组的单元。 数据是按水平方式分区的，因此多组行映射到单个的分区。 单个索引或表的所有分区都必须位于同一个数据库中。 对数据进行查询或更新时，表或索引将被视为单个逻辑实体。 在 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供已分区的表和索引。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在默认情况下支持多达 15,000 个分区。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前的版本中，分区数默认限制为 1000。在基于 x86 的系统上，可以创建分区数超过 1000 的表或索引，但不受支持。  
  
## <a name="benefits-of-partitioning"></a>分区的优点  
 通过对大型表或索引进行分区，可以具有以下可管理性和性能优点。  
  
-   可以快速、高效地传输或访问数据的子集，同时又能维护数据收集的完整性。 例如，将数据从 OLTP 加载到 OLAP 系统之类的操作仅需几秒钟即可完成，而如果不对数据进行分区，执行此操作需要几分钟或几小时。  
  
-   您可以更快地对一个或多个分区执行维护操作。 这些操作的效率更高，因为它们仅针对这些数据子集，而非整个表。 例如，您可以选择在一个或多个分区中压缩数据，或者重新生成索引的一个或多个分区。  
  
-   您可以根据经常执行的查询类型和硬件配置，提高查询性能。 例如，在两个或更多的已分区表中的分区列相同时，查询优化器可以更快地处理这些表之间的同等联接查询，因为可以联接这些分区本身。  
  
     当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 针对 I/O 操作执行数据排序时，它会首先按分区对数据进行排序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次访问一个驱动器，这样可能会降低性能。 为了提高数据排序性能，可以通过设置 RAID 将多个磁盘中的分区数据文件条带化。 这样一来，尽管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍按分区对数据进行排序，但它可以同时访问每个分区的所有驱动器。  
  
     此外，您可以通过对在分区级别而不是整个表启用锁升级来提高性能。 这可以减少表上的锁争用。  
  
## <a name="components-and-concepts"></a>组件和概念  
 以下术语适用于表和索引分区。  
  
 分区函数  
 一种数据库对象，它定义如何根据某个列（称为分区列）的值将表或索引的行映射到一组分区。 也就是说，分区函数定义表将具有的分区数和分区边界的定义方式。 例如，如果有一个包含销售订单数据的表，你可能想要基于“日期时间”  列（如销售日期）将表划分为 12 个（按月）分区。  
  
 分区方案  
 将分区函数的分区映射到一组文件组的数据库对象。 在各个文件组上放置分区的主要原因是为了确保可以在分区上独立执行备份操作。 这是因为您可以在各个文件组上执行备份。  
  
 分区列  
 分区函数对表或索引进行分区时所使用的表或索引列。 参与分区函数的计算列必须显式标记为 PERSISTED。 用作索引列时有效的所有数据类型都可以用作分区依据列， **timestamp**除外。 无法指定 **ntext**、 **text**、 **image**、 **xml**、 **varchar(max)**、 **nvarchar(max)**或 **varbinary(max)** 数据类型。 此外，无法指定 Microsoft .NET Framework 公共语言运行时 (CLR) 用户定义类型和别名数据类型列。  
  
 对齐的索引  
 与其对应的表建立在同一个分区方案之上的一种索引。 如果表与其索引对齐，SQL Server 则可以快速高效地切换分区，同时又能维护表及其索引的分区结构。 索引要与其基表对齐，并不需要与基表参与相同的命名分区函数。 但是，索引和基表的分区函数在实质上必须相同，即：1) 分区函数的参数具有相同的数据类型；2) 分区函数定义了相同数目的分区；3) 分区函数为分区定义了相同的边界值。  
  
 非对齐的索引  
 独立于其相应的表进行分区的一种索引。 也就是说，索引具有不同的分区方案或者放置于不同于基表的单独文件组中。 在下列情况下，设计非对齐的分区索引可能会很有用：  
  
-   基表未分区。  
  
-   索引键是唯一的，不包含表的分区依据列。  
  
-   您希望基表与使用不同联接列的多个表一起参与并置联接。  

 分区排除：查询优化器用来仅访问相关分区以便满足查询的筛选条件的过程。  
  
## <a name="performance-guidelines"></a>性能准则  
 这个新的、更高的 15,000 个分区的限制将影响内存、分区的索引操作、DBCC 命令和查询。 本节介绍将分区数目增加到超过 1,000 个的性能影响并根据需要提供解决方法。 由于对分区最大数目的限制已增加到 15,000 个，因此您可以存储更长时间的数据。 不过，您应该仅保留所需时长的数据，并且在性能和分区数目之间保持平衡。  
  
### <a name="processor-cores-and-number-of-partitions-guidelines"></a>处理器核心和分区数指导方针  
 为了最大发挥并行操作的性能，建议将分区数设置为与处理器核心数相同，最大为 64（这是 SQL Server 可以利用的最大并行处理器数）。  
  
### <a name="memory-usage-and-guidelines"></a>内存使用情况和指导方针  
 如果正在使用大量分区，我们建议您使用至少 16 GB 的 RAM。 如果系统没有足够的内存，则数据操作语言 (DML) 语句、数据定义语言 (DDL) 语句和其他操作可能会由于内存不足而失败。 如果系统具有 16 GB 的 RAM 并且运行许多大量占用内存的进程，则在运行大量分区的操作时，可能会出现内存不足的情况。 因此，您具有超过 16 GB 的内存越多，您遇到性能和内存问题的可能性就越低。  
  
 内存限制可能会影响 SQL Server 生成已分区索引的性能或能力。 如果表中已应用聚集索引，当索引未与其基表或聚集索引对齐时更是如此。  
  
### <a name="partitioned-index-operations"></a>已分区索引操作  
 内存限制可能会影响 SQL Server 生成已分区索引的性能或能力。 具有非对齐索引的情况尤其是这样。 对超过 1,000 个分区的表创建和重新生成非对齐索引是可能的，但不支持。 这样做可能会导致性能下降，或在执行这些操作的过程中占用过多内存。  
  
 随着分区数目的增加，创建和重新生成对齐索引的执行时间可能会更长。 我们建议您不要同时运行多个创建和重新生成索引命令，因为可能会遇到性能和内存问题。  
  
 当 SQL Server 执行排序以生成已分区索引时，它首先为每个分区生成一个排序表。 然后在每个分区各自的文件组中生成排序表，或者在 **tempdb**中生成排序表（如果指定了 SORT_IN_TEMPDB 索引选项）。 每个排序表都需要一个最小内存量才能生成。 在生成与其基表对齐的已分区索引时，将一次生成一个排序表，因此使用的内存较少。 但是，在生成非对齐的已分区索引时，将同时生成排序表。 因此，必须有足够的内存来处理这些并发的排序。 分区数越多，所需的内存越多。 每个分区的每个排序表的最小大小为 40 页，每页 8 KB。 例如，具有 100 个分区的非对齐已分区索引需要足够的内存才能同时连续地对 4,000 (40 * 100) 页进行排序。 如果有这么多的可用内存，生成操作将成功，但性能可能会降低。 如果没有这么多可用内存，生成操作将失败。 而具有 100 个分区的对齐已分区索引只需要具有对 40 页进行排序的内存就足够了，因为不会同时执行排序。  
  
 无论是对齐索引还是非对齐索引，如果 SQL Server 对多处理器计算机上的生成操作应用了并行度，需要的内存可能会更多。 这是因为并行度越高，需要的内存就越多。 例如，如果 SQL Server 将并行度设置为 4，那么具有 100 个分区的非对齐已分区索引将需要使四个处理器同时分别对 4,000 页（即，共 16,000 页）进行排序的足够内存。 如果已分区索引是对齐的，需要的内存将减少，只要够四个处理器分别对 40 页（共 160 页，即 4 * 40）进行排序就行了。 您可以使用 MAXDOP 索引选项手动降低并行度。  
  
### <a name="dbcc-commands"></a>DBCC 命令  
 在具有较多分区的情况下，随着分区数目的增加，DBCC 命令可能需要更长的时间来执行。  
  
### <a name="queries"></a>查询  
 与具有大量分区的查询相比，使用分区排除的查询在性能上相当或更高。 随着分区数目的增加，未使用分区排除的查询可能需要更长的时间来执行。  
  
 例如，假定一个表具有 1 亿行和列的 `A`、 `B`和 `C`。 在方案 1 中，该表在列 `A`上划分为 1000 个分区。 在方案 2 中，该表在列 `A`上划分为 10,000 个分区。 针对该表的一个查询（该查询对列 `A` 具有 WHERE 子句筛选）将执行分区排除并且扫描一个分区。 同一个查询在方案 2 中的运行速度可能会更快，因为在分区中要扫描的行数更少。 对列 B 具有 WHERE 子句筛选的查询将扫描所有分区。 与在方案 2 中相比，该查询在方案 1 中的运行速度会更快，因为要扫描更少的分区。  
  
 在分区列之外的其他列上使用运算符（如 TOP 或 MAX/MIN）的查询可能会遇到分区性能降低的情况，因为所有分区都必须进行评估。  
  
## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>已分区索引操作期间统计信息计算中的行为更改  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，当创建或重新生成已分区索引时，将通过扫描表中的所有行来创建统计信息。 相反，查询优化器使用默认采样算法来生成统计信息。 在升级具有已分区索引的数据库后，您可以在直方图数据中注意到针对这些索引的差异。 此行为更改可能不会影响查询性能。 若要通过扫描表中所有行的方法获得有关已分区索引的统计信息，请使用 CREATE STATISTICS 或 UPDATE STATISTICS 以及 FULLSCAN 子句。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**任务**|**主题**|  
|说明如何创建分区函数和分区方案，然后如何将它们应用于表和索引。|[创建已分区表和索引](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>相关内容  
 对于已分区表和索引策略以及实现方式，以下白皮书可能对您很有用。  
  
-   [使用 SQL Server 2008 的已分区表和索引策略](http://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)  
  
-   [如何实现自动滑动窗口](http://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)  
  
-   [大容量加载到已分区表](http://msdn.microsoft.com/library/cc966380.aspx)  
  
-   [Project REAL：数据生命周期 -- 分区](https://technet.microsoft.com/library/cc966424.aspx)  
  
-   [关于已分区表和索引的查询处理增强功能](http://msdn.microsoft.com/library/ms345599.aspx)  
  
-   [生成大型关系数据仓库的前 10 大最佳做法](http://sqlcat.com/top10lists/archive/2008/02/06/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse.aspx)  
  
  
