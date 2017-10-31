---
title: "rowversion (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47bcf3007657c1cf8f77c364aa21839cdd27d1ba
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

公开数据库中自动生成的唯一二进制数字的数据类型。 **rowversion**通常用作版本戳表行的机制。 存储大小为 8 个字节。 **Rowversion**数据类型是一个递增的数字，并且不保留日期或时间。 若要记录的日期或时间，使用**datetime2**数据类型。
  
## <a name="remarks"></a>注释  
每个数据库有对于每个插入递增的计数器或对包含的表执行的更新操作**rowversion**数据库中的列。 此计数器是数据库行版本。 这可以跟踪数据库内的相对时间，而不是时钟相关联的实际时间。 一个表只能有一个**rowversion**列。 每次的某一行而该行**rowversion** 、 修改或插入列中插入的递增的数据库 rowversion 值**rowversion**列。 此属性，则可以**rowversion**列密钥，尤其是主键的不佳候选项。 对行的任何更新都会更改行版本值，从而更改键值。 如果该列属于主键，那么旧的键值将无效，进而引用该旧值的外键也将不再有效。 如果该表在动态游标中引用，则所有更新均会更改游标中行的位置。 如果该列属于索引键，则对数据行的所有更新还将导致索引更新。  **Rowversion**该值递增与任何 update 语句，即使不更改了任何行值。 (例如，如果列的值为 5，且 update 语句将值设置为 5，此操作被视为更新即使没有任何更改，与**rowversion**即会递增。)
  
**时间戳**是同义词**rowversion**数据类型，并受到的行为的数据类型的同义词。 在 DDL 语句、 使用**rowversion**而不是**时间戳**只要有可能。 有关详细信息，请参阅[数据类型同义词 &#40;Transact SQL &#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] **时间戳**数据类型是不同于**时间戳**ISO 标准中定义的数据类型。
  
> [!NOTE]  
>  **时间戳**语法已弃用。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
在 CREATE TABLE 或 ALTER TABLE 语句中，你不必指定的列名称**时间戳**数据类型，例如：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
如果不指定列名，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]生成**时间戳**列名称; 但是， **rowversion**同义词不遵循此行为。 当你使用**rowversion**，你必须指定列名称，例如：
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  重复**rowversion**值可以由在其中使用 SELECT INTO 语句生成**rowversion**列是选择列表中。 我们不建议使用**rowversion**以这种方式。  
  
为 null **rowversion**列在语义上等效于**binary （8)**列。 可以为 null **rowversion**列在语义上等效于**varbinary （8)**列。
  
你可以使用**rowversion**自上次读取后，对其运行某一行来轻松地确定行是否已经 update 语句的列。 如果对行下，运行 update 语句，将更新 rowversion 值。 如果对行运行语句没有更新，rowversion 值是与之前读取读取相同。 若要返回数据库的当前 rowversion 值，使用[@@DBTS](../../t-sql/functions/dbts-transact-sql.md)。
  
你可以添加**rowversion**到表，以帮助保持数据库的完整性，多个用户都在同一时间更新行时的列。 此外，您可能还想要在不重新查询表的情况下了解有多少行被更新以及哪些行被更新。
  
例如，假定您创建了一个名为 `MyTest` 的表。 通过运行以下填充表中的某些数据[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
然后，可以使用以下示例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在更新期间实现 `MyTest` 表的乐观并发控制。
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`是**rowversion**指示上次读取行的行的列值。 此值必须替换为实际**rowversion**值。 举例说明的实际**rowversion**值是 0x00000000000007D3。
  
还可以将示例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句放在事务中。 通过在事务的作用域中查询 `@t` 变量，可以在不重新查询 `myKey`t 表的情况下检索表的更新后的 `MyTes` 列。
  
以下是相同的示例使用**时间戳**语法：
  
```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)  
[INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)
  
  

