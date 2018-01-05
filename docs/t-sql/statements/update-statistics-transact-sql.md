---
title: "更新统计信息 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: "74"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7c69949773ff1dae533c98d087780a2f4b436b62
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  更新表或索引视图的查询优化统计信息。 默认情况下，查询优化器已更新统计信息根据需要来改进查询计划中;在某些情况下您可以通过使用 UPDATE STATISTICS 或存储的过程中提高查询性能[sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)比默认更新更频繁地更新统计信息。  
  
 更新统计信息可确保查询使用最新的统计信息进行编译。 不过，更新统计信息会导致查询重新编译。 我们建议不要太频繁地更新统计信息，因为需要在改进查询计划和重新编译查询所用时间之间权衡性能。 具体的折衷方案取决于你的应用程序。 UPDATE STATISTICS 可以使用 tempdb 对行样本进行排序以生成统计信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
UPDATE STATISTICS table_or_indexed_view_name   
    [   
        {   
            { index_or_statistics__name }  
          | ( { index_or_statistics_name } [ ,...n ] )   
                }  
    ]   
    [    WITH   
        [  
            FULLSCAN   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | SAMPLE number { PERCENT | ROWS }   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | RESAMPLE   
              [ ON PARTITIONS ( { <partition_number> | <range> } [, …n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ] 
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
UPDATE STATISTICS schema_name . ] table_name   
    [ ( { statistics_name | index_name } ) ]  
    [ WITH   
       {  
              FULLSCAN   
            | SAMPLE number PERCENT   
            | RESAMPLE   
        }  
    ]  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *table_or_indexed_view_name*  
 是表或索引的视图中包含的统计信息对象的名称。  
  
 *index_or_statistics_name*  
 要更新其统计信息的索引的名称，或要更新的统计信息的名称。 如果*index_or_statistics_name*未指定，则查询优化器更新的表或索引的视图的所有统计信息。 这包括使用 CREATE STATISTICS 语句创建的统计信息、在 AUTO_CREATE_STATISTICS 为 ON 时创建的单列统计信息以及为索引创建的统计信息。  
  
 AUTO_CREATE_STATISTICS 有关的详细信息，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 若要查看所有索引的表或都视图，你可以使用[sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)。  
  
 FULLSCAN  
 通过扫描表或索引视图中的所有行来计算统计信息。 FULLSCAN 和 SAMPLE 100 PERCENT 的结果相同。 FULLSCAN 不能与 SAMPLE 选项一起使用。  
  
 示例*数*{%|行}  
 指定当查询优化器更新统计信息时要为其使用的表或索引视图中近似的百分比或行数。 %，*数*可以是从 0 到 100 而为的行，*数*可以为从 0 到行的总数。 查询优化器抽样的实际行百分比或行数可能与指定的行百分比或行数不匹配。 例如，查询优化器扫描数据页上的所有行。  
  
 对于基于默认抽样的查询计划并非最佳的特殊情况，SAMPLE 非常有用。 在大多数情况下，不必指定 SAMPLE，这是因为在默认情况下，查询优化器根据需要采用抽样，并以统计方式确定大量样本的大小，以便创建高质量的查询计划。 
 
从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，使用兼容性级别 130 上，若要提高性能统计信息收集时，在并行中, 完成的采样数据以生成统计信息。 表大小超过特定阈值时，查询优化器将使用并行示例统计信息。 
   
 SAMPLE 不能与 FULLSCAN 选项一起使用。 如果未指定 SAMPLE 和 FULLSCAN，查询优化器则默认使用抽样数据并计算样本大小。  
  
 我们建议不指定 0 PERCENT 或 0 ROWS。 如果指定 0 PERCENT 或 0 ROWS，则将更新统计信息对象，但该对象不包含任何统计信息数据。  
  
 对于大多数工作负载，完全扫描不是必需的并默认采样已足够。  
但是，对完全不同的数据分布很敏感某些工作负荷可能需要增加的示例大小或甚至完全扫描。  
有关详细信息，请参阅[CSS SQL 升级服务博客](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx)。  
  
 RESAMPLE  
 使用最近的采样速率更新每个统计信息。  
  
 使用 RESAMPLE 会导致全表扫描。 例如，索引的统计信息使用全表扫描来获取其采样速率。 如果未指定采样选项（SAMPLE、FULLSCAN、RESAMPLE），则查询优化器默认将对数据进行抽样并计算样本大小。  

PERSIST_SAMPLE_PERCENT = {ON |关闭}  
当**ON**，统计信息将保留不显式指定抽样百分比的后续更新集采样百分比。 当**OFF**，将获取统计信息抽样百分比重置为默认采样中未显式指定抽样百分比的后续更新。 默认值是**OFF**。 
 
 > [!NOTE]
 > 如果执行 AUTO_UPDATE_STATISTICS，则它将使用持久化的抽样百分比如果可用，或如果不使用默认采样百分比。
 > 对重新取样行为不受此选项。
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)和[sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)公开选定的统计数据的持久化的示例百分比值。
 
 **适用于**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU4) 通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU1)。  
 
 ON PARTITIONS ({ \<partition_number > |\<范围 >}[，… n])] 强制涵盖 ON PARTITIONS 子句重新计算，并然后合并，以生成全局统计信息中指定的分区的叶级统计信息。 需要 WITH RESAMPLE，因为使用不同抽样率生成的分区统计信息不能合并在一起。  
  
**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 更新所有现有统计信息、在一列或多列上创建的统计信息或为索引创建的统计信息。 如果未指定上述任何选项，则 UPDATE STATISTICS 语句将更新表或索引视图上的所有统计信息。  
  
 NORECOMPUTE  
 为指定统计信息禁用自动统计信息更新选项 AUTO_UPDATE_STATISTICS。 如果指定此选项，则查询优化器将完成此统计信息更新并禁用将来的更新。  
  
 重新启用 AUTO_UPDATE_STATISTICS 选项的行为，而无需 NORECOMPUTE 选项重新运行更新统计信息或运行**sp_autostats**。  
  
> [!WARNING]  
>  使用此选项可能会产生并非最佳的查询计划。 建议您尽量少用此选项，并且此选项只能由有资格的系统管理员使用。  
  
 有关 AUTO_STATISTICS_UPDATE 选项的详细信息，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 当**ON**，根据分区统计信息重新创建统计信息。 当**OFF**，删除统计信息树和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新计算统计信息。 默认值是**OFF**。  
  
 如果不支持每个分区统计信息，将生成错误。 对于以下统计信息类型，不支持增量统计信息：  
  
-   使用未与基表的分区对齐的索引创建的统计信息。  
-   对 Always On 可读辅助数据库创建的统计信息。  
-   对只读数据库创建的统计信息。  
-   对筛选的索引创建的统计信息。  
-   对视图创建的统计信息。  
-   对内部表创建的统计信息。  
-   使用空间索引或 XML 索引创建的统计信息。  
  
**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]

MAXDOP = *max_degree_of_parallelism*  
**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3)。  
  
 重写**最大并行度**统计信息操作的持续时间的配置选项。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 @shouldalert  
 取消生成并行计划。  
  
 \>1  
 限制最大并行统计信息操作为指定的数或更少基于当前的系统工作负荷中使用的处理器数。  
  
 0（默认值）  
 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
 \<update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="remarks"></a>Remarks  
  
## <a name="when-to-use-update-statistics"></a>何时使用 UPDATE STATISTICS  
 有关何时使用更新统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  

## <a name="limitations-and-restrictions"></a>限制和局限  
* 外部表不支持更新统计信息。 若要更新对外部表的统计信息，请除去并重新创建统计信息。  
* MAXDOP 选项不兼容与 STATS_STREAM、 行计数和 PAGECOUNT 选项。

## <a name="updating-all-statistics-with-spupdatestats"></a>使用 sp_updatestats 更新所有统计信息  
 有关如何为数据库中的所有用户定义表和内部表更新统计信息的信息，请参阅存储过程 [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)。 例如，以下命令调用 sp_updatestats 来更新数据库的所有统计信息。  
  
```sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>确定最近的统计信息更新  
 若要确定最近一次更新统计信息的时间，请使用 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 函数。  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL 数据仓库  
 下面的语法不受 PDW / SQL 数据仓库  
  
```sql  
update statistics t1 (a,b);   
```  
  
```sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>权限  
 要求对表或视图具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-update-all-statistics-on-a-table"></a>A. 更新表的所有统计信息  
 下面的示例更新上的所有索引的统计信息`SalesOrderDetail`表。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>B. 更新索引的统计信息  
 以下示例更新 `AK_SalesOrderDetail_rowguid` 表的 `SalesOrderDetail` 索引的统计信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>C. 通过使用 50% 抽样更新统计信息  
 以下示例将创建并更新 `Name` 表中的 `ProductNumber` 和 `Product` 列的统计信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS Products  
    ON Production.Product ([Name], ProductNumber)  
    WITH SAMPLE 50 PERCENT  
-- Time passes. The UPDATE STATISTICS statement is then executed.  
UPDATE STATISTICS Production.Product(Products)   
    WITH SAMPLE 50 PERCENT;  
```  
  
### <a name="d-update-statistics-by-using-fullscan-and-norecompute"></a>D. 通过使用 FULLSCAN 和 NORECOMPUTE 更新统计信息  
 以下示例更新 `Products` 表中的 `Product` 统计信息，强制对 `Product` 表中的所有行进行完全扫描，并关闭 `Products` 统计信息的自动统计信息功能。  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>E. 表中更新统计信息  
 下面的示例更新`CustomerStats1`统计信息`Customer`表。  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. 通过使用完全扫描更新统计信息  
 下面的示例更新`CustomerStats1`基于扫描的所有行中的统计信息`Customer`表。  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. 更新表的所有统计信息  
 下面的示例将更新所有统计信息上`Customer`表。  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>另请参阅  
 [统计信息](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS (Transact-SQL)](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40;Transact SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  



