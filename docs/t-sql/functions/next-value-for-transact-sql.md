---
title: "接下来值 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a4e6ca2ce4c89e1e608d9762d1562a78f7908c23
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  通过指定的序列对象生成序列号。  
  
 有关创建和使用序列的完整讨论，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。 使用[sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)生成保留的一系列序列号。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 包含序列对象的数据库的名称。  
  
 *schema_name*  
 包含序列对象的架构的名称。  
  
 *sequence_name*  
 生成该编号的序列对象的名称。  
  
 *over_order_by_clause*  
 确定将序列值分配给分区中的行的顺序。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 使用序列类型返回一个数字。  
  
## <a name="remarks"></a>注释  
 **NEXT VALUE FOR**函数可在存储的过程和触发器。  
  
 当**NEXT VALUE FOR**查询或默认的约束，使用函数，如果多次使用相同的序列对象，或在提供值，该语句和默认约束中使用相同的序列对象正在执行，将引用相同的序列中的结果集行中的所有列返回相同的值。  
  
 **NEXT VALUE FOR**函数具有不确定性，并且只允许在生成的序列值的数目是定义完善的上下文中。 下面定义了给定语句中的每个引用的序列对象使用的值数目：  
  
-   **选择**-对于每个引用的序列对象，新值会生成一次语句的结果中的每一行。  
  
-   **插入**... **值**-对于每个引用的序列对象，新值会生成一次为每个语句中插入的行。  
  
-   **更新**-对于每个引用的序列对象，新值生成语句正在更新每个行。  
  
-   过程的语句 (如**DECLARE**，**设置**等)-对于每个引用的序列对象，新值为每个语句生成。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 **NEXT VALUE FOR**函数不能在以下情况下：  
  
-   数据库处于只读模式时。  
  
-   作为表值函数的参数。  
  
-   作为聚合函数的参数。  
  
-   在子查询中，包括公用表表达式和派生表。  
  
-   在视图、用户定义的函数或计算列中。  
  
-   在语句中使用**DISTINCT**，**联合**， **UNION ALL**， **EXCEPT**或**INTERSECT**运算符。  
  
-   在语句中使用**ORDER BY**子句除非**NEXT VALUE FOR** ... **通过**(**ORDER BY** ...) 使用。  
  
-   在以下子句：**提取**，**通过**，**输出**， **ON**， **PIVOT**， **逆透视**，**分组依据**， **HAVING**，**计算**，**来计算**，或**FOR XML**.  
  
-   在条件表达式中使用**用例**，**选择**， **COALESCE**， **IIF**， **ISNULL**，或**NULLIF**。  
  
-   在**值**子句不属于**插入**语句。  
  
-   在检查约束的定义中。  
  
-   在规则或默认对象的定义中。 （它可用于默认约束。）  
  
-   作为用户定义表类型中的默认值。  
  
-   在语句中使用**顶部**，**偏移量**，或当**行计数**设置选项。  
  
-   在**其中**语句子句。  
  
-   在**合并**语句。 (时除外**NEXT VALUE FOR**函数用于目标表中的默认约束中，在使用默认的**创建**的语句**合并**语句。)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>在默认约束中使用序列对象  
 使用时**NEXT VALUE FOR**函数中默认约束，适用以下规则：  
  
-   可以从多个表的默认约束中引用单个序列对象。  
  
-   表和序列对象必须位于同一数据库中。  
  
-   添加默认约束的用户必须对序列对象具有 REFERENCES 权限。  
  
-   在删除默认约束之前，无法删除从默认约束中引用的序列对象。  
  
-   如果多个默认约束使用相同的序列对象，或者在提供这些值的语句以及执行的默认约束中使用相同的序列对象，则为行中的所有列返回相同的序列号。  
  
-   引用**NEXT VALUE FOR**默认约束中的函数不能指定**通过**子句。  
  
-   可以更改默认约束中引用的序列对象。  
  
-   情况下`INSERT … SELECT`或`INSERT … EXEC`插入的数据来自何处查询时使用的语句**ORDER BY**子句时，返回的值**NEXT VALUE FOR**函数将是中指定的顺序生成**ORDER BY**子句。  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>通过 OVER ORDER BY 子句使用序列对象  
 **NEXT VALUE FOR**函数支持通过应用生成排序的序列值**通过**子句**NEXT VALUE FOR**调用。 通过使用**通过**子句，保证用户返回的值所生成的顺序**通过**子句的**顺序 B**Y 子子句。 使用时应用以下的其他规则**NEXT VALUE FOR**起作用**通过**子句：  
  
-   多次调用**NEXT VALUE FOR**函数在单个语句中的同一序列生成器必须都使用相同**通过**子句定义。  
  
-   多次调用**NEXT VALUE FOR**函数引用不同的序列生成器，在单个语句中可以具有不同**通过**子句定义。  
  
-   **通过**子句应用于**NEXT VALUE FOR**函数不支持**PARTITION BY**子子句。  
  
-   如果所有调用**NEXT VALUE FOR**函数中**选择**语句指定**通过**子句， **ORDER BY**可能在中使用子句**选择**语句。  
  
-   **通过**子句允许与**NEXT VALUE FOR**函数中使用时**选择**语句或`INSERT … SELECT …`语句。 利用**通过**子句**NEXT VALUE FOR**中不允许函数**更新**或**合并**语句。  
  
-   如果另一个进程同时访问序列对象，则返回的编号可能会出现间断。  
  
## <a name="metadata"></a>元数据  
 有关序列的信息，请查询[sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)目录视图。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**更新**序列对象或序列的架构的权限。 有关授予权限的示例，请参阅本主题后面的示例 F。  
  
### <a name="ownership-chaining"></a>所有权链接  
 序列对象支持所有权链接。 如果序列对象具有与调用存储过程、触发器或表相同的所有者（将序列对象作为默认约束），则不需要对序列对象进行权限检查。 如果序列对象与调用存储过程、触发器或表归不同的用户所有，则需要对序列对象进行权限检查。  
  
 当**NEXT VALUE FOR**函数用作表中的默认值，用户需要两**插入**对表的权限和**更新**序列对象的权限若要使用默认值插入数据。  
  
-   如果默认约束具有与序列对象相同的所有者，则在调用默认约束时不需要具有序列对象的权限。  
  
-   如果默认约束和序列对象归不同的用户所有，即使通过默认约束调用序列对象，也需要具有序列对象的权限。  
  
### <a name="audit"></a>审核  
 审核**NEXT VALUE FOR**函数中，监视 SCHEMA_OBJECT_ACCESS_GROUP。  
  
## <a name="examples"></a>示例  
 有关创建序列和使用的示例**NEXT VALUE FOR**函数来生成序列号，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 以下示例在名为 `CountBy1` 的架构中使用名为 `Test` 的序列。 将执行以下语句以创建 `Test.CountBy1` 序列。 示例 C 和 E 使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库，因此，将在该数据库中创建 `CountBy1` 序列。  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. 在 SELECT 语句中使用序列  
 以下示例创建一个名为 `CountBy1` 的序列，每次使用该序列时将增加 1。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. 将变量设置为下一个序列值  
 以下示例介绍了三种将变量设置为下一个序列号值的方法。  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. 将序列与排名窗口函数一起使用  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. 在默认约束定义中使用 NEXT VALUE FOR 函数  
 使用**NEXT VALUE FOR**支持默认约束定义中的函数。 有关使用示例**NEXT VALUE FOR**中**CREATE TABLE**语句，请参阅示例 C[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。 以下示例使用 `ALTER TABLE` 将序列作为默认值添加到当前表中。  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. 在 INSERT 语句中使用 NEXT VALUE FOR 函数  
 以下示例创建一个名为 `TestTable` 的表，然后使用 `NEXT VALUE FOR` 函数插入一行。  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. 将 NEXT VALUE FOR 函数与 SELECT … 一起使用 INTO  
 下面的示例使用`SELECT … INTO`语句以创建名为的表`Production.NewLocation`并使用`NEXT VALUE FOR`函数若要为每个行编号。  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. 授予执行 NEXT VALUE FOR 的权限  
 下面的示例授予**更新**名为的用户权限`AdventureWorks\Larry`权执行`NEXT VALUE FOR`使用`Test.CounterSeq`序列。  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建序列 &#40;Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER 序列 &#40;Transact SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
