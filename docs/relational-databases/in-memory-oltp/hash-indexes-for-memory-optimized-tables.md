---
title: "内存优化表的哈希索引 | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de23d5625c883792f5c99de75dc90ccd1cabe326
ms.lasthandoff: 04/11/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>内存优化表的哈希索引
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
本文介绍可用于内存优化表的*哈希*索引类型。 本文内容：  
  
- 提供简短代码示例来演示 Transact-SQL 语法。  
- 介绍哈希索引的基础知识。  
- 介绍 [如何估计适当的桶计数](#configuring_bucket_count)。  
- 描述如何设计和管理哈希索引。  
  
  
#### <a name="prerequisite"></a>先决条件  
  
有关了解本文的重要的上下文信息，请参阅：  
  
- [内存优化表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. 内存优化索引的语法  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 语法的代码示例  
  
本小节包含一个 Transact-SQL 代码块，用于演示在内存优化表中创建哈希索引时可用的语法：  
  
- 此示例说明在 CREATE TABLE 语句内声明哈希索引。  
  - 也可以改为在单独的 [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) 语句中声明哈希索引。  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    “应用程序适配器” 区域）  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

若要为你的数据确定合适的 `BUCKET_COUNT` ，请参阅 [配置哈希索引桶计数](#configuring_bucket_count)。 
  
## <a name="b-hash-indexes"></a>B. 哈希索引  
  
  
### <a name="b1-performance-basics"></a>B.1 性能基础知识  
  
哈希索引的性能为：  
  
- 当 WHERE 子句为哈希索引键中的每一列指定 *确切* 值时表现极好。  
- 当 WHERE 子句查找索引键中的 *一系列* 值时表现不佳。  
- 当 WHERE 子句为双列哈希索引键的第一列指定了一个特定值，但没有为该键的 *第二个* 列指定值时表现不佳。  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 声明限制  
  
哈希索引只能存在于内存优化表中， 而不能存在于基于磁盘的表中。  
  
可以将哈希索引声明为：  
  
- UNIQUE，或可以默认为 Nonunique。  
- NONCLUSTERED 为默认值。   
  
  
下面是在 CREATE TABLE 语句之外创建哈希索引的语法示例：  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 桶和哈希函数  
  
哈希索引将其键值定位在所谓的 *桶* 数组中：  
  
- 每个桶为 8 个字节，用于存储键项的链接列表的内存地址。  
- 每个条目是索引键的值，以及其在基础内存优化表中的对应行的地址。  
  - 每个条目指向条目的链接列表中的下一个条目，所有都链接到当前桶。  
  
  
哈希算法尝试在其桶之间平均展开所有唯一或非重复键值，但完全均匀是不能达到的理想。 任何给定键值的所有实例都链接到同一桶中。 此外，桶可能混合在不同键值的所有实例中。  
  
- 此组合称为 *哈希冲突*。 冲突很常见，但不是理想状态。  
- 现实的目标是 30% 的桶包含两个不同的键值。  
  
  
你需要声明一个哈希索引应有多少个桶。  
  
- 桶与表行或非重复值的比例越低，桶链接列表的平均长度就越长。  
- 较短的链接列表比较长的链接列表执行更快。  
  
  
SQL Server 有一个用于所有哈希索引的哈希函数：  
  
- 该哈希函数是确定性的：假设输入的键值相同，它将以一致的方式输出相同的桶槽。  
- 经反复调用，该哈希函数的输出往往会形成泊松分布或钟形曲线分布，而不是平坦的线性分布。  
  
  
下图汇总了哈希索引和桶的交互作用。  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "索引键输入到哈希函数，输出是哈希桶的地址，用于指向链的头。")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 行版本和垃圾回收  
  
  
在内存优化表中，如果某行受 SQL UPDATE 影响，表将创建该行的更新版本。 在更新事务期间，其他会话也许能够读取较旧版本的行，从而避免与行锁相关的性能下降。  
  
哈希索引可能也会提供不同的条目版本来适应更新。  
  
以后，当不再需要旧版本时，垃圾回收 (GC) 线程将遍历桶及其链接列表，以清理旧条目。 如果链接列表链长度较短，GC 线程的执行效果会更佳。   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>C. 配置哈希索引桶计数  
  
在创建时指定哈希索引桶计数，并可使用 ALTER TABLE...ALTER INDEX REBUILD 语法进行更改。  
  
在大多数情况下，桶计数在理想情况下应该介于索引键中非重复值数目的 1 到 2 倍之间。   
您不见得始终都能够预测到某个特定索引键可能具有或将具有多少个值。 如果 **BUCKET_COUNT** 值在键值的实际数目的 10 倍以内，性能表现通常依然良好，并且高估通常比低估要好。  
  
桶 *太少* 会带来以下缺点：  
  
- 增多非重复键值的哈希冲突。  
  - 每个非重复值被迫与其他非重复值共享同一个桶。  
  - 每个桶的平均链长度将会增加。  
  - 桶链的长度越长，在索引中相等性查找的速度就越慢。  
  
桶 *太多* 会带来以下缺点：  
  
- 桶计数过高可能会导致空桶增多。  
  - 空桶会影响全文检索扫描的性能。 如果定期执行这些操作，请考虑选择接近非重复索引键值数目的桶计数。  
  - 空桶会使用内存，尽管每个桶只用 8 个字节。  
    
  
> [!NOTE]
> 添加更多的桶无益于减少共享重复值的、链接在一起的条目。 值重复率用于确定哈希是否为适当的索引类型，而不是用于计算桶计数。  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 可行的数字  
  
即使 **BUCKET_COUNT** 适度低于或高于偏好范围，但哈希索引的性能有可能可容许或可接受。 这不会造成不便。  
  
为哈希索引指定的 **BUCKET_COUNT** 应大致等于内存优化表增长后预计包含的行数。  
  
假设不断增长的表包含 2,000,000 行，但你预计该数量将增长 10 倍，即 20,000,000 行。 那么，首先可以指定一个为表中行数 10 倍的桶计数。 这样，便为行数增加提供了空间。  
  
- 理想情况下，当行的数量达到初始桶计数时，你则会增加桶计数。  
- 即使行的数量增长到桶计数的 5 倍，在大多数情况下，性能表现依然良好。  
  
假设某个哈希索引包含 10,000,000 个非重复键值。  
  
- 桶计数 2,000,000 大致是你可以接受的下限。 这种性能下降的程度是可容忍的。  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 索引中存在过多的重复值？  
  
如果哈希索引值的重复率太高，哈希桶将遇到较长的链。  
  
假设你的 SupportEvent 表与前面 T-SQL 语法代码块中的表相同。 以下 T-SQL 代码演示了如何查找并显示 *所有* 值与 *唯一* 值的比率：  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- 如果比率等于或大于 10.0，则表示哈希是一种较差的索引类型。 考虑改用非聚集索引，   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>D. 对哈希索引桶计数进行故障排除  
  
本节介绍如何为哈希索引的桶计数进行故障排除。  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 监视链和空桶的统计信息  
  
你可以通过运行以下 T-SQL SELECT 来监视哈希索引的统计运行状况。 SELECT 语句使用名为 **sys.dm_db_xtp_hash_index_stats**的数据管理视图 (DMV)。  
  
  
```t-sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
      
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM  
         sys.dm_db_xtp_hash_index_stats  as h   
    JOIN sys.indexes                     as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
```
  
  
将 SELECT 结果与以下统计指导原则进行比较：  
  
- 空桶：  
  - 33% 是一个很好的目标值，但更大比例（甚至 90%）通常也是没问题的。  
  - 如果桶计数等于非重复键值的数目，则大约 33% 的桶是空的。  
  - 小于 10% 的值就太小。  
- 桶中的链：  
  - 平均链长为 1 是理想选择，以防出现没有重复索引键值的情况。 链长在 10 以内通常都是可接受的。  
  - 如果平均链长度大于 10，并且空桶百分比大于 10%，则重复的数据就会太多，哈希索引可能不是最适合的类型。  
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 链和空桶的演示  
  
  
以下 T-SQL 代码块为你提供了一种简单的方法来测试 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`。 该代码块在 1 分钟内完成。 以下是以下代码块阶段：  
  
  
1. 创建包含一些哈希索引的内存优化表。  
2. 在表中填充数千行。  
    A. 取模运算符用于配置 StatusCode 列中的值重复率。  
    B. 该循环将在大约 1 分钟内插入 262144 行。  
3. 列显一条消息，要求你从 **sys.dm_db_xtp_hash_index_stats**运行上述 SELECT。  
  
  
```t-sql
    DROP TABLE IF EXISTS SalesOrder_Mem;  
    go  
      
      
    CREATE TABLE SalesOrder_Mem  
    (  
      SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
      OrderSequence  int               NOT NULL,  
      OrderDate      datetime2(3)      NOT NULL,  
      StatusCode     tinyint           NOT NULL,  
      
      PRIMARY KEY NONCLUSTERED  
          HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
      
      INDEX ix_OrderSequence  
          HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
      
      INDEX ix_StatusCode  
          HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
      
      INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
    )  
      WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    go  
      
        --------------------  
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
上述 INSERT 循环将执行以下操作：  
  
- 插入主键索引和 ix_OrderSequence 的唯一值。  
- 插入了几十万行，但只呈现了 StatusCode 的 8 个非重复值。 因此，索引 ix_StatusCode 中的值重复率很高。  
  
为了在桶计数不最佳时进行问题排查，请从 **sys.dm_db_xtp_hash_index_stats**检查 SELECT 的以下输出。 对于这些结果，我们添加 `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` 到从 D.1 部分复制的 SELECT。  
  
  
  
我们的 SELECT 结果显示在代码后面，将它人工拆分为两个较窄的结果表以便更好地显示。  
  
- 这里是 *桶计数*的结果。  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
  
- 接下来是 *链长度*的结果。  
  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
  
  
  
让我们解释上述结果表中的三个哈希索引：  
  
*ix_StatusCode：*  
  
- 50% 的桶是空的，这很好。  
- 但是，平均链长度非常大，为65,536。  
  - 这表明值重复率很高。  
  - 因此，在此情况下不适合使用哈希索引。 应改用非聚集索引。  
  
*ix_OrderSequence：*  
  
- 0% 的桶是空的，这太低了。  
- 平均链长度是 8，不过，此索引中的所有值都是唯一的。  
  - 因此，应增加桶计数，以便将平均链长度减小到接近 2 或 3。  
- 由于索引键具有 262144 个唯一值，因此桶计数应至少为 262144。  
  - 如果预期将来会增长，则桶计数还应该更高。  
  
*主键索引 (PK_SalesOrd_...)：*  
  
- 36% 的桶是空的，这很好。  
- 平均链长度为 1，这也不错。 无需进行更改。  
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 权衡利弊  
  
OLTP 工作负载注重每个行。 全表扫描通常不是影响 OLTP 工作负载的关键因素。 因此，必须权衡以下两者之间的利弊：  
  
- 内存使用量；以及  
- 相等性测试和插入操作的性能。  
  
  
*如果内存使用量是更大的考虑因素：*  
  
- 选择近似于索引键记录数的桶计数。  
- 该 Bucket 计数不应显著小于索引键值数，因为这会影响大多数 DML 操作以及在服务器重新启动后恢复数据库所需的时间。  
  
  
*如果相等性测试的性能是更大的考虑因素：*  
  
- 提高桶计数，唯一索引值数目的两倍或三倍比较合适。 提高计数意味着：  
  - 查找某个特定值时检索速度更快。  
  - 内存使用量增加。  
  - 完全扫描哈希索引所需的时间增加。  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>E. 哈希索引的优势  
  
  
在以下情况下，哈希索引比非聚集索引更有优势：  
  
- 查询通过使用包含等式的 WHERE 语句来测试索引列，如下所示：  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 多列哈希索引键  
  
  
两个列索引可能是非聚集索引或哈希索引。 假设索引列是 col1 和 col2。 在给定以下 SQL SELECT 语句的情况下，仅非聚集索引将对查询优化器有用：  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
哈希索引需要 WHERE 子句为其键中的每列指定相等测试。 否则哈希索引将对优化器无用。  
  
如果 WHERE 子句仅指定索引键中的第二个列，这两种索引类型则都将无用。  
  
  
  
\<!--   
Hash_Indexes_for_Memory-Optimized_Tables.md，这是...  
CAPS guid: {e922cc3a-3d6e-453b-8d32-f4b176e98488}  
父级的 CAP guid 是: {eecc5821-152b-4ed5-888f-7c0e6beffed9}  
  
  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent | avg_chain_length | max_chain_length |  
| :-------- | -----------------: | -----------------: | -----------------: | ---------------: | ---------------: |  
| ix_OrderSequence | 32768 | 13 | 0 | 8 | 26 |  
| ix_StatusCode | 8 | 4 | 50 | 65536 | 65536 |  
| PK_SalesOrd_B14003E308C1A23C | 262144 | 96525 | 36 | 1 | 8 |  
  
  
  
  
GeneMi  ,  2016-05-05  Thursday  15:01pm  
-->  
  
  
  


