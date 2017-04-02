---
title: "内存优化表的索引 | Microsoft Docs"
ms.custom: 
  - "MSDN content"
  - "MSDN - SQL DB"
ms.date: "10/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-database"
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 14
---
# 内存优化表的索引
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
本文介绍可用于内存优化表的索引类型。 本文内容：  
  
- 提供简短代码示例来演示 Transact-SQL 语法。  
- 描述内存优化索引与传统的基于磁盘的索引有何不同。  
- 解释每种类型的内存优化索引的最佳使用场合。  
  
  
一篇内容与哈希索引[密切相关的文章](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)中对*哈希*索引进行了更详尽地探讨和介绍。  
  
  
[另一篇文章](Columnstore%20Indexes%20Guide.xml)介绍了 *Columnstore* 索引。  
  
  
## A. 内存优化索引的语法  
  
内存优化表的每个 CREATE TABLE 语句必须包含 1 到 8 子句来声明索引。 索引必须是以下类型之一：  
  
- 哈希索引。  
- 非聚集索引（表示 btree的默认内部结构）。  
  
  
要使用默认 DURABILITY=SCHEMA_AND_DATA 进行声明，内存优化表必须具有主键。 以下 CREATE TABLE 语句中的 PRIMARY KEY NONCLUSTERED 子句满足两个要求：  
  
- 提供一个索引以满足 CREATE TABLE 语句中至少需要一个索引的最低要求。  
- 提供 SCHEMA_AND_DATA 子句所需的主键。  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    “应用程序适配器” 区域）  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
### A.1 语法的代码示例  
  
本小节包含一个 Transact-SQL 代码块，用于演示在内存优化表中创建各种索引时使用的语法。 代码将演示以下操作：  
  
  
1. 创建内存优化表。  
2. 使用 ALTER TABLE 语句添加两条索引：  
3. 插入几行数据。  
  
  
  
    DROP TABLE IF EXISTS SupportEvent；  
    go  
  
    CREATE TABLE SupportEvent  
    (  
      SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
  
      StartDateTime        datetime2     not null,  
      CustomerName         nvarchar(16)  not null,  
      SupportEngineerName  nvarchar(16)      null,  
      Priority             int               null,  
      Description          nvarchar(64)      null  
    “应用程序适配器” 区域）  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_AND_DATA);  
    go  
      
        --------------------  
      
    ALTER TABLE SupportEvent  
      ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC、CustomerName)  
    go  
  
    ALTER TABLE SupportEvent  
      ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
      
        --------------------  
      
    INSERT INTO SupportEvent  
        (StartDateTime、CustomerName、SupportEngineerName、Priority、Description)  
      VALUES  
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ），  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ），  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ），  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go  
  
  
  
## B. 内存优化索引的性质  
  
在内存优化表中，每个索引也经过内存优化。 内存优化索引中的索引与基于磁盘的表中的传统索引在以下几个方面不同。  
  
每个内存优化索引只存在于活动内存中。 索引在磁盘上没有任何表示形式。  
  
- 当数据库重新联机时，将重新生成内存优化索引。  
  
  
当 SQL UPDATE 语句修改内存优化表中的数据时，不会在日志中写入对该表的索引所做的相应更改。  
  
  
内存优化索引中的条目包括表中行的直接内存地址。  
  
- 相比之下，磁盘上传统的 B 树索引中的条目包括一个键值，系统必须首先使用该键值来来查找关联表行的内存地址。  
  
  
与基于磁盘的索引不同，内存优化索引没有固定的页。  
  
- 它们不会在页面内累积典型的碎片类型，因而不具有填充因子。  
  
## C. 重复的索引键值

重复的索引键值可能会影响对内存优化表的操作的性能。 大量的重复项（例如，100+）会导致索引维护作业效率低下，因为必须针对大多数索引操作遍历重复链。 其影响可见之于对内存优化表的 INSERT、UPDATE 和 DELETE 操作。 对于哈希索引，此问题更加明显，因为对于哈希索引，每个操作成本更低，加之大型重复链会对哈希冲突链产生干扰。 若要减少索引中的重复，可以使用非聚集索引并将其他列（例如主键中的列）添加到索引键末尾，以减少重复项的数量。

可以试想一个例子，一个 Customers 表，其 CustomerId 上存在主键且 CustomerCategoryID 列上存在索引。 通常，一个给定的类别中会有许多客户，因此 CustomerCategoryID 列上的索引中的给定键会有许多重复值。 在这种情况下，最佳做法是在 (CustomerCategoryID, CustomerId) 上使用非聚集索引。 此索引可用于某些查询，这些查询使用涉及“CustomerCategoryID”的谓词，且索引不含重复内容，因此不会导致索引维护效率低下。

下面的查询显示表 `Sales.Customers` 中的 `CustomerCategoryID` 索引的平均重复索引键值数，该表位于示例数据库 [WideWorldImporters](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx) 中。

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

若要计算自己的表和索引的平均索引键重复项数，请将 `Sales.Customers` 替换为自己的表名，将 `CustomerCategoryID` 替换为索引键列的列表。

## D. 每个索引类型的使用时机比较  
  
  
特定查询的性质决定了哪种类型的索引是最佳选择。  

在现有应用程序中实现内存优化表时，常规建议是从使用非聚集索引开始，因为其功能更接近于传统聚集索引和基于磁盘的表上的非聚集索引。 
  
  
### D.1 非聚集索引的优势  
  
  
在以下情况下，非聚集索引比哈希索引更有优势：  
  
- 查询对索引列使用 ORDER BY 子句。  
- 只测试多列索引第一列的位置的查询。  
- 查询通过使用 WHERE 语句来测试索引列：  
  - 不等式：*WHERE StatusCode != 'Done'*  
  - 值范围：*WHERE Quantity >= 100*  
  
  
在以下所有 SELECT 中，非聚集索引比哈希索引更有优势：  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### D.2 哈希索引的优势  
  
  
在以下情况下，[哈希索引](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)比非聚集索引更有优势：  
  
- 查询通过对所有索引键列使用完全相同的 WHERE 子句来测试索引列，如下所示：  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### D.3 比较索引优势的摘要表  
  
  
下表列出了不同索引类型支持的所有操作。  
  
  
| 运算 | 内存优化， <br/> 哈希 | 内存优化， <br/> 非聚集 | 基于磁盘， <br/> （非）聚集 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 索引扫描，检索所有表行。 | 是 | 用户帐户控制 | 是 |  
| 采用相等谓词 (=) 的索引查找。 | 是 <br/> （需要完整键。） | 是  | 是 |  
| 采用不相等和范围谓词 <br/> （>、<、\<=、>=、BETWEEN）的索引查找。 | 是 <br/> （索引扫描中的结果。） | 是 | 是 |  
| 按与索引定义匹配的排序顺序检索行。 | 是 | 用户帐户控制 | 是 |  
| 按与索引定义相反的排序顺序检索行。 | 是 | “否” | 是 |  
  
  
在表中，“是”表示索引能够有效地为请求提供服务，“否”表示索引无法有效地满足请求。  


  
  
\<!--   
Indexes_for_Memory-Optimized_Tables.md , which is....  
CAPS guid: {eecc5821-152b-4ed5-888f-7c0e6beffed9}  
mt670614.aspx  
  
Application-Level%20Partitioning.xml , {162d1392-39d2-4436-a4d9-ee5c47864c5a}  
  
/Image/hekaton_tables_23d.png , fbc511a0-304c-42f7-807d-d59f3193748f  
  
  
Replaces dn511012.aspx , which is....  
CAPS guid: {86805eeb-6972-45d8-8369-16ededc535c7}  
  
GeneMi  ,  2016-05-05  Thursday  17:25pm  (Hash content moved to new child article, e922cc3a-3d6e-453b-8d32-f4b176e98488.)  
-->  
  
  
  
