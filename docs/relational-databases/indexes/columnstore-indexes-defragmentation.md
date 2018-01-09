---
title: "列存储索引 - 碎片整理 | Microsoft Docs"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3efda1a-7bdb-47f5-80bf-f075329edee5
caps.latest.revision: "17"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9c4ca97bfc2bb8edd783913c8c2c3ad712eac57d
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="columnstore-indexes---defragmentation"></a>列存储索引 - 碎片整理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  对列存储索引进行碎片整理的任务。  
  
## <a name="use-alter-index-reorganize-to-defragment-a-columnstore-index-online"></a>使用 ALTER INDEX REORGANIZE 对列存储索引进行在线碎片整理  
 **适用对象：**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本）、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
加载任何类型的数据之后，增量存储中会有多个较小的行组。 可以使用 `ALTER INDEX REORGANIZE` 将所有行组强制载入列存储，然后将行组合并成具有更多行的较少行组。  重新组织操作还将删除已从列存储中删除的行。  
  
有关详细信息，请参阅 SQL 数据库引擎团队博客中的以下博客文章。  
-   [最小化列存储索引中的索引碎片](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
-   [列存储索引和行组的合并策略](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
### <a name="recommendations-for-reorganizing"></a>进行重新组织的建议  
在执行一次或多次数据加载后，为了尽快优化查询性能，需要重新组织列存储索引。 重新组织最初需要额外的 CPU 资源来压缩数据，这可能降低整体系统性能。 但是，压缩数据后，可以提高查询性能。  
  
使用 [sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) 中的示例来计算碎片。 这可帮助你确定它是否值得执行 REORGANIZE 操作。  
  
### <a name="example-how-reorganizing-works"></a>示例：重新组织的工作原理  
 此示例演示 ALTER INDEX REORGANIZE 如何将所有增量存储行组强制转到列存储中，然后合并行组。  
  
1.  运行此 Transact SQL 以创建包含 300,000 行的临时表。 我们将使用它来将行批量加载到列存储索引中。  
  
    ```sql  
    USE master;  
    GO  
  
    IF EXISTS (SELECT name FROM sys.databases  
        WHERE name = N'[columnstore]')  
        DROP DATABASE [columnstore];  
    GO  
  
    CREATE DATABASE [columnstore];  
    GO  
  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'staging'  
        AND object_id = OBJECT_ID (N'staging'))  
    DROP TABLE dbo.staging;  
    GO  
  
    CREATE TABLE [staging] (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int  
    );  
    GO  
  
    -- Load data  
    DECLARE @loop int;  
    DECLARE @AccountDescription varchar(50);  
    DECLARE @AccountKey int;  
    DECLARE @AccountType varchar(50);  
    DECLARE @AccountCode int;  
  
    SELECT @loop = 0;  
    BEGIN TRAN  
        WHILE (@loop < 300000)   
          BEGIN  
            SELECT @AccountKey = CAST (RAND()*10000000 AS int);  
            SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountCode =  CAST (RAND()*10000000 AS int);  
  
            INSERT INTO staging VALUES (  
               @AccountKey,   
               @AccountDescription,   
               @AccountType,   
               @AccountCode  
            );  
  
            SELECT @loop = @loop + 1;  
          END  
    COMMIT  
    ```  
  
2.  创建存储为列存储索引的表。  
  
    ```sql  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'cci_target'  
        AND object_id = OBJECT_ID (N'cci_target'))  
    DROP TABLE dbo.cci_target;  
    GO  
  
    -- Create a table with a clustered columnstore index  
    -- and the same columns as the rowstore staging table.  
    CREATE TABLE cci_target (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int,  
         INDEX idx_cci_target CLUSTERED COLUMNSTORE  
    )  
    GO  
    ```  
  
3.  将临时表行批量插入到列存储表中。 `INSERT INTO ... SELECT` 用于执行批量插入。 `TABLOCK` 允许以并行方式执行 `INSERT`。  
  
    ```sql  
    -- Insert rows in parallel  
    INSERT INTO cci_target WITH (TABLOCK)  
    SELECT TOP (300000) * FROM staging;  
    GO  
    ```  
  
4.  通过使用 sys.dm_db_column_store_row_group_physical_stats 动态管理视图 (DMV) 来查看行组。  
  
    ```sql  
    -- Run this dynamic management view (DMV) to see the OPEN rowgroups.   
    -- The number of rowgroups depends on the degree of parallelism.   
    -- You will see multiple OPEN rowgroups depending on the degree of parallelism.   
    -- This is because insert operation can run in parallel in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     在此示例中，结果显示 8 个 OPEN 行组，每个包含 37,500 行。 OPEN 行组的数目取决于 max_degree_of_parallelism 设置。  
  
     ![OPEN 行组](../../relational-databases/indexes/media/cci-openrowgroups.png "OPEN 行组")  
  
5.  使用带有 `COMPRESS_ALL_ROW_GROUPS` 选项的 `ALTER INDEX REORGANIZE` 强制所有行组压缩到列存储。  
  
    ```sql  
    -- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
    ALTER INDEX idx_cci_target ON cci_target   
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     结果显示 8 个 COMPRESSED 行组和 8 个 TOMBSTONE 行组。 无论行组的大小如何，都压缩到列存储中。 TOMBSTONE 行组将由系统删除。  
  
     ![TOMBSTONE 和 COMPRESSED 行组](../../relational-databases/indexes/media/cci-tombstone-compressed-rowgroups.png "TOMBSTONE 和 COMPRESSED 行组")  
  
6.  就查询性能而言，将小行组合并在一起会更好。 `ALTER INDEX REORGANIZE` 用于将 `COMPRESSED` 行组合并在一起。 将增量行组压缩到列存储中后，再次运行 ALTER INDEX REORGANIZE 以合并小的 COMPRESSED 行组。 此时不需要 `COMPRESS_ALL_ROW_GROUPS` 选项。  
  
    ```sql  
    -- Run this again and you will see that smaller rowgroups   
    -- combined into one compressed rowgroup with 300,000 rows  
    ALTER INDEX idx_cci_target ON cci_target REORGANIZE;  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     结果显示 8 个 COMPRESSED 行组合并成一个 COMPRESSED 行组。  
  
     ![合并行组](../../relational-databases/indexes/media/cci-compressed-rowgroups.png "合并行组")  
  
## <a name="rebuild"></a> 使用 ALTER INDEX REBUILD 对列存储索引进行离线碎片整理  
 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本中，通常不需要重新生成列存储索引，因为 `REORGANIZE` 以在线操作形式在后台执行重要的重新生成。  
  
 重新生成列存储索引会删除碎片，并将所有行移到列存储中。 使用 [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md) 或 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md) 执行完全重新生成现有聚集列存储索引。 此外，你也可以使用 ALTER INDEX... REBUILD，用于重新生成特定分区。  
  
### <a name="rebuild-process"></a>重新生成过程  
 要重新生成列存储索引， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：  
  
1.  在重新生成进行时获取表或分区上的排他锁。 数据是“离线”的，在重新生成期间不可用，即使使用 `NOLOCK`、RCSI 或 SI 也是如此。  
  
2.  将所有数据重新压缩到列存储中。 在进行重新生成时存在列存储索引的两个副本。 在重新生成完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将删除原始列存储索引。  
  
### <a name="recommendations-for-rebuilding-a-columnstore-index"></a>有关重新生成列存储索引的建议  
 重新生成列存储索引适用于删除碎片，并且适用于将所有行移到列存储中。 请考虑以下建议：  
  
1.  重新生成分区而不是整个表。  
    -   如果索引很大，并且在重新生成期间需要足够的磁盘空间来存储索引的额外副本，则重新生成整个表将很费时间。 通常仅需要重新生成最近使用的分区。  
    -   对于已分区的表，您不需要重新生成整个列存储索引，因为碎片仅可能在最近修改的分区中出现。 事实表和大型的维度表通常已分区，以便对表的特定块执行备份和管理操作。  

2.  在执行了大量 DML 操作后重新生成分区  
    -   重新生成某一分区将会对该分区进行碎片整理，并且缩小磁盘存储空间。 重新生成将会从列存储中删除标记为要删除的所有行，并且会将所有行组从增量存储移到列存储中。 请注意，增量存储中可以有多个行组，每个包含少于一百万行。  
  
3.  在加载数据后重新生成分区。  
    -   这可确保所有数据都存储于列存储中。 当并发进程在同一时间将少于 100K 行的行组加载到同一分区时，该分区可以得到多个增量存储。 重新生成会将所有增量存储行都移到列存储中。  

## <a name="automatic-index-and-statistics-management"></a>自动索引和统计信息管理

利用[自适应索引碎片整理](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解决方案，自动管理一个或多个数据库的索引碎片整理和统计信息更新。 此过程根据碎片级别以及其他参数，自动选择是重新生成索引还是重新组织索引，并使用线性阈值更新统计信息。

## <a name="see-also"></a>另请参阅        
[列存储索引 - 新增功能](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)    
[Columnstore Indexes Query Performance](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
[开始使用列存储进行实时运营分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
[针对数据仓库的列存储索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
[列存储索引体系结构](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)    
[自适应索引碎片整理](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)    
  
  
