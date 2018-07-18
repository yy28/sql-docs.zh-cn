---
title: 内存优化表的索引 | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: in-memory-oltp
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2b2ce7ce7e891e0750f80637c3ebc42176167834
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34329568"
---
# <a name="indexes-on-memory-optimized-tables"></a>内存优化的表的索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

所有内存优化表都至少必须有一个索引，因为行正是通过索引才连接在一起。 在内存优化表中，每个索引也经过内存优化。 内存优化索引中的索引与基于磁盘的表中的传统索引在以下几个方面不同：  

- 由于数据行并未存储在页面上，因此既没有页面或盘区集合，也没有为了获取表的所有页面可以引用的分区或分配单元。 虽然可用索引类型之一存在索引页的概念，但它们的存储方式不同于本地表的索引。 它们不会在页面内累积典型的碎片类型，因而不具有填充因子。
- 在数据控制期间对内存优化表的索引所做的更改绝不会写入磁盘， 只会将数据行和对数据做出的更改写入事务日志。 
- 当数据库重新联机时，将重新生成内存优化索引。 

内存优化表的所有索引都是以数据库恢复期间的索引定义为依据进行创建。

索引必须是以下类型之一：  
  
- 哈希索引  
- 内存优化表的非聚集索引（即 B 树的默认内部结构） 
  
[内存优化表的哈希索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)更深入地介绍了哈希索引。
[内存优化表的非聚集索引](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)更深入地介绍了非聚集索引。  
*另一篇文章* 介绍了 [Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)索引。  

## <a name="syntax-for-memory-optimized-indexes"></a>内存优化索引的语法  
  
内存优化表的每个 CREATE TABLE 语句都必须包含索引，可以通过 INDEX 显式添加，也可以通过 PRIMAY KEY 或 UNIQUE 约束隐式添加。
  
内存优化表必须包含主键，才能使用默认 DURABILITY = SCHEMA\_AND_DATA 进行声明。 以下 CREATE TABLE 语句中的 PRIMARY KEY NONCLUSTERED 子句满足两个要求：  
  
- 提供一个索引以满足 CREATE TABLE 语句中至少需要一个索引的最低要求。  
- 提供 SCHEMA\_AND_DATA 子句所要求的主键。  

    ```sql
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA\_AND_DATA);  
    ```
> [!NOTE]  
> 对于每个内存优化表或表类型，[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 的索引数限制为 8 个。 自 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 起，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]中不再有内存优化表和表类型专属的索引数量限制。
  
### <a name="code-sample-for-syntax"></a>语法代码示例  
  
本小节包含一个 Transact-SQL 代码块，用于演示在内存优化表中创建各种索引时使用的语法。 代码将演示以下操作：  
  
1. 创建内存优化表。  
2. 使用 ALTER TABLE 语句添加两条索引：  
3. 插入几行数据。  
   
    ```sql
    DROP TABLE IF EXISTS SupportEvent;  
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
    )  
        WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA\_AND_DATA);  
    go  
        
        --------------------  
        
    ALTER TABLE SupportEvent  
        ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  

    ALTER TABLE SupportEvent  
        ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
        
        --------------------  
        
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
        VALUES  
        ('2016-02-23 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-24 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-26 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go 
    ``` 
  
## <a name="duplicate-index-key-values"></a>重复的索引键值

重复的索引键值可能会影响对内存优化表的操作的性能。 大量的重复项（例如，100+）会导致索引维护作业效率低下，因为必须针对大多数索引操作遍历重复链。 这可能会影响对内存优化表执行的 `INSERT`、`UPDATE` 和 `DELETE` 操作。 

对于哈希索引，此问题更加明显，这是因为对于哈希索引，每项操作的成本都更低，加之大型重复链会对哈希冲突链产生干扰。 若要减少索引中的重复，可以使用非聚集索引并将其他列（例如主键中的列）添加到索引键末尾，以减少重复项的数量。 若要详细了解哈希冲突，请参阅[内存优化表的哈希索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)。

例如，假设 `Customers` 表的列 `CustomerId` 上有主键，列 `CustomerCategoryID` 上有索引。 通常，一个给定的类别中会有许多客户，因此 CustomerCategoryID 列上的索引中的给定键会有许多重复值。 在此示例中，最佳做法是对 `(CustomerCategoryID, CustomerId)` 使用非聚集索引。 因为此索引可用于使用涉及 `CustomerCategoryID` 的谓词且不含重复内容的查询，所以不会导致索引维护效率低下。

下面的查询显示表 `CustomerCategoryID` 中的 `Sales.Customers`索引的平均重复索引键值数，该表位于示例数据库 [WideWorldImporters](../../sample/world-wide-importers/wide-world-importers-documentation.md)中。

```sql
SELECT AVG(row_count) FROM
    (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

若要计算自己的表和索引的平均索引键重复项数，请将 `Sales.Customers` 替换为自己的表名，将 `CustomerCategoryID` 替换为索引键列的列表。

## <a name="comparing-when-to-use-each-index-type"></a>每个索引类型的使用时机比较  
  
特定查询的性质决定了哪种类型的索引是最佳选择。  

在现有应用程序中实现内存优化表时，常规建议是从使用非聚集索引开始，因为其功能更接近于传统聚集索引和基于磁盘的表上的非聚集索引。 
  
### <a name="recommendations-for-nonclustered-index-use"></a>非聚集索引使用建议  
  
在以下情况下，非聚集索引比哈希索引更有优势：  
  
- 查询对索引列使用 `ORDER BY` 子句。  
- 只测试多列索引第一列的位置的查询。  
- 查询使用 `WHERE` 子句测试索引列：  
  - 不相等：`WHERE StatusCode != 'Done'`  
  - 值范围扫描：`WHERE Quantity >= 100`  
  
在以下所有 SELECT 中，非聚集索引比哈希索引更有优势：  

```sql
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE StartDateTime > DateAdd(day, -7, GetUtcDate());  
    
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE CustomerName != 'Ben';  
    
SELECT StartDateTime, CustomerName  
FROM SupportEvent  
ORDER BY StartDateTime;  
    
SELECT CustomerName  
FROM SupportEvent  
WHERE StartDateTime = '2016-02-26';  
```
  
### <a name="recommendations-for-hash-index-use"></a>哈希索引使用建议   
  
[哈希索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)主要用于点查阅，而不用于范围扫描。

如果使用相等谓词进行查询，且 `WHERE` 子句映射到所有索引键列，那么首选哈希索引，而不是非聚集索引，如下面的示例所示：  
  
```sql
SELECT CustomerName 
FROM SupportEvent  
WHERE SupportEngineerName = 'Liz';
```  

### <a name="multi-column-index"></a>多列索引  
  
多列索引可以是非聚集索引，也可以是哈希索引。 假设索引列是 col1 和 col2。 如果使用以下 `SELECT` 语句，只有非聚集索引对查询优化器有用：  
  
```sql
SELECT col1, col3  
FROM MyTable_memop  
WHERE col1 = 'dn';  
```

哈希索引需要 `WHERE` 子句为键中的所有列指定相等测试。 否则，哈希索引对查询优化器无用。  
  
如果 `WHERE` 子句仅指定索引键中的第二列，这两种索引类型都没有用。  

### <a name="summary-table-to-compare-index-use-scenarios"></a>比较索引使用方案的摘要表  
  
下表列出了不同索引类型支持的所有操作。 “是”表示索引能够有效地满足请求，“否”表示索引无法有效地满足请求。 
  
| 运算 | 内存优化， <br/> 密切相关的文章 | 内存优化， <br/> 非聚集 | 基于磁盘， <br/> （非）聚集 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 索引扫描，检索所有表行。 | 是 | 是 | 是 |  
| 采用相等谓词 (=) 的索引查找。 | 是 <br/> （需要完整键。） | 是  | 是 |  
| 采用不相等和范围谓词 <br/> （>、<、<=、>=、`BETWEEN`）。 | “否” <br/> （索引扫描中的结果。） | 是 <sup>1</sup> | 是 |  
| 按与索引定义匹配的排序顺序检索行。 | “否” | 是 | 是 |  
| 按与索引定义相反的排序顺序检索行。 | “否” | 否 | 是 |  

<sup>1</sup>对于内存优化表的非聚集索引，不需要完整键，也可以执行索引查找。  

## <a name="automatic-index-and-statistics-management"></a>自动索引和统计信息管理

利用[自适应索引碎片整理](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解决方案，自动管理一个或多个数据库的索引碎片整理和统计信息更新。 此过程根据碎片级别以及其他参数，自动选择是重新生成索引还是重新组织索引，并使用线性阈值更新统计信息。

## <a name="Additional_Reading"></a> 另请参阅   
 [SQL Server 索引设计指南](../../relational-databases/sql-server-index-design-guide.md)   
 [内存优化表的哈希索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [内存优化表的非聚集索引](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)    
 [自适应索引碎片整理](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)  
