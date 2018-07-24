---
title: MERGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
caps.latest.revision: 76
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d55da07e2011cf611525f1ba5edd904ad5d6095c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38028979"
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  根据与源表联接的结果，对目标表执行插入、更新或删除操作。 例如，根据在另一个表中找到的差异在一个表中插入、更新或删除行，可以对两个表进行同步。  
  
 **性能提示：** 当两个表具有匹配特性的复杂混合时，针对 MERGE 语句介绍的条件行为的效果最佳。 例如，在行不存在时插入行，或是在行匹配时更新行。 仅仅基于其他表的行更新一个表时，可以通过基本的 INSERT、UPDATE 和 DELETE 语句提高性能和可伸缩性。 例如：  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ WITH <common_table_expression> [,...n] ]  
MERGE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>   
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]      
;  
  
<target_table> ::=  
{   
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]   
        [ WITH ( table_hint [ [ , ]...n ] ) ]   
  | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>   
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]   
  | <joined_table>   
  | <pivoted_table>   
  | <unpivoted_table>   
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]   
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]   
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '< contains_search_condition >' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery ) }   
  
<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }   
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>参数  
 WITH \<common_table_expression>  
 指定在 MERGE 语句作用域内定义的临时命名结果集或视图，也称为公用表表达式。 该结果集派生自一个简单查询，并由 MERGE 语句引用。 有关详细信息，请参阅 [WITH common_table_expression (Transact-SQL)](../../t-sql/queries/with-common-table-expression-transact-sql.md)。  
  
 TOP ( *expression* ) [ PERCENT ]  
 指定受影响的行数或行百分比。 *expression* 可以是行数或行百分比。 在 TOP 表达式中引用的行不是以任意顺序排列的。 有关详细信息，请参阅 [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md)。  
  
 在联接整个源表和整个目标表并且删除了不符合插入、更新或删除操作条件的联接行之后，应用 TOP 子句。 TOP 子句将联接行的数量进一步减少为指定值，并且以一种无序方式对其余联接行应用插入、更新或删除操作。 也就是说，在 WHEN 子句中定义的操作中，这些行是无序分布的。 例如，如果指定 TOP (10)，将会影响 10 行；在这些行中，可能会更新 7 行而插入 3 行，或者可能删除 1 行、更新 5 行并且插入 4 行，等等。  
  
 由于 MERGE 语句对源表和目标表都进行完全表扫描，因此在使用 TOP 子句通过创建多个批处理来修改大型表时，I/O 性能可能会受到影响。 在这种情况下，一定要确保所有连续批处理都以新行作为处理目标。  
  
 *database_name*  
 *target_table* 所在数据库的名称。  
  
 *schema_name*  
 *target_table* 所属架构的名称。  
  
 *target_table*  
 表或视图，\<table_source> 中的数据行将根据 \<clause_search_condition> 与该表或视图进行匹配。 *target_table* 是由 MERGE 语句的 WHEN 子句指定的任何插入、更新或删除操作的目标。  
  
 如果 *target_table* 为视图，则针对它的任何操作都必须满足更新视图所需的条件。 有关详细信息，请参阅[通过视图修改数据](../../relational-databases/views/modify-data-through-a-view.md)。  
  
 *target_table* 不能是远程表。 *target_table* 不能具有针对它定义的任何规则。  
  
 [ AS ] *table_alias*  
 用于引用表的替代名称。  
  
 USING \<table_source>  
 指定根据 \<merge_search condition> 与 *target_table* 中的数据行进行匹配的数据源。 此匹配的结果指出了要由 MERGE 语句的 WHEN 子句采取的操作。 \<table_source> 可以是一个远程表，或者是一个能够访问远程表的派生表。 
  
 \<table_source> 可以是一个派生表，它使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [表值构造函数](../../t-sql/queries/table-value-constructor-transact-sql.md)通过指定多行来构造表。  
  
 有关此子句的语法和参数的详细信息，请参阅 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)。  
  
 ON \<merge_search_condition>  
 指定在 \<table_source> 与 *target_table* 进行联接以确定它们的匹配位置时所遵循的条件。 
  
> [!CAUTION]  
>  重要的是，应仅指定目标表中用于匹配目的的列。 也就是说，指定与源表中的对应列进行比较的目标表列。 不要尝试通过在 ON 子句中筛选掉目标表中的行来提高查询性能，例如，指定 `AND NOT target_table.column_x = value`。 这样做可能会返回意外和不正确的结果。  
  
 WHEN MATCHED THEN \<merge_matched>  
 指定 *target_table* 中与 \<table_source> ON \<merge_search_condition> 返回的行匹配并满足所有其他搜索条件的所有行均应根据 \<merge_matched> 子句进行更新或删除。  
  
 MERGE 语句最多可以有两个 WHEN MATCHED 子句。 如果指定了两个子句，则第一个子句必须同时带有一个 AND \<search_condition> 子句。 对于任何给定的行，只有在未应用第一个 WHEN MATCHED 子句的情况下，才会应用第二个 WHEN MATCHED 子句。 如果有两个 WHEN MATCHED 子句，那么其中的一个必须指定 UPDATE 操作，而另一个必须指定 DELETE 操作。 如果在 \<merge_matched> 子句中指定了 UPDATE，并且根据 \<merge_search_condition>，\<table_source> 中的多个行与 *target_table* 中的某一行匹配，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。 MERGE 语句无法多次更新同一行，也无法更新和删除同一行。  
  
 WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
 指定对于 \<table_source> ON \<merge_search_condition> 返回的每一行，如果该行与 *target_table* 中的行不匹配但是满足其他搜索条件（如果存在），则在 *target_table* 中插入一行。 要插入的值是由 \<merge_not_matched> 子句指定的。 MERGE 语句只能有一个 WHEN NOT MATCHED 子句。  
  
 WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
 指定 *target_table* 中与 \<table_source> ON \<merge_search_condition> 返回的行不匹配但满足其他所有搜索条件的所有行均应根据 \<merge_matched> 子句进行更新或删除。  
  
 MERGE 语句最多可以有两个 WHEN NOT MATCHED BY SOURCE 子句。 如果指定了两个子句，则第一个子句必须同时带有一个 AND \<clause_search_condition> 子句。 对于任何给定的行，只有当未应用第一个 WHEN NOT MATCHED BY SOURCE 子句时才会应用第二个子句。 如果有两个 WHEN NOT MATCHED BY SOURCE 子句，那么其中的一个必须指定 UPDATE 操作，而另一个必须指定 DELETE 操作。 在 \<clause_search_condition> 中只能引用目标表中的列。  
  
 当 \<table_source> 未返回任何行时，无法访问源表中的列。 如果 \<merge_matched> 子句中指定的更新或删除操作引用了源表中的列，则会返回错误 207（列名无效）。 例如，由于无法访问源表中的 `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1`，因此 `Col1` 子句可能导致该语句失败。  
  
 AND \<clause_search_condition>  
 指定任何有效的搜索条件。 有关详细信息，请参阅[搜索条件 (Transact-SQL)](../../t-sql/queries/search-condition-transact-sql.md)。  
  
 \<table_hint_limited>  
 为由 MERGE 语句执行的每个插入、更新或删除操作指定对目标表应用的一个或多个表提示。 需要有 WITH 关键字和括号。  
  
 不允许 NOLOCK 和 READUNCOMMITTED。 有关表提示的详细信息，请参阅[表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 对作为 INSERT 语句目标的表指定 TABLOCK 提示与指定 TABLOCKX 提示具有相同的效果。 对表采用排他锁。 如果指定了 FORCESEEK，会将其应用于与源表联接的目标表的隐式实例。  
  
> [!CAUTION]  
>  指定带有 WHEN NOT MATCHED [ BY TARGET ] THEN INSERT 的 READPAST 可能会导致违反 UNIQUE 约束的 INSERT 操作。  
  
 INDEX ( index_val [，...n ] )  
 指定目标表上的一个或多个索引的名称或 ID，以执行与源表的隐式联接。 有关详细信息，请参阅[表提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 \<output_clause>  
 不按照任何特定顺序为 *target_table* 中更新、插入或删除的每一行返回一行。 **$action** 可在 output 子句中指定。 **$action** 是 **nvarchar(10)** 类型的列，它为每行返回以下三个值之一：“INSERT”、“UPDATE”或“DELETE”，具体取决于对该行执行的操作。 有关该子句的参数的详细信息，请参阅 [OUTPUT 子句 (Transact-SQL)](../../t-sql/queries/output-clause-transact-sql.md)。  
  
 OPTION ( \<query_hint> [ ,...n ] )  
 指定使用优化器提示来自定义数据库引擎处理语句的方式。 有关详细信息，请参阅[查询提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)。  
  
 \<merge_matched>  
 指定更新或删除操作，该操作应用于 *target_table* 中与 \<table_source> ON \<merge_search_condition> 返回的行不匹配但满足其他所有搜索条件的所有行。  
  
 UPDATE SET \<set_clause>  
 指定目标表中要更新的列或变量名的列表，以及用于更新它们的值。  
  
 有关该子句的参数的详细信息，请参阅 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)。 不允许将变量设置为与列相同的值。  
  
 删除  
 指定删除与 *target_table* 中的行匹配的行。  
  
 \<merge_not_matched>  
 指定要插入到目标表中的值。  
  
 (*column_list*)  
 要在其中插入数据的目标表中的一个或多个列的列表。 必须使用单一部分名称格式来指定这些列，否则 MERGE 语句将失败。 必须用括号将 column_list 括起来，并且用逗号进行分隔。  
  
 VALUES ( *values_list*)  
 一个逗号分隔列表，其中包含常量、变量或者返回要插入到目标表中的值的表达式。 表达式不能包含 EXECUTE 语句。  
  
 DEFAULT VALUES  
 强制插入的行包含为每个列定义的默认值。  
  
 有关此子句的详细信息，请参阅 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)。  
  
 \<search condition>  
 指定用于指定 \<merge_search_condition> 或 \<clause_search_condition> 的搜索条件。 有关此子句的参数的详细信息，请参阅[搜索条件 (Transact-SQL)](../../t-sql/queries/search-condition-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 必须指定三个 MATCHED 子句中的至少一个子句，但可以按任何顺序指定。 不能在同一个 MATCHED 子句中多次更新一个变量。  
  
 由 MERGE 语句指定的目标表中的任何插入、更新或删除操作都受为它定义的任何约束的限制，包括任何级联引用完整性约束。 如果 IGNORE_DUP_KEY 对于目标表中的任何唯一索引都设置为 ON，则 MERGE 将忽略此设置。  
  
 MERGE 语句需要一个分号 (;) 作为语句终止符。 如果运行没有终止符的 MERGE 语句，将引发错误 10713。  
  
 如果在 MERGE 之后使用，[@@ROWCOUNT (Transact-SQL)](../../t-sql/functions/rowcount-transact-sql.md) 会返回为客户端插入、更新和删除的行的总数。  
  
 在数据库兼容级别设置为 100 或更高时，MERGE 为完全保留的关键字。 MERGE 语句可用于设置为 90 和 100 的数据库兼容级别；但是，在将数据库兼容级别设置为 90 时，MERGE 为非完全保留的关键字。  
  
 使用排队更新复制时，不应使用 **MERGE** 语句。 **MERGE** 和排队更新触发器不兼容。 使用 insert 或 update 语句替换 **MERGE** 语句。  
  
## <a name="trigger-implementation"></a>触发器的实现  
 对于在 MERGE 语句中指定的每个插入、更新或删除操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都会激发针对目标表定义的任何对应的 AFTER 触发器，但不保证哪个操作最先或最后激发触发器。 为相同操作定义的触发器会遵循您指定的顺序进行触发。 有关设置触发器激发顺序的详细信息，请参阅[指定第一个和最后一个触发器](../../relational-databases/triggers/specify-first-and-last-triggers.md)。  
  
 对于由 MERGE 语句执行的插入、更新或删除操作，如果目标表具有针对自己定义的已启用 INSTEAD OF 触发器，那么对于在 MERGE 语句中指定的所有操作，它都必须具有已启用的 INSTEAD OF 触发器。  
  
 如果对 *target_table* 定义了任何 INSTEAD OF UPDATE 或 INSTEAD OF DELETE 触发器，则不会执行更新或删除操作， 而是会激发触发器并相应地填充 **inserted** 和 **deleted** 表。  
  
 如果对 *target_table* 定义了任何 INSTEAD OF INSERT 触发器，则不会执行插入操作， 而是会激发触发器并相应地填充 **inserted** 表。  
  
## <a name="permissions"></a>Permissions  
 需要对源表的 SELECT 权限和对目标表的 INSERT、UPDATE 或 DELETE 权限。 有关其他信息，请参阅 [SELECT](../../t-sql/queries/select-transact-sql.md)、[INSERT](../../t-sql/statements/insert-transact-sql.md)、[UPDATE](../../t-sql/queries/update-transact-sql.md) 和 [DELETE](../../t-sql/statements/delete-transact-sql.md) 主题中的“权限”部分。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. 使用 MERGE 在单个语句中对表执行 INSERT 和 UPDATE 操作  
 一种常见的应用场景是在存在匹配行时更新表中的一个或多个列，或在不存在匹配行时将数据作为新行插入。 此操作一般通过将参数传递给包含相应 UPDATE 和 INSERT 语句的存储过程来执行。 借助 MERGE 语句，将可以在单个语句中一起执行这两项任务。 下面的示例显示了 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中一个同时包含 INSERT 语句和 UPDATE 语句的存储过程。 随后，此示例对该过程进行了修改，以使用单个 MERGE 语句执行等效的操作。  
  
```  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.      
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the 
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values 
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN   
        UPDATE SET Name = source.Name  
WHEN NOT MATCHED THEN  
    INSERT (UnitMeasureCode, Name)  
    VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup   
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. 使用 MERGE 在单个语句中对表执行 UPDATE 和 DELETE 操作  
 下面的示例使用 MERGE 根据 `ProductInventory` 表中已处理的订单，每天更新 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据库中的 `SalesOrderDetail` 表。 通过减去每天对 `Quantity` 表中的每种产品所下的订单数，更新 `ProductInventory` 表的 `SalesOrderDetail` 列。 如果某种产品的订单数导致该产品的库存量下降到 0 或更少，则从 `ProductInventory` 表中删除该产品对应的行。  
  
```  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED   
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,   
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity, 
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. 借助派生的源表，使用 MERGE 对目标表执行 UPDATE 和 INSERT 操作  
 下面的示例使用 MERGE 以更新或插入行的方式来修改 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的 `SalesReason` 表。 当源表中的 `NewName` 值与目标表 (`Name`) 的 `SalesReason` 列中的值匹配时，就会更新此目标表中的 `ReasonType` 列。 当 `NewName` 的值不匹配时，就会将源行插入到目标表中。 此源表是一个派生表，它使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表值构造函数指定源表的多个行。 有关在派生表中使用表值构造函数的详细信息，请参阅[表值构造函数 (Transact-SQL)](../../t-sql/queries/table-value-constructor-transact-sql.md)。 该示例还说明了如何在表变量中存储 OUTPUT 子句的结果，并且说明存储结果之后如何通过执行返回已插入和更新的行的计数的简单选择操作来汇总 MERGE 语句的结果。  
  
```  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), 
              ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. 将 MERGE 语句的执行结果插入到另一个表中  
 下面的示例捕获从 MERGE 语句的 OUTPUT 子句返回的数据，并将该数据插入到另一个表中。 MERGE 语句根据在 `Quantity` 表中处理的订单更新 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `ProductInventory` 表的 `SalesOrderDetail` 列。 本示例捕获已更新的行并将这些行插入到用于跟踪库存变化的另一个表中。  
  
```  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty   
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)   
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0   
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0   
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID, 
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty) 
 WHERE Action = 'UPDATE';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [OUTPUT 子句 (Transact-SQL)](../../t-sql/queries/output-clause-transact-sql.md)   
 [在 Integration Services 包中执行 MERGE](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [表值构造函数 (Transact-SQL)](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  

