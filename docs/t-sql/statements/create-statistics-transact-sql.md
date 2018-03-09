---
title: "创建统计信息 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 088b79e73be6258afc5c664aaf14ba3cad9d2f5f
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在一个或多个列的表、 索引的视图或外部表上创建查询优化统计信息。 对于大多数查询，查询优化器已为高质量查询计划生成必要的统计信息；在少数情况下，您需要使用 CREATE STATISTICS 创建附加的统计信息或修改查询设计以提高查询性能。  
  
 若要了解详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | <update_stats_stream_option> [ ,...n ]    
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ]
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
    
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ] 
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>参数  
 *statistics_name*  
 是要创建的统计信息的名称。  
  
 *table_or_indexed_view_name*  
 是的表、 索引的视图或在其上创建统计信息的外部表的名称。 若要在另一个数据库中创建统计信息，请指定限定的表名。  
  
 *列 [，… n]*  
 要包含在统计信息的一个或多个列。 列应按从左到右的优先级顺序。 仅第一列用于创建直方图。 所有列都用于调用密度的跨列相关性统计信息。  
  
 您可以指定任何可指定为索引键列的列，但下列情况除外：  
  
-   **Xml**、 全文索引，并且不能指定 FILESTREAM 列。  
  
-   只有当 ARITHABORT 和 QUOTED_IDENTIFIER 数据库设置为 ON 时，才能指定计算列。  
  
-   如果 CLR 用户定义类型支持二进制排序，则可以指定 CLR 用户定义类型列。 如果方法具有确定性标记，可以指定定义为用户定义类型的列的方法调用的计算列。  
  
 其中\<filter_predicate > 指定用于选择要创建的统计信息对象时包括的行子集的表达式。 使用筛选谓词创建的统计信息称作筛选统计信息。 筛选器谓词使用简单比较逻辑，并且不能引用计算的列、 UDT 列中，空间数据类型列，或**hierarchyID**数据类型列。 比较运算符不允许使用 NULL 文本的比较。 请改用 IS NULL 和 IS NOT NULL 运算符。  
  
 下面是 Production.BillOfMaterials 表的筛选谓词的一些示例：  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 有关筛选器谓词的详细信息，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
 FULLSCAN  
 通过扫描所有行来计算统计信息。 FULLSCAN 和 SAMPLE 100 PERCENT 的结果相同。 FULLSCAN 不能与 SAMPLE 选项一起使用。  
  
 如果省略，SQL Server 将使用采样创建统计信息，并且确定创建高质量查询计划所需的样本大小  
  
 示例*数*{%|行}  
 指定在查询优化器创建统计信息时所使用的表或索引视图中的近似行百分比或行数。 %，*数*可以是从 0 到 100 而为的行，*数*可以为从 0 到行的总数。 查询优化器抽样的实际行百分比或行数可能与指定的行百分比或行数不匹配。 例如，查询优化器扫描数据页上的所有行。  
  
 对于基于默认抽样的查询计划并非最佳的特殊情况，SAMPLE 非常有用。 在大多数情况下，不必指定 SAMPLE，这是因为在默认情况下，查询优化器已根据需要采用抽样，并以统计方式确定大量样本的大小，以便创建高质量的查询计划。  
  
 SAMPLE 不能与 FULLSCAN 选项一起使用。 如果未指定 SAMPLE 和 FULLSCAN，查询优化器则默认使用抽样数据并计算样本大小。  
  
 我们建议不指定 0 PERCENT 或 0 ROWS。 如果指定 0 PERCENT 或 0 ROWS，则将创建统计信息对象，但该对象不包含任何统计信息数据。  
 
 PERSIST_SAMPLE_PERCENT = {ON |关闭}  
 当**ON**，统计信息将保留不显式指定抽样百分比的后续更新创建抽样百分比。 当**OFF**，将获取统计信息抽样百分比重置为默认采样中未显式指定抽样百分比的后续更新。 默认值是**OFF**。 
 
 **适用于**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU4) 通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU1)。    
  
 STATS_STREAM  **=**  *stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 禁用自动统计信息更新选项，AUTO_STATISTICS_UPDATE， *statistics_name*。 如果指定此选项，则查询优化器将在完成任何正在进行中的统计信息更新*statistics_name*和禁用将来的更新。  
  
 若要重新启用统计信息更新，删除统计与[DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md)就然后运行 NORECOMPUTE 选项创建统计信息。  
  
> [!WARNING]  
>  使用此选项可能会产生并非最佳的查询计划。 建议您尽量少用此选项，并且此选项只能由有资格的系统管理员使用。  
  
 有关 AUTO_STATISTICS_UPDATE 选项的详细信息，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 有关禁用并重新启用统计信息更新的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
 INCREMENTAL = { ON | OFF }  
 当**ON**，创建的统计信息是每个分区统计信息。 当**OFF**，为所有分区合并统计信息。 默认值是**OFF**。  
  
 如果不支持每个分区统计信息，将生成错误。 对于以下统计信息类型，不支持增量统计信息：  
  
-   使用未与基表的分区对齐的索引创建的统计信息。  
-   对 Always On 可读辅助数据库创建的统计信息。  
-   对只读数据库创建的统计信息。  
-   对筛选的索引创建的统计信息。  
-   对视图创建的统计信息。  
-   对内部表创建的统计信息。  
-   使用空间索引或 XML 索引创建的统计信息。  
  
**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
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

## <a name="permissions"></a>权限  
 需要下列权限之一：  
  
-   ALTER TABLE  
-   用户是表所有者  
-   中的成员身份**db_ddladmin**固定的数据库角色  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以使用 tempdb 对行进行排序的抽样生成统计信息之前。  
  
### <a name="statistics-for-external-tables"></a>外部表的统计信息  
 创建外部表统计信息时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将外部表导入一个临时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，然后再创建统计信息。 对于示例统计数据，导入仅抽样的行。 如果你有大型的外部表，它将使用默认采样而不是完全扫描选项要快得多。  
  
### <a name="statistics-with-a-filtered-condition"></a>统计与筛选条件  
 筛选统计信息可以提高以下从定义完善的数据子集选择数据的查询的查询性能。 筛选的统计信息在 WHERE 子句中使用筛选谓词来选择统计信息中包含的数据子集。  
  
### <a name="when-to-use-create-statistics"></a>何时使用 CREATE STATISTICS  
 有关何时使用创建统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>筛选统计信息的引用依赖项  
 [Sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)目录视图跟踪作为引用的依赖关系的筛选的统计信息谓词中每一列。 由于您无法删除、重命名或修改在筛选统计信息谓词中定义的表列的定义，因此在创建筛选统计信息之前应考虑清楚要对表列执行哪些操作。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
* 外部表不支持更新统计信息。 若要更新对外部表的统计信息，请除去并重新创建统计信息。  
* 你可以列出每个统计信息对象的最多为 64 列。
* MAXDOP 选项不兼容与 STATS_STREAM、 行计数和 PAGECOUNT 选项。
  
## <a name="examples"></a>示例  

### <a name="examples-use-the-adventureworks-database"></a>示例使用 AdventureWorks 数据库。  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. 将 CREATE STATISTICS 与 SAMPLE number PERCENT 一起使用  
 下面的示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `ContactMail1` 表的 `BusinessEntityID` 和 `EmailPromotion` 列的 5% 作为随机抽样来创建 `Contact` 统计信息。  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. 将 CREATE STATISTICS 与 FULLSCAN 和 NORECOMPUTE 一起使用  
 以下示例对 `ContactMail2` 表的 `BusinessEntityID` 和 `EmailPromotion` 列中的所有行创建 `Contact` 统计信息，并禁用自动重新计算统计信息。  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. 使用 CREATE STATISTICS 创建筛选统计信息  
 以下示例创建筛选统计信息 `ContactPromotion1`。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]对 50% 的数据进行采样，然后选择 `EmailPromotion` 等于 2 的行。  
  
```sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. 在外部表上创建统计信息  
 唯一需要进行外部表，除了提供的列，列表上创建统计信息时的决定是由采样行或通过扫描的所有行来创建统计信息。  
  
 由于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入到临时表创建统计信息，完全扫描选项外部表中的数据需要更长的时间。 对于大型表，默认采样方法就足够了。  
  
```sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>E. 使用指定 FULLSCAN 和 PERSIST_SAMPLE_PERCENT 创建统计信息  
 下面的示例创建`ContactMail2`中的所有行的统计信息`BusinessEntityID`和`EmailPromotion`列`Contact`表，然后执行不明确的所有后续更新指定采样设置的 100%采样百分比百分比。  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>示例使用 AdventureWorksDW 数据库。 
  
### <a name="f-create-statistics-on-two-columns"></a>F. 两个列创建统计信息  
 下面的示例创建`CustomerStats1`统计信息，基于`CustomerKey`和`EmailAddress`列`DimCustomer`表。 统计信息基于中的行具有统计学意义采样创建`Customer`表。  
  
```sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. 通过使用完全扫描创建统计信息  
 下面的示例创建`CustomerStatsFullScan`基于扫描的所有行中的统计信息`DimCustomer`表。  
  
```sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. 通过指定抽样百分比创建统计信息  
 下面的示例创建`CustomerStatsSampleScan`基于扫描中的行的 50%的统计信息`DimCustomer`表。  
  
```sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [统计信息](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS (Transact-SQL)](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

