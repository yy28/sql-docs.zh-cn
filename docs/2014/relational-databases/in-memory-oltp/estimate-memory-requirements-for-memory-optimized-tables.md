---
title: 估算内存优化表的内存需求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 15b3b27f859b2ea2ed3008d33f19a682aeef833b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533466"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>估算内存优化表的内存需求
  是否要创建一个新[!INCLUDE[hek_2](../../includes/hek-2-md.md)]内存优化的表或将现有的基于磁盘的表迁移到内存优化表，务必要有的合理估计的每个表的内存需求，因此你可以设置与具有足够的服务器内存。 本节介绍如何估算使用内存优化表存放数据时所需的内存大小。  
  
 如果考虑从基于磁盘的表迁移至内存优化表，在继续阅读本主题前，请先阅读主题 [确定表或存储过程是否应移植到内存中 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) ，了解哪类表适合迁移。 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md) 下的所有主题均提供了有关从基于磁盘的表迁移至内存优化表的指导。  
  
## <a name="sections-in-this-topic"></a>本主题的内容  
  
-   [内存优化表示例](#bkmk_ExampleTable)  
  
-   [表占用的内存](#bkmk_MemoryForTable)  
  
-   [索引占用的内存](#bkmk_IndexMeemory)  
  
-   [行版本控制占用的内存](#bkmk_MemoryForRowVersions)  
  
-   [表变量占用的内存](#bkmk_TableVariables)  
  
-   [表增长占用的内存](#bkmk_MemoryForGrowth)  
  
##  <a name="bkmk_ExampleTable"></a> 内存优化表示例  
 考虑以下内存优化的表架构：  
  
```sql  
  
CREATE TABLE t_hk (  
col1 int NOT NULL PRIMARY KEY NONCLUSTERED,  
col2 int NOT NULL INDEX t1c2_index   
     HASH WITH (bucket_count = 5000000),  
col3 int NOT NULL INDEX t1c3_index   
     HASH WITH (bucket_count = 5000000),  
col4 int NOT NULL INDEX t1c4_index   
     HASH WITH (bucket_count = 5000000),  
col5 int NOT NULL INDEX t1c5_index NONCLUSTERED,  
col6 char (50) NOT NULL,  
col7 char (50) NOT NULL,   
col8 char (30) NOT NULL,   
col9 char (50) NOT NULL  
     WITH (memory_optimized = on)  
GO  
  
```  
  
 我们将使用该架构来确定此内存优化表所需的最低内存。  
  
##  <a name="bkmk_MemoryForTable"></a> 表占用的内存  
 内存优化表行包含三个部分：  
  
-   **时间戳**   
    行标题/时间戳 = 24 个字节。  
  
-   **索引指针**   
    对于表中的每个哈希索引，每行包含一个指向索引中下一行的 8 字节地址指针。  因为有 4 个索引，每行将为索引指针分配 32 个字节（每个索引需要一个 8 字节的指针）。  
  
-   **数据**   
    行中数据部分的大小由各数据列类型大小的总和决定。  示例表中包含五个 4 字节整数、三个 50 字节的字符列和一个 30 字节的字符列。  因此，每行的数据部分为 4 + 4 + 4 + 4 + 4 + 50 + 50 + 30 + 50 共 200 个字节。  
  
 下面是内存优化表中 5,000,000（5 百万）行的大小计算： 按以下方式估计数据行使用的总内存：  
  
 **表的行的内存**  
  
 根据上述计算，内存优化表中每行的大小为 24 + 32 + 200，即 256 个字节。  总共有 5 百万行，则表将占用 5,000,000 * 256 字节，共 1,280,000,000 字节 - 大约 1.28 GB。  
  
##  <a name="bkmk_IndexMeemory"></a> 索引占用的内存  
 **对于每个哈希索引的内存**  
  
 每个哈希索引是一个由 8 字节地址指针组成的哈希数组。  该数组的大小最好通过索引中唯一索引键的数目确定，例如：使用唯一 Col2 键的个数作为 t1c2_index 的数组大小。 哈希数组太大，浪费内存。  哈希数组太小，又会降低性能（许多索引键经哈希操作后映射至同一索引，导致冲突过多）。  
  
 哈希索引可实现高速查找，如：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 = 3  
  
```  
  
 非聚集索引在执行范围查找时更快，如：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 >= 3  
  
```  
  
 如果是迁移磁盘表，可使用下面的方法确定索引 t1c2_index 的唯一键的个数。  
  
```sql  
  
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk  
  
```  
  
 如果是创建新表，则需要估算数组大小或在部署前通过测试收集数据。  
  
 关于 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 内存优化表中哈希索引的工作原理，请参阅 [哈希索引](../../database-engine/hash-indexes.md)。  
  
 **注意：** 哈希索引数组的大小不能实时更改。 要更改哈希索引数组的大小，必须删除表，更改 bucket_count 值，然后重新创建表。  
  
 **设置哈希索引数组的大小**  
  
 设置哈希数组大小`(bucket_count= <value>)`其中\<值 > 是一个整数值大于零。 如果\<值 > 不为 2，实际的 bucket_count 舍入为下一个最近的 2 的幂。  在示例表中，(bucket_count = 5000000)，由于 5,000,000 并非 2 的幂，实际 bucket 计数舍入为 8,388,608 (2<sup>23</sup>)。  在计算此哈希数组所需的内存时，必须使用该值，而非 5,000,000。  
  
 因此，在本示例中，每个哈希数组所需的内存为：  
  
 8,388,608 * 8 = 2<sup>23</sup> \* 8 = 2<sup>23</sup> \* 2<sup>3</sup> = 2<sup>26</sup> = 67108864，约 64 MB。  
  
 有三个哈希索引，所以哈希索引占用的内存为 3 * 64MB = 192MB。  
  
 **非聚集索引占用的内存**  
  
 非聚集索引采用 B 树实现（内部节点包含索引键和指向后续节点的指针）。  叶节点包含索引键和指向内存中表行的指针。  
  
 与哈希索引不同的是，非聚集索引的 Bucket 大小不固定。 非聚集索引随数据动态扩展/收缩。  
  
 可按如下方式计算非聚集索引占用的内存：  
  
-   **为非叶节点分配的内存**   
    对于典型配置，分配给非叶节点的内存只占索引所占用的整个内存的很小的百分比。 其占用的内存少到可以安全地忽略。  
  
-   **叶节点占用的内存**   
    叶节点对于表中的每个唯一键都具有 1 行，并且指向具有该唯一键的数据行。  如果多行具有相同的键（即，存在不唯一的非聚集索引），则索引页节点中只有一行指向这些行中的某一个，其他行则相互链接在一起。  因此，可通过下面的公式估算所需的总内存：   
    非聚集索引所需内存 = （指针大小 + Sum (键列数据类型大小))* 唯一键行数  
  
 非聚集索引的最佳应用是范围查找，下面的查询即为例证：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE c2 > 5  
```  
  
##  <a name="bkmk_MemoryForRowVersions"></a> 行版本控制占用的内存  
 为避免锁定，内存 OLTP 在更新或删除行时采用乐观并发策略。 也就是说，对某行进行更新时，将额外创建一个该行的版本。 系统将保持旧版本可用，直至可能会用到该版本的所有事务执行完毕为止。 在删除某行时，系统按与更新操作类似的方式操作，即：保持版本可用，直至不再需要为止。 读取和插入操作不会创建额外的行版本。  
  
 在任意时刻，内存中都可能存在一定数量的额外行等待垃圾回收周期释放其内存，因此，必须具有足够的内存来容纳这些额外的行。  
  
 可通过下面的公式估算额外行的数目：每秒行更新和行删除的高峰次数 * 执行事务所需的最长秒数（最少为 1）。  
  
 再用该值乘以行大小即可获得行版本控制所需占用的字节数。  
  
 `rowVersions = durationOfLongestTransactionInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
 陈旧行的内存需求估算陈旧行数目乘以内存优化表行的大小 (请参阅[用于表的内存](#bkmk_MemoryForTable)上面)。  
  
 `memoryForRowVersions = rowVersions * rowSize`  
  
##  <a name="bkmk_TableVariables"></a> 表变量占用的内存  
 只有在表变量超出范围时，才能释放表变量占用的内存。 来自表变量的行（包括作为更新的一部分删除的行）不会进行垃圾回收。 在表变量退出作用域之前不会释放内存。  
  
 与过程作用域相反，用于许多事务的在大型 SQL 批处理中定义的表变量可能会占用大量内存。 因为不对它们进行垃圾回收，所以，表变量中已删除的行可能会使用大量内存并且降低性能，这是因为读取操作需要扫描已删除的行。  
  
##  <a name="bkmk_MemoryForGrowth"></a> 表增长占用的内存  
 上述计算结果为表当前所需的内存。 除该内存大小外，还需对表的增长作出预测并提供充足的内存来满足增长所需。  例如，如预测表会有 10% 的增长，则需将上述结果乘以 1.1 来算出表所需的总内存。  
  
## <a name="see-also"></a>请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
