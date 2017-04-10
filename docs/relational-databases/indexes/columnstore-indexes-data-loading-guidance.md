---
title: "列存储索引数据加载 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# 列存储索引数据加载
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  使用标准的 SQL 批量加载和渗透插入方法将数据载入列存储索引。 这些方法包括 bcp、Integration Services 和 Transact-SQL merge 或 insert 语句。  
  
 你是列存储索引的初学者？ 查看[列存储索引指南](../Topic/Columnstore%20Indexes%20Guide.md)中的术语和概念。  
  
 需要更深入的介绍？ 请参阅此 [博客文章](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx)。  
  
##  <a name="dataload_cci"></a> 批量加载到聚集列存储索引中  
 若要将行批量加载到聚集列存储索引中，可以使用 bcp 命令行工具、Integration Services，或者从临时表中选择行。  
  
 ![加载到聚集列存储索引中](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "加载到聚集列存储索引中")  
  
 如图所示，批量加载：  
  
1.  不会预先为数据排序。 按接收顺序将数据插入行组。  
  
2.  如果批大小 >= 102400，行将直接插入压缩的行组。 建议选择 >= 102400 的批大小以提高批量导入的效率，因为这样可以避免后台线程“元组发动机”(TM) 最终将行移到压缩行组之前，将数据行移到增量行组。  
  
3.  如果批大小 < 102400 或者剩余行数 < 102400，行将会载入增量行组。  
  
 批量载入聚集列存储索引的过程已经过以下优化  
  
-   并行加载：可以同时执行多个并发批量导入（使用 bcp 或批量插入），每次加载一个独立的数据文件。 与行存储不同，你不需要指定 TABLOCK，因为每个批量导入线程以独占方式将数据载入具有排他锁的独立行组（压缩或增量行组）。   使用 TABLOCK 会在表中强制排他锁，并且你无法并行导入数据。  
  
-   日志优化：将数据载入压缩行组时，将记录少量的批量加载信息。 使用 < 102400 的批大小将数据载入增量行组时，不会进行少量的日志记录。  
  
-   锁优化：载入压缩行组时，将在行组上获取 X 锁。 但是，批量加载到增量行组时，将在行组上获取 X 锁，但 SQL Server 仍会锁定 PAGE/EXTENT 锁，因为 X 行组锁不是锁定层次结构的一部分。  
  
 如果你有一个或多个非聚集索引，则索引本身不会经过锁定或日志记录优化，但是，针对聚集列存储索引的上述优化仍然存在。  
  
## 增量存储的工作原理  
 聚集列存储索引先在增量存储中收集多达 1,048,576 行，然后将其压缩到压缩行组中。 这可以提高列存储索引的压缩率。 如果增量存储行组包含 1,048,576 行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将行组标记为已关闭。 名为*元组发动机*的后台进程将查找每个关闭的行组并将其压缩到列存储中  
  
 每个聚集列存储索引可以有多个增量存储。  
  
-   如果锁定一个增量存储， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将尝试获取其他增量存储的锁。 如果没有可用的增量存储， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将创建新的增量存储。  
  
-   对于已分区的表，每个分区可以有多个增量存储。  
  
 以下方案说明何时将加载的行直接转到列存储中以及何时将它们转到增量存储中。  
  
 在示例中，每个行组可以具有 102,400-1,048,576 行。 在实践中，如果内存有压力，行组的最大大小可以小于 1,048,576 行。  
  
|要大容量加载的行|已添加到压缩行组的行|已添加到增量行组的行|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 行组大小：145,000|0|  
|1,048,577|1,048,576<br /><br /> 行组大小：1,048,576。|1|  
|2,252,152|2,252,152<br /><br /> 行组大小：1,048,576、1,048,576、155,000。|0|  
  
 以下示例显示将 1,048,577 行加载到表的结果。 这些结果显示列存储（作为压缩的列段）中的一个 COMPRESSED 行组以及增量存储中的 1 行。  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## 从临时表加载  
 数据加载的常见模式是将数据加载到临时表，执行某种转换，然后使用以下命令将其加载到目标表  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 此命令以类似于 BCP 或批量插入的方式将数据加载到列存储索引，但操作是以单个批完成的。 如果临时表中的行数 < 102400，行将加载到增量行组；否则，行将直接加载到压缩行组。  一个重要限制是此 INSERT 操作是单个线程的。 若要并行加载数据，你可以创建多个临时表，或者针对临时表中不重叠的行范围发出 INSERT/SELECT。  SQL Server 2016 中解除了这种限制。 以下命令将从临时表并行加载数据，但你需要指定 TABLOCK  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 从临时表加载到聚集列存储索引时，可以使用以下优化  
  
-   日志优化：将数据载入压缩行组时，将记录少量的信息。 将数据载入增量行组时，不会进行少量的日志记录。  
  
-   锁优化：载入压缩行组时，将在行组上获取 X 锁。 但是，对于增量行组，将在行组上获取 X 锁，但 SQL Server 仍会锁定 PAGE/EXTENT 锁，因为 X 行组锁不是锁定层次结构的一部分。  
  
 如果你有一个或多个非聚集索引，则索引本身不会经过锁定或日志记录优化，但是，针对聚集列存储索引的上述优化仍然存在  
  
## 使用渗透插入进行加载  
 *渗透插入* 是指使用 INSERT INTO 将行载入列存储的方法。 每个行将添加到增量行组。 渗透的行直接转到增量存储行组并在其中不断累积，直到到达 1,048,576 行之后行组关闭，或者重新生成了列存储索引。  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 请注意，使用 INSERT INTO 将值插入聚集列存储索引的并发线程可能会将行插入相同的增量存储行组。  
  
 一旦行组包含 1,048,576 行，增量行组将被标记为已关闭但仍可供查询和更新/删除操作使用，但新插入的行将进入现有或新建的增量存储行组。 后台线程*元组发动机 (TM)* 将每隔大约 5 分钟定期压缩已关闭的增量行组。 你可以显式调用以下命令来压缩已关闭的增量行组  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 如果你要强制关闭并压缩增量行组，可以执行以下命令。 如果你已完成加载行并且不希望插入任何新行，则可能需要运行此命令。 通过显式关闭并压缩增量行组，可以进一步节省存储空间，提高分析查询性能。 最佳做法之一是在不希望插入新行时调用此命令。  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## 加载到已分区表中  
 对于已分区数据， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 首先将每一行分配给一个分区，然后对该分区内的数据执行列存储操作。 每个分区都具有自己的行组以及至少一个增量存储。  
  
## 加载到非聚集列存储索引中  
 在包含非聚集列存储索引数据的行存储表上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 始终将数据插入到基表。 数据永远不会直接插入到列存储索引。  
  
## 另请参阅  
 [列存储索引指南](../Topic/Columnstore%20Indexes%20Guide.md)   
 [列存储索引版本的功能摘要](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [Columnstore Indexes Query Performance](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [开始使用列存储适进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [针对数据仓库的列存储索引](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [列存储索引碎片整理](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  