---
title: 列存储索引 - 概述 | Microsoft Docs
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
caps.latest.revision: 80
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1987c099ba787f36dac77eb08a8e88b1e7c71869
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32941012"
---
# <a name="columnstore-indexes---overview"></a>列存储索引 - 概述
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

列存储索引是存储和查询大型数据仓库事实数据表的标准。 它使用基于列的数据存储和查询处理，与传统的面向行的存储相比，可对数据仓库最多提高 **10 倍查询性能** ，与使用非压缩数据大小相比，可提供多达 **10 倍数据压缩率** 。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，列存储索引支持操作分析，这是一种针对事务工作负荷运行高性能实时分析的功能。  
  
 跳到方案：  
  
-   [针对数据仓库的列存储索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
-   [开始使用列存储适进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
## <a name="what-is-a-columnstore-index"></a>什么是列存储索引？  
 *columnstore index* 是使用列式数据格式（称为列存储）存储、检索和管理数据的技术。  
  
### <a name="key-terms-and-concepts"></a>重要术语和概念  
 以下重要概念和术语与列存储索引相关。  
  
 列存储  
 “列存储”是在逻辑上组织为包含行和列的表、在物理上以按列数据格式存储的数据。  
  
 行存储  
 “行存储”是在逻辑上组织为包含行和列的表、在物理上以按行数据格式存储的数据。 这是存储关系表数据的传统方法。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，行存储是指基础数据存储格式为堆、聚集索引或内存优化表的表。  
  
> [!NOTE]  
> 在提到列存储索引时，我们经常使用术语“行存储”和“列存储”来强调数据存储的格式。  
  
 行组  
 “行组”是同时压缩为列存储格式的一组行。 每个行组通常可包含的最大行数是 1,048,576 行。  
  
 为获得高性能和高压缩率，列存储索引将表划分为由行构成的组，称为行组，然后以按列形式压缩每个行组。 行组中的行数必须足够大，以便提高压缩率，并且还要足够小，以便从内存中操作中受益。  
 列段  
 “列段”是来自行组内的数据列。  
  
-   每个行组包含表中每个列的一个列段。  
-   每个列段一起压缩并且存储于物理介质上。  
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
  
 聚集列存储索引  
 “聚集列存储索引”是整个表的物理存储。  
  
 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")  
  
 若要减少列段的碎片和改进性能，列存储索引可能会将一些数据暂时存储于称作增量存储的聚集索引中，同时还存储针对已删除行的 ID 的 btree 列表。 增量存储操作在后台处理。 若要返回正确的查询结果，聚集列存储索引将合并来自列存储和增量存储的查询结果。  
  
 增量行组  
 “增量行组”仅用于列存储索引，它是一个聚集索引，可以不断地存储行，并在行数达到某个阈值后，将行移入列存储，从而提高列存储压缩率和性能。  

 在增量行组达到最大行数后，它会关闭。 元组移动进程会检查是否有已关闭行组。 在它找到已关闭行组后，会对其进行压缩并且将其存储到列存储中。  
  
增量存储：列存储索引可具有多个增量行组。  所有增量行组统称为增量存储。   

在大容量加载期间，大多数行直接转到列存储，而不通过增量存储中转。 在大容量加载结束时，某些行的数量可能无法满足行组的最小大小要求（即 102,400 行）。 在发生这种情况时，将最后的这些行转到增量存储而非列存储中。 对于少于 102,400 行的较小的大容量加载，所有行都直接转到增量存储中。  
  

  
 非聚集列存储索引  
 “非聚集列存储索引”和聚集列存储索引在功能上相同。 不同之处在于，非聚集索引是在行存储表上创建的辅助索引，而聚集列存储索引是整个表的主存储。  
  
 非聚集索引包含基础表中部分或全部行与列的副本。 索引将定义为表的一个或多个列，并具有一个用于筛选行的可选条件。  
  
 非聚集列存储索引支持实时运营分析，其中，OLTP 工作负载使用基础聚集索引，同时对列存储索引并发运行分析。 有关详细信息，请参阅 [开始使用列存储进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
 批处理执行  
 “批处理执行”是一种查询处理方法，其中查询将统一处理多个行。 对列存储索引的查询使用批处理模式执行，这通常可将查询性能提高 2-4 倍。 批处理执行与列存储存储格式紧密集成，并且围绕列存储存储格式进行了优化。 批处理模式执行有时候称作基于向量或向量化的执行。  
  
##  <a name="benefits"></a> 为何要使用列存储索引？  
 列存储索引可提供极高的数据压缩级别（通常是传统方法的 10 倍），从而明显降低数据仓库存储成本。 此外，对于分析，它们提供的性能比 btree 索引高出一个量级。 它们是数据仓库和分析工作负载的首选数据存储格式。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，可以使用列存储索引对操作工作负荷执行实时分析。  
  
 列存储索引速度较快的原因：  
  
-   列存储来自同一个域的值，并且通常具有相似的值，从而提高了压缩率。 这可以最大程度地减少或消除系统中的 IO 瓶颈，同时大大减少内存占用量。  
  
-   较高的压缩率通过使用更小的内存中空间提高查询性能。 反过来，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在内存中执行更多查询和数据操作，因此可以提高查询性能。  
  
-   批处理执行可同时处理多个行，通常可将查询性能提高 2-4 倍。  
  
-   查询通常仅从表中选择几列，这减少了从物理介质的总 I/O。  
  
## <a name="when-should-i-use-a-columnstore-index"></a>何时应使用列存储索引？  
 建议的用例：  
  
-   使用聚集列存储索引来存储数据仓库工作负载的事实数据表和大型维度表。 这样可将查询性能和数据压缩率最多提高 10 倍。 请参阅 [Columnstore Indexes for Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)。  
  
-   使用聚集列存储索引对 OLTP 工作负载执行实时分析。 请参阅 [开始使用列存储进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
### <a name="how-do-i-choose-between-a-rowstore-index-and-a-columnstore-index"></a>如何在行存储索引与列存储索引之间做出选择？  
 行存储索引最适合用于查找数据、搜索特定值的查询，或者针对较小范围的值执行的查询。 可对事务工作负载使用行存储索引，因为这些工作负载往往需要进行表查找而不是表扫描。  
  
 对于扫描大量数据（尤其是大型表中）的分析查询，列存储索引可提高性能。  可对数据仓库和分析工作负载（尤其是对事实数据表）使用列存储索引，因为它们往往需要进行全表扫描而不是表查找。  
  
### <a name="can-i-combine-rowstore-and-columnstore-on-the-same-table"></a>是否可以在同一个表中组合行存储与列存储？  
 是。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，你可以在行存储表上创建可更新的非聚集列存储索引。 列存储索引将存储所选列的副本，因此你确实需要为此准备额外的空间，但是，数据的压缩率平均可提高 10 倍。 如果采取这种做法，你可以同时对列存储索引以及行存储索引上的事务运行分析。 当行存储表中的数据更改时，列存储将会更新，因此这两个索引适用于相同的数据。  
  
 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，你可以对一个列存储索引使用一个或多个非聚集行存储索引。 这样，便可以针对基础列存储上执行有效的表查找。 其他选项也可供使用。 例如，可以通过在行存储表中使用 UNIQUE 约束来强制主键约束。 由于不唯一的值无法插入行存储表，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法将值插入列存储。  
  
## <a name="metadata"></a>元数据  
 列存储索引中的所有列在元数据中作为包含性列存储。 列存储索引中没有任何键列。  

|||
|-|-|  
|[sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)|[sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)|  
|[sys.partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)|[sys.internal_partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)|  
|[sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)|[sys.column_store_dictionaries (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)|  
|[sys.column_store_row_groups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)|[sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)|[sys.dm_column_store_object_pool (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|[sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)|  
|[sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)||  
  
## <a name="related-tasks"></a>Related Tasks  
 所有关系表（除非指定为非聚集列存储索引）使用行存储作为基础数据格式。 如果不指定 `WITH CLUSTERED COLUMNSTORE INDEX` 选项，则 `CREATE TABLE` 将创建行存储表。  
  
 使用 `CREATE TABLE` 语句创建表时，可通过指定 `WITH CLUSTERED COLUMNSTORE INDEX` 选项将表创建为列存储。 如果你已有一个行存储表并想要将其转换为列存储，可以使用 `CREATE COLUMNSTORE INDEX` 语句。  
  
|任务|参考主题|说明|  
|----------|----------------------|-----------|  
|将表创建为列存储。|[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)|从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，你可以将表创建为聚集列存储索引。 不需要先创建行存储表，然后将其转换为列存储。|  
|创建具有列存储索引的内存表。|[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)|从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，你可以创建具有列存储索引的内存优化表。 也可以在创建表后使用 ALTER TABLE ADD INDEX 语法添加列存储索引。|  
|将行存储表转换为列存储。|[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)|将现有堆集或二进制树转换为列存储。 示例演示了如何在执行此转换时处理现有的索引以及索引的名称。|  
|将列存储表转换为行存储。|[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)|通常这不需要这样做，但有时需要执行此转换。 示例演示如何将列存储转换为堆或聚集索引。|  
|在行存储表中创建列存储索引。|[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)|一个行存储表可以有一个列存储索引。  从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]开始，列存储索引可以包含筛选条件。 示例演示了基本语法。|  
|为操作分析创建高性能索引。|[开始使用列存储适进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|介绍如何创建互补性列存储索引和 btree 索引，以便 OLTP 查询使用 btree 索引，分析查询使用列存储索引。|  
|为数据仓库创建高性能列存储索引。|[针对数据仓库的列存储索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|介绍如何使用列存储表上的 btree 索引来创建高性能数据仓库查询。|  
|使用 btree 索引对列存储索引强制主键约束。|[针对数据仓库的列存储索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|演示如何合并 btree 和列存储索引，以便对列存储索引强制主键约束。|  
|删除列存储索引|[DROP INDEX (Transact-SQL)](../../t-sql/statements/drop-index-transact-sql.md)|删除列存储索引使用 btree 索引所用的标准 DROP INDEX 语法。 删除聚集列存储索引会将列存储表转换为堆。|  
|从列存储索引中删除行|[DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)|使用 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md) 删除行。<br /><br /> **列存储** 行： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将它标记为已逻辑删除但是未回收行的物理存储空间，直到重新生成索引。<br /><br /> **增量存储** 行： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以逻辑和物理方式删除该行。|  
|更新列存储索引中的行|[UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)|使用 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md) 更新行。<br /><br /> **列存储** 行：  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将它标记为已逻辑删除，然后将更新的行插入增量存储中。<br /><br /> **增量存储** 行： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在增量存储中更新它。|  
|将数据载入列存储索引|[列存储索引数据加载](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)||  
|强制增量存储中的所有行进入列存储。|[ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md) ...REBUILD<br /><br /> [列存储索引碎片整理](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)|结合 REBUILD 选项的 ALTER INDEX 会强制所有行进入列存储。|  
|对列存储索引进行碎片整理|[ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE 可在线对列存储索引进行碎片整理。|  
|合并具有列存储索引的表。|[MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅  
 [列存储索引数据加载](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [列存储索引版本的功能摘要](~/relational-databases/indexes/columnstore-indexes-what-s-new.md)   
 [Columnstore Indexes Query Performance](~/relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [开始使用列存储适进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [针对数据仓库的列存储索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [列存储索引碎片整理](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)   
 [SQL Server 索引设计指南](../../relational-databases/sql-server-index-design-guide.md)   
 [列存储索引体系结构](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
  
  





