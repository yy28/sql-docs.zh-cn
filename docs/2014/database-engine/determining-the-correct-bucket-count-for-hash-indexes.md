---
title: 确定哈希索引的正确存储桶计数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b79c0908f8639df869d01a8ff862afc5be77cb
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241955"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>决定哈希索引的正确存储桶数
  在您创建内存优化表时，必须为 `BUCKET_COUNT` 参数指定值。 本主题将提出一些建议，帮助您为 `BUCKET_COUNT` 参数确定适当的值。 如果您无法确定实际 Bucket 计数，则改用非聚集索引。  不正确的 `BUCKET_COUNT` 值（特别是过低的值）可能会显著影响工作负荷性能以及数据库的恢复时间。 最好将 Bucket 计数估计得高一些。  
  
 重复的索引键会降低哈希索引性能，因为键已哈希处理至同一个 Bucket，导致该 Bucket 的链增加。  
  
 有关非聚集哈希索引的详细信息，请参阅 [Hash Indexes](hash-indexes.md) 和 [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 将为内存优化表上的每个哈希索引分配一个哈希表。 为指定的索引分配的哈希表的大小`BUCKET_COUNT`中的参数[CREATE TABLE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql)或[CREATE TYPE &#40;-&#41; ](/sql/t-sql/statements/create-type-transact-sql). Bucket 数将在内部舍入到 2 的下一次幂。 例如，指定 300,000 的 Bucket 计数将导致 524,288 的实际 Bucket 计数。  
  
 有关 Bucket 计数的文章和视频链接，请参阅 [如何确定哈希索引（内存 OLTP）的正确 Bucket 计数](https://www.mssqltips.com/sqlservertip/3104/determine-bucketcount-for-hash-indexes-for-sql-server-memory-optimized-tables/)。  
  
## <a name="recommendations"></a>建议  
 在大多数情况下，Bucket 计数应该介于索引键中非重复值数目的 1 到 2 倍之间。 如果索引键包含许多重复值，且平均而言对于每个索引键值超过 10 行，则改用非聚集索引  
  
 您不见得始终都能够预测到某个特定索引键可能具有或将具有多少个值。 如果 `BUCKET_COUNT` 值处于实际键值数目的 5 倍之内，性能就应该是可接受的。  
  
 若要确定现有数据中唯一索引键的数目，请使用与下面的示例相似的查询：  
  
### <a name="primary-key-and-unique-indexes"></a>主键和唯一索引  
 因为主键索引是唯一的，所以，键中非重复值的数目与表中的行数相对应。 对于 AdventureWorks 数据库的表 Sales.SalesOrderDetail 中 (SalesOrderID, SalesOrderDetailID) 上的示例主键，发出以下查询以便计算非重复主键值的数目，该数目与表中的行数相对应：  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 此查询显示 121,317 的行计数。 如果行计数不会显著更改，则使用桶计数 240,000。 如果表中的销售订单数可能会变成原来的四倍，则使用桶计数 480,000。  
  
### <a name="non-unique-indexes"></a>非唯一索引  
 对于其他索引，例如 (SpecialOfferID, ProductID) 上的多列索引，发出以下查询以便确定唯一索引键值的数目：  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 此查询返回 (SpecialOfferID, ProductID) 的索引键计数 484，指示应使用非聚集索引而不是非聚集哈希索引。  
  
### <a name="determining-the-number-of-duplicates"></a>确定重复项的数目  
 若要确定某一索引键值的重复值的平均数目，请用总行数除以唯一索引键的数目。  
  
 对于 (SpecialOfferID, ProductID) 上的示例索引，这导致 121317 / 484 = 251。 这意味着索引键值具有平均值 251，并因此应该是一个非聚集索引。  
  
## <a name="troubleshooting-the-bucket-count"></a>Bucket 计数故障排除  
 若要对内存优化表中的 bucket 计数问题进行故障排除，请使用[sys.dm_db_xtp_hash_index_stats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql)若要获取的空 bucket 和行链长度有关的统计信息。 可以使用下面的查询获取与当前数据库中所有哈希索引有关的统计信息。 如果数据库中有大型表，查询可能会用几分钟时间运行。  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 用于评估哈希索引运行状况的两个关键指标是：  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* 指示哈希索引中空 Bucket 的数目。  
  
 如果 *empty_bucket_percent* 小于 10%，则该 Bucket 计数可能过低。 理想状态下， *empty_bucket_percent* 应该为 33% 或更高。 如果 Bucket 计数与索引键值的数目匹配，则由于哈希分布，大约 1/3 的 Bucket 是空的。  
  
 *avg_chain_length*  
 *avg_chain_length* 指示哈希桶中行链的平均长度。  
  
 如果 *avg_chain_length* 大于 10 并且 *empty_bucket_percent* 大于 10%，则可能有许多重复索引键值并且非聚集索引可能更适合。 理想的平均链长度应该是 1。  
  
 有两个因素会影响链长度：  
  
1.  重复项；所有重复行在哈希索引中都属于相同链。  
  
2.  多个键值映射到相同的 Bucket。 桶计数越低，映射多个值的 Bucket 就越多。  
  
 例如，考虑以下表和脚本以便在表中插入示例行：  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 该脚本在表中插入 262,144 行。 它在主键索引和 IX_OrderSequence 中插入唯一值。 它在索引 IX_Status 中插入许多重复值：该脚本仅生成 8 个非重复值。  
  
 该 BUCKET_COUNT 故障排除查询的输出如下所示：  
  
|索引名称|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 考虑此表上的三个哈希索引：  
  
-   IX_Status：50% 的 Bucket 是空的，这很好。 但是，平均链长非常高 (65,536)。 这指示存在大量重复值。 因此，在此情况下使用非聚集哈希索引是不恰当的。 应改用非聚集索引。  
  
-   IX_OrderSequence：0% 的 Bucket 是空的，这太低了。 此外，平均链长度是 8。 因为此索引中的值是唯一的，所以，这意味着平均而言 8 个值映射到每个 Bucket。 应增加 Bucket 计数。 因为索引键具有 262,144 个唯一值，所以，Bucket 计数应至少为 262,144。 如果预期将来会出现增长，则该数目还应该更高。  
  
-   主键索引 (PK__SalesOrder...):36% 的 Bucket 是空的，这很好。 此外，平均链长度为 1，这也不错。 无需进行更改。  
  
 有关排除与内存优化哈希索引有关的问题的详细信息，请参阅 [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md)。  
  
## <a name="detailed-considerations-for-further-optimization"></a>为进一步优化需要周全考虑的方面  
 本节概述为优化 Bucket 计数而需要进一步考虑的方面。  
  
 若要实现哈希索引的最佳性能，应平衡分配给哈希表的内存量和索引键中非重复值的数目。 还需要对点查找和表扫描间的性能进行平衡：  
  
-   Bucket 计数值越大，索引中存在的空 Bucket 就越多。 这会影响内存使用情况（每个 Bucket 8 个字节）和表扫描的性能，因为将在表扫描期间对每个 Bucket 进行扫描。  
  
-   Bucket 计数越低，分配给单个 Bucket 的值就越多。 这会降低点查找和插入的性能，因为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可能需要遍历单个 Bucket 中的多个值才能找到搜索谓词指定的值。  
  
 如果 Bucket 计数显著低于唯一索引键数，则许多值将映射到每个 Bucket。 这会减少大部分 DML 操作（尤其是查找个别索引键的点查找操作）和插入操作的性能。 例如，包含相等谓词（与 WHERE 子句中的索引键列匹配）的 SELECT 查询、UPDATE 和 DELETE 操作的性能可能较差。 较低的 Bucket 计数还将影响数据库的恢复时间，因为在数据库启动时会重新创建这些索引。  
  
### <a name="duplicate-index-key-values"></a>重复的索引键值  
 重复值可能增加对哈希冲突的性能影响。 如果每个索引键的重复项的数目较低，则上述性能影响通常不是问题。 但是，如果表中唯一索引键的数目和行数之间的差异变得非常大，则该影响可能就会是问题。  
  
 具有相同索引键的所有行将进入同一个重复链。 如果多个索引键由于哈希冲突处于同一个 Bucket 中，则索引扫描程序将始终需要扫描整个重复链以便找到第一个值，然后才能相对于第二个值定位第一行。 重复键还使得垃圾收集更难以定位行。 例如，假设任意键有 1,000 个重复项并删除了一行，则垃圾收集器需要扫描 1,000 个重复项，从索引中取消该行的链接。 即使发现该删除行的查询使用更高效的索引（主键索引）来定位行，也要遵循上述方法，因为垃圾收集器需要从每个索引取消链接。  
  
 对于哈希索引，可通过两种方式减少重复索引键值导致的工作量：  
  
-   改用非聚集索引。 您可以向索引键添加列来减少重复项，而不需要对应用程序做任何更改。  
  
-   为索引指定非常高的 Bucket 计数。 例如，可达到唯一索引键数目的 20 到 100 倍。 这将减少哈希冲突。  
  
### <a name="small-tables"></a>小型表  
 对于较小的表，内存使用量通常不是问题，因为与数据库的总体大小相比，索引的大小通常较小。  
  
 您现在必须基于想要的性能类型进行选择：  
  
-   如果在索引上对性能起到关键作用的操作主要是点查找和/或插入操作，则为了降低哈希冲突的可能性，较高的 Bucket 计数应该更合适。 最好选择三倍于行数甚至更高的计数。  
  
-   如果全文检索扫描是对性能起着主要作用的操作，则使用接近于索引键值实际数目的 Bucket 计数。  
  
### <a name="big-tables"></a>大型表  
 对于大型表，内存使用量可能成问题。 例如，2.5 亿行的表具有 4 个哈希索引，每个都有一个 10 亿的 bucket 计数与哈希表的开销是 4 个索引 * 10 亿 bucket \* 8 字节 = 32 千兆字节的内存使用率。 在为每个索引选择 2.5 亿的 Bucket 计数时，针对哈希表的总开销将是 8 GB。 请注意，这是除了 8 字节的内存使用情况的每个索引将添加到每个单独的行，这是在此方案中的 8 千兆字节 (4 个索引\*8 个字节\*2.5 亿行)。  
  
 全表扫描通常不是影响 OLTP 工作负荷的关键因素。 因此，需要在内存使用量与点查找和插入操作的性能之间进行权衡：  
  
-   如果内存使用量是问题，则选择接近于索引键值数目的 Bucket 计数。 该 Bucket 计数不应显著小于索引键值数，因为这会影响大多数 DML 操作以及在服务器重新启动后恢复数据库所需的时间。  
  
-   在优化点查找的性能时，Bucket 计数最好是唯一索引值的两倍甚至三倍。 较高的 Bucket 计数意味着内存使用量的增加，并且也意味着全文检索扫描所需时间的增加。  
  
## <a name="see-also"></a>请参阅  
 [内存优化的表的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
