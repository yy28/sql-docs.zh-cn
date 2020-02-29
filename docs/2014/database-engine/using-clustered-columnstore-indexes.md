---
title: 使用聚集列存储索引 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 04cb8ea2505340cb90221b328c04efc390296c19
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175356"
---
# <a name="using-clustered-columnstore-indexes"></a>使用聚集列存储索引
  用于在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中使用聚集列存储索引的任务。

 有关列存储索引的概述，请参阅 [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)。

 有关聚集列存储索引的信息，请参阅 [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)。

## <a name="contents"></a>目录

-   [创建聚集列存储索引](#create)

-   [删除聚集列存储索引](#drop)

-   [将数据加载到聚集列存储索引中](#load)

-   [更改聚集列存储索引中的数据](#change)

-   [重新生成聚集列存储索引](#rebuild)

-   [重新组织聚集列存储索引](#reorganize)

##  <a name="create"></a>创建聚集列存储索引
 若要创建聚集列存储索引，请先创建一个行存储表作为堆或聚集索引，然后使用[CREATE 聚集列存储索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)语句将该表转换为聚集列存储索引。 如果您想要让该聚集列存储索引具有与聚集索引相同的名称，则使用 DROP_EXISTING 选项。

 此示例将一个表作为堆创建，然后将其转换为名为 cci_Simple 的聚集列存储索引。 这会将整个表的存储从行存储转换为列存储。

```
CREATE TABLE T1(
    ProductKey [int] NOT NULL, 
    OrderDateKey [int] NOT NULL, 
    DueDateKey [int] NOT NULL, 
    ShipDateKey [int] NOT NULL);
GO
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;
GO
```

 有关更多示例，请参阅[CREATE 聚集列存储索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)中的 "示例" 部分。

##  <a name="drop"></a>删除聚集列存储索引
 使用[DROP INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/drop-index-transact-sql)语句删除聚集列存储索引。 此操作将删除该索引并将列存储表转换为行存储堆。

##  <a name="load"></a>将数据加载到聚集列存储索引
 您可以使用任何标准加载方法，将数据添加到现有聚集列存储索引。  例如，bcp 大容量加载工具、Integration Services 和 INSERT .。。选择 "可以将所有数据都加载到聚集列存储索引中"。

 聚集列存储索引利用增量存储以便防止在列存储的列段中出现碎片。

### <a name="loading-into-a-partitioned-table"></a>加载到已分区表中
 对于已分区数据， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 首先将每一行分配给一个分区，然后对该分区内的数据执行列存储操作。 每个分区都具有自己的行组以及至少一个增量存储。

### <a name="deltastore-loading-scenarios"></a>增量存储加载方案
 行在增量存储中累积，直到行数达到行组允许的最大行数。 如果增量存储包含每个行组的最大行数[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，则将行组标记为 "已关闭"。 称为 "元组-移动器" 的后台进程将查找关闭的行组，并将其移到列存储中，其中，行组压缩为列段，列段存储在列存储中。

 每个聚集列存储索引可以有多个增量存储。

-   如果锁定一个增量存储， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将尝试获取其他增量存储的锁。 如果没有可用的增量存储， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将创建新的增量存储。

-   对于已分区的表，每个分区可以有一个或多个增量存储。

 仅对于聚集列存储索引，以下方案说明何时将加载的行直接转到列存储中以及何时将它们转到增量存储中。

 在示例中，每个行组可以具有 102,400-1,048,576 行。

|要大容量加载的行|已添加到列存储的行|已添加到增量存储的行|
|-----------------------|-----------------------------------|----------------------------------|
|102,000|0|102,000|
|145,000|145,000<br /><br /> 行组大小：145,000|0|
|1,048,577|1,048,576<br /><br /> 行组大小：1,048,576。|1|
|2,252,152|2,252,152<br /><br /> 行组大小：1,048,576、1,048,576、155,000。|0|

 以下示例显示将 1,048,577 行加载到分区的结果。 这些结果显示列存储（作为压缩的列段）中的一个 COMPRESSED 行组以及增量存储中的 1 行。

```
SELECT * FROM sys.column_store_row_groups
```

 ![用于批加载的行组和 deltastore](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "用于批加载的行组和 deltastore")



##  <a name="change"></a>更改聚集列存储索引中的数据
 聚集列存储索引支持插入、更新和删除 DML 操作。

 使用[insert &#40;transact-sql&#41;](/sql/t-sql/statements/insert-transact-sql)插入行。 该行将添加到增量存储中。

 使用 [DELETE (Transact-SQL)](/sql/t-sql/statements/delete-transact-sql) 删除行。

-   如果该行在列存储中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将它标记为已逻辑删除但是未回收行的物理存储空间，直到重新生成索引。

-   如果该行在增量存储中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在逻辑上和物理上删除该行。

 使用 [UPDATE (Transact-SQL)](/sql/t-sql/queries/update-transact-sql) 更新行。

-   如果该行在列存储中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将它标记为已逻辑删除，然后将更新的行插入增量存储中。

-   如果该行在增量存储中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在增量存储中更新它。

##  <a name="rebuild"></a>重新生成聚集列存储索引
 使用[CREATE 聚集列存储索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)或[ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql)来执行现有聚集列存储索引的完整重新生成。 此外，还可以使用 ALTER INDEX .。。重新生成以重新生成特定分区。

### <a name="rebuild-process"></a>重新生成过程
 若要重新生成聚集列存储索引，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将：

-   在重新生成进行时获取表或分区上的排他锁。  在重新生成期间数据“处于脱机状态”并且不可用。

-   通过物理删除已从表中逻辑上删除的行对列存储进行碎片整理；已删除的字节在物理介质上回收。

-   在重新生成索引前将增量存储区中的行存储数据与列存储区中的数据进行合并。 在重新生成完成后，所有数据都以列存储格式存储，并且增量存储为空。

-   将所有数据重新压缩到列存储中。 在进行重新生成时存在列存储索引的两个副本。 在重新生成完成后， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将删除原始列存储索引。

### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>有关重新生成聚集列存储索引的建议
 重新生成聚集列存储索引适用于删除碎片，并且适用于将所有行都移到列存储中。 请考虑以下建议：

-   重新生成分区而不是整个表。

    1.  如果索引很大，并且在重新生成期间需要足够的磁盘空间来存储索引的额外副本，则重新生成整个表将很费时间。 通常仅需要重新生成最近使用的分区。

    2.  对于已分区的表，您不需要重新生成整个列存储索引，因为碎片仅可能在最近修改的分区中出现。 事实表和大型的维度表通常已分区，以便对表的特定块执行备份和管理操作。

-   在执行了大量 DML 操作后重新生成分区

     重新生成某一分区将会对该分区进行碎片整理，并且缩小磁盘存储空间。 重新生成将会从列存储中删除标记为要删除的所有行，并且会将所有行从增量存储移到列存储中。

-   在加载数据后重新生成分区。

     这可确保所有数据都存储于列存储中。 如果同时发生多个加载，每个分区可能最终有多个增量存储。 重新生成会将所有增量存储行都移到列存储中。

##  <a name="reorganize"></a>重新组织聚集列存储索引
 重新组织聚集列存储索引会将所有已关闭行组都移到列存储中。 若要执行重新组织，请将[ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql)与 "重新组织" 选项一起使用。

 为了将关闭的行组移到列存储中，不需要重新组织索引。 元组搬运者进程最终将找到所有关闭的行组并且移动它们。 但是，tuple-mover 是单线程的，因此，对于您的工作负荷来说它移动行组的速度可能不够快。

### <a name="recommendations-for-reorganizing"></a>进行重新组织的建议
 何时重新组织聚集列存储索引：

-   在执行一次或多次数据加载后，为了尽快优化查询性能，需要重新组织聚集列存储索引。 重新组织最初需要额外的 CPU 资源来压缩数据，这可能降低整体系统性能。 但是，压缩数据后，可以提高查询性能。


