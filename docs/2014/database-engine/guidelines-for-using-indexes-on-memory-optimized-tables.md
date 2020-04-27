---
title: 在内存优化表上使用索引的准则 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71d26e3f46034019d51bd69b86686f40eb9ce63e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779221"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>在内存优化表上使用索引的指导原则
  索引用于高效访问 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表中的数据。 指定正确索引可以显著提高查询性能。 例如，请考虑以下查询：  
  
```sql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 如果 c1 列上没有索引，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 需要扫描整个表 t，然后筛选满足条件 c1=1 的行。 但是，如果 t 在 c1 列上具有索引，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以直接查找值 1 并对行进行检索。  
  
 针对表中一列或多列搜索具有特定值或值范围的记录时，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用这些列上的索引来快速找到对应记录。 基于磁盘的表和内存优化表都会受益于索引。 但是，在使用内存优化的表时，需要考虑索引结构之间的一些区别。 （内存优化表上的索引称为内存优化索引。）一些主要的区别是：  
  
-   必须[CREATE TABLE &#40;transact-sql&#41;](/sql/t-sql/statements/create-table-transact-sql)创建内存优化索引。 基于磁盘上的索引可以使用 `CREATE TABLE` 和 `CREATE INDEX` 创建。  
  
-   内存优化索引仅存在于内存中。 索引结构在磁盘中不持久化，并且不在事务日志中记录索引操作。 CREATE TABLE 过程中以及数据库启动过程中，在内存中创建内存优化的表时，将创建索引结构。  
  
-   内存优化索引本质上是覆盖性的。 覆盖表示真正在索引中包括所有列，因此内存优化的表不需要查找书签。 内存优化索引仅包含指向表数据结构中的实际行的内存指针，而不是对主键的引用。  
  
-   碎片和填充因子不适用于内存优化索引。 在基于磁盘的索引中，碎片是指无序写入磁盘的 B 树中的页。 内存优化索引不会写入磁盘或从磁盘读取。 基于磁盘的 B 树索引中的填充因子是指使用实际数据填充物理页结构的程度。 内存优化索引结构没有固定大小的页。  
  
 内存优化的索引具有以下两种类型：  
  
-   非聚集哈希索引，为点查找编制此类索引。 有关哈希索引的详细信息，请参阅[哈希索引](hash-indexes.md)。  
  
-   非聚集索引，为范围扫描和有序扫描编制此类索引。  
  
 借助于哈希索引，可通过内存中的哈希表来访问数据。 哈希索引没有页，并且始终为固定大小。 但是，哈希索引的哈希存储桶可为空，这样会浪费一些空间，但数量有限。 对于使用哈希索引从查询返回的值不进行排序。 哈希索引为针对相等谓词的索引查找进行优化，还支持完整索引扫描。  
  
 非聚集索引（而非哈希索引）支持哈希索引支持的所有功能，外加针对不等谓词（例如大于或小于）的查找操作以及排序顺序。 可以根据索引创建时指定的顺序检索行。 如果索引的排序顺序匹配特定查询所需的排序顺序，例如，如果索引键匹配 ORDER BY 子句，则无需作为查询执行的一部分对行进行排序。 内存优化的非聚集索引是无方向的；它们不支持按与索引的排序顺序反向的排序顺序来检索行。 例如，对于被指定为 (c1 ASC) 的一个索引，不可能以反向顺序（如 (c1 DESC)）浏览该索引。  
  
 每个索引都会占用内存。 哈希索引的内存用量固定不变，是存储桶数量的函数。 对于非聚集索引，内存用量是行数和索引键列大小的函数，还有一些其他开销取决于工作负荷。 内存优化的索引所用的内存不计入用于在内存优化的表中存储行的内存，并区别于此类内存。  
  
 重复键值始终共享同一哈希桶。 如果一个哈希索引包含了多个重复键值，那么产生的长哈希链会损坏性能。 发生在任何哈希索引中的哈希冲突将会进一步减弱此方案中的性能。 出于此原因，如果唯一索引键的数目至少为100倍于行计数，则可以通过使 bucket 计数更大（至少8倍唯一索引键的数目，请参阅[确定哈希索引的正确存储桶计数](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)），或者通过使用非聚集索引来完全消除哈希冲突。  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>确定要用于内存优化表的索引  
 每个内存优化的表都必须具有至少一个索引。 请注意，每个 PRIMARY KEY 约束都会隐式创建一个索引。 因此，如果表中包含主键，则该表具有索引。 主键是对持久内存优化表的要求。  
  
 查询内存优化的表时，在谓词子句仅包含相等谓词的情况下，哈希索引的性能更好。 谓词必须包括哈希索引键中的所有列。 如果有不等谓词，则哈希索引将恢复为扫描。  
  
 内存优化的表中的列可以同时为哈希索引和非聚集索引的一部分。  
  
 在用不等谓词查询内存优化的表时，非聚集索引的性能将高于非聚集哈希索引。  
  
 哈希索引需要键（哈希）才能仔细查找索引。 如果索引键由两列组成，但仅提供第一列，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 没有完整的键可进行哈希运算。  这将产生索引扫描查询计划。 由用法决定应编制哪些列的索引。  
  
 当非聚集索引中的列在许多行中的值相同（索引键列有许多重复值）时，更新、插入和删除的性能会降低。  在这种情况下提高性能的一种方法是向非聚集索引添加另一列。  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>针对内存优化表和基于磁盘的表的操作。  
  
|Operation|内存优化、非聚集哈希索引|内存优化的非聚集索引|基于磁盘的索引|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|索引扫描，检索所有表行。|是|是|是|  
|采用相等谓词 (=) 的索引查找。|是<br /><br /> （需要完整的键。）|是<sup>1</sup>|是|  
|对不相等谓词（>、<、 \<=、>=、BETWEEN）的索引查找。|否（索引扫描中的结果）|是<sup>1</sup>|是|  
|按与索引定义匹配的排序顺序检索行。|否|是|是|  
|按与索引定义相反的排序顺序检索行。|否|否|是|  
  
 在表格中，“是”意味着索引能充分地服务需求，而“否”则意味着索引不能用来成功地满足需求。  
  
 <sup>1</sup>对于非聚集内存优化索引，不需要完整的键即可执行索引查找。 即便如此，给定索引键的列顺序后，如果缺少的列后面出现列值，则进行扫描。  
  
## <a name="index-count"></a>索引计数  
 内存优化表可以具有多达 8 个索引，包括通过主键创建的索引。  
  
 关于在内存优化表上创建的索引数目，请考虑以下几点：  
  
-   指定创建表时所需的索引。 不能在创建内存优化表之后再为该表创建索引。 如果要向内存优化表添加索引，请删除并重新创建该表。  
  
-   请勿创建很少使用的索引：  
  
     如果表上的所有索引都经常使用，则垃圾收集效果最好。 很少使用的索引可能会导致垃圾收集系统对于旧的版本无法以最佳方式执行。  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>创建内存优化的索引：代码示例  
 列级别哈希索引：  
  
```sql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 表级别哈希索引：  
  
```sql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 列级别主键哈希索引：  
  
```sql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 表级别主键哈希索引：  
  
```sql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 列级非聚集索引：  
  
```sql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 表级非聚集索引：  
  
```sql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 列级主键非聚集索引：  
  
```sql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 表级主键非聚集索引：  
  
```sql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 定义列后定义的多列索引：  
  
```sql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表的索引](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [确定哈希索引的正确存储桶计数](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [哈希索引](hash-indexes.md)  
  
  
