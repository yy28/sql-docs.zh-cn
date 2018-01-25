---
title: "创建 TABLE AS SELECT （Azure SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 10/07/2016
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: "40"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 429c2dc727d844c35943fa599e6fbcb911df04ac
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>创建 TABLE AS SELECT （Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

创建表 AS SELECT (CTAS) 是可用的最重要的 T-SQL 功能之一。 它是创建新的表根据 SELECT 语句的输出完全并行化的操作。 CTAS 是创建表的副本的最简单、 最快方法。   
 
 例如，使用 CTAS 到：  
  
-   重新创建具有不同的哈希分布列的表。
-   按复制，重新创建表。   
-   对表中的列的其中一些创建列存储索引。  
-   查询或导入的外部数据。  

> [!NOTE]  
> 因为 CTAS 将添加到创建表的功能，本主题尝试不重复的 CREATE TABLE 主题。 相反，它描述 CTAS 和 CREATE TABLE 语句之间的差异。 创建表的详细信息，请参阅[CREATE TABLE （Azure SQL 数据仓库）](https://msdn.microsoft.com/library/mt203953/)语句。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>语法   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>参数  
有关详细信息，请参阅[参数部分](https://msdn.microsoft.com/library/mt203953/#Arguments)创建表中。  

<a name="column-options-bk"></a>

### <a name="column-options"></a>列选项
`column_name` [ ,...`n` ]   
 列名称不允许[列选项](https://msdn.microsoft.com/library/mt203953/#ColumnOptions)创建表中提到。  相反，你可以提供可选的新表的一个或多个列名称的列表。 新表中的列将使用指定的名称。 指定列名称时，列列表中的列数必须与所选结果中的列数匹配。 如果未指定任何列名称，新的目标表将在 select 语句结果中使用的列名称。 
  
 不能指定任何其他列选项，例如数据类型、 排序规则或为空性。 每个这些属性派生自的结果`SELECT`语句。 但是，你可以使用 SELECT 语句来更改的属性。 有关示例，请参阅[使用 CTAS 来更改列属性](#ctas-change-column-attributes-bk)。   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>表分发选项

`DISTRIBUTION` = `HASH` ( *distribution_column_name* ) | ROUND_ROBIN | REPLICATE      
CTAS 语句需要分发选项，并且没有默认值。 这是不同于具有默认值创建表。 

有关详细信息，以及若要了解如何选择最佳的分布列，请参阅[表分布选项](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions)创建表中的部分。 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>表分区选项
即使源表进行分区，CTAS 语句默认情况下，创建未分区的表。 若要使用 CTAS 语句创建已分区的表，必须指定分区选项。 

有关详细信息，请参阅[表分区选项](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions)创建表中的部分。

<a name="select-options-bk"></a>

### <a name="select-options"></a>选择选项
Select 语句是 CTAS 和创建表之间的基本差异。  

 `WITH` *common_table_expression*  
 指定临时命名的结果集，这些结果集称为公用表表达式 (CTE)。 有关详细信息，请参阅[使用 common_table_expression &#40;Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT` *select_criteria*  
 将填充新的表的结果与 SELECT 语句。 *select_criteria*是确定要将复制到新表的数据的 SELECT 语句的正文。 SELECT 语句有关的信息，请参阅[选择 &#40;Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>权限  
CTAS 需要`SELECT`中引用的任何对象权限*select_criteria*。

有关创建表的权限，请参阅[权限](https://msdn.microsoft.com/library/mt203953/#Permissions)创建表中。 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>一般备注
有关详细信息，请参阅[常规备注](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks)创建表中。

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>限制和局限  
Azure SQL 数据仓库尚不支持自动创建或自动更新统计信息。  若要从您的查询中获取最佳性能，请务必并在数据中发生的任何重大更改运行 CTAS 后的所有表的所有列都创建统计信息。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)。

[设置行计数 &#40;Transact SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md) CTAS 没有影响。 若要实现类似的行为，使用[顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
 
有关详细信息，请参阅[限制和局限](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions)创建表中。

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>锁定行为  
 有关详细信息，请参阅[锁定行为](https://msdn.microsoft.com/library/mt203953/#LockingBehavior)创建表中。
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>性能 

对于哈希分布式表，可以使用 CTAS 来选择的其他分发列，以实现更好的性能，联接和聚合。 如果选择其他分发列不你的目标，你将具有最佳的 CTAS 性能，如果你指定相同的分布列，因为这样可以避免重新分发的行。 

如果你使用 CTAS 来创建表，并且性能不是因素，你可以指定`ROUND_ROBIN`来避免不得不决定对分布列。

若要避免在后续查询中的数据移动，可以指定`REPLICATE`但代价是增加的存储，用于加载每个计算节点上的表的完整副本。  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>将一个表复制的示例

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. 使用 CTAS 复制表 
适用范围： Azure SQL 数据仓库和并行数据仓库

可能是最常见的一个用途`CTAS`创建表的副本，以便你可以更改 DDL。 如果最初创建与你表例如`ROUND_ROBIN`并且现在想要将其更改为分布的列的表`CTAS`是如何将更改分布列。 `CTAS`此外可以用于更改分区、 索引或列的类型。

假设你创建此表使用的默认分布类型`ROUND_ROBIN`分布中指定了任何分发列`CREATE TABLE`。

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

现在你想要创建此表的新副本具有聚集列存储索引，以便你可以利用聚集列存储表的性能。 你还想要分发 ProductKey 上的此表，因为预期此列的联接，并想要在联接 ProductKey 期间避免数据移动。 最后还想要添加在 OrderDateKey 上分区，以便你可以通过删除旧分区来快速删除旧数据。 下面是会将旧表复制到新表的 CTAS 语句。

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

最后，你可以重命名表以交换到新表，然后删除旧表。

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>列选项的示例

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. 使用 CTAS 来更改列属性 
适用范围： Azure SQL 数据仓库和并行数据仓库

此示例使用 CTAS 来更改数据类型、 可为 null 性和 DimCustomer2 表中的多个列的排序规则。  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
作为最后一步，你可以使用[重命名 &#40;Transact SQL &#41;](../../t-sql/statements/rename-transact-sql.md)切换表名称。 这使得 DimCustomer2 为新表。

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>表分发的的示例

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. 使用 CTAS 来更改为表的分发方法
适用范围： Azure SQL 数据仓库和并行数据仓库

这个简单的示例演示如何更改为表的分发方法。 若要显示如何执行此操作的机制，它更改为轮循机制的哈希分布式表，然后更改回哈希分布的轮循机制表。 最终的表匹配原始表。 

在大多数情况下不会需要将哈希分布式表更改为轮循机制表。 更多时候，你可能需要将轮循机制表更改为哈希分布式表。 例如，您可能最初加载一个新表作为轮循机制，然后会更高版本将其移到哈希分布式表，以获取更好的联接性能。

此示例使用 AdventureWorksDW 示例数据库。 若要加载的 SQL 数据仓库版本，请参阅[示例数据载入 SQL 数据仓库](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
接下来，将其更改回哈希分布式表中。

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. 使用 CTAS 将表转换为复制的表  
适用范围： Azure SQL 数据仓库和并行数据仓库 

此示例适用于将轮循机制或哈希分布式表转换为复制的表。 此特定示例将更改分发类型更进一步的上一个方法。  由于 DimSalesTerritory 维度和可能较小的表，你可以选择按复制以避免数据移动，联接到其他表时重新创建表。 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. 使用 CTAS 来创建具有较少的列的表
适用范围： Azure SQL 数据仓库和并行数据仓库 

下面的示例创建名为的轮循机制分布式的表`myTable (c, ln)`。 新表仅包含两列。 它使用列别名的 SELECT 语句中列的名称。  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>有关查询提示示例

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. 使用查询提示与 CREATE TABLE AS SELECT (CTAS)  
适用范围： Azure SQL 数据仓库和并行数据仓库
  
此查询显示使用 CTAS 语句的查询联接提示的基本语法。 提交该查询后，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]适用的哈希联接策略时它会生成每个单独的分发的查询计划。 哈希联接查询提示的详细信息，请参阅[OPTION 子句 &#40;Transact SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>外部表的示例

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. 使用 CTAS 来从 Azure Blob 存储导入数据  
适用范围： Azure SQL 数据仓库和并行数据仓库  

若要从外部表导入数据，只需使用 CREATE TABLE AS SELECT 选择从外部表。 用于从外部到表中选择数据的语法[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]从常规表中选择数据的语法相同。  
  
 下面的示例定义外部表上的 Azure blob 存储帐户中的数据。 它然后使用 CREATE TABLE AS SELECT 从外部表中选择。 这从 Azure blob 存储文本分隔文件导入数据并将数据存储到新[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]表。  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. 使用 CTAS 来从外部表导入 Hadoop 数据  
适用于：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
若要从外部表导入数据，只需使用 CREATE TABLE AS SELECT 选择从外部表。 用于从外部到表中选择数据的语法[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]从常规表中选择数据的语法相同。  
  
 下面的示例定义的 Hadoop 群集上的外部表。 它然后使用 CREATE TABLE AS SELECT 从外部表中选择。 这从 Hadoop 文本分隔文件导入数据并将数据存储到新[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]表。  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>使用 CTAS 替换 SQL Server 代码的示例

使用 CTAS 解决某些不受支持的功能。 除了能够在数据仓库上运行你的代码之外，重写现有代码以使用 CTAS 将通常提高性能。 这是其完全并行化设计的结果。 

> [!NOTE]
> 尽量考虑"CTAS 第一个"。 如果你认为可以解决问题使用`CTAS`，则通常最好的方法处理它-即使你正在编写更多的数据，因此。
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. 而不是选择使用 CTAS...到  
适用范围： Azure SQL 数据仓库和并行数据仓库

SQL Server 代码通常使用 SELECT...INTO 将填充包含 SELECT 语句的结果的表。 这是一个示例的 SQL Server SELECT...到语句。

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

在 SQL 数据仓库和并行数据仓库不支持此语法。 此示例演示如何重写以前选择...到作为 CTAS 语句的语句。 你可以选择任何 CTAS 语法中所述的分布选项。 此示例使用 round_robin 均可分发方法。

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. 使用 CTAS 和隐式联接替换中的 ANSI join`FROM`子句`UPDATE`语句  
适用范围： Azure SQL 数据仓库和并行数据仓库  

你可能会发现具有复杂的更新，它联接多个两个表一起使用 ANSI 联接语法来执行 UPDATE 或 DELETE。

假设你必须更新此表：

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

原始查询看起来可能如下：

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

由于不支持 SQL 数据仓库中使用 ANSI join`FROM`子句`UPDATE`语句，而无需略有更改上，不能使用通过此 SQL Server 代码。

你可以使用的组合`CTAS`和隐式联接来替换此代码：

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. 使用 CTAS 来指定哪些数据来使而不是使用 ANSI 联接的 DELETE 语句的 FROM 子句中  
适用范围： Azure SQL 数据仓库和并行数据仓库  

删除数据的最佳方法是使用有时`CTAS`。 除了删除数据，只需选择你想要保留的数据。 此尤其适用于`DELETE`使用的 ansi 联接语法，因为 SQL 数据仓库不支持 ANSI 联接中的语句`FROM`子句`DELETE`语句。

转换后的 DELETE 语句的示例所示：

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. 使用 CTAS 来简化 merge 语句  
适用范围： Azure SQL 数据仓库和并行数据仓库  

Merge 语句可以更换，至少在部分中，通过使用`CTAS`。 你可以合并`INSERT`和`UPDATE`成一条语句。 任何已删除的记录需要关闭第二个语句中。

一个示例`UPSERT`如下所示：

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. 显式声明数据类型和为 null 性输出  
适用范围： Azure SQL 数据仓库和并行数据仓库  

当 SQL Server 代码迁移到 SQL 数据仓库时，你可能会发现遇到这种类型的编码模式：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

自然而然你可能认为应将此代码迁移到 CTAS，并且你会正确。 但是，没有一个隐含的问题。

下面的代码不会生成相同的结果：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

请注意列"result"沿用表达式的数据类型以及为空值。 如果你不小心处理，这可能导致值存在细微的差异。

请尝试以下内容作为示例：

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

为结果存储的值不相同。 为在其他表达式中使用结果列中保留的值变得更加严重错误。

![CREATE TABLE AS SELECT 结果](../../t-sql/statements/media/create-table-as-select-results.png)

这一点对于数据迁移特别重要。 即使第二个查询看起来更准确的数据无效。 数据将会不同的与源系统相比，这产生了有关在迁移中的完整性的问题。 这是一个极少的情况下，其中"错误"答案是实际正确 ！

我们可以看到两个结果之间的这种不一致的原因是隐式类型强制转换。 在第一个示例表定义的列定义。 插入行时将发生隐式类型转换。 在第二个示例是任何隐式类型的转换过程，因为表达式定义的列的数据类型。 另请注意，第二个示例中的列已定义为可以为 Null 的列而第一个示例还没有。 在第一个示例列可为 null 创建表时，尚未显式定义。 在第二个示例，它只留给了表达式，默认情况下这将导致 NULL 定义。  

若要解决这些问题必须显式设置的类型转换和中的为 null 性`SELECT`部分`CTAS`语句。 在创建表的部分中，无法设置这些属性。

下面的示例演示如何修复代码：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

请注意以下事项：
- 可能已使用 CAST 或 CONVERT
- ISNULL 用于强制可为 Null 不是 COALESCE
- ISNULL 是最外层的函数
- ISNULL 的第二个部分是一个常数，即 0

> [!NOTE]
> 空性，要正确设置是至关重要的使用`ISNULL`而不`COALESCE`。 `COALESCE`不是确定性函数，因此表达式的结果将始终是可以为 Null。 `ISNULL`是不同的。 它是确定性的。 因此时的第二部分`ISNULL`函数为常量或文本，则生成的值将为 NOT NULL。

此提示不不仅可用于确保计算的完整性。 还有一点为表分区切换。 假设你有此表根据事实定义：

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

但是，值字段是计算的表达式不是源数据的一部分。

若要创建分区数据集可能想要执行此操作：

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

查询将会顺利运行。 当你尝试执行分区切换时，将出现问题。 表定义不匹配。 若要使表定义匹配 CTAS 需要进行修改。

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

您可以因此看到类型一致性并维护 CTAS 上的可为 null 属性是良好的工程最佳做法。 它有助于维护计算的完整性，而且还可确保分区切换能够实现。
 
## <a name="see-also"></a>另请参阅  
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
 [创建外部 TABLE AS SELECT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [创建 TABLE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [DROP EXTERNAL TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  


