---
title: "创建表 （Azure SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
caps.latest.revision: 59
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11df71495b55ca72074c6ab928caaf6474bb2576
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-azure-sql-data-warehouse"></a>创建表 （Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  创建一个新表中的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
 
若要了解表以及如何使用它们，请参阅[SQL 数据仓库中的表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/)。

注意： 有关本文中的 SQL 数据仓库的讨论适用于 SQL 数据仓库和并行数据仓库除非另行说明。 
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>   
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new table. 
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]   
    )  
    [ WITH [ <table_option> [ ,...n ] ) ]  
[;]  
   
<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC 
    }  
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }   
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )  
  
<data type> ::=   
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>   
## <a name="arguments"></a>参数  
 *database_name*  
 将包含新表的数据库名称。 默认为当前数据库。  
  
 *schema_name*  
 表的架构。 指定*架构*是可选的。 如果为空，则将使用默认架构。  
  
 *table_name*  
 新的表的名称。 若要创建本地临时表，表名称前面加上 #。  有关说明和在临时表上的指南，请参阅[Azure SQL 数据仓库中的临时表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/)。 
 
 *column_name*  
 表列的名称。
   
### <a name="ColumnOptions"></a>列选项

 `COLLATE`*Windows_collation_name*  
 指定表达式的排序规则。 排序规则必须是支持的 Windows 排序规则之一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关支持的 Windows 排序规则的列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[Windows 排序规则名称 (Transact SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/)。  
  
 `NULL` | `NOT NULL`  
 指定是否`NULL`列中允许值。 默认值为 `NULL`。  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 指定列的默认值。  
  
 | 参数 | 解释 |
 | -------- | ----------- |
 | *constraint_name* | 约束可选名称。 约束名称是唯一的数据库中。 名称可以是其他数据库中重复使用。 |
 | *constant_expression* | 列的默认值。 表达式必须是文字值或常量。 例如，允许这些常量的表达式： `'CA'`， `4`。 这些不允许： `2+3`， `CURRENT_TIMESTAMP`。 |
  

### <a name="TableOptions"></a>表结构选项
有关选择的表类型的指南，请参阅[对 Azure SQL 数据仓库中的表创建索引](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/)。
  
 `CLUSTERED COLUMNSTORE INDEX`  
将表存储为聚集列存储索引。 聚集列存储索引适用于所有表数据。 这是默认值[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。   
 
 `HEAP`   
  将表存储为堆。 这是默认值[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 `CLUSTERED INDEX`( *index_column_name* [，...*n* ] )  
 将表存储为具有一个或多个键列的聚集索引。 这可以按行存储数据。 使用*index_column_name*索引中指定一个或多个键列的名称。  有关详细信息，请参阅常规备注中的行存储表。
 
 `LOCATION = USER_DB`   
 此选项已弃用。 它语法接受，但不再需要并不会再影响行为。   
  
### <a name="TableDistributionOptions"></a>表分发选项
若要了解如何选择最佳的分发方法和使用分布式的表，请参阅[分发 Azure SQL 数据仓库中的表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/)。

`DISTRIBUTION = HASH`( *distribution_column_name* )   
由哈希中存储的值将每一行分配到一个分发*distribution_column_name*。 这意味着始终哈希到相同的分布的相同值的算法是确定性。  自 NULL 将分配到相同的分布的所有行，应将分发列定义为 NOT NULL。

`DISTRIBUTION = ROUND_ROBIN`   
将行均匀地分布到一种轮循机制的方式中的所有分布区。 这是默认值[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。

`DISTRIBUTION = REPLICATE`    
将表的一个副本存储在每个计算节点上。 有关[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]表存储在每个计算节点上的分发数据库上。 有关[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，则表存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]跨计算节点的文件组。 这是默认值[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。
  
### <a name="TablePartitionOptions"></a>表分区选项
有关使用表分区的指南，请参阅[对 SQL 数据仓库中的表进行分区](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)。

 `PARTITION`( *partition_column_name* `RANGE` [ `LEFT`  |  `RIGHT` ] `FOR VALUES` ([*小于 boundary_value* [，...*n*] ] ))   
创建一个或多个表分区。 这些是可用于执行操作而不考虑是否将表存储为堆、 聚集的索引或聚集列存储索引的行子集的水平表切片。 与不同的分布列，表分区不用于确定每个行的存储位置的分布。 相反，表分区确定如何行分组，并存储在每个分布。  
 
| 参数 | 解释 |
| -------- | ----------- |
|*partition_column_name*| 指定的列，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将用于分区的行。 此列可以是任何数据类型。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]分区列值以升序排序。 从低到高顺序转`LEFT`到`RIGHT`为了`RANGE`规范。 |  
| `RANGE LEFT` | 指定的边界值属于左侧 （较低的值） 的分区。 默认值为左侧。 |
| `RANGE RIGHT` | 指定边界值所属的权限 （较高的值） 上的分区。 | 
| `FOR VALUES`(*小于 boundary_value* [，...*n*] ) | 指定分区的边界值。 *小于 boundary_value*是常量表达式。 它不能为 NULL。 它必须匹配，或者为隐式转换的数据类型为*partition_column_name*。 它不能被截断隐式转换的过程以使的大小和值的小数位数不匹配的数据类型*partition_column_name*<br></br><br></br>如果指定`PARTITION`子句，但未指定边界值，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将创建已分区的表具有一个分区。 如果适用，你拆分为两个分区在以后的表。<br></br><br></br>如果指定了一个边界值，生成的表具有两个分区;一个用于低于的边界值和一个用于大于边界值的值的值。 请注意，是否将分区移动到未分区表，则未分区表将接收的数据，但将不具有其元数据中的分区边界。| 
 
 请参阅[创建已分区的表](#PartitionedTable)示例部分中。

### <a name="DataTypes"></a>数据类型
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]支持最常用的数据类型。 下面是支持的数据类型以及它们的详细信息和存储字节的列表。 若要更好地了解数据类型以及如何使用它们，请参阅[SQL 数据仓库中的表的数据类型](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types)。

数据类型转换的表，请参阅隐式转换部分中的[CAST 和 CONVERT (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms187928/)。

`datetimeoffset` [ ( *n* ) ]  
 默认值为 *n* 为 7。  
  
 `datetime2` [ ( *n* ) ]  
与相同`datetime`，只不过你可以指定的小数部分组成的秒数。 默认值为 *n* 是`7`。  
  
|*n*值|精度|小数位数|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 存储日期和时间与根据公历的 19 到 23 个字符。 日期可以包含年、 月和日。 次将包含小时、 分钟、 秒。作为一个选项，可以秒的小数部分显示三个数字。 存储大小为 8 个字节。  
  
 `smalldatetime`  
 将存储的日期和时间。 存储大小为 4 个字节。  
  
 `date`  
 存储用于最多 10 个字符的年、 月和天根据公历日期。 存储大小为 3 个字节。 日期存储为整数。  
  
 `time` [ ( *n* ) ]  
 默认值为 *n* 是`7`。  
  
 `float` [ ( *n* ) ]  
 与浮点数字数据一起使用的近似数字数据类型。 浮点数据是近似，这意味着可以准确表示数据类型范围内的不是所有值。 *n*指定用于存储的尾数的比特数`float`科学记数法。 因此，  *n* 规定的精度和存储大小。 如果 *n* 指定，则它必须是介于`1`和`53`。 默认值 *n* 是`53`。  
  
| *n*值 | 精度 | 存储大小 |  
| --------: | --------: | -----------: |  
| 1-24   | 7 位  | 4 个字节      |  
| 25-53  | 15 位数 | 8 字节      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将 *n* 作为两个可能值之一。 如果`1` <=   *n*   <=  `24`，  *n* 将被视为`24`。 如果`25`  <=   *n*   <=  `53`，  *n* 将被视为`53`。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float`数据类型符合 ISO 标准的所有值 *n* 从`1`通过`53`。 双精度同义词是`float(53)`。  
  
 `real` [ ( *n* ) ]  
 实际的定义是与 float 相同。 `real` 的 ISO 同义词为 `float(24)`。  
  
 `decimal`[(*精度*[ *，缩放*])] |`numeric` [(*精度*[ *，缩放*])]  
 固定精度和小数位数的数字的存储。  
  
 *精度*  
 可能会存储，同时向左和小数点右侧的十进制数字的最大的总数。 此精度必须介于`1`通过最大精度为`38`。 默认精度是`18`。  
  
 *小数位数*  
 小数点右边可以存储的十进制数字的最大位数。 *缩放*必须是一个介于`0`通过*精度*。 你只能指定*缩放*如果*精度*指定。 默认小数位数是`0`; 因此， `0`  <= *缩放* <= *精度*。 最大存储大小基于精度而变化。  
  
| 精度 | 存储字节数  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 表示货币值的数据类型。  
  
| 数据类型 | 存储字节数 |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 使用整数数据的精确数字数据类型。 存储以下表所示。  
  
| 数据类型 | 存储字节数 |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 整数数据类型可以采用的值`1`， `0`，或 NULL。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]优化位列的存储。 如果表中有 8 或更少位列，列存储为 1 个字节。 如果有从 9-16 位列，列存储为 2 个字节，依次类推。  
  
 `nvarchar`[(  *n*   |  `max` )]-`max`仅适用于[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
 可变长度 Unicode 字符数据。 *n*可以是介于 1 和 4000 值。 `max` 指示最大存储大小是 2^31-1 个字节 (2 GB)。 以字节为单位的存储大小是两次输入的字符 + 2 个字节的数目。 所输入数据的长度可以为 0 个字符。  
  
 `nchar` [ ( *n* ) ]  
 固定长度的长度的 Unicode 字符数据 *n* 字符。 *n*必须为从值`1`通过`4000`。 存储大小是两次 *n* 字节。  
  
 `varchar`[(  *n*    |  `max` )]-`max`仅适用于[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。   
 长度可变，非 Unicode 字符数据长度为 *n* 字节。 *n*必须为从值`1`到`8000`。 `max`指示最大存储大小为 2 ^31-1 个字节 (2 GB)。存储大小为输入的数据的实际长度 + 2 个字节。  
  
 `char` [ ( *n* ) ]  
 固定长度的长度的非 Unicode 字符数据 *n* 字节。 *n*必须为从值`1`到`8000`。 存储大小是 *n* 字节。 默认值为 *n* 是`1`。  
  
 `varbinary`[(  *n*    |  `max` )]-`max`仅适用于[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
 可变长度二进制数据。 *n*可从值`1`到`8000`。 `max` 指示最大存储大小是 2^31-1 个字节 (2 GB)。 存储大小是输入数据的实际长度加 2 个字节。 默认值为 *n* 为 7。  
  
 `binary` [ ( *n* ) ]  
 固定长度的二进制数据长度为 *n* 字节。 *n*可从值`1`到`8000`。 存储大小是 *n* 字节。 默认值为 *n* 是`7`。  
  
 `uniqueidentifier`  
 16 字节 GUID。  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Permissions  
 创建一个表需要在权限`db_ddladmin`固定数据库角色或：
 - `CREATE TABLE`针对数据库的权限
 - `ALTER SCHEMA`将包含表的架构的权限。 

创建已分区的表需要在权限`db_ddladmin`固定数据库角色，或

- `ALTER ANY DATASPACE`权限
  
 创建一个本地临时表的登录名接收`CONTROL`， `INSERT`， `SELECT`，和`UPDATE`表的权限。  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>一般备注  
 
最小和最大限制，请参阅[SQL 数据仓库容量限制](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/)。 
 
### <a name="determining-the-number-of-table-partitions"></a>确定表分区的数目
每个用户定义表划分为多个较小的表存储在不同调用分发的位置。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用 60 个分布区。 在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，分布区数目取决于计算节点数。
 
每个发行版本包含所有表分区。 例如，如果有 60 个分布区和四个表分区，将有 320 分区。 如果表是聚集列存储索引，将每个分区，这意味着你将可以 320 列存储索引的一个列存储索引。

我们建议使用更少的表分区以确保每个列存储索引具有足够的行以充分利用列存储索引的优势。 有关更多指导，请参阅[对 SQL 数据仓库中的表进行分区](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/)和[对 SQL 数据仓库中的表创建索引](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>行存储表 （堆或聚集的索引）  
 行存储表是行的行顺序中存储的表。 它是堆或聚集的索引。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]创建含页压缩; 的所有行存储表这不是用户可配置的。   
 
 ### <a name="columnstore-table-columnstore-index"></a>列存储表 （列存储索引）
列存储表中列的列顺序存储的表。 列存储索引是管理存储在列存储表中数据的技术。  聚集列存储索引不会影响数据的分布方式;它会影响每个分布内存储数据的方式。

要将行存储表更改为列存储表，在表上删除所有现有索引，然后创建聚集列存储索引。 有关示例，请参阅[CREATE COLUMNSTORE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).

有关详细信息，请参阅以下文章：
- [列存储索引版本的功能摘要](https://msdn.microsoft.com/library/dn934994/)
- [对 SQL 数据仓库中的表创建索引](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不能定义分布列的默认约束。  
  
 ### <a name="partitions"></a>分区
 在使用分区，分区列不能具有仅限 Unicode 的排序规则。 例如，以下语句将失败。  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 如果*小于 boundary_value*是必须隐式转换为中的数据类型的文本值*partition_column_name*，会出现差异。 通过显示的文本值[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]系统视图，但转换后的值用于[!INCLUDE[tsql](../../includes/tsql-md.md)]操作。 
 
  
 ### <a name="temporary-tables"></a>临时表
 开头的全局临时表 # # 不支持。  
  
 本地临时表具有以下限制和局限：  
  
-   它们是仅对当前会话可见。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将它们放置自动在该会话的末尾。 若要删除这些架构 explicitlt，使用 DROP TABLE 语句。   
-   它们不能重命名。 
-   它们不能有分区或视图。  
-   不能更改它们的权限。 `GRANT``DENY`，和`REVOKE`语句不能用于本地临时表。   
-   数据库控制台命令将被临时表阻塞。   
-   如果一个批次内使用多个本地临时表，则每个必须具有唯一名称。 如果多个会话运行同一个批处理和创建相同的本地临时表，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]内部将数字后缀追加到本地临时表名称，以维护每个本地临时表的唯一名称。  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>锁定行为  
 将在表上的排他锁。 对数据库、 架构和 SCHEMARESOLUTION 对象采用共享的锁。  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>列的示例

### <a name="ColumnCollation"></a> A. 指定的列排序规则 
 在下面的示例中，表`MyTable`创建具有两个不同的列排序规则。 默认情况下，列， `mycolumn1`，具有默认排序规则 Latin1_General_100_CI_AS_KS_WS。 列，`mycolumn2`具有 Frisian_100_CS_AS 的排序规则。  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> B. 指定列的默认约束  
 下面的示例演示用于指定列的默认值的语法。 可乐列具有名为 constraint_colA 和默认值为 0 的默认约束。  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>临时表的示例

### <a name="TemporaryTable"></a> C. 创建一个本地临时表  
 以下命令将创建名为 #myTable 的本地临时表。 具有三个部分组成的名称指定的表。 临时表名称用 # 开头。   
  
```  
CREATE TABLE AdventureWorks.dbo.#myTable   
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>有关表结构的示例

### <a name="ClusteredColumnstoreIndex"></a> D. 创建具有聚集列存储索引的表  
 下面的示例创建分布式的表具有聚集列存储索引。 每个分布将存储为列存储中。  
  
 聚集列存储索引不会影响数据的分布方式;始终按行分布数据。 聚集列存储索引会影响每个分布内存储数据的方式。  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```  
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>表分发的的示例

### <a name="RoundRobin"></a> E. 创建 ROUND_ROBIN 表  
 下面的示例创建 ROUND_ROBIN 表，其中包含三列和但不进行分区。 数据分布在所有分布区。 使用群集列存储索引，这可提供更好的性能和数据压缩比堆集或行存储聚集索引创建表。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. 创建哈希分布式表  
 下面的示例创建与前面的示例相同的表。 但是，对于此表，行分发 (上`id`列) 而不是随机分布 ROUND_ROBIN 表所示。 使用群集列存储索引，这可提供更好的性能和数据压缩比堆集或行存储聚集索引创建表。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="Replicated"></a>G。 创建复制的表  
 下面的示例创建复制的表类似于前面的示例。 复制的表将完全复制到每个计算节点。 与每个计算节点上的此副本，查询减少了数据移动。 此示例将创建具有聚集索引，这将向比堆更好的数据压缩并不能包含足够的行以实现较好的聚集列存储索引压缩。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,   
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>表分区的示例

###  <a name="PartitionedTable"></a>H。 创建已分区的表  
 下面的示例创建同一个表，示例 A，加上 RANGE LEFT 分区上的中所示`id`列。 它指定四个分区边界值，这将导致在五个分区。  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
  (   
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX      
  )  
;  
```  
  
 在此示例中，数据将被归入各个下列分区：  
  
-   分区 1： 列 < = 10   
-   分区 2: 10 < 列 < = 20   
-   分区 3: 20 < 列 < = 30   
-   分区 4: 30 < 列 < = 40   
-   分区 5: 40 < 列  
  
 如果此同一个表已分区而不是 RANGE LEFT （默认） 数据的 RANGE RIGHT 将排序为下列分区：  
  
-   分区 1： 列 < 10  
-   分区 2: 10 < = col < 20   
-   分区 3: 20 < = col < 30    
-   分区 4: 30 < = col < 40   
-   分区 5: 40 < = 列  
  
### <a name="OnePartition"></a>我。 使用一个分区中创建已分区的表  
 下面的示例使用一个分区创建已分区的表。 而不指定任何边界值，这将导致一个分区。  
  
```  
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
    (   
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="DatePartition"></a>J 编写。 创建具有日期分区的表  
 下面的示例创建名为的新表`myTable`，分区上`date`列。 通过使用 RANGE RIGHT 和日期为边界值，它将一个月的数据放在每个分区。  
  
```  
CREATE TABLE myTable (  
    l_orderkey      bigint,       
    l_partkey       bigint,                                             
    l_suppkey       bigint,                                           
    l_linenumber    bigint,        
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH   
  (   
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES   
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>    
## <a name="see-also"></a>另请参阅 
 
 [创建 TABLE AS SELECT &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

