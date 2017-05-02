---
title: "快速入门 1：用于提高 Transact-SQL 性能的内存中 OLTP 技术 | Microsoft Docs"
ms.custom: 
ms.date: 12/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82286b0d52ff37697ad9197b88c45935137a8dae
ms.lasthandoff: 04/11/2017

---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>内存中 OLTP 内的初始领域调查
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
本文适用于急于了解 Microsoft SQL Server 和 Azure SQL 数据库的内存中 OLTP 性能功能基础知识的开发人员。  
  
有关内存中 OLTP，本文提供以下内容：  
  
- 功能简介。  
- 实现功能的核心代码示例。  
  
  
SQL Server 和 SQL 数据库在内存中技术支持方面只有细微的不同。  
  
  
在现实中，一些博客主将内存中 OLTP 称为 *Hekaton*。  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>内存中功能的优点  
  
SQL Server 提供的内存中功能可极大提升许多应用程序系统的性能。 本部分以直接明了的方式介绍了相关注意事项。  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>OLTP（联机事务处理）的功能  
  
  
必须同时处理大量 SQL INSERT 的系统最适合采用 OLTP 功能。  
  
- 我们的基准显示，通过采用内存中功能，速度可提升 5 倍到超过 20 倍不等。  
  
  
处理 Transact-SQL 中的繁重计算的系统很适合采用此功能。  
  
- 专用于繁重计算的存储过程可提速高达 99 倍。  
  
  
稍后你可以查看以下文章，这些文章提供从内存中 OLTP 获取性能的演示：  
  
- [演示：内存中 OLTP 的性能改善](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) 提供了更大的潜在性能提升的小规模演示。  
- [内存中 OLTP 的示例数据库](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) 提供了更大规模的演示。  
  
  
  
### <a name="features-for-operational-analytics"></a>操作分析的功能  
  
内存中分析是指 SQL SELECT，它聚合事务数据，通常通过包含一个 GROUP BY 子句来实现。 称为 *columnstore* 的索引类型是操作分析的核心。  
  
有两种主要方案：  
  
- “批操作分析”** 是指在工作时间后运行或在具有事务数据副本的辅助硬件上运行的聚合进程。  
  - [Azure SQL 数据仓库](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) 也与批操作分析相关。  
- “实时操作分析”** 是指工作时间内在用于事务工作负荷的主硬件上运行的聚合进程。  
  
  
本文重点介绍 OLTP，而不是介绍相关分析。 有关列存储索引如何将分析引入 SQL 的信息，请参阅：  
  
- [开始使用列存储进行实时运行分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> 有关内存中功能的一个两分钟视频可在 [Azure SQL 数据库 - 内存中技术](http://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies)中找到。 该视频的发布日期为 2015 年 12 月。  


### <a name="columnstore"></a>columnstore

一系列精彩的博客文章从多个视角完美地介绍了列存储索引。 大部分文章都在深入介绍列存储支持的实时运行分析的概念。  这些文章由 Microsoft 项目经理 Sunil Agarwal 于 2016年 3 月创作。

#### <a name="real-time-operational-analytics"></a>实时运行分析

1. [Real-Time Operational Analytics Using In-Memory Technology](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [Real-Time Operational Analytics – Overview nonclustered columnstore index (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [Real-Time Operational Analytics: Simple example using nonclustered clustered columnstore index (NCCI) in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [Real-Time Operational Analytics: DML operations and nonclustered columnstore index (NCCI) in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [Real-Time Operational Analytics: Filtered nonclustered columnstore index (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [Real-Time Operational Analytics: Compression Delay Option for Nonclustered Columnstore Index (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [Real-Time Operational Analytics: Compression Delay option with NCCI and the performance](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [Real-Time Operational Analytics: Memory-Optimized Tables and Columnstore Index](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>对列存储索引进行碎片整理

1. [Columnstore Index Defragmentation using REORGANIZE Command](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [Columnstore Index Merge Policy for REORGANIZE](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>批量导入数据

1. [Clustered Column Store: Bulk Load](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [Clustered Columnstore Index: Data Load Optimizations – Minimal Logging](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [Clustered columnstore Index: Data Load Optimization – Parallel Bulk Import](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>内存中 OLTP 的功能  
  
让我们来了解一下内存中 OLTP 的主要功能。  
  
  
#### <a name="memory-optimized-tables"></a>内存优化表  
  
CREATE TABLE 语句上的 T-SQL 关键字 MEMORY_OPTIMIZED 是表格被创建的方式，目的是令表格存在于活动内存而非磁盘上。  
  
  
[内存优化表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) 在活动内存中有自身的一种表示形式，在磁盘上有辅助副本。  
  
- 磁盘副本用于在关闭然后重新启动服务器或数据库后进行常规恢复。 此内存加磁盘的双重性对你和你的代码处于完全隐藏的状态。  
  
  
#### <a name="natively-compiled-modules"></a>本机编译模块  
  
CREATE PROCEDURE 语句上的 T-SQL 关键字 NATIVE_COMPILATION 是本机进程的创建方式。 每次数据库联机循环中首次使用本机进程时，会将 T-SQL 语句编译为机器代码。 T-SQL 指令不再接受对每个指令的慢速解释。  
  
- 我们看到本机编译结果所需的持续时间是解释持续时间的 1/100。  
  
  
本机模块只能引用内存优化表，而不能引用基于磁盘的表。  
  
有三种类型的本机编译模块：  
  
- [本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
- 本机编译的用户定义函数 (UDF)，它们是标量。  
- 本机编译的触发器。  
  
  
#### <a name="availability-in-azure-sql-database"></a>Azure SQL 数据库中的可用性  
  
内存中 OLTP 和列存储在 Azure SQL 数据库中可用。 有关详细信息，请参阅 [Optimize Performance using In-Memory Technologies in SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)（在 SQL 数据库中使用内存中技术优化性能）。
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1.确保兼容级别 >= 130  
  
  
本部分一开始有编号的几节说明可用于实现内存中 OLTP 功能的 Transact-SQL 语法。  
  
  
首先，应将数据库的兼容级别至少设置为 130。 下面是 T-SQL 代码，用于查看当前数据库所设置的当前兼容级别。  
  
  
  
  
  
    SELECT d.compatibility_level  
        FROM sys.databases as d  
        WHERE d.name = Db_Name();  
  
  
  
  
下面是用于更新级别的 T-SQL 代码（如有必要）。  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET COMPATIBILITY_LEVEL = 130;  
  
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2.提升为快照  
  
  
当事务同时涉及基于磁盘的表和内存优化表时，我们将该事务称为*跨容器事务*。 在此类事务中，事务的内存优化部分必须以名为“快照”的事务隔离级别运行。  
  
若要可靠地对跨容器事务中的内存优化表强制执行此级别，请通过执行以下 T-SQL 来[变更数据库设置](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
  
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3.创建优化文件组  
  
  
在 Microsoft SQL Server 中，你必须先创建声明 CONTAINS MEMORY_OPTIMIZED_DATA 的文件组，然后才能创建内存优化表。 将该文件组分配给你的数据库。 有关详细信息，请参阅：  
  
- [内存优化的文件组](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
在 Azure SQL 数据库中，无需且不能创建此类文件组。  

下面的示例 T-SQL 脚本可为内存中 OLTP 启用数据库，并配置所有推荐设置。 它适用于 SQL Server 和 Azure SQL 数据库：[enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)。
  
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4.创建内存优化表  
  
  
  
  
重要的 Transact-SQL 关键字为关键字 MEMORY_OPTIMIZED。  
  
  
  
  
    CREATE TABLE dbo.SalesOrder  
    (  
        SalesOrderId   integer        not null  IDENTITY  
            PRIMARY KEY NONCLUSTERED,  
        CustomerId     integer        not null,  
        OrderDate      datetime       not null  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
  
针对内存优化表的 Transact-SQL INSERT 和 SELECT 语句与针对常规表的这些语句相同。  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>针对内存优化表的 ALTER TABLE  
  
ALTER TABLE...ADD/DROP 可以在内存优化表中添加或删除列或索引。  
  
- 不能对内存优化表运行 CREATE INDEX 和 DROP INDEX，但可使用 ALTER TABLE...ADD/DROP INDEX。  
- 有关详细信息，请参阅[变更内存优化表](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)。  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>规划内存优化表和索引  
  
  
- [内存优化表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [内存中 OLTP 不支持的 Transact-SQL 构造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5.创建本机编译的存储过程（本机过程）  
  
  
重要的关键字为 NATIVE_COMPILATION。  
  
  
  
  
    CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;  
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
  
  
  
  
关键字 SCHEMABINDING 表示，除非先删除本机过程，否则不能删除本机过程中引用的表。 有关详细信息，请参阅[创建本机编译的存储过程](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)。  
  
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6.执行本机过程  
  
  
使用两行数据填充表。  
  
  
  
  
    INSERT into dbo.SalesOrder  
            ( CustomerId, OrderDate )  
        VALUES  
            ( 42, '2013-01-13 03:35:59' ),  
            ( 42, '2015-01-15 15:35:59' );  
  
  
  
  
然后，对本机编译的存储过程调用 EXECUTE。  
  
  
  
  
    DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);  
      
    EXECUTE @LatestSalesOrderId =  
        ncspRetrieveLatestSalesOrderIdForCustomerId 42;  
      
    SET @mesg = CONCAT(@LatestSalesOrderId,  
        ' = Latest SalesOrderId, for CustomerId = ', 42);  
    PRINT @mesg;  
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>文档指南和后续步骤  
  
  
前面的简单示例为你学习内存中 OLTP 的更高级功能打下基础。 以下各节是可能需要知道的特殊注意事项，以及在哪里可以查看每个注意事项的相关详细信息的指南。  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>内存中 OLTP 功能如何执行得这样快  
  
  
以下各小节简要介绍内存中 OLTP 功能如何在内部工作以提高性能。  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>内存优化表如何执行速度更快  
  
  
**双重特性：** 内存优化表具有双重特性：在活动内存中是一种表示形式，在硬盘上是另一种表示形式。 每个事务将提交到该表的这两种表示形式。 事务针对更快的活动内存表示形式运行。 内存优化表从活动内存比磁盘速度更快受益。 此外，活动内存的更大灵活性使得实现针对速度进行优化的更高级表结构切实可行。 高级结构也是无页的，因此它可以避免闩锁和自旋锁的开销和争用。  
  
  
**无锁：** 内存优化表依赖于 *乐观* 方法来实现数据完整性与并发性和高吞吐量这两个对立的目标。 在事务处理期间，该表不在任何版本的已更新数据行上放置锁。 在某些大容量系统中，这可以大大减少争用。  
  
  
**行版本：** 内存优化表不使用锁，而是在表本身中（不是在 tempdb 中）添加新版本的已更新行。 原始行将一直保留，直到提交事务之后。 在事务处理期间，其他进程可以读取行的原始版本。  
  
- 为基于磁盘的表创建某一行的多个版本时，行版本将暂时存储在 tempdb 中。  
  
  
**更少的日志记录：** 已更新行的之前和之后版本将保存在内存优化表中。 行对提供了很多通常写入到日志文件的信息。 这使得系统将更少信息更少次数地写入到日志。 还确保事务完整性。  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>本机过程如何执行速度更快  
  
将常规解释型存储过程转换为本机编译的存储过程可大大减少要在运行时执行的指令数。  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>内存中功能的权衡  
  
  
正如在计算机科学中所常见的，内存中功能提供的性能提升是一种折中方案。 相比功能的额外成本，更好的功能带来的好处要更有价值得多。 可在此处找到关于权衡的全面指南：

- [在 SQL Server 中计划内存中 OLTP 功能的应用](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

本部分的剩余部分列出了一些主要规划和权衡注意事项。
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>内存优化表的权衡  
  
  
**估计内存：** 你必须估计内存优化表要使用的活动内存量。 计算机系统必须具有足够的内存容量，才能托管内存优化表。 有关详细信息，请参阅：  
  
- [内存使用情况的监视和故障排除](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [估算内存优化表的内存需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [内存优化表中的表和行大小](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**对大型表分区：** 满足大量活动内存需求的一种方法是将大型表划分为几部分，内存中的部分存储 *热度高的最近* 数据行，磁盘上的其他部分存储 *冷旧* 数据行（如已完全发货和已完成的销售订单）。 此分区是一个需要设计和实现的手动过程。 请参阅：  
  
- [应用程序级分区](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [用于对内存优化表进行分区的应用程序模式](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>本机过程的权衡  
  
  
- 本机编译的存储过程不能访问基于磁盘的表。 本机过程只能访问内存优化表。  
- 如果本机过程在服务器或数据库最近一次重新联机后第一次运行，则本机过程必须重新编译一次。 这会导致在本机过程开始运行前出现延迟。  
  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>内存优化表的高级注意事项  
  
  
[内存优化表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) 在某些方面与传统的磁盘上表中的索引有所不同。  
  
- 仅内存优化表可使用[哈希索引](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 。  
  
  
你必须计划以确保有足够的活动内存可用于计划的内存优化表及其索引。 请参阅：  
  
- [创建和管理用于内存优化对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
可使用 DURABILITY = SCHEMA_ONLY 声明内存优化表：  
  
- 此语法指示系统，在数据库已脱机时，丢弃内存优化表中的所有数据。 仅保留表定义。  
- 当数据库重新联机时，将内存优化表重新加载到活动内存中，数据为空。  
- 当涉及到成千上万个行时，SCHEMA_ONLY 表可作为 tempdb 中 [#temporary 表](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) 的上级替代项。  
  
  
也可以将表变量声明为内存优化变量。 请参阅：  
  
- [通过使用内存优化获得更快的临时表和表变量](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>本机编译模块的高级注意事项  
  
  
通过 Transact-SQL 提供的本机编译模块的类型包括：  
  
- 本机编译的存储过程（本机过程）。  
- 本机编译的 [标量用户定义函数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
- 本机编译的触发器（本机触发器）。  
  - 只允许对内存优化表使用本机编译的触发器。  
- 本机编译的 [表值函数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)。  
  - [Improving temp table and table variable performance using memory optimization](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
  
本机编译的用户定义函数 (UDF) 比解释型 UDF 运行速度更快。 下面是一些关于 UDF 的注意事项：  
  
- 当 T-SQL SELECT 使用 UDF 时，始终会在返回每行后调用 UDF。  
  - UDF 从不以内联方式运行，而是始终被调用。  
  - 编译的区别与所有 UDF 固有的重复调用的开销相比，并没有那么重要。  
  - 尽管如此，UDF 调用的开销在实用级别上通常是可接受的。  
  
有关本机 UDF 性能的测试数据和说明，请参阅：  
  
  - [Soften the RBAR impact with Native Compiled UDFs in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - [Gail Shaw 编写的好博客文章](http://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/)，发布日期为 2016 年 1 月。  
  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>内存优化表的文档指南  
  
  
以下是讨论内存优化表的特殊注意事项的其他文章的链接：  
  
- [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [确定表或存储过程是否应移植到内存中 OLTP](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - 通过 SQL Server Management Studio 中的事务性能分析报告，可帮助你评估内存中 OLTP 是否将改进数据库应用程序的性能。  
  - 使用 [内存优化顾问](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) 可帮助你将基于磁盘的数据库表迁移到内存中 OLTP。   
- [内存优化表的备份、还原和恢复](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - 内存优化表使用的存储可以比其在内存中的大小大得多，会影响数据库备份的大小。  
- [具有内存优化表的事务](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - 对于内存优化表上的事务，在 T-SQL 中包括有关重试逻辑的信息。  
- [对内存中 OLTP 的 Transact-SQL 支持](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - 内存优化表和本机过程支持和不支持的 T-SQL 和数据类型。  
- [将具有内存优化表的数据库绑定至资源池](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)，它讨论可选的高级注意事项。  
  
  
  
<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>本机过程的文档指南  
  
  
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>相关链接  
  
- 初始文章： [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
以下文章介绍了某些代码，演示了通过使用内存中 OLTP 可实现的性能提升：  
  
- [演示：内存中 OLTP 的性能改善](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) 提供了更大的潜在性能提升的小规模演示。  
- [内存中 OLTP 的示例数据库](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) 提供了更大规模的演示。  
  
  
  
\<!--  
  
e1328615-6b59-4473-8a8d-4f360f73187d，dn817827.aspx，“开始使用列存储进行实时运行分析”  
  
f98af4a5-4523-43b1-be8d-1b03c3217839，gg492088.aspx，“列存储索引指南”  
  
14dddf81-b502-49dc-a6b6-d18b1ae32d2b，dn133165.aspx，“内存优化表”  
  
d5ed432c-10c5-4e4f-883c-ef4d1fa32366，dn133184.aspx，“本机编译的存储过程”  
  
14106cc9-816b-493a-bcb9-fe66a1cd4630，dn639109.aspx，“内存优化文件组”  
  
f222b1d5-d2fa-4269-8294-4575a0e78636，dn465873.aspx，“将具有内存优化表的数据库绑定至资源池”  
  
86805eeb-6972-45d8-8369-16ededc535c7，dn511012.aspx，“内存优化表上的索引”  
  
16ef63a4-367a-46ac-917d-9eebc81ab29b，dn133166.aspx，“使用内存优化表上的索引的指导原则”  
  
e3f8009c-319d-4d7b-8993-828e55ccde11，dn246937.aspx，“内存中 OLTP 不支持的 Transact-SQL 构造”  
  
2cd07d26-a1f1-4034-8d6f-f196eed1b763，dn133169.aspx，“内存优化表中的事务”  
注意：请参阅 mt668425.aspx“将事务与内存优化表配合使用的行为和指导原则”，它很快会替换这些！  
f2a35c37-4449-49ee-8bba-928028f1de66，dn169141.aspx，“内存优化表上事务重试逻辑的指导原则”  
  
7a458b9c-3423-4e24-823d-99573544c877，dn465869.aspx，“监视内存使用情况并排查其问题”  
  
5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8，dn282389.aspx，“估算内存优化表的内存需求”  
  
b0a248a4-4488-4cc8-89fc-46906a8c24a1， dn205318.aspx，“内存优化表中的表和行大小”  
  
162d1392-39d2-4436-a4d9-ee5c47864c5a，dn296452.aspx，“应用程序级分区”  
  
3f867763-a8e6-413a-b015-20e9672cc4d1，dn133171.aspx，“用于对内存优化表进行分区的应用程序模式”  
  
86805eeb-6972-45d8-8369-16ededc535c7，dn511012.aspx，“内存优化表上的索引”  
  
d82f21fa-6be1-4723-a72e-f2526fafd1b6，dn465872.aspx，“为内存优化 OLTP 管理内存”  
  
622aabe6-95c7-42cc-8768-ac2e679c5089，dn133174.aspx，“为内存优化对象创建和管理存储”  
  
bd102e95-53e2-4da6-9b8b-0e4f02d286d3，dn535766.aspx，“内存优化表变量”；“内存优化表的表变量”  
已过时。 请改为参阅 38512a22-7e63-436f-9c13-dde7cf5c2202，mt718711.aspx，“使用内存优化提高访问临时表和表变量的速度”  
  
  
f0d5dd10-73fd-4e05-9177-07f56552bdf7， ms191320.aspx，“创建用户定义的函数（数据库引擎）”；“表值函数”  
  
d2546e40-fdfc-414b-8196-76ed1f124bf5，dn935012.aspx，“用于内存中 OLTP 的用户定义标量函数”；“用户定义的标量函数”  
  
405cdac5-a0d4-47a4-9180-82876b773b82，dn247639.aspx，“迁移到内存中 OLTP”  
  
3f083347-0fbb-4b19-a6fb-1818d545e281，dn624160.aspx，“备份、还原和恢复内存优化表”  
  
690b70b7-5be1-4014-af97-54e531997839，dn269114.aspx，“更改内存优化表”  
  
  
b1cc7c30-1747-4c21-88ac-e95a5e58baac，dn133080.aspx，“内存中 OLTP 的全新和更新的属性、系统视图、存储过程、等待类型和 DMV”  
。 。 。 。 。  
另请参阅：“对内存中 OLTP 的 Transact-SQL 支持”  
  
  
c1ef96f1-290d-4952-8369-2f49f27afee2，dn205133.aspx，“确定表或存储过程是否应移植到内存中 OLTP”  
  
181989c2-9636-415a-bd1d-d304fc920b8a，dn284308.aspx，“内存优化顾问”  
  
55548cb2-77a8-4953-8b5a-f2778a4f13cf，dn452282.aspx，“监视本机编译的存储过程性能”  
  
d3898a47-2985-4a08-bc70-fd8331a01b7b，dn358355.aspx，“本机编译顾问”  
  
f43faad4-2182-4b43-a76a-0e3b405816d1，dn296678.aspx，“本机编译的存储过程的迁移问题”  
  
e1d03d74-2572-4a55-afd6-7edf0bc28bdb，dn133186.aspx，“内存中 OLTP（内存中优化）”  
  
c6def45d-d2d4-4d24-8068-fab4cd94d8cc，dn530757.aspx，“演示：内存中 OLTP 的性能改进”  
  
405cdac5-a0d4-47a4-9180-82876b773b82，dn247639.aspx，“迁移到内存中 OLTP”  
  
f76fbd84-df59-4404-806b-8ecb4497c9cc，bb522682.aspx，“ALTER DATABASE SET 选项 (Transact-SQL)”  
  
e6b34010-cf62-4f65-bbdf-117f291cde7b，dn452286.aspx，“创建本机编译的存储过程”  
  
df347f9b-b950-4e3a-85f4-b9f21735eae3，mt465764.aspx，“内存中 OLTP 的示例数据库”  
  
38512a22-7e63-436f-9c13-dde7cf5c2202，mt718711.aspx，“使用内存优化提高访问临时表和表变量的速度”  
  
38512a22-7e63-436f-9c13-dde7cf5c2202，mt718711.aspx，“使用内存优化提高访问临时表和表变量的速度”  
  
  
  
  
H1 # 快速入门 1：用于提高事务工作负荷处理速度的内存中技术  
{1c25a164-547d-43c4-8484-6b5ee3cbaf3a} 采用大写  
MSDN 上的 mt718711.aspx  
  
GeneMi，2016-05-07  00:07am  
-->  
  
  
  


