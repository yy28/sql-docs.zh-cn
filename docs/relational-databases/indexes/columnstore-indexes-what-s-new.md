---
title: 列存储索引 - 新增功能 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 690455f8dba76b45643ac4971c988059c56e33f9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "70009426"
---
# <a name="columnstore-indexes---what39s-new"></a>列存储索引 - 新增功能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  列存储功能摘要可用于各个版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、最新版 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  

 > [!NOTE]
 > 对于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，列存储索引可用于 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 高级层、标准层（S3 及更高）以及所有 vCore 层。 对于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 及更高版本，列存储索引可用于所有版本。 对于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]（早于 SP1）及更早版本，列存储索引仅可用于企业版。
 
## <a name="feature-summary-for-product-releases"></a>产品版本的功能摘要  
 此表概述了列存储索引的主要功能以及提供这些功能的产品。  

|列存储索引功能|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]|  
|-------------------------------|---------------------------|---------------------------|---------------------------|--------------------------------------------|-------------------------|---|  
|多线程查询的批模式执行|是|是|是|是|是|是| 
|单线程查询的批模式执行|||是|是|是|是|  
|存档压缩选项||是|是|是|是|是|  
|快照隔离和读提交快照隔离|||是|是|是|是| 
|创建表时，请指定列存储索引|||是|是|是|是|  
|Always On 支持列存储索引|是|是|是|是|是|是| 
|Always On 可读次要副本支持只读非聚集列存储索引|是|是|是|是|是|是|  
|Always On 可读次要副本支持可更新列存储索引|||是|是|||  
|堆或 B 树上的只读非聚集列存储索引|是|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|  
|堆或 B 树上的可更新非聚集列存储索引|||是|是|是|是|  
|允许在使用非聚集列存储索引的堆或 B 树上实施额外的 B 树索引|是|是|是|是|是|是|  
|可更新的聚集列存储索引||是|是|是|是|是|  
|基于聚集列存储索引的 B 树索引|||是|是|是|是|  
|基于内存优化表的列存储索引|||是|是|是|是|  
|非聚集列存储索引定义支持使用筛选的条件|||是|是|是|是|  
|`CREATE TABLE` 和 `ALTER TABLE` 中的列存储索引的压缩延迟选项|||是|是|是|是|
|列存储索引具有一个非持久化计算列||||是|||   
  
 <sup>1</sup> 要创建只读非聚集列存储索引，请将索引存储在只读文件组内。  

## [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 
 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 将添加这些新功能。

### <a name="functional"></a>功能
- [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 支持聚集列存储索引中的非持久化计算列。 聚集列存储索引不支持持久化计算列。 无法在具有计算列的列存储索引上创建非聚集索引。 

## [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 添加了重要的增强功能，以此来改善列存储索引的性能和灵活性。 这些改进功能可以增强数据仓库方案的效果，并实现实时运营分析。  
  
### <a name="functional"></a>功能  
  
-   一个行存储表可以有一个可更新的非聚集列存储索引。 以前，非聚集列存储索引是只读的。  
  
-   非聚集列存储索引定义支持使用筛选的条件。 若要尽量减少在 OLTP 表中添加列存储索引的性能影响，请使用筛选条件，以便创建仅关于运行工作负荷冷数据的非聚集列存储索引。 
  
-   一个内存中表可以有一个列存储索引。 你可以在创建表时创建它，也可以稍后使用 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md) 来添加。 以前，仅基于磁盘的表可以有列存储索引。  
  
-   聚集列存储索引可以有一个或多个非聚集行存储索引。 以前，列存储索引不支持非聚集索引。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动维护 DML 操作的非聚集索引。  
  
-   支持主键和外键，即可通过使用 B 树索引在聚集列存储索引上强制实施这些约束。  
  
-   列存储索引有一个压缩延迟选项，该选项可以最大限度地减少事务工作负荷对实时运营分析的影响。  此选项允许通过频繁地更改行来保持稳定，然后再将这些行压缩到列存储中。 有关详细信息，请参阅[创建列存储索引 (Transact SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md) 和[开始使用列存储索引进行实时运营分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
### <a name="performance-for-database-compatibility-level-120-or-130"></a>数据库兼容级别 120 或 130 的性能  
  
-   列存储索引支持读提交快照隔离级别 (RCSI) 和快照隔离 (SI)。 这样可以在无锁的情况下进行事务一致性分析查询。  
  
-   列存储支持索引碎片整理，即可以移除已删除的行而无需显式重新生成索引。 `ALTER INDEX ... REORGANIZE` 语句将根据内部定义的策略，以联机操作的方式从列存储移除已删除的行  
  
-   可以在 AlwaysOn 可读次要副本上访问列存储索引。 你可以将分析查询卸载到 AlwaysOn 次要副本，从而改进运行分析的性能。  
  
-   为了改进性能，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会在表扫描期间计算聚合函数 `MIN`、`MAX`、`SUM`、`COUNT` 和 `AVG`，前提是数据类型不超过 8 个字节的长度，且不是字符串类型。 聚合列存储索引和非聚合列存储索引都支持聚合下推，不管有没有 Group By 子句。  
  
-   谓词下推可加快查询在比较 [v]archar 或 n[v]archar 类型的字符串时的速度。 这适用于常用的比较运算符，包括 LIKE 这样的使用位图筛选器的运算符。 这适用于 SQL Server 支持的所有排序规则。  
  
### <a name="performance-for-database-compatibility-level-130"></a>数据库兼容级别 130 的性能  
  
-   对于使用任何下述操作的查询，新提供了批处理模式执行支持：  
    -   SORT  
    -   使用多个不同函数的聚合函数。 一些示例：`COUNT/COUNT`、`AVG/SUM`、`CHECKSUM_AGG`、`STDEV/STDEVP`。  
    -   窗口聚合函数：`COUNT`、`COUNT_BIG`、`SUM`、`AVG`、`MIN`、`MAX` 和 `CLR`。  
    -   窗口用户定义聚合：`CHECKSUM_AGG`、`STDEV`、`STDEVP`、`VAR`、`VARP` 和 `GROUPING`。  
    -   窗口聚合分析函数：`LAG`、`LEAD`、`FIRST_VALUE`、`LAST_VALUE`、`PERCENTILE_CONT`、`PERCENTILE_DISC`、`CUME_DIST` 和 `PERCENT_RANK`。  
-   在 `MAXDOP 1` 下运行或使用串行查询计划以批处理模式执行的单线程查询。 以前，仅多线程查询以批处理执行的方式运行。  
-   内存优化表查询可以有 SQL 互操作模式的并行计划，不管是按行存储索引方式还是按列存储索引方式访问数据  
  
### <a name="supportability"></a>可支持性  
以下系统视图是针对列存储的新视图：  

||| 
|-|-|
|[sys.column_store_row_groups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)|[sys.dm_column_store_object_pool (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)|  
|[sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)|[sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)|  
|[sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)|[sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)|  
|[sys.internal_partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)||  
  
以下内存中 OLTP 式 DMV 包含列存储的更新：  

||| 
|-|-|
|[sys.dm_db_xtp_hash_index_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)|[sys.dm_db_xtp_index_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)|  
|[sys.dm_db_xtp_memory_consumers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)|[sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)|  
|[sys.dm_db_xtp_object_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)|[sys.dm_db_xtp_table_memory_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)|  
  
### <a name="limitations"></a>限制    
-   对于内存中表，列存储索引必须包括所有列；列存储索引不能有经过筛选的条件。  
-   对于内存中表，基于列存储索引的查询仅在互操作模式下运行，不在内存中本机模式下运行。 支持并行执行。  
  
## [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 引入了聚集列存储索引作为主存储格式。 这样就可以进行常规加载以及更新、删除和插入操作。  
  
-   表可以使用聚集列存储索引作为主表存储。 不允许在表上使用其他索引，但可对聚集列存储索引进行更新，因此可执行常规加载并对各个行进行更改。  
-   非聚集列存储索引的功能仍与 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中的一样，区别是增加了能够以批处理模式执行的运算符。 该索引仍然不能进行更新，只能重新生成和使用分区切换。 非聚集列存储索引只能用于基于磁盘的表，不能用于内存中表。  
-   聚集和非聚集列存储索引有一个存档压缩选项，允许进一步压缩数据。 存档选项用于减少内存中数据和磁盘上数据的大小，但会降低查询执行速度。 它适用于访问不频繁的数据。  
-   聚集列存储索引和非聚集列存储索引的作用方式非常类似：使用相同的列存储格式、相同的查询处理引擎，以及相同的动态管理视图集。 不同之处在于，一个是主要索引类型，一个是次要索引类型，而非聚集列存储索引为只读。  
-   对于多线程查询来说，以下运算符以批处理模式运行：scan、filter、project、join、group by 和 union all。  
  
## [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引入了非聚集列存储索引作为另一基于行存储表的索引类型，并为基于列存储数据的查询引入了批处理。  
  
-   一个行存储表可以有一个非聚集列存储索引。  
-   列存储索引是只读的。 创建列存储索引以后，不能通过`INSERT`、`DELETE`和`UPDATE`操作来更新表；要执行这些操作，必须在删除索引后更新表，然后重新生成列存储索引。 可以使用分区切换将其他数据加载到表中。 分区切换的优点是，你可以在不删除和重新生成列存储索引的情况下加载数据。  
-   列存储索引始终需要额外的存储空间，通常需要在行存储的基础上再多出 10%，因为它会存储数据的副本。  
-   批处理的查询性能会翻倍，或者说批处理会改善查询性能，但这仅适用于并行执行查询的情况。  
  
## <a name="see-also"></a>另请参阅  
 [列存储索引设计指南](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [列存储索引数据加载指南](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Columnstore Indexes Query Performance](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [开始使用列存储进行实时运营分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [针对数据仓库的列存储索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)
  
