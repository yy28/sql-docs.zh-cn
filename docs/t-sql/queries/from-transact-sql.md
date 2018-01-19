---
title: "从 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: "97"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9ddc3ee291d4e3b498dd6dfd9bbb49ca4299bea6
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 DELETE、SELECT 和 UPDATE 语句中使用的表、视图、派生表和联接表。 在 SELECT 语句中，FROM 子句是必需的，除非选择列表只包含常量、变量和算术表达式（没有列名）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>参数  
\<table_source>  
 指定要在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用的表、视图、表变量或派生表源（有无别名均可）。 虽然语句中可用的表源个数的限值根据可用内存和查询中其他表达式的复杂性而有所不同，但一个语句中最多可使用 256 个表源。 单个查询可能不支持最多有 256 个表源。  
  
> [!NOTE]  
>  如果查询中引用了许多表，查询性能会受到影响。 编译和优化时间也受到其他因素的影响。 其中包括索引和索引的视图在每台上是否存在\<table_source > 和大小\<select_list > SELECT 语句中。  
  
 表源在 FROM 关键字后的顺序不影响返回的结果集。 如果 FROM 子句中出现重复的名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会返回错误。  
  
 *table_or_view_name*  
 表或视图的名称。  
  
 同一个实例上的另一个数据库中是否存在的表或视图[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在窗体中使用完全限定的名称*数据库*。*架构*。*object_name*。  
  
 表或视图是否存在的实例之外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l，在窗体中使用由四部分构成的名称*linked_server*。*目录*。*架构*。*对象*。 有关详细信息，请参阅 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的数据。 通过使用构造一个由四部分构成名称[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)发挥还可以使用名称的服务器部分以指定远程表源。 当指定 OPENDATASOURCE 时， *database_name*和*schema_name*不一定适用于所有数据源，并受到访问远程对象的 OLE DB 访问接口的功能。  
  
 [AS] *table_alias*  
 是的别名*table_source* ，可以使用是为方便起见或用于区分的表或视图中自联接或子查询。 别名往往是一个缩短了的表名，用于在联接中引用表的特定列。 如果联接中的多个表中存在相同的列名，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要求使用表名、视图名或别名来限定列名。 如果定义了别名，则不能使用表名。  
  
 使用派生的表、 行集或表值函数或运算符 （如 PIVOT 或 UNPIVOT） 的子句时，所需*table_alias*子句末尾是所有列，包括对列分组，关联的表名称返回。  
  
 使用 (\<table_hint >)  
 指定查询优化器对此表和此语句使用优化或锁定策略。 有关详细信息，请参阅[表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 *rowset_function*  

**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 指定其中一个行集函数（如 OPENROWSET），该函数返回可用于替代表引用的对象。 行集函数列表的详细信息，请参阅[行集函数 &#40;Transact SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 使用 OPENROWSET 和 OPENQUERY 函数指定远程对象依赖于访问该对象的 OLE DB 访问接口的性能。  
  
 *bulk_column_alias*  

**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 代替结果集内列名的可选别名。 只允许在使用 OPENROWSET 函数和 BULK 选项的 SELECT 语句中使用列别名。 当你使用*bulk_column_alias*，在文件中的列的顺序相同中指定每个表列的别名。  
  
> [!NOTE]  
>  此别名覆盖 XML 格式化文件的 COLUMN 元素中的 NAME 属性（如果有该属性）。  
  
 *user_defined_function*  
 指定表值函数。  
  
 OPENXML \<openxml_clause>  

**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 通过 XML 文档提供行集视图。 有关详细信息，请参阅[OPENXML &#40;Transact SQL &#41;](../../t-sql/functions/openxml-transact-sql.md).  
  
 *derived_table*  
 从数据库中检索行的子查询。 *derived_table*用作输入到外部查询。  
  
 *派生* *_table*可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]表值构造函数的新功能来指定多个行。 例如， `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`。 有关详细信息，请参阅[表值构造函数 &#40;Transact SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 代替派生表的结果集内列名的可选别名。 在选择列表中的每个列包括一个列别名，并将整个列别名列表用圆括号括起来。  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time >  

**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 指定返回从指定的临时表和及其链接的系统版本控制历史记录表的数据的特定版本  
  
\<tablesample_clause>  
 指定返回来自表的数据样本。 该样本可以是近似的。 此子句可对 SELECT、UPDATE 或 DELETE 语句中的任何主表或联接表使用。 不能对视图指定 TABLESAMPLE。  
  
> [!NOTE]  
>  对升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据库使用 TABLESAMPLE 时，数据库的兼容级别必须设置为 110 或更高，在递归公用表表达式 (CTE) 查询中不允许 PIVOT。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
 SYSTEM  
 ISO 标准指定的依赖于实现的抽样方法。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这是唯一可用的抽样方法，并且是默认应用的方法。 SYSTEM 应用基于页的抽样方法，即从表中选择一组随机页作为样本，这些页上的所有行作为样本子集返回。  
  
 *sample_number*  
 表示行的百分比或行数的精确或近似的常量数值表达式。 如果指定百分比，与*sample_number*隐式转换为**float**值; 否则，转换为**bigint**。 PERCENT 是默认设置。  
  
 PERCENT  
 指定*sample_number*应从表中检索表的行的百分比。 指定 PERCENT 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回指定的百分比的近似值。 指定百分比的情况*sample_number*表达式的结果必须为一个值从 0 到 100。  
  
 ROWS  
 这大约指定*sample_number*将检索的行。 指定 ROWS 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回指定的行数的近似值。 当指定行时， *sample_number*表达式的计算结果必须为大于零的整数值。  
  
 REPEATABLE  
 指示可以再次返回选定的样本。 指定具有相同时*repeat_seed*值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将返回的行的同一子集，只要到表中的任何行中进行了任何更改。 如果替换为其他指定*repeat_seed*值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将可能的返回表中的行的某些不同的采样。 对表的以下操作可视为更改：插入、更新、删除、索引重新生成或碎片整理以及数据库还原或附加。  
  
 *repeat_seed*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于生成随机数的常量整数表达式。 *repeat_seed*是**bigint**。 如果*repeat_seed*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将随机分配一个值。 对特定*repeat_seed*值，采样结果始终是相同如果不更改已应用于表。 *Repeat_seed*表达式的计算结果必须为大于零的整数。  
  
 \<joined_table>  
 由两个或更多表的积构成的结果集。 对于多个联接，请使用圆括号来更改联接的自然顺序。  
  
\<join_type>  
 指定联接操作的类型。  
  
 **INNER**  
 指定返回所有匹配的行对。 放弃两个表中不匹配的行。 如果未指定任何联接类型，此设置为默认设置。  
  
 FULL [ OUTER ]  
 指定在结果集中包括左表或右表中不满足联接条件的行，并将对应于另一个表的输出列设为 NULL。 这是对通常由 INNER JOIN 返回的所有行的补充。  
  
 LEFT [ OUTER ]  
 指定在结果集中包括左表中所有不满足联接条件的行，除了由内部联接返回所有的行之外，还将另外一个表的输出列设置为 NULL。  
  
 RIGHT [OUTER]  
 指定在结果集中包括右表中所有不满足联接条件的行，除了由内部联接返回所有的行之外，还将与另外一个表对应的输出列设置为 NULL。  
  
\<join_hint>  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查询优化器使用一个联接提示或执行算法，每个查询的 FROM 子句中指定的联接。 有关详细信息，请参阅[联接提示 &#40;Transact SQL &#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 有关[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，这些联接提示应用于两个分发不兼容的列上的内部联接。 它们可以通过限制在查询处理期间发生的数据移动的量来提高查询性能。 允许联接提示的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]如下所示：  
  
 减少  
 可以减少要移动的表联接右侧为了使两个分发兼容表兼容的行数。 REDUCE 提示也称为半部联接提示。  
  
 REPLICATE  
 从要复制到所有节点的联接左侧表中的联接列导致值。 在右侧表联接到这些列的复制版本。  
  
 重新分发  
 强制两个数据源，以分发到 JOIN 子句中指定的列上。 对于分布式表，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将执行随机排布移动。 对于复制的表，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将执行剪裁移动。 若要了解这些移动类型，请参阅中的"了解查询计划"主题中的"DMS 查询计划操作"一节[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。 查询计划使用广播的移动解决分发不兼容的联接时，此提示可以提高性能。  
  
 JOIN  
 指示指定的联接操作应在指定的表源或视图之间执行。  
  
 ON \<search_condition>  
 指定联接所基于的条件。 虽然常常使用列运算符和比较运算符，但该条件可指定任何谓词，例如：  
  
```sql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 当该条件指定列时，列不必具有相同的名称或数据类型；但是，如果数据类型不相同，则这些列要么必须相互兼容，要么是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够隐式转换的类型。 如果数据类型不能隐式转换，则在条件中必须使用 CONVERT 函数显式转换数据类型。  
  
 在 ON 子句中可能有仅涉及一个联接表的谓词。 这样的谓词也可能出现在查询中的 WHERE 子句中。 虽然这种谓词的放置对于 INNER 联接不会产生差别，但是在涉及 OUTER 联接时可能会导致不同的结果。 这是因为 ON 子句中的谓词在应用于联接之前先应用于表，而 WHERE 子句在语义上应用于联接结果。  
  
 有关搜索条件和谓词的详细信息，请参阅[搜索条件 &#40;Transact SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 指定两个表的叉积。 返回相同的行，就好像在旧式的非 SQL-92 式联接中并没有指定 WHERE 子句。  
  
 *left_table_source* {跨 |外部} 应用*right_table_source*  
 指定*right_table_source*运算符针对的每一行的应用的计算*left_table_source*。 时，此功能非常有用*right_table_source*包含采用列值的表值函数*left_table_source*作为其自变量之一。  
  
 必须使用 APPLY 指定 CROSS 或 OUTER。 指定跨时，生成任何行时*right_table_source*计算对指定的行的*left_table_source*并返回空结果集。  
  
 指定外部时，将一个行生成的每一行*left_table_source*即使*right_table_source*对该行计算并返回空结果集。  
  
 有关详细信息，请参见“备注”部分。  
  
 *left_table_source*  
 上一个参数中定义的一个表源。 有关详细信息，请参见“备注”部分。  
  
 *right_table_source*  
 上一个参数中定义的一个表源。 有关详细信息，请参见“备注”部分。  
  
 *table_source* PIVOT \<pivot_clause>  
 指定*table_source*透视基于*pivot_column*。 *table_source*是表或表表达式。 输出是包含的所有列的表*table_source*除*pivot_column*和*value_column*。 列*table_source*，除*pivot_column*和*value_column*，被称为 pivot 运算符分组列。 有关透视和逆透视的详细信息，请参阅[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
 PIVOT 对输入表执行分组列的分组操作，并为每个组返回一行。 此外，输出包含每个值中指定的一个列*column_list*出现在*pivot_column*的*input_table*。  
  
 有关详细信息，请参见后面的“备注”部分。  
  
 *aggregate_function*  
 接受一个或多个输入的系统聚合函数或用户定义的聚合函数。 聚合函数应该对 Null 值固定不变。 对 Null 值固定不变的聚合函数在求聚合值时不考虑组中的 Null 值。  
  
 不允许使用 COUNT(*) 系统聚合函数。  
  
 *value_column*  
 PIVOT 运算符的值列。 与逆透视，一起使用时*value_column*不能为现有列中输入名称*table_source*。  
  
 FOR *pivot_column*  
 PIVOT 运算符的透视列。 *pivot_column*的隐式或显式转换为类型必须为**nvarchar()**。 此列不能为**映像**或**rowversion**。  
  
 当使用逆透视时， *pivot_column*是将成为从变窄的输出列的名称*table_source*。 不能有中的现有列*table_source*具有该名称。  
  
 IN (*column_list* )  
 在 PIVOT 子句中，列出了中的值*pivot_column*的将成为输出表的列名称。 列表不能指定输入中存在的任何列名称*table_source*正在透视。  
  
 在 UNPIVOT 子句中，列出中的列*table_source*将能收缩到单个*pivot_column*。  
  
 *table_alias*  
 输出表的别名。 *pivot_table_alias*必须指定。  
  
 逆透视\<unpivot_clause >  
 指定的输入的表将变窄从多个列*column_list*到一个单列调用*pivot_column*。 有关透视和逆透视的详细信息，请参阅[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
 AS OF \<date_time>  

**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 返回一个表，其中为包含过去指定时间点的实际（当前）值的每个行提供一条记录。 在内部，临时表及其历史记录表之间进行联合，然后对结果进行筛选以返回的值中指定的时间点有效的行 *\<date_time >*参数。 某一行的值被视为有效如果*system_start_time_column_name*值是否小于或等于 *\<date_time >*参数值和*system_end_time_column_name*值是否大于 *\<date_time >*参数值。   
  
 FROM \<start_date_time> TO \<end_date_time>

**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。

  
 返回具有的处于活动状态中指定的时间范围，而不管它们是否启动处于活动状态之前的所有记录版本值的表 *\<start_date_time >*发件人的参数值自变量或上限时间停止处于活动状态后 *\<end_date_time >* TO 自变量的参数值。 在内部，将在临时表及其历史记录表之间进行联合，然后筛选结果，以返回在指定时间范围内任意时间保持活动状态的所有行版本的值。 正好在 FROM 终结点定义的下限的行将包括在内，正好在 TO 终结点所定义的上限的行将不包括在内。  
  
 BETWEEN \<start_date_time> AND \<end_date_time>  

**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 与上面相同中**FROM \<start_date_time > 收件人\<end_date_time >**说明，但它包含行变为活动状态由定义的上限， \<end_date_time >终结点。  
  
 包含在 CONTAINED IN (\<start_date_time >， \<end_date_time >)  

**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 返回一个表，其中包含在 CONTAINED IN 参数的两个日期时间值定义的时间范围内打开和关闭的所有记录版本的值。 正好在下限时间激活的记录，或者在上限时间停止活动的行将包括在内。  
  
 ALL  
 从当前表和历史记录表中的所有行中返回的值的表。  
  
## <a name="remarks"></a>注释  
 FROM 子句支持用于联接表和派生表的 SQL-92-SQL 语法。 SQL-92 语法提供 INNER、LEFT OUTER、RIGHT OUTER、FULL OUTER 和 CROSS 联接运算符。  
  
 视图、派生表和子查询中均支持 FROM 子句内的 UNION 和 JOIN。  
  
 自联接是与自身联接的表。 基于自联接的插入和更新操作遵循 FROM 子句中的顺序。  
  
 因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会考虑来自提供列分布统计信息的链接服务器的分布及基数统计信息，所以，无需 REMOTE 联接提示来强制远程评估联接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询处理器将考虑远程统计信息，并确定远程联接策略是否适当。 REMOTE 联接提示对不提供列分发统计信息的提供程序非常有用。  
  
## <a name="using-apply"></a>使用 APPLY  
 APPLY 运算符的左操作数和右操作数都是表表达式。 这些操作数之间的主要区别在于*right_table_source*可以使用采用中的列的表值函数*left_table_source*作为函数的参数之一。 *Left_table_source*可以包括表值函数，但它不能包含从列的自变量*right_table_source*。  
  
 APPLY 运算符通过以下方式工作，以便为 FROM 子句生成表源：  
  
1.  计算结果*right_table_source*针对的每一行*left_table_source*来生成行集。  
  
     中的值*right_table_source*依赖于*left_table_source*。 *right_table_source*可以表示大约这种方式： `TVF(left_table_source.row)`，其中`TVF`是表值函数。  
  
2.  在计算中的每一行生成结果集结合在一起*right_table_source*与*left_table_source*通过执行 UNION ALL 操作。  
  
     由应用运算符的结果生成的列的列表是从列集中的*left_table_source*结合从列的列表*right_table_source*。  
  
## <a name="using-pivot-and-unpivot"></a>使用 PIVOT 和 UNPIVOT  
 *Pivot_column*和*value_column*是由 PIVOT 运算符的列进行分组。 PIVOT 遵循以下过程获得输出结果集：  
  
1.  对执行分组依据其*input_table*对分组的列，并生成一个输出的行对于每个组。  
  
     输出行中的分组列获取该组中的相应列值*input_table*。  
  
2.  通过执行以下操作，为每个输出行生成列列表中的列的值：  
  
    1.  此外分组在 GROUP BY 针对上一步中生成的行*pivot_column*。  
  
         每个输出列中*column_list*，选择子组中满足条件：  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function*针对计算*value_column*此子组和其结果作为值返回的相应*output_column*。 如果子组为空， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null 值生成该*output_column*。 如果聚合函数是 COUNT，且子组为空，则返回零 (0)。  

> [!NOTE]
> 中的列标识符`UNPIVOT`子句按照目录排序规则。 有关[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，排序规则是始终`SQL_Latin1_General_CP1_CI_AS`。 有关[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]部分包含的数据库，排序规则是始终`Latin1_General_100_CI_AS_KS_WS_SC`。 如果与其他列，然后 collate 子句结合使用的列 (`COLLATE DATABASE_DEFAULT`) 要求，以避免冲突。   
  
 有关透视和逆透视包括示例的详细信息，请参阅[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
## <a name="permissions"></a>权限  
 需要 DELETE、SELECT 或 UPDATE 语句的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-a-simple-from-clause"></a>A. 使用简单 FROM 子句  
 下面的示例从 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库中的 `TerritoryID` 表中检索 `Name` 和 `SalesTerritory` 列。  
  
```sql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. 使用 TABLOCK 和 HOLDLOCK 优化器提示  
 下面的部分事务说明了如何在 `Employee` 上放置一个显式共享表锁，以及如何读取索引。 该锁将在整个事务中被持有。  
  
```sql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. 使用 SQL-92 CROSS JOIN 语法  
 下面的示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `Employee` 和 `Department` 这两个表的叉积。 所有可能组合列表`BusinessEntityID`行和所有`Department`名称的行返回。  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. 使用 SQL-92 FULL OUTER JOIN 语法  
 下面的示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中产品名称以及 `SalesOrderDetail` 表中任何对应的销售订单。 该示例还将返回在 `Product` 表中没有列出产品的任何销售订单，以及销售订单不同于在 `Product` 表中列出的销售订单的任何产品。  
  
```sql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. 使用 SQL-92 LEFT OUTER JOIN 语法  
 下面的示例基于 `ProductID` 联接两个表，并保留左表中不匹配的行。 `Product` 表与每个表中的 `SalesOrderDetail` 列上的 `ProductID` 表相匹配。 所有产品，无论是否已订购，都将在结果集中显示。  
  
```sql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. 使用 SQL-92 INNER JOIN 语法  
 下面的示例返回所有产品名称和销售订单 ID。  
  
```sql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. 使用 SQL-92 RIGHT OUTER JOIN 语法  
 下面的示例基于 `TerritoryID` 联接两个表，并保留右表中不匹配的行。 `SalesTerritory`与匹配表`SalesPerson`表上`TerritoryID`每个表中的列。 不论是否分配了区域，所有销售人员均在结果集中显示。  
  
```sql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. 使用 HASH 和 MERGE 联接提示  
 下面的示例在 `Product`、`ProductVendor` 和 `Vendor` 表之间执行三表联接，生成产品及其供应商的列表。 查询优化器使用 MERGE 联接来联接 `Product` 和 `ProductVendor`（`p` 和 `pv`）。 然后，`Product` 和 `ProductVendor` MERGE 联接（`p` 和 `pv`）的结果被 HASH 联接到 `Vendor` 表，生成（`p` 和 `pv`）和 `v`。  
  
> [!IMPORTANT]  
>  指定了联接提示后，要执行 INNER JOIN 时，INNER 关键字不再为可选，而必须显式说明。  
  
```sql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>I. 使用派生表  
 下面的示例使用派生表（`SELECT` 子句后的 `FROM` 语句）返回所有员工的名字和姓氏及其居住的城市。  
  
```sql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. 使用 TABLESAMPLE 从表中的行样本中读取数据  
 下面的示例在 `TABLESAMPLE` 子句中使用 `FROM`，大约返回 `10` 表中所有行的 `Customer`%。  
  
```sql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>K. 使用 APPLY  
 下面的示例假定数据库中存在具有如下架构的以下表：  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 还有一个表值函数 (`GetReports(MgrID)`) 可以返回指定的 `EmpID` 直接或间接领导的所有员工的列表（`EmpLastName`、`EmpSalary`、`MgrID`）。  
  
 该示例使用 `APPLY` 返回所有部门和部门中的所有员工。 如果某个部门没有任何员工，则将不返回该部门的任何行。  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 如果您希望查询为那些没有员工的部门生成行（这将为 `EmpID`、`EmpLastName` 和 `EmpSalary` 列生成 Null 值），请改用 `OUTER APPLY`。  
  
```sql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>L. 使用 CROSS APPLY  
 以下示例将检索驻留在计划缓存中的所有查询计划的快照，方法是通过查询 `sys.dm_exec_cached_plans` 动态管理视图来检索缓存中所有查询计划的计划句柄。 然后，指定 `CROSS APPLY` 运算符以将计划句柄传递给 `sys.dm_exec_query_plan`。 当前在计划缓存中的每个计划的 XML 显示计划输出位于返回的表的 `query_plan` 列中。  
  
```sql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>M. 使用 FOR SYSTEM_TIME  
  
**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 下面的示例使用的 SYSTEM_TIME AS OF date_time_literal_or_variable 参数可返回自 2014 年 1 月 1 日起已实际 （当前版） 的表行。  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下面的示例使用到 date_time_literal_or_variable 自变量的 SYSTEM_TIME 从 date_time_literal_or_variable 返回定义为从 2013 年 1 月 1 日开始，2014 年 1 月 1 日，期间处于活动状态的所有行以外的上限。  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下面的示例使用的 SYSTEM_TIME 之间 date_time_literal_or_variable 和 date_time_literal_or_variable 参数来返回所有行，定义为从 2013 年 1 月 1 日开始，2014 年 1 月 1 日，期间处于活动状态非独占的上限。  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下面的示例使用 FOR SYSTEM_TIME CONTAINED IN （date_time_literal_or_variable，date_time_literal_or_variable） 参数可返回已打开和关闭期间定义以及从 2013 年 1 月 1 日开始、 结束的时间段的所有行2014 年 1 月 1日日。  
  
```sql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 下面的示例使用变量，而不是文本的查询提供日期边界值。  
  
```sql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>N. 使用 INNER JOIN 语法  
 下面的示例返回`SalesOrderNumber`， `ProductKey`，和`EnglishProductName`中的列`FactInternetSales`和`DimProduct`表 where 联接键`ProductKey`，在这两个表中匹配项。 `SalesOrderNumber`和`EnglishProductName`每个列存在于其中一个表，因此不需要使用这些列中，指定表别名，如所示; 这些别名可供可读性。 Word **AS**之前别名名称不是必需的但建议以提高可读性并使其符合 ANSI 标准。  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 由于`INNER`关键字不需要对内部联接，此相同的查询可以写成：  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 A`WHERE`子句可能还用于与此查询来限制结果。 此示例将结果限制为`SalesOrderNumber`高于 SO5000 的值：  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>O. 使用左外部联接和 RIGHT OUTER JOIN 语法  
 以下示例联接`FactInternetSales`和`DimProduct`表上`ProductKey`列。 左外部联接语法保留从左侧不匹配的行 (`FactInternetSales`) 表。 由于`FactInternetSales`表不包含任何`ProductKey`不匹配的值`DimProduct`表，此查询将返回第一个内部联接上面的示例中为相同的行。  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 此外可以编写而无需为此查询`OUTER`关键字。  
  
 在右外部联接中，保留右表不匹配的行。 下面的示例返回与左外部联接示例上述相同的行。  
  
```sql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 下面的查询使用`DimSalesTerritory`与左外部联接中的左表的表。 它检索`SalesOrderNumber`值从`FactInternetSales`表。 如果没有为特定未下的订单`SalesTerritoryKey`，查询将返回 NULL`SalesOrderNumber`该行。 按此查询进行排序`SalesOrderNumber`列中，以便此列中的任何 Null 将出现在结果的顶部。  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 此查询无法改写为右外部联接检索相同的结果：  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>P. 使用 FULL OUTER JOIN 语法  
 下面的示例演示完全外部联接，它返回所有行从这两个联接的表，但另一个表不匹配的值都返回 NULL。  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 此外可以编写而无需为此查询`OUTER`关键字。  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>Q. 使用 CROSS JOIN 语法  
 下面的示例返回的叉积`FactInternetSales`和`DimSalesTerritory`表。 所有可能组合列表`SalesOrderNumber`和`SalesTerritoryKey`返回。 注意到缺少`ON`交叉联接查询中的子句。  
  
```sql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>R. 使用派生表  
 下面的示例使用派生的表 (`SELECT`后的语句`FROM`子句) 返回`CustomerKey`和`LastName`列中的所有客户`DimCustomer`表与`BirthDate`晚于 1 月 1 日值1970 和姓氏 Smith。  
  
```sql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S. 减少联接提示示例  
 下面的示例使用`REDUCE`联接提示，更改在查询内派生表中的处理。 使用时`REDUCE`在此查询中，联接提示`fis.ProductKey`投影、 复制和进行不同的并且然后加入`DimProduct`期间的随机排布`DimProduct`上`ProductKey`。 在分布式生成派生的表`fis.ProductKey`。  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="t-replicate-join-hint-example"></a>T. 复制联接提示示例  
 下一个示例演示与前面的示例，但同样的查询`REPLICATE`联接提示使用而不是`REDUCE`联接提示。 利用`REPLICATE`提示会导致中的值`ProductKey`（联接） 列从`FactInternetSales`表复制到所有节点。 `DimProduct`表联接到这些值的复制版本。  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>U. 使用 REDISTRIBUTE 提示要保证分发不兼容的联接随机排布移动邮箱  
 下面的查询上分发不兼容的联接使用 REDISTRIBUTE 查询提示。 这可确保查询优化器将在查询计划中使用随机排布移动。 这还可确保查询计划不会使用广播移动，后者将分布式的表移动到复制的表。  
  
 在下面的示例中，REDISTRIBUTE 提示强制 FactInternetSales 表上的随机排布移动，因为 ProductKey 是 DimProduct，分布列，而不是 FactInternetSales 分布列。  
  
```sql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40;Transact SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
