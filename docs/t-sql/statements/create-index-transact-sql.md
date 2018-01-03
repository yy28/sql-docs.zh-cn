---
title: "创建索引 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/21/2017
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
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
caps.latest.revision: "223"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 16335773aba9cc005911434d5090223e7e6f8209
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

对表或视图创建关系索引。 也称为行存储索引，因为它是任一非聚集索引或非聚集 B 树索引。 表中数据之前，你可以创建行存储索引。 使用行存储索引来提高查询性能，尤其是在查询从特定的列中选择，或需要值来以特定顺序排序。  
  
> [!NOTE]  
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目前不支持的唯一约束。 任何引用 Unique 约束的示例是只适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。    

> [!TIP]
> 有关索引设计指南的信息，请参阅[SQL Server 索引设计指南](../../relational-databases/sql-server-index-design-guide.md)。

 **简单示例：**  
  
```  
-- Create a nonclustered index on a table or view  
CREATE INDEX i1 ON t1 (col1);  
```  
  
```  
--Create a clustered index on a table and use a 3-part name for the table  
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);  
```  
  
```  
-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint 
-- on 3 columns and specify the sort order for each column  
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);  
```  
  
 **重要的方案：**  
  
-   从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，使用列存储索引的非聚集索引以提高数据仓库查询性能。 有关详细信息，请参阅[列存储索引的数据仓库](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)。  
  
**需要创建不同类型的索引？**  
  
-   [创建 XML 索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)  
-   [CREATE SPATIAL INDEX (Transact-SQL)](../../t-sql/statements/create-spatial-index-transact-sql.md)  
-   [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)     
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )   
    [ INCLUDE ( column_name [ ,...n ] ) ]  
    [ WHERE <filter_predicate> ]  
    [ WITH ( <relational_index_option> [ ,...n ] ) ]  
    [ ON { partition_scheme_name ( column_name )   
         | filegroup_name   
         | default   
         }  
    ]  
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<relational_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | STATISTICS_INCREMENTAL = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE | ROW | PAGE}   
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
     [ , ...n ] ) ]  
}  
  
<filter_predicate> ::=   
    <conjunct> [ AND <conjunct> ]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...n)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
Backward Compatible Relational Index  
Important   The backward compatible relational index syntax structure 
will be removed in a future version of SQL Server. Avoid using this 
syntax structure in new development work, and plan to modify 
applications that currently use the feature. Use the syntax structure 
specified in <relational_index_option> instead.  
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
  
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}  
```  

  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON [ database_name . [ schema ] . | schema . ] table_name   
        ( { column [ ASC | DESC ] } [ ,...n ] )  
    WITH ( DROP_EXISTING = { ON | OFF } )  
[;]  
```  
  
## <a name="arguments"></a>参数  
UNIQUE  
为表或视图创建唯一索引。 唯一索引不允许两行具有相同的索引键值。 视图的聚集索引必须唯一。  
  
 无论 IGNORE_DUP_KEY 是否设置为 ON，[!INCLUDE[ssDE](../../includes/ssde-md.md)]都不允许为已包含重复值的列创建唯一索引。 否则，[!INCLUDE[ssDE](../../includes/ssde-md.md)]会显示错误消息。 必须先删除重复值，然后才能为一列或多列创建唯一索引。 唯一索引中使用的列应设置为 NOT NULL，因为在创建唯一索引时，会将多个 Null 值视为重复值。  
  
CLUSTERED  
创建索引时，键值的逻辑顺序决定表中对应行的物理顺序。 聚集索引的底层（或称叶级别）包含该表的实际数据行。 一个表或视图只允许同时有一个聚集索引。  
  
 具有唯一聚集索引的视图称为索引视图。 为一个视图创建唯一聚集索引会在物理上具体化该视图。 必须先为视图创建唯一聚集索引，然后才能为该视图定义其他索引。 有关详细信息，请参阅 [创建索引视图](../../relational-databases/views/create-indexed-views.md)。  
  
 在创建任何非聚集索引之前创建聚集索引。 创建聚集索引时会重新生成表中现有的非聚集索引。  
  
 如果没有指定 CLUSTERED，则创建非聚集索引。  
  
> [!NOTE]  
> 聚集的索引和数据页的叶级别都定义相同的因为创建聚集的索引和使用 ON *partition_scheme_name*或亮*filegroup_name*子句有效地将表从在其创建表的文件组移动到新的分区方案或文件组。 对特定的文件组创建表或索引之前，应确认哪些文件组可用并且有足够的空间供索引使用。  
  
 在某些情况下，创建聚集索引可以启用以前禁用的索引。 有关详细信息，请参阅[Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md)和[禁用索引和约束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。  
  
**非聚集**  
创建一个指定表的逻辑排序的索引。 对于非聚集索引，数据行的物理排序独立于索引排序。  
  
 无论是使用 PRIMARY KEY 和 UNIQUE 约束隐式创建索引，还是使用 CREATE INDEX 显式创建索引，每个表都最多可包含 999 个非聚集索引。  
  
 对于索引视图，只能为已定义唯一聚集索引的视图创建非聚集索引。  
  
 如果未另行指定，默认索引类型将为 NONCLUSTERED。  
  
 *index_name*  
 索引的名称。 索引名称在表或视图中必须唯一，但在数据库中不必唯一。 索引名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 column  
 索引所基于的一列或多列。 指定两个或多个列名，可为指定列的组合值创建组合索引。 列出要包含在复合索引，按排序优先级顺序，在后括号内的列*table_or_view_name*。  
  
 可以成为单个组合索引键组合最多 32 列。 组合索引键中的所有列必须在同一个表或视图中。 组合的索引值的最大大小是聚集索引为 900 字节或非聚集索引为 1,700 字节。 限制为 16 个列和之前的版本为 900 字节[!INCLUDE[ssSDS](../../includes/sssds-md.md)]V12 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
 属于大型对象 (LOB) 数据类型的列**ntext**，**文本**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**， **xml**，或**映像**不能指定为索引的键列。 此外，不能包含视图定义**ntext**，**文本**，或**映像**列，即使它们不会以 CREATE INDEX 语句引用。  
  
 如果 CLR 用户定义类型支持二进制排序，则可以为该类型的列创建索引。 另外，对于已定义为用户定义类型列的方法调用的计算列，只要这些方法标记为确定性方法且不执行数据访问操作，便可为该计算列创建索引。 有关 CLR 用户定义类型的列编制索引的详细信息，请参阅[CLR 用户定义的类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
 [ **ASC** |DESC]  
 确定特定索引列的升序或降序排序方向。 默认值为 ASC。  
  
 包括**(***列*[ **，**...*n* ] **)**  
 指定要添加到非聚集索引的叶级别的非键列。 非聚集索引可以唯一，也可以不唯一。  
  
 在 INCLUDE 列表中列名不能重复，且不能同时用于键列和非键列。 如果对表定义了聚集索引，则非聚集索引始终包含聚集索引列。 有关详细信息，请参阅 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
 允许除 **text**、 **ntext**和 **image**之外的所有数据类型。 必须创建或重新脱机生成索引 （ONLINE = OFF） 是否指定非键任何的列一个**varchar （max)**， **nvarchar (max)**，或**varbinary （max)**数据类型。  
  
 精确或不精确的确定性计算列都可以是包含列。 从派生的计算列**映像**， **ntext**，**文本**， **varchar （max)**， **nvarchar (max)**，**varbinary （max)**，和**xml**可以中非键列包含数据类型，只要计算的列数据类型是作为包含性列。 有关详细信息，请参阅 [计算列上的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
 有关创建 XML 索引的信息，请参阅[CREATE XML INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md).  
  
 其中\<filter_predicate > 通过指定要包含在索引将哪些行来创建筛选的索引。 筛选索引必须是对表的非聚集索引。 为筛选索引中的数据行创建筛选统计信息。  
  
 筛选谓词使用简单比较逻辑且不能引用计算列、UDT 列、空间数据类型列或 hierarchyID 数据类型列。 比较运算符不允许使用 NULL 文本的比较。 请改用 IS NULL 和 IS NOT NULL 运算符。  
  
 下面是一些 `Production.BillOfMaterials` 表筛选谓词示例：  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 筛选索引不适用于 XML 索引和全文检索。 对于 UNIQUE 索引，仅选定的行必须具有唯一的索引值。 筛选索引不允许有 IGNORE_DUP_KEY 选项。  
  
ON *partition_scheme_name* **( *column_name* )**  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定分区方案，该方案定义要将分区索引的分区映射到的文件组。 分区方案必须通过执行任何一个数据库中不存在[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)或[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)。 *column_name*指定将对其分区已分区的索引的列。 此列必须与匹配的数据类型，长度，并且分区的自变量的精度函数*partition_scheme_name*正在使用。 *column_name*不限于索引定义中的列。 可以指定基表中的任何列，除时分区唯一索引， *column_name*必须选择从那些作为唯一键。 通过此限制，[!INCLUDE[ssDE](../../includes/ssde-md.md)]可验证单个分区中的键值唯一性。  
  
> [!NOTE]  
> 在对非唯一的聚集索引进行分区时，如果尚未指定分区依据列，则默认情况下[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在聚集索引键列表中添加分区依据列。 在对非唯一的非聚集索引进行分区时，如果尚未指定分区依据列，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]会添加分区依据列作为索引的非键（包含）列。  
  
 如果*partition_scheme_name*或*文件组*未指定和表分区、 检索均被放置在相同的分区方案中，使用相同的分区依据列，与基础表。  
  
> [!NOTE]  
> 您不能对 XML 索引指定分区方案。 如果基表已分区，则 XML 索引与该表使用相同的分区方案。  
  
 有关分区索引， [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 ON *filegroup_name*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 为指定文件组创建指定索引。 如果未指定位置且表或视图尚未分区，则索引将与基础表或视图使用相同的文件组。 该文件组必须已存在。  
  
 ON **"**默认**"**  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssCurrent](../../includes/sssdsfull-md.md)]。  
  
 为默认文件组创建指定索引。  
  
 在此上下文中，“default”一词不是关键字。 它是默认文件组的标识符和必须分隔，如下所示 ON **"**默认**"**或亮**[**默认**]**。 如果指定了 "default"，则当前会话的 QUOTED_IDENTIFIER 选项必须为 ON。 这是默认设置。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* |"NULL"}]  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 在创建聚集索引时，指定表的 FILESTREAM 数据的位置。 FILESTREAM_ON 子句用于将 FILESTREAM 数据移动到不同的 FILESTREAM 文件组或分区方案。  
  
 *filestream_filegroup_name*是 FILESTREAM 文件组的名称。 文件组必须有通过使用文件组定义的一个文件[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)或[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)语句; 否则，将引发错误。  
  
 如果表已分区，则必须包含 FILESTREAM_ON 子句并且必须指定 FILESTREAM 文件组的分区方案，且此分区方案需使用与该表分区方案相同的分区函数和分区列。 否则将引发错误。  
  
 如果该表未分区，则无法对 FILESTREAM 列分区。 该表的 FILESTREAM 数据必须存储在一个由 FILESTREAM_ON 子句指定的文件组中。  
  
 如果创建的是聚集索引且该表不包含 FILESTREAM 列，则可在 CREATE INDEX 语句中指定 FILESTREAM_ON NULL。  
  
 有关详细信息，请参阅 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)。  
  
 **\<对象 >:: =**  
  
 要为其建立索引的完全限定对象或非完全限定对象。  
  
 *database_name*  
 数据库的名称。  
  
 *schema_name*  
 表或视图所属架构的名称。  
  
 *table_or_view_name*  
 要为其建立索引的表或视图的名称。  
  
 必须使用 SCHEMABINDING 定义视图，才能为视图创建索引。 必须先为视图创建唯一的聚集索引，才能为该视图创建非聚集索引。 有关索引视图的详细信息，请参阅“备注”部分。  
  
 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，该对象可以为存储具有聚集列存储索引的表。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]支持三个部分组成的名称格式*database_name***。**[*schema_name*]**。***object_name*时*database_name*是当前数据库或*database_name*是 tempdb 和*object_name*# 开头。  
  
 **\<relational_index_option >:: =**  
  
 指定创建索引时要使用的选项。  
  
 PAD_INDEX = {ON |**OFF** }  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定索引填充。 默认为 OFF。  
  
 ON  
 通过指定的可用空间的百分比*fillfactor*应用于索引中间级别页。  
  
 关闭或*fillfactor*未指定  
 考虑到中间级页上的键集，将中间级页填充到接近其容量的程度，以留出足够的空间，使之至少能够容纳索引的最大的一行。  
  
 PAD_INDEX 选项只有在指定了 FILLFACTOR 时才有用，因为 PAD_INDEX 使用由 FILLFACTOR 指定的百分比。 如果为 FILLFACTOR 指定的百分比不够大，无法容纳一行，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在内部覆盖该百分比以允许最小值。 将中间级索引页上的行数为永远不会小于 2，而不考虑如何低值*fillfactor*。  
  
 在向后兼容的语法中，WITH PAD_INDEX 等效于 WITH PAD_INDEX = ON。  
  
 填充因子 **=** *填充因子*  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或重新生成索引的过程中，应将每个索引页面的叶级填充到什么程度。 *填充因子*必须是介于 1 到 100 的整数值。 如果*fillfactor*为 100，[!INCLUDE[ssDE](../../includes/ssde-md.md)]与完全填充叶级页创建索引。  
  
 FILLFACTOR 设置仅在创建或重新生成索引时应用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]并不会在页中动态保持指定的可用空间百分比。 若要查看的填充因子设置，请使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目录视图。  
  
> [!IMPORTANT]  
> 使用低于 100 的 FILLFACTOR 值创建聚集索引会影响数据占用的存储空间量，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]在创建聚集索引时会重新分布数据。  
  
 有关详细信息，请参阅 [为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。  
  
 SORT_IN_TEMPDB = {ON |**OFF** }  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否存储在临时排序结果**tempdb**。 默认为 OFF。  
  
 ON  
 用于生成索引的中间排序结果存储在**tempdb**。 这可能会降低仅当创建索引所需的时间**tempdb**位于不同的与用户数据库的磁盘集。 但是，这会增加索引生成期间所使用的磁盘空间量。  
  
 OFF  
 中间排序结果与索引存储在同一数据库中。  
  
 除了创建索引，在用户数据库中所需的空间**tempdb**必须具有相同数量的额外空间来存储的中间排序结果有关。 有关详细信息，请参阅[SORT_IN_TEMPDB 选项为索引](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)。  
  
 在向后兼容的语法中，WITH SORT_IN_TEMPDB 等效于 WITH SORT_IN_TEMPDB = ON。  
  
 IGNORE_DUP_KEY = {ON |**OFF** }  
 指定在插入操作尝试向唯一索引插入重复键值时的错误响应。 IGNORE_DUP_KEY 选项仅适用于创建或重新生成索引后发生的插入操作。 选项不起作用时执行[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)， [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)，或[更新](../../t-sql/queries/update-transact-sql.md)。 默认为 OFF。  
  
 ON  
 向唯一索引插入重复键值时将出现警告消息。 只有违反唯一性约束的行才会失败。  
  
 OFF  
 向唯一索引插入重复键值时将出现错误消息。 整个 INSERT 操作将被回滚。  
  
 对于对视图创建的索引、非唯一索引、XML 索引、空间索引以及筛选的索引，IGNORE_DUP_KEY 不能设置为 ON。  
  
 若要查看 IGNORE_DUP_KEY，使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在向后兼容的语法中，WITH IGNORE_DUP_KEY 等效于 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE = {ON |**OFF**}  
 指定是否重新计算分布统计信息。 默认为 OFF。  
  
 ON  
 不会自动重新计算过时的统计信息。  
  
 OFF  
 启用统计信息自动更新功能。  
  
 若要恢复统计信息自动更新，请将 STATISTICS_NORECOMPUTE 设置为 OFF，或执行 UPDATE STATISTICS 但不包含 NORECOMPUTE 子句。  
  
> [!IMPORTANT]  
> 如果禁用分布统计的自动重新计算，可能会妨碍查询优化器为涉及该表的查询选取最佳执行计划。  
  
 在向后兼容的语法中，WITH STATISTICS_NORECOMPUTE 等效于 WITH STATISTICS_NORECOMPUTE = ON。  
  
STATISTICS_INCREMENTAL = {ON |**OFF** }  
当**ON**，创建的统计信息是每个分区统计信息。 当**OFF**，删除统计信息树和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新计算统计信息。 默认值是**OFF**。  
  
 如果不支持每个分区统计信息，将忽略该选项并生成警告。 对于以下统计信息类型，不支持增量统计信息：  
  
-   使用未与基表的分区对齐的索引创建的统计信息。  
-   对 Always On 可读辅助数据库创建的统计信息。  
-   对只读数据库创建的统计信息。  
-   对筛选的索引创建的统计信息。  
-   对视图创建的统计信息。  
-   对内部表创建的统计信息。  
-   使用空间索引或 XML 索引创建的统计信息。  
  
DROP_EXISTING = {ON |**OFF** }  
是一个选项以删除和重新生成现有的群集或非聚集索引使用已修改的列规范，并保持索引相同的名称。 默认为 OFF。  
  
 ON  
 指定要除去并重新生成现有索引，其必须具有相同名称作为参数*index_name*。  
  
 OFF  
 指定不删除和重新生成现有的索引。 如果指定的索引名称已经存在，SQL Server 将显示一个错误。  
  
使用 DROP_EXISTING，您可以更改：  
  
-   聚集行存储索引的非聚集行存储索引。  
  
使用 DROP_EXISTING，则无法更改。  
  
-   非聚集行存储索引的聚集行存储索引。  
-   任何类型的行存储索引的聚集列存储索引。  
  
在向后兼容的语法中，WITH DROP_EXISTING 等效于 WITH DROP_EXISTING = ON。  
  
ONLINE = {ON |**OFF** }  
指定在索引操作期间基础表和关联的索引是否可用于查询和数据修改操作。 默认为 OFF。  
  
> [!NOTE]  
> 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供联机索引操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ON  
 在索引操作期间不持有长期表锁。 在索引操作的主要阶段，源表上只使用意向共享 (IS) 锁。 这使得能够继续对基础表和索引进行查询或更新。 操作开始时，在很短的时间内对源对象持有共享 (S) 锁。 操作结束时，如果创建非聚集索引，将在短期内获取对源的 S（共享）锁；当联机创建或删除聚集索引时，以及重新生成聚集或非聚集索引时，将在短期内获取 SCH-M（架构修改）锁。 对本地临时表创建索引时，ONLINE 不能设置为 ON。  
  
 OFF  
 在索引操作期间应用表锁。 创建、重新生成或删除聚集索引或者重新生成或删除非聚集索引的脱机索引操作将对表获取架构修改 (Sch-M) 锁。 这样可以防止所有用户在操作期间访问基础表。 创建非聚集索引的脱机索引操作将对表获取共享 (S) 锁。 这样可以防止更新基础表，但允许读操作（如 SELECT 语句）。  
  
 有关详细信息，请参阅[联机索引操作的工作原理](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
 可以联机创建包括全局临时表上的索引在内的索引，但下列索引例外：  
  
-   XML 索引  
-   对局部临时表的索引。  
-   视图唯一的初始聚集索引。  
-   已禁用的聚集索引。  
-   如果基础表包含 LOB 数据类型的聚集的索引：**映像**， **ntext**，**文本**，和空间类型。  
-   **varchar （max)**和**varbinary （max)**列不能为索引的一部分。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ) 并在[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]，当表包含**varchar （max)**或**varbinary （max)**列，包含其他列的聚集索引可以是生成或重新生成使用**联机**选项。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]不允许**联机**选项时基表包含**varchar （max)**或**varbinary （max)**列。  
  
有关详细信息，请参阅 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
ALLOW_ROW_LOCKS = { **ON** |关闭}  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否允许行锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用行锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用行锁。  
  
 OFF  
 不使用行锁。  
  
ALLOW_PAGE_LOCKS = { **ON** |关闭}  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定是否允许使用页锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用页锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用页锁。  
  
 OFF  
 不使用页锁。  
  
MAXDOP = *max_degree_of_parallelism*  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 重写**最大并行度**索引操作的持续时间的配置选项。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 @shouldalert  
 取消生成并行计划。  
  
 \>1  
 基于当前系统工作负荷，将并行索引操作中使用的最大处理器数限制为指定数量或更少。  
  
 0（默认值）  
 根据当前系统工作负荷使用实际的处理器数量或更少数量的处理器。  
  
 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
> 并行索引操作不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2016 的版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 DATA_COMPRESSION  
 为指定的索引、分区号或分区范围指定数据压缩选项。 这些选项如下：  
  
 无  
 不压缩索引或指定的分区。  
  
 ROW  
 使用行压缩来压缩索引或指定的分区。  
  
 PAGE  
 使用页压缩来压缩索引或指定的分区。  
  
 有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
在分区上**(** { \<partition_number_expression > |\<范围 >}[ **,**...*n* ] **)**      
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定对其应用 DATA_COMPRESSION 设置的分区。 如果索引未分区，则 ON PARTITIONS 参数将产生错误。 如果不提供 ON PARTITIONS 子句，则 DATA_COMPRESSION 选项将应用于分区索引的所有分区。  
  
 \<partition_number_expression > 可以通过以下方式指定：  
  
-   提供一个分区号，例如：ON PARTITIONS (2)。  
-   提供若干单独分区的分区号并用逗号将它们隔开，例如：ON PARTITIONS (1, 5)。  
-   同时提供范围和单个分区，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
 \<范围 > 可以指定为分区号分隔逐字，例如： ON PARTITIONS (6 TO 8)。  
  
 若要为不同分区设置不同的数据压缩类型，请多次指定 DATA_COMPRESSION 选项，例如：  
 
```  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
## <a name="remarks"></a>Remarks  
 CREATE INDEX 语句同其他查询一样优化。 为了节省 I/O 操作，查询处理器可以选择扫描另一个索引，而不是执行表扫描。 在某些情况下，可不必执行排序操作。 在多处理器计算机上，CREATE INDEX 可按照与其他查询相同的方式，使用多个处理器执行与创建索引相关的扫描和排序操作。 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
 如果数据库恢复模型被设置为大容量日志模型或简单模型，则可以记录最少的创建索引操作。  
  
 可以为临时表创建索引。 在删除表或结束会话时，将删除索引。  
  
 索引支持扩展属性。  
  
## <a name="clustered-indexes"></a>聚集索引  
 对表（堆）创建聚集索引或删除和重新创建现有聚集索引时，要求数据库具有额外的可用工作区来容纳数据排序结果和原始表或现有聚集索引数据的临时副本。 有关聚集索引的详细信息，请参阅[创建聚集索引](../../relational-databases/indexes/create-clustered-indexes.md)。  
  
## <a name="nonclustered-indexes"></a>非聚集索引  
 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]并在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，你可以存储为聚集列存储索引的表创建非聚集索引。 如果你第一次上存储的表中创建非聚集索引作为堆或聚集的索引，如果你更高版本转换为聚集列存储索引的表保留索引。 它也并不删除非聚集索引，重新生成聚集列存储索引时所需。  
  
 限制和局限：  
  
-   存储为聚集列存储索引的表创建非聚集索引时，FILESTREAM_ON 选项无效。  
  
## <a name="unique-indexes"></a>唯一索引  
 如果存在唯一索引，[!INCLUDE[ssDE](../../includes/ssde-md.md)]会在每次插入操作添加数据时检查重复值。 可生成重复键值的插入操作将被回滚，同时[!INCLUDE[ssDE](../../includes/ssde-md.md)]显示错误消息。 即使插入操作更改多行但只导致出现一个重复值时，也是如此。 如果在存在唯一索引并且 IGNORE_DUP_KEY 子句设置为 ON 的情况下输入数据，则只有违反 UNIQUE 索引的行才会失败。  
  
## <a name="partitioned-indexes"></a>分区索引  
 创建和维护分区索引的方式与已分区表相同，但与普通索引一样，将分区索引作为单独数据库对象来进行处理。 可以在未分区的表中使用分区索引，也可以在已分区表中使用未分区索引。  
  
 如果要对已分区表创建索引，并且不指定用于放置该索引的文件组，则会按照与基础表相同的方式为该索引分区。 这是因为在默认情况下，索引与其基础表放在同一文件组中，并且对应使用相同分区依据列的相同分区方案中的已分区表。 当索引的表使用的同一个分区方案和分区依据列时，索引是*对齐*与表。  
  
> [!WARNING]  
> 对超过 1,000 个分区的表创建和重新生成非对齐索引是可能的，但不支持。 这样做可能会导致性能下降，或在执行这些操作的过程中占用过多内存。 我们建议当分区数超过 1000 时，仅使用对齐索引。  
  
 在对非唯一的聚集索引分区时，如果尚未指定分区依据列，则默认情况下[!INCLUDE[ssDE](../../includes/ssde-md.md)]将在聚集索引键列表中添加任意分区依据列。  
  
 可以使用与为表创建索引时相同的方式，为已分区表创建索引视图。 有关已分区索引的详细信息，请参阅 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，当创建或重新生成已分区索引时，将通过扫描表中的所有行来创建统计信息。 相反，查询优化器使用默认采样算法来生成统计信息。 若要通过扫描表中所有行的方法获得有关已分区索引的统计信息，请使用 CREATE STATISTICS 或 UPDATE STATISTICS 以及 FULLSCAN 子句。  
  
## <a name="filtered-indexes"></a>筛选索引  
 筛选索引是一种经过优化的非聚集索引，适用于从表中选择少数行的查询。 筛选索引使用筛选谓词对表中的部分数据进行索引。 设计良好的筛选索引可以提高查询性能，降低存储成本和维护成本。  
  
### <a name="required-set-options-for-filtered-indexes"></a>筛选索引所需的 SET 选项  
 如果下列任何条件成立，则需要“必需的值”列中的 SET 选项：  
  
-   创建筛选索引。  
-   INSERT、UPDATE、DELETE 或 MERGE 操作修改筛选索引中的数据。  
-   查询优化器使用筛选的索引来生成查询计划。  
  
    |SET 选项|必需的值|默认服务器值|，则“默认”<br /><br /> OLE DB 和 ODBC 值|，则“默认”<br /><br /> DB-Library 值|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *当数据库兼容性级别设置为 90 或更高时，如果将 ANSI_WARNINGS 设置为 ON，则将使 ARITHABORT 隐式设置为 ON。 如果数据库兼容性级别设置为 80 或更低，则必须将 ARITHABORT 选项显式设置为 ON。  
  
 如果 SET 选项不正确，则可能会出现以下情况：  
  
-   不会创建筛选索引。  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]生成错误并回滚对索引中的数据进行更改的 INSERT、UPDATE、DELETE 或 MERGE 语句。  
-   查询优化器不考虑任何 Transact-SQL 语句的执行计划中的索引。  
  
 有关筛选索引的详细信息，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
## <a name="spatial-indexes"></a>空间索引  
 关于空间索引的信息，请参阅[CREATE SPATIAL INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)和[空间索引概述](../../relational-databases/spatial/spatial-indexes-overview.md)。  
  
## <a name="xml-indexes"></a>XML 索引  
 有关信息有关 XML 索引，请参阅[CREATE XML INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)和[XML 索引 &#40;SQL server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="index-key-size"></a>索引键大小  
 索引键的最大大小是聚集索引为 900 字节和非聚集索引为 1700 字节。 (之前[!INCLUDE[ssSDS](../../includes/sssds-md.md)]V12 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]限制始终为 900 个字节。)上的索引**varchar**可以创建超过字节的限制的列，如果列中的现有数据不能超过限制时创建的索引; 但是，后续插入或更新操作导致的列总大小大于此限制将会失败。 聚集索引的索引键不能包含在 ROW_OVERFLOW_DATA 分配单元中具有现有数据的 **varcharr** 列。 如果对 **varchar** 列创建了聚集索引，并且 IN_ROW_DATA 分配单元中存在现有数据，则对该列执行的将数据推送到行外的后续插入或更新操作将会失败。  
  
 非聚集索引可以在索引的叶级别包含非键列。 不考虑这些列[!INCLUDE[ssDE](../../includes/ssde-md.md)]时计算索引键大小。 有关详细信息，请参阅 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
> [!NOTE]  
> 在对表进行分区时，如果分区键列尚未出现在非唯一聚集索引中时，它们将由[!INCLUDE[ssDE](../../includes/ssde-md.md)]添加到索引中。 索引列的合并后的大小（不将包含列计算在内）加上任何添加的分区列在非唯一聚集索引中不能超过 1800 字节。  
  
## <a name="computed-columns"></a>计算列  
 可以对计算列创建索引。 此外，计算列可以具有 PERSISTED 属性。 这意味着 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在表中存储计算值，并且在计算列所依赖的任何其他列发生更新时更新这些值。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 对列创建了索引并且该索引由某查询引用，则会使用这些持久值。  
  
 若要对计算列建立索引则该计算列必须具有确定性并精确。 但是，使用 PERSISTED 属性会将可建立索引的计算列类型扩展为包含以下类型：  
  
-   基于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 函数以及由用户标记为确定性的 CLR 用户定义类型方法的计算列。  
-   基于[!INCLUDE[ssDE](../../includes/ssde-md.md)]定义为确定性但不精确的表达式的计算列。  
  
 持久化计算列需要将以下 SET 选项设置为在上一部分“索引视图所需的 SET 选项”中显示的内容。  
  
 UNIQUE 或 PRIMARY KEY 约束只要满足所有索引条件，就可以包含计算列。 具体来说，计算列必须具有确定性并精确，或者具有确定性并持久化。 有关确定性的详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
 从派生的计算列**映像**， **ntext**，**文本**， **varchar （max)**， **nvarchar (max)**，**varbinary （max)**，和**xml**数据类型可以创建索引作为键或包含非键列，只要计算的列数据类型是允许作为索引键列或非键列。 例如，无法对计算创建主 XML 索引**xml**列。 如果索引键大小超过 900 字节，会显示一条警告消息。  
  
 对计算列创建索引可能导致之前正常运行的插入或更新操作失败。 当计算列导致算术错误时可能产生这样的失败。 例如，虽然下表中的计算列 `c` 将导致算术错误，但是 `INSERT` 语句仍有效。  
  
```sql  
CREATE TABLE t1 (a int, b int, c AS a/b);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 相反，如果创建表之后对计算列 `c` 创建索引，则上述 `INSERT` 语句将失败。  
  
```sql  
CREATE TABLE t1 (a int, b int, c AS a/b);  
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 有关详细信息，请参阅 [计算列上的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
## <a name="included-columns-in-indexes"></a>索引中的包含列  
 可以将非键列（称为包含列）添加到非聚集索引的叶级别，从而通过涵盖查询来提高查询性能。 也就是说，查询中引用的所有列都作为键列或非键列包含在索引中。 这样，查询优化器可以通过索引扫描找到所需的全部信息，而无需访问表或聚集索引数据。 有关详细信息，请参阅 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
## <a name="specifying-index-options"></a>指定索引选项  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引入了新的索引选项，还修改了指定选项的方式。 在向后兼容语法中，WITH *option_name*等效于 WITH **(** \<option_name > **= ON)**。 在设置索引选项时，下列规则适用： 
  
-   新的索引选项只能指定通过使用 WITH (***option_name* = ON |关闭**)。  
-   指定选项时不能在同一语句中同时使用向后兼容语法和新语法。 例如，指定 WITH (**DROP_EXISTING、 ONLINE = ON**) 会导致语句失败。  
-   在创建 XML 索引时，必须通过使用 WITH 指定的选项 (***option_name*= ON |关闭**)。  
  
## <a name="dropexisting-clause"></a>DROP_EXISTING 子句  
 可使用 DROP_EXISTING 子句重新生成索引、添加或删除列、修改选项、修改列排序顺序或更改分区方案或文件组。  
  
 如果索引强制 PRIMARY KEY 或 UNIQUE 约束，且索引定义没有任何改变，则会删除并重新创建该索引并保留现有约束。 不过，如果索引定义已改变，则该语句将失败。 若要更改 PRIMARY KEY 或 UNIQUE 约束的定义，请删除该约束并添加具有新定义的约束。  
  
 为已经具有非聚集索引的表重建聚集索引时（使用相同或不同的键集），DROP_EXISTING 可以提高性能。 DROP_EXISTING 代替先对旧的聚集索引执行 DROP INDEX 语句，然后再对新的聚集索引执行 CREATE INDEX 语句的过程。 而是将重新生成一次非聚集索引，之后仅在索引定义已更改时再重新生成。 如果索引定义与原始索引具有相同的索引名称、键列和分区列、唯一性属性以及排序顺序，则 DROP_EXISTING 子句不会重新生成非聚集索引。  
  
 无论是否重新生成非聚集索引，它们都将始终保留在其原始文件组或分区方案中，并使用原始的分区函数。 如果聚集索引被重新生成到其他文件组或分区方案中，这些非聚集索引不会通过移动来与聚集索引的新位置保持一致。 所以，即使非聚集索引以前与聚集索引对齐，现在可能也不再与其对齐。 有关对齐已分区索引的详细信息，请参阅有关内容。  
  
 如果以相同顺序使用相同索引键列，且具有相同升序和降序，则 DROP_EXISTING 子句不会重新对数据排序，除非索引语句指定非聚集索引且 ONLINE 选项设置为 OFF。 如果聚集索引被禁用，则必须在 ONLINE 设置为 OFF 的情况下执行 CREATE INDEX WITH DROP_EXISTING 操作。 如果非聚集索引被禁用且不与禁用的聚集索引关联，则可以在 ONLINE 设置为 OFF 或 ON 时执行 CREATE INDEX WITH DROP_EXISTING 操作。  
  
 删除或重新生成具有 128 个或更多区数的索引时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]会将实际页释放及其关联的锁推迟到事务提交后。  
  
## <a name="online-option"></a>ONLINE 选项  
 下列指南适用于联机执行索引操作：  
  
-   不能在执行联机索引操作的过程中更改、截断或删除基础表。  
-   索引操作期间需要额外的临时磁盘空间。  
-   可以对分区索引以及包含持久性计算列或包含列的索引执行联机操作。  
  
 有关详细信息，请参阅 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
## <a name="row-and-page-locks-options"></a>行锁和页锁选项  
 如果 ALLOW_ROW_LOCKS = ON 且 ALLOW_PAGE_LOCK = ON，则访问索引时允许行级、页级和表级锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]将选择相应的锁，并且可以将锁从行锁或页锁升级到表锁。  
  
 如果 ALLOW_ROW_LOCKS = OFF 且 ALLOW_PAGE_LOCK = OFF，则访问索引时仅允许使用表级锁。  
  
## <a name="viewing-index-information"></a>查看索引信息  
 若要返回有关索引的信息，可以使用目录视图、系统函数和系统存储过程。  
  
## <a name="data-compression"></a>Data Compression  
 主题中介绍数据压缩[数据压缩](../../relational-databases/data-compression/data-compression.md)。 以下是要考虑的关键点：  
  
-   通过压缩可将更多的行存储在页上，但不能更改最大行大小。  
-   对索引的非叶页不会进行页压缩，但可进行行压缩。  
-   每个非聚集索引都有单独的压缩设置，并且不会继承基础表的压缩设置。  
-   对堆创建聚集索引时，聚集索引会继承该堆的压缩状态，除非指定了另一压缩状态。  
  
 以下限制适用于已分区索引：  
  
-   如果表具有非对齐索引，则无法更改单个分区的压缩设置。  
-   ALTER INDEX\<索引 >...REBUILD PARTITION ... 语法可重新生成索引的指定分区。  
-   ALTER INDEX\<索引 >...REBUILD WITH ... 语法可重新生成索引的所有分区。  
  
 若要评估更改压缩状态将对表、索引或分区有何影响，请使用 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 存储过程。  
  
## <a name="permissions"></a>权限  
 要求对表或视图具有 ALTER 权限。 用户必须是 **sysadmin** 固定服务器角色的成员，或者是 **db_ddladmin** 和 **db_owner** 固定数据库角色的成员。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，无法创建：  
  
-   数据仓库表已存在列存储索引时聚集或非聚集行存储索引。 此行为是不同于 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]这样行存储和列存储索引，以便在同一个表上共存。  
-   无法对视图创建索引。  
  
## <a name="metadata"></a>元数据  
 若要查看现有索引的信息，请可以查询[sys.indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目录视图。  
  
## <a name="version-notes"></a>版本说明  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]不支持文件组和 filestream 选项。  
  
## <a name="examples-all-versions-uses-the-adventureworks-database"></a>示例： 所有版本。 使用 AdventureWorks 数据库。  
  
### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. 创建简单的非聚集行存储索引  
 下面的示例在创建非聚集索引`VendorID`列`Purchasing.ProductVendor`表。  
  
```sql  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. 创建一个简单的非聚集行存储复合索引  
 下面的示例创建非聚集复合索引`SalesQuota`和`SalesYTD`列`Sales.SalesPerson`表。  
  
```sql  
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  
```  
  
### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. 在另一个数据库中表上创建索引  
 下面的示例创建非聚集索引`VendorID`列`ProductVendor`表中`Purchasing`数据库。  
  
```sql  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);   
```  
  
### <a name="d-add-a-column-to-an-index"></a>D. 将列添加到索引  
 下面的示例使用两个列从 dbo 创建索引 IX_FF。FactFinance 表。  下一个语句重新生成与一个多个列的索引，并使现有的名称。  
  
```sql  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey ASC, DateKey ASC );  
  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)  
WITH ( DROP_EXISTING = ON );  
 ```  
  
## <a name="examples-sql-server-azure-sql-database"></a>示例： SQL Server，Azure SQL 数据库  
  
### <a name="e-create-a-unique-nonclustered-index"></a>E. 创建唯一非聚集索引  
 以下示例为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `Name` 表的 `Production.UnitMeasure` 列创建唯一非聚集索引。 该索引将强制插入 `Name` 列中的数据具有唯一性。  
  
```sql  
CREATE UNIQUE INDEX AK_UnitMeasure_Name   
    ON Production.UnitMeasure(Name);  
```  
  
 以下查询通过尝试插入与现有行包含相同值的一行来测试唯一性约束。  
  
```sql  
--Verify the existing value.  
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';  
GO  
INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)  
    VALUES ('OC', 'Ounces', GetDate());  
```  
  
 生成如下错误消息：  
  
```  
Server: Msg 2601, Level 14, State 1, Line 1  
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.  
```  
  
### <a name="f-use-the-ignoredupkey-option"></a>F. 使用 IGNORE_DUP_KEY 选项  
 以下示例首先在该选项设置为 `IGNORE_DUP_KEY` 时在临时表中插入多行，然后在该选项设置为 `ON` 时执行相同操作，以演示 `OFF` 选项的影响。 单个行被插入 `#Test` 表，在执行第二个多行 `INSERT` 语句时将导致出现重复值。 表中的行计数会返回插入的行数。  
  
```sql  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = ON);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 下面是第二个 `INSERT` 语句的结果。  
  
```  
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.  
  
Number of rows   
--------------   
38  
```  
  
 请注意，从 `Production.UnitMeasure` 表中插入的、不违反唯一性约束的行将成功插入。 会发出警告并忽略重复行，但不会回滚整个事务。  
  
 将再次执行相同语句，但将 `IGNORE_DUP_KEY` 设置为 `OFF`。  
  
```sql  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = OFF);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 下面是第二个 `INSERT` 语句的结果。  
  
```  
Server: Msg 2601, Level 14, State 1, Line 5  
Cannot insert duplicate key row in object '#Test' with unique index  
'AK_Index'. The statement has been terminated.  
  
Number of rows   
--------------   
1  
```  
  
 请注意，即使 `Production.UnitMeasure` 表中只有一行违反 `UNIQUE` 索引约束，也不会将其中任何一行插入该表。  
  
### <a name="g-using-dropexisting-to-drop-and-re-create-an-index"></a>G. 使用 DROP_EXISTING 删除和重新创建索引  
 以下示例使用 `ProductID` 选项在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Production.WorkOrder` 表的 `DROP_EXISTING` 列上删除并重新创建现有索引。 还设置了 `FILLFACTOR` 和 `PAD_INDEX` 选项。  
  
```sql  
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID  
    ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80,  
        PAD_INDEX = ON,  
        DROP_EXISTING = ON);  
GO  
```  
  
### <a name="h-create-an-index-on-a-view"></a>H. 对视图创建索引  
 以下示例将创建一个视图并为该视图创建索引。 包含两个使用该索引视图的查询。  
  
```sql  
--Set the options to support indexed views.  
SET NUMERIC_ROUNDABORT OFF;  
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
    QUOTED_IDENTIFIER, ANSI_NULLS ON;  
GO  
--Create view with schemabinding.  
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
DROP VIEW Sales.vOrders ;  
GO  
CREATE VIEW Sales.vOrders  
WITH SCHEMABINDING  
AS  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
        OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
    FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
    WHERE od.SalesOrderID = o.SalesOrderID  
    GROUP BY OrderDate, ProductID;  
GO  
--Create an index on the view.  
CREATE UNIQUE CLUSTERED INDEX IDX_V1   
    ON Sales.vOrders (OrderDate, ProductID);  
GO  
--This query can use the indexed view even though the view is   
--not specified in the FROM clause.  
SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
    OrderDate, ProductID  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND ProductID BETWEEN 700 and 800  
        AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
GROUP BY OrderDate, ProductID  
ORDER BY Rev DESC;  
GO  
--This query can use the above indexed view.  
SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND DATEPART(mm,OrderDate)= 3  
        AND DATEPART(yy,OrderDate) = 2002  
GROUP BY OrderDate  
ORDER BY OrderDate ASC;  
GO  
```  
  
### <a name="i-create-an-index-with-included-non-key-columns"></a>I. 创建带有包含性 （非键） 列的索引  
 以下示例创建具有一个键列 (`PostalCode`) 和四个非键列（`AddressLine1`、`AddressLine2`、`City`、`StateProvinceID`）的非聚集索引。 然后执行该索引覆盖的查询。 若要显示的索引上的所选查询优化器，**查询**菜单中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，选择**显示实际的执行计划**之前执行查询。  
  
```sql  
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
GO  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
GO  
```  
  
### <a name="j-create-a-partitioned-index"></a>J. 创建已分区的索引  
 以下示例为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中现有分区方案 `TransactionsPS1` 创建非聚集分区索引。 此示例假定安装了分区索引示例。  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
```sql  
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
GO  
```  
  
### <a name="k-creating-a-filtered-index"></a>K. 创建筛选索引  
 下面的示例将对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 Production.BillOfMaterials 表创建筛选索引。 筛选谓词可包含那些不是筛选索引中的键列的列。 本示例中的谓词将仅选择其中的 EndDate 为非 NULL 的行。  
  
```sql  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
### <a name="l-create-a-compressed-index"></a>L. 创建压缩的索引  
 下面的示例将使用行压缩对无分区表创建索引。  
  
```sql  
CREATE NONCLUSTERED INDEX IX_INDEX_1   
    ON T1 (C2)  
WITH ( DATA_COMPRESSION = ROW ) ;   
GO  
```  
  
 下面的示例将通过对索引的所有分区使用行压缩来创建对已分区表的索引。  
  
```sql  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH ( DATA_COMPRESSION = ROW ) ;  
GO  
```  
  
 下面的示例将通过对索引的分区 `1` 使用页压缩并对索引的分区 `2` 至 `4` 使用行压缩来创建对已分区表的索引。  
  
```sql  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),  
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="m-basic-syntax"></a>M. 基本语法  
  
```sql  
CREATE INDEX IX_VendorID   
    ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID   
    ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID   
    ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="n-create-a-non-clustered-index-on-a-table-in-the-current-database"></a>N. 在当前数据库中表上创建非聚集索引  
 下面的示例创建非聚集索引`VendorID`列`ProductVendor`表。  
  
```sql  
CREATE INDEX IX_ProductVendor_VendorID   
    ON ProductVendor (VendorID);   
```  
  
### <a name="o-create-a-clustered-index-on-a-table-in-another-database"></a>O. 另一个数据库中的表创建聚集的索引  
 下面的示例创建非聚集索引`VendorID`列`ProductVendor`表中`Purchasing`数据库。  
  
```sql  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID   
    ON Purchasing..ProductVendor (VendorID);   
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 索引设计指南](../../relational-databases/sql-server-index-design-guide.md)   
 [索引和 ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md#indexes-and-alter-table)     
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION (Transact-SQL)](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [创建空间索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [创建 XML 索引 &#40;Transact SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
 

