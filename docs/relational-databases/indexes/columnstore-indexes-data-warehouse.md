---
title: "针对数据仓库的列存储索引 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21fd153b-116d-47fc-a926-f1528299a391
caps.latest.revision: 15
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 14
---
# 针对数据仓库的列存储索引
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  列存储索引与分区结合使用对于构建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据仓库而言必不可少。  
  
## <a name="whats-new"></a>新增功能  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 引入了以下用于增强列存储性能的功能：  
  
-   AlwaysOn 支持查询可读次要副本上的列存储索引。  
  
-   多个活动的结果集 (MARS) 支持列存储索引。  
  
-   新的动态管理视图 [sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) 提供行组级别的性能故障排除信息。  
  
-   对列存储索引的单线程查询可以在批处理模式下运行。 以前，只有多线程查询可以在批处理模式下运行。  
  
-   SORT 运算符在批处理模式下运行。  
  
-   多个 DISTINCT 操作在批处理模式下运行。  
  
-   窗口聚合在数据库兼容性级别 130 的批处理模式下运行  
  
-   针对高效处理聚合的聚合下推。 所有数据库兼容性级别均支持此功能。  
  
-   针对高效处理字符串谓词的字符串谓词下推。 所有数据库兼容性级别均支持此功能。  
  
-   数据库兼容级别 130 的快照隔离  
  
## <a name="improve-performance-by-combining-nonclustered-and-columnstore-indexes"></a>通过结合使用非聚集索引和列存储索引来提高性能  
 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，可以在聚集列存储索引上定义非聚集索引。  
  
### <a name="example-improve-efficiency-of-table-seeks-with-a-nonclustered-index"></a>示例︰借助非聚集索引提高表查找的效率  
 若要提高数据仓库中表查找的效率，可以创建专用于运行查询的非聚集索引，这种查询对于表查找的效率最高。 例如，查找匹配值或返回较小范围值的查询对于 btree 索引效果更好，而不是列存储索引。 它们无需通过列存储索引进行完整表扫描，只需通过 btree 索引执行二进制搜索就可以更快地返回正确结果。  
  
```  
--BASIC EXAMPLE: Create a nonclustered index on a columnstore table.  
  
--Create the table  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int  
);  
GO  
  
--Store the table as a columnstore.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account;  
GO  
  
--Add a nonclustered index.  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
```  
  
### <a name="example-use-a-nonclustered-index-to-enforce-a-primary-key-constraint-on-a-columnstore-table"></a>示例︰使用非聚集索引对列存储表实施强制主键约束  
 按照设计，列存储表不允许实施主键约束。 现在可以在列存储表上使用非聚集索引，以强制实施主键约束。 主键等同于非 NULL 列上的唯一约束，SQL Server 将唯一约束作为非聚集索引实施。 结合这些事实，下面的示例定义了非 NULL 列帐户密钥上的唯一约束。 结果获得非聚集索引，它将主键约束强制实施为非 NULL 列上的唯一约束。  
  
 接下来，将表转换为聚集列存储索引。 在转换期间，非聚集索引仍然存在。 结果获得聚集列存储索引和非聚集索引，强制实施主键约束。 因为在列存储表中的任何更新或插入都会影响非聚集索引，违反唯一约束和非 NULL 的所有操作都将都导致整个操作失败。  
  
 结果获得聚集列存储索引和非聚集索引，在两种索引上都强制实施主键约束。  
  
```  
--EXAMPLE: Enforce a primary key constraint on a columnstore table.   
  
--Create a rowstore table with a unique constraint.  
--The unique constraint is implemented as a nonclustered index.  
CREATE TABLE t_account (  
    AccountKey int NOT NULL,  
    AccountDescription nvarchar (50),  
    AccountType nvarchar(50),  
    UnitSold int,  
  
    CONSTRAINT uniq_account UNIQUE (AccountKey)  
);  
  
--Store the table as a columnstore.   
--The unique constraint is preserved as a nonclustered index on the columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX t_account_cci ON t_account  
  
--By using the previous two steps, every row in the table meets the UNIQUE constraint  
--on a non-NULL column.  
--This has the same end-result as having a primary key constraint  
--All updates and inserts must meet the unique constraint on the nonclustered index or they will fail.  
  
--If desired, add a foreign key constraint on AccountKey.  
  
ALTER TABLE [dbo].[t_account]  
WITH CHECK ADD FOREIGN KEY([AccountKey]) REFERENCES my_dimension(Accountkey)  
;  
  
```  
  
### <a name="improve-performance-by-enabling-row-level-and-row-group-level-locking"></a>通过启用行级和行组级锁定来提高性能  
 为了在列存储索引功能上补充非聚集索引， [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 针对选择、更新和删除操作提供细粒度锁定功能。 可以通过在索引查找中对非聚集索引实施行级锁定，并在全表扫描中对列存储索引实施行组级锁定的方法来运行查询。 通过使用适当的行级和行组级锁定，可提高读/写并发效率。  
  
```  
--Granular locking example  
--Store table t_account as a columnstore table.  
CREATE CLUSTERED COLUMNSTORE INDEX taccount_cci ON t_account  
GO  
  
--Add a nonclustered index for use with this example  
CREATE UNIQUE INDEX taccount_nc1 ON t_account (AccountKey);  
GO  
  
--Look at locking with access through the nonclustered index  
SET TRANSACTION ISOLATION LEVEL repeatable read;  
GO  
  
BEGIN TRAN  
    -- The query plan chooses a seek operation on the nonclustered index  
    -- and takes the row lock  
    SELECT * FROM t_account WHERE AccountKey = 100;  
END TRAN  
  
```  
  
### <a name="snapshot-isolation-and-read-committed-snapshot-isolations"></a>快照隔离和读提交快照隔离  
 针对列存储索引的查询，使用快照隔离 (SI) 可保证事务一致性，使用读提交快照隔离 (RCSI) 可保证语句级一致性。 从而运行查询时就不会阻止数据写入程序。 这种不会产生阻止的行为也大大降低了复杂事务出现死锁的可能性。 有关详细信息，请参阅 MSDN 上的 [SQL Server 中的快照隔离](http://msdn.microsoft.com/library/tcbchxcb\(v=vs.110\).aspx) 。  
  
## <a name="see-also"></a>另请参阅  
 [列存储索引指南](../Topic/Columnstore%20Indexes%20Guide.md)   
 [列存储索引数据加载](../Topic/Columnstore%20Indexes%20Data%20Loading.md)   
 [列存储索引版本的功能摘要](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [列存储索引查询性能](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [开始使用列存储进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [列存储索引碎片整理](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  