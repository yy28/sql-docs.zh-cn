---
title: 重新组织和重新生成索引 | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 263c11f0fe5087fc0f1647f5fd5ca3c7f2477195
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009441"
---
# <a name="reorganize-and-rebuild-indexes"></a>重新组织和重新生成索引

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文介绍了如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中重新整理或重新生成碎片索引。 无论何时对基础数据执行插入、更新或删除操作，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 都会自动修改索引。 随着时间的推移，这些修改可能会导致索引中的信息分散在数据库中（含有碎片）。 当索引包含的页中的逻辑排序（基于键值）与数据文件中的物理排序不匹配时，就存在碎片。 碎片非常多的索引可能会降低查询性能，导致应用程序响应缓慢，特别是扫描操作。

您可以通过重新组织或重新生成索引来修复索引碎片。 对于在分区方案的基础之上生成的已分区索引，可以对完整索引或索引的单个分区使用下列方法之一：

-  重新组织索引  使用的系统资源最少，并且是联机操作。 也就是说，不保留长期阻塞性表锁，且对基础表的查询或更新可以在 `ALTER INDEX REORGANIZE` 事务处理期间继续进行。     
   -  对于行存储  索引，它通过以物理方式重新排序叶级别页，以匹配从左到右的叶节点逻辑顺序，从而对表和视图中的聚集索引和非聚集索引的叶级别进行碎片整理。 重新组织还会压缩索引页。 压缩基于现有的填充因子值。 若要查看填充因子设置，请使用 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。      
   -  如果使用的是列存储  索引，在数据加载后，增量存储中可能会有多个小型行组。 重新组织列存储索引会强制将所有行组转到列存储中，然后将行组合并为行数更多的更少行组。 重新组织操作还将删除已从列存储中删除的行。 重新组织最初需要额外的 CPU 资源来压缩数据，这可能降低整体系统性能。 但是，压缩数据后，可以提高查询性能。 
   
-  重新生成索引  会删除并重新创建索引。 这可以联机完成，也可以脱机完成，具体视索引类型和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 版本而定。      
   -  对于行存储  索引，重新生成操作不仅会删除碎片，根据指定的或现有的填充因子设置来压缩页，从而回收磁盘空间，还会在连续页中重新排序索引行。 如果指定 `ALL`，将删除表中的所有索引，然后在一个事务中重新生成。 不必预先删除外键约束。 重新生成具有 128 个区或更多区的索引时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]延迟实际的页释放及其关联的锁，直到事务提交。       
   -  对于列存储  索引，重新生成操作会删除碎片，将所有行移到列存储中，并通过以物理方式删除已在逻辑上从表中删除的行，从而回收磁盘空间。 自 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 起，通常不需要重新生成列存储索引，因为 `REORGANIZE` 以联机操作形式在后台执行重新生成的基本操作。 
   
在旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，有时可以重新生成行存储非聚集索引，以更正由硬件故障引起的不一致问题。    
自 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 起，仍可以通过脱机重新生成非聚集索引，修复索引和聚集索引之间的这种不一致问题。 但是，您不能通过联机重新生成索引来纠正非聚集索引的不一致，因为联机重新生成机制将会使用现有的非聚集索引作为重新生成的基础，因此仍存在不一致。 脱机重新生成索引有时会强制扫描聚集索引（或堆）并因此删除不一致。 要确保从聚集索引重新生成，请删除并重新创建非聚集索引。 与早期版本一样，建议通过从备份还原受影响的数据来从不一致状态进行恢复；但是，您可以通过脱机重新生成非聚集索引来纠正索引的不一致。 有关详细信息，请参阅 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)。 

## <a name="Fragmentation"></a> 检测碎片
决定使用哪种碎片整理方法的第一步是分析索引以确定碎片程度。 

### <a name="detecting-fragmentation-on-rowstore-indexes"></a>检测行存储索引中的碎片
通过使用系统函数 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)，你可以检测特定索引中的碎片、表或索引视图的所有索引、某个数据库中的所有索引或所有数据库中的所有索引。 对于已分区索引， **sys.dm_db_index_physical_stats** 还提供每个分区的碎片信息。

sys.dm_db_index_physical_stats  函数返回的结果集包含以下列：

|“列”|描述|
|------------|-----------------|
|**avg_fragmentation_in_percent**|逻辑碎片（索引中的无序页）的百分比。|
|**fragment_count**|索引中的碎片（物理上连续的叶页）数量。|
|**avg_fragment_size_in_pages**|索引中一个碎片的平均页数。|

知道碎片程度后，可以使用下表确定修复碎片的最佳方法。

|**avg_fragmentation_in_percent** 值|修复语句|
|-----------------------------------------------|--------------------------|
|> 5% 且 < = 30%|ALTER INDEX REORGANIZE|
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> 重新生成索引可以联机执行，也可以脱机执行。 重新组织索引始终联机执行。 若要获得与重新组织选项相似的可用性，应联机重新生成索引。 有关详细信息，请参阅 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。

> [!TIP]
> 这些值提供了一个大致指导原则，用于确定应在 `ALTER INDEX REORGANIZE` 和 `ALTER INDEX REBUILD` 之间进行切换的点。 不过，实际值可能会随情况而变化。 必须要通过试验来确定最适合您环境的阈值。 例如，如果给定索引主要用于扫描操作，则删除碎片可以提高这些操作的性能。 对于主要用于查找操作的索引，性能优势不太明显。 同样，删除堆中的碎片（不包含聚集索引的表）对于非聚集索引扫描操作特别有用，但在查找操作中不起作用。

通常情况下，非常低的碎片级别（小于 5%）不应通过这些命令来解决，因为删除如此少量的碎片所获得的收益始终远低于重新组织或重新生成索引的开销。 有关 `ALTER INDEX REORGANIZE` 和 `ALTER INDEX REBUILD` 的详细信息，请参阅 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)。

> [!NOTE]
> 重新生成或重新组织小型行存储索引通常不会减少碎片。 小索引的页面有关存储在混合盘区中。 混合区最多可由八个对象共享，因此在重新组织或重新生成小索引之后可能不会减少小索引中的碎片。 

### <a name="detecting-fragmentation-on-columnstore-indexes"></a>检测列存储索引中的碎片
使用 DMV [sys.dm_db_column_store_row_group_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)，可以确定已删除行所占的百分比，这可以很好地度量行组中的碎片。 使用此类信息，可以计算特定索引、表中所有索引、数据库中所有索引或所有数据库中全部索引上的碎片。 

sys.dm_db_column_store_row_group_physical_stats  DMV 返回的结果集包含以下列：

|“列”|描述|
|------------|-----------------|
|**total_rows**|以物理方式存储在行组中的行数。 对于压缩行组，这包括标记为已删除的行。|
|**deleted_rows**|以物理方式存储在压缩行组中且标记为要删除的行数。 对于增量存储中的行组，值为 0。|

这可用于使用公式 `100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0)` 计算碎片。 知道碎片程度后，可以使用下表确定修复碎片的最佳方法。

|“计算的碎片(%)”  值|适用于版本|修复语句|
|-----------------------------------------------|--------------------------|--------------------------|
|> = 20%|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|ALTER INDEX REBUILD|
|> = 20%|自 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 起|ALTER INDEX REORGANIZE|

## <a name="index-defragmentation-considerations"></a>索引碎片整理注意事项
在某些情况下，如果非聚集索引记录中包含的物理或逻辑标识符需要更改，重新生成聚集索引会自动重新生成任何引用聚集键的非聚集索引。

强制在表上自动重新生成所有行存储非聚集索引的情况：

-  在表上创建聚集索引
-  删除聚集索引，从而使表存储为堆
-  更改聚集键以包括或排除列

不需要在表上自动重新生成所有行存储非聚集索引的情况：

-  重新生成唯一聚集索引
-  重新生成非唯一聚集索引
-  更改索引架构，例如将分区方案应用于聚集索引或将聚集索引移到其他文件组

> [!IMPORTANT]
> 如果索引所在的文件组脱机或设置为只读，则无法重新组织或重新生成索引。 如果指定了关键字 ALL，但有一个或多个索引位于脱机文件组或只读文件组中，该语句将失败。  

> [!IMPORTANT]
> 当索引重新生成发生时，物理介质必须有足够的空间来存储索引的两个副本。 在重新生成完成后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会删除原始索引。

如果使用 `ALTER INDEX` 语句指定了 `ALL`，表中的关系索引（包括聚集索引和非聚集索引）和 XML 索引都会进行重新组织。   

### <a name="considerations-specific-to-rebuilding-a-columnstore-index"></a>有关重新生成列存储索引的注意事项  
重新生成列存储索引时，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 会从原始列存储索引（包括增量存储）中读取所有数据。 它将数据合并到新的行组中，并且将行组压缩到列存储中。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 通过以物理方式删除已在逻辑上从表中删除的行，对列存储进行碎片整理；回收磁盘上的已删除字节。   

重新生成分区，而不是整个表：  
-   如果索引很大，并且在重新生成期间需要足够的磁盘空间来存储索引的额外副本，则重新生成整个表将很费时间。 通常仅需要重新生成最近使用的分区。  

-   对于已分区的表，您不需要重新生成整个列存储索引，因为碎片仅可能在最近修改的分区中出现。 事实表和大型的维度表通常已分区，以便对表的特定块执行备份和管理操作。  

在执行了大量 DML 操作后重新生成分区：  
-   重新生成某一分区将会对该分区进行碎片整理，并且缩小磁盘存储空间。 重新生成操作会从列存储中删除标记为要删除的所有行，并将所有行组从增量存储移到列存储中。 请注意，增量存储中可以有多个行组，它们的行数少于一百万。  
  
在数据加载后重新生成分区：  
-   这可确保所有数据都存储于列存储中。 当并发进程分别在同一时间将不到 100,000 行加载到同一分区时，分区最终可能会有多个增量存储。 重新生成操作会将所有增量存储行都移到列存储中。  

### <a name="considerations-specific-to-reorganizing-a-columnstore-index"></a>有关重新组织列存储索引的注意事项  
重新组织列存储索引时，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 会将每个 CLOSED 增量行组作为压缩行组压缩到列存储中。 自 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 起以及在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，`REORGANIZE` 命令会联机执行以下额外的碎片整理优化：  
  
-   在逻辑删除了 10% 或更多行时从行组中物理移除行。 删除的字节会在物理媒体上进行回收。 例如，如果具有 100 万行的压缩行组删除了 10 万行，则 SQL Server 会移除已删除的行，并使用 90 万行重新压缩行组。 它通过移除已删除的行来节省存储。  

-   合并一个或多个压缩行组以将每个行组的行增加到最多为 1,024,576 行。 例如，如果批量导入 5 批 102,400 行，则会获得 5 个压缩行组。 如果运行 REORGANIZE，则这些行组会合并为 1 个大小为 512,000 的压缩行组。 这假定不存在任何字典大小或内存限制。  
  
-   对于逻辑上已有 10% 或更多行遭删除的行组，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 会尝试将此行组与一个或多个行组合并。 例如，行组 1 使用 500,000 行进行压缩，行组 21 使用最大值 1,048,576 行进行压缩。  行组 21 删除了 60% 的行，剩下 409,830 行。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 倾向于合并这两个行组来压缩一个新行组，这个行组有 909,830 行。

在数据加载后，增量存储中可能会有多个小型行组。 可以使用 `ALTER INDEX REORGANIZE` 将所有行组强制载入列存储，然后将行组合并成具有更多行的较少行组。  重新组织操作还将删除已从列存储中删除的行。 

## <a name="Restrictions"></a> 限制和局限
盘区超过 128 个的行存储索引通过两个单独的阶段重新生成：逻辑阶段和物理阶段。 在逻辑阶段，将把由索引使用的现有分配单元标记为释放，对数据行进行复制并排序，然后将它们移到为存储重新生成的索引而创建的新分配单元。 在物理阶段，先前标记为取消分配的分配单元在发生在后台的短事务中被物理删除，而且不需要很多锁。 有关区的详细信息，请参考[页和区体系结构指南](../../relational-databases/pages-and-extents-architecture-guide.md)。

`ALTER INDEX REORGANIZE` 语句要求包含索引的数据文件具有可用的空间，因为该操作仅可在同一文件中分配临时工作，而不能在文件组内的另一个文件中进行分配。 因此，尽管文件组可能有可用的空闲页，用户仍可能会遇到错误 1105：`Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

> [!WARNING]
> 对超过 1,000 个分区的表创建和重新生成非对齐索引是可能的，但不支持。 这样做可能会导致性能下降，或在执行这些操作的过程中占用过多内存。 Microsoft 建议，当分区数超过 1,000 时，只使用对齐索引。  

如果索引所在的文件组脱机  或设置为只读  ，便无法重新组织或重新生成索引。 如果指定了关键字 `ALL`，但有一个或多个索引位于脱机文件组或只读文件组中，该语句将失败。

当索引在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建  或重新生成  后，通过扫描表中的所有行来创建或更新统计信息。 但是，从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，当创建或重新生成已分区索引时，不会通过扫描表中的所有行来创建或更新统计信息。 相反，查询优化器使用默认采样算法来生成这些统计信息。 若要通过扫描表中所有行的方法获得有关已分区索引的统计信息，请使用 `CREATE STATISTICS` 或 `UPDATE STATISTICS` 以及 `FULLSCAN` 子句。

当索引在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中重新组织  后，统计信息不会更新。

当 `ALLOW_PAGE_LOCKS` 设置为 OFF 时，无法重新组织索引。

在 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 及更低版本中，重新生成聚集列存储索引是一项脱机操作。 在重新生成操作执行时，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 必须获取表或分区上的排他锁。 即使在使用 `NOLOCK`、读取已提交的照隔离 (RCSI) 或快照隔离时，数据在重新生成期间仍处于脱机状态且不可用。         
自 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 起，可以使用 `ONLINE=ON` 选项重新生成聚集列存储索引。 

对于包含有序聚集列存储索引的 Azure SQL 数据仓库表，`ALTER INDEX REBUILD` 会使用 TempDB 对数据进行重新排序。 在重新生成操作期间监视 TempDB。 如果需要更多 TempDB 空间，请纵向扩展数据仓库。 完成索引重新生成之后，缩小为原空间大小。 

对于具有有序聚合列存储索引的 Azure SQL 数据仓库表，`ALTER INDEX REORGANIZE` 不会对数据重新排序。 要对数据重新排序，可使用 `ALTER INDEX REBUILD`。

## <a name="Security"></a> Security

### <a name="Permissions"></a> 权限
要求具有对表或视图的 `ALTER` 权限。 用户至少必须是以下某个角色的成员：

- db_ddladmin 数据库角色 <sup>1</sup> 
- db_owner 数据库角色 
- sysadmin 服务器角色 

<sup>1</sup>db_ddladmin 数据库角色是[最低权限角色](/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models)  。

## <a name="SSMSProcedureFrag"></a> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 检查索引碎片

> [!NOTE]
> [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 无法用于计算列存储索引的碎片。 使用[下面](#TsqlProcedureFrag)的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 示例。

1. 在“对象资源管理器”中，展开其中包含要检查索引碎片的表的数据库。
2. 展开 **“表”** 文件夹。
3. 展开要检查索引碎片的表。
4. 展开 **“索引”** 文件夹。
5. 右键单击要检查碎片的索引，然后选择 **“属性”** 。
6. 在 **“选择页”** 下，选择 **“碎片”** 。

   **“碎片”** 页将提供以下信息：

   **页填充度**     
   指示索引页的平均填充率（以百分比表示）。 100% 表示索引页完全填充。 50% 表示每个索引页平均填充一半。

   **碎片总计**：逻辑碎片百分比。 用于指示索引中未按顺序存储的页数。

   **平均行大小**     
   叶级别行的平均大小。

   **深度**     
   索引中的级别数（包括叶级别）。

   **前推记录数**     
   堆中具有指向另一个数据位置的转向指针的记录数。 （在更新过程中，如果在原始位置存储新行的空间不足，将会出现此状态。）

   **虚影行数**     
   标记为已删除，但尚未移除的行数。 当服务器不忙时，将通过清除线程移除这些行。 此值不包括由于某个快照隔离事务未完成而保留的行。

   **索引类型**     
   索引的类型。 可能的值包括 **“聚集索引”** 、 **“非聚集索引”** 和 **“主 XML”** 。 表也可以存储为堆（不带索引），但此后将无法打开此“索引属性”页。

   **叶级别行数**     
   叶级别行数。

   **行大小上限**     
   叶级行最大大小。

   **行大小下限**     
   叶级行最小大小。

   **页数**     
   数据页总数。

   **分区 ID**     
   包含该索引的 B 树的分区 ID。

   **版本虚影行数**     
   由于某个快照隔离事务未完成而保留的虚影记录的数目。

## <a name="TsqlProcedureFrag"></a> 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 检查索引碎片

### <a name="to-check-the-fragmentation-of-a-rowstore-index"></a>检查行存储索引的碎片的具体步骤

下面的示例查找 `AdventureWorks2016` 数据库中 `HumanResources.Employee` 表内所有索引的平均碎片百分比。

```sql
SELECT a.object_id, object_name(a.object_id) AS TableName,
      a.index_id, name AS IndedxName, avg_fragmentation_in_percent
FROM sys.dm_db_index_physical_stats
    (DB_ID (N'AdventureWorks2016_EXT')
        , OBJECT_ID(N'HumanResources.Employee')
        , NULL
        , NULL
        , NULL) AS a
INNER JOIN sys.indexes AS b
    ON a.object_id = b.object_id
    AND a.index_id = b.index_id;
GO
```

上一语句返回如下的结果集。

```
object_id   TableName    index_id    IndexName                                             avg_fragmentation_in_percent
----------- ------------ ----------- ----------------------------------------------------- ------------------------------
1557580587  Employee     1           PK_Employee_BusinessEntityID                          0
1557580587  Employee     2           IX_Employee_OrganizationalNode                        0
1557580587  Employee     3           IX_Employee_OrganizationalLevel_OrganizationalNode    0
1557580587  Employee     5           AK_Employee_LoginID                                   66.6666666666667
1557580587  Employee     6           AK_Employee_NationalIDNumber                          50
1557580587  Employee     7           AK_Employee_rowguid                                   0

(6 row(s) affected)
```

有关详细信息，请参阅 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)。

### <a name="to-check-the-fragmentation-of-a-columnstore-index"></a>检查列存储索引的碎片的具体步骤

下面的示例查找 `AdventureWorksDW2016` 数据库中 `dbo.FactResellerSalesXL_CCI` 表内所有索引的平均碎片百分比。

```sql
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.index_id,   
    i.name AS IndexName,  
    100*(ISNULL(SUM(CSRowGroups.deleted_rows),0))/NULLIF(SUM(CSRowGroups.total_rows),0) AS 'Fragmentation'
FROM sys.indexes AS i  
INNER JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id 
      AND i.index_id = CSRowGroups.index_id   
WHERE object_name(i.object_id) = 'FactResellerSalesXL_CCI'  
GROUP BY i.object_id, i.index_id, i.name 
ORDER BY object_name(i.object_id), i.name;
```
上一语句返回如下的结果集。

```
object_id   TableName                   index_id    IndexName                       Fragmentation
----------- --------------------------- ----------- ------------------------------- ---------------
114099447   FactResellerSalesXL_CCI     1           IndFactResellerSalesXL_CCI      0

(1 row(s) affected)
```

## <a name="SSMSProcedureReorg"></a> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 删除碎片

### <a name="to-reorganize-or-rebuild-an-index"></a>重新组织或重新生成索引

1. 在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。
2. 展开 **“表”** 文件夹。
3. 展开要为其重新组织索引的表。
4. 展开 **“索引”** 文件夹。
5. 右键单击要重新组织的索引，然后选择 **“重新组织”** 。
6. 在 **“重新组织索引”** 对话框中，确认正确的索引位于 **“要重新组织的索引”** 网格中，然后单击 **“确定”** 。
7. 选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。
8. 单击“确定” **。**

> [!NOTE]
> 如果使用 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 重新组织列存储索引，会将 `COMPRESSED` 行组合并在一起，但不会强制将所有行组压缩到列存储中。 将压缩 CLOSED 行组，但不会将 OPEN 行组压缩到列存储中。 若要压缩所有行组，请使用[下面](#TsqlProcedureReorg)的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 示例。 

### <a name="to-reorganize-all-indexes-in-a-table"></a>重新组织表中的所有索引

1. 在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。
2. 展开 **“表”** 文件夹。
3. 展开要为其重新组织索引的表。
4. 右键单击 **“索引”** 文件夹，然后选择 **“全部重新组织”** 。
5. 在 **“重新组织索引”** 对话框中，确认正确的索引位于 **“要重新组织的索引”** 中。 若要从 **“要重新组织的索引”** 网格中删除索引，请选择该索引，再按 Delete 键。
6. 选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。
7. 单击“确定” **。**

### <a name="to-rebuild-an-index"></a>重新生成索引

1. 在“对象资源管理器”中，展开包含您要重新组织索引的表的数据库。
2. 展开 **“表”** 文件夹。
3. 展开要为其重新组织索引的表。
4. 展开 **“索引”** 文件夹。
5. 右键单击要重新组织的索引，然后选择“重新生成”  。
6. 在 **“重新生成索引”** 对话框中，确认正确的索引位于 **“要重新生成的索引”** 网格中，然后单击 **“确定”** 。
7. 选中 **“压缩大型对象列数据”** 复选框，以指定也压缩所有包含大型对象 (LOB) 数据的页。
8. 单击“确定” **。**

## <a name="TsqlProcedureReorg"></a> 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 删除碎片

> [!NOTE]
> 有关使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 重新生成或重新组织索引的更多示例，请参阅 [ALTER INDEX 示例：列存储索引](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes)和 [ALTER INDEX 示例：行存储索引](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes)。

### <a name="to-reorganize-a-fragmented-index"></a>重新组织碎片索引

下面的示例重新组织 `AdventureWorks2016` 数据库中 `HumanResources.Employee` 表内的 `IX_Employee_OrganizationalLevel_OrganizationalNode` 索引。

```sql
ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode
   ON HumanResources.Employee
   REORGANIZE;
```

下面的示例重新组织 `AdventureWorksDW2016` 数据库中 `dbo.FactResellerSalesXL_CCI` 表内的 `IndFactResellerSalesXL_CCI` 列存储索引。

```sql  
-- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
ALTER INDEX IndFactResellerSalesXL_CCI 
   ON FactResellerSalesXL_CCI   
   REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON); 
```

### <a name="to-reorganize-all-indexes-in-a-table"></a>重新组织表中的所有索引

下面的示例重新组织 `AdventureWorks2016` 数据库中 `HumanResources.Employee` 表内的所有索引。

```sql
ALTER INDEX ALL ON HumanResources.Employee
   REORGANIZE;
```

### <a name="to-rebuild-a-fragmented-index"></a>重新生成碎片索引

下面的示例在 `AdventureWorks2016` 数据库的 `Employee` 表中重新生成单个索引。

[!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]

### <a name="to-rebuild-all-indexes-in-a-table"></a>重新生成表中的所有索引

下面的示例使用 `ALL` 关键字重新生成所有与 `AdventureWorks2016` 数据库中的表关联的索引。 其中指定了三个选项。

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]

有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)。

### <a name="automatic-index-and-statistics-management"></a>自动索引和统计信息管理

利用[自适应索引碎片整理](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解决方案，自动管理一个或多个数据库的索引碎片整理和统计信息更新。 此过程根据碎片级别以及其他参数，自动选择是重新生成索引还是重新组织索引，并使用线性阈值更新统计信息。

## <a name="see-also"></a>另请参阅
[SQL Server 索引体系结构和设计指南](../../relational-databases/sql-server-index-design-guide.md)     
[联机执行索引操作](../../relational-databases/indexes/perform-index-operations-online.md)  
[ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)      
[自适应索引碎片整理](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)       
[CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)     
[UPDATE STATISTICS (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)      
[Columnstore Indexes Query Performance](../../relational-databases/indexes/columnstore-indexes-query-performance.md)     
[开始使用列存储进行实时运营分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)      
[针对数据仓库的列存储索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)     
[列存储索引和行组的合并策略](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)      
