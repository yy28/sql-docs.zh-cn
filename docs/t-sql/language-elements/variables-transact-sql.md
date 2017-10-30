---
title: "变量 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f372ae86-a003-40af-92de-fa52e3eea13f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c77c323f8e9dbb2abc010c3fbc9e6d2b349c8ae1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="variables-transact-sql"></a>变量 (Transact-SQL)
[!INCLUDE[tsql-appliesto-tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

TRANSACT-SQL 本地变量是可以包含特定类型的单个数据值的对象。 批处理和脚本中的变量通常用于： 

* 作为计数器计算循环执行的次数或控制循环执行的次数。
* 保存数据值以供控制流语句测试。
* 保存存储过程返回代码要返回的数据值或函数返回值。

> [!NOTE]
> 某些 TRANSACT-SQL 系统函数的名称开头使用两个*在*符号 （@ @）。 尽管在早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 @@functions被引用到作为全局变量，它们不是变量，但没有作为变量相同的行为。 @@functions是系统函数，以及其语法用法遵循函数的规则。

以下脚本创建一个小的测试表并向其填充 26 行。 脚本使用变量来执行下列三个操作： 

* 通过控制循环执行的次数来控制插入的行数。
* 提供插入整数列的值。
* 作为表达式一部分生成插入字符列的字母的函数。  

```sql
-- Create the table.
CREATE TABLE TestTable (cola int, colb char(3));
GO
SET NOCOUNT ON;
GO
-- Declare the variable to be used.
DECLARE @MyCounter int;

-- Initialize the variable.
SET @MyCounter = 0;

-- Test the variable to see if the loop is finished.
WHILE (@MyCounter < 26)
BEGIN;
   -- Insert a row into the table.
   INSERT INTO TestTable VALUES
       -- Use the variable to provide the integer value
       -- for cola. Also use it to generate a unique letter
       -- for each row. Use the ASCII function to get the
       -- integer value of 'a'. Add @MyCounter. Use CHAR to
       -- convert the sum back to the character @MyCounter
       -- characters after 'a'.
       (@MyCounter,
        CHAR( ( @MyCounter + ASCII('a') ) )
       );
   -- Increment the variable to count this iteration
   -- of the loop.
   SET @MyCounter = @MyCounter + 1;
END;
GO
SET NOCOUNT OFF;
GO
-- View the data.
SELECT cola, colb
FROM TestTable;
GO
DROP TABLE TestTable;
GO
```

## <a name="declaring-a-transact-sql-variable"></a>声明 Transact-SQL 变量
DECLARE 语句初始化通过 TRANSACT-SQL 变量： 
* 指定一个名称。 名称的第一个字符必须为一个 @。
* 指定系统提供的或用户定义的数据类型和长度。 对于数值变量还指定精度和小数位数。 对于 XML 类型的变量，可以指定一个可选的架构集合。
* 将值设置为 NULL。

例如，以下**DECLARE**语句将创建一个名为的本地变量 **@mycounter** 属于 int 数据类型。  
```sql
DECLARE @MyCounter int;
```
若要声明多个局部变量，请在定义的第一个局部变量后使用一个逗号，然后指定下一个局部变量名称和数据类型。

例如，以下**DECLARE**语句创建名为的三个本地变量 **@LastName** ，  **@FirstName** 和 **@StateProvince** ，并初始化每个为 NULL:  
```sql
DECLARE @LastName nvarchar(30), @FirstName nvarchar(20), @StateProvince nchar(2);
```

变量的作用域是可以引用该变量的范围的 TRANSACT-SQL 语句。 变量的作用域从声明变量的地方开始到声明变量的批处理或存储过程的结尾。 例如，下面的脚本存在语法错误，因为在一个批处理中引用了在另一个批处理中声明的变量：  
```sql
USE AdventureWorks2014;
GO
DECLARE @MyVariable int;
SET @MyVariable = 1;
-- Terminate the batch by using the GO keyword.
GO 
-- @MyVariable has gone out of scope and no longer exists.

-- This SELECT statement generates a syntax error because it is
-- no longer legal to reference @MyVariable.
SELECT BusinessEntityID, NationalIDNumber, JobTitle
FROM HumanResources.Employee
WHERE BusinessEntityID = @MyVariable;
```

变量具有局部作用域，只在定义它们的批处理或过程中可见。 在下面的示例中，为执行 sp_executesql 创建的嵌套作用域不能访问在更高作用域中声明的变量，从而返回错误。  

```sql
DECLARE @MyVariable int;
SET @MyVariable = 1;
EXECUTE sp_executesql N'SELECT @MyVariable'; -- this produces an error
```

## <a name="setting-a-value-in-a-transact-sql-variable"></a>为 Transact-SQL 变量设置值

第一次声明变量时，其值设置为 NULL。 若要为变量赋值，请使用 SET 语句。 这是为变量赋值的首选方法。 也可以通过 SELECT 语句的选择列表中当前所引用值为变量赋值。

若要通过使用 SET 语句为变量赋值，请包含变量名和需要赋给变量的值。 这是为变量赋值的首选方法。 例如，下面的批处理声明两个变量、为它们赋值并在 `WHERE` 语句的 `SELECT` 子句中予以使用：  

```sql
USE AdventureWorks2014;
GO
-- Declare two variables.
DECLARE @FirstNameVariable nvarchar(50),
   @PostalCodeVariable nvarchar(15);

-- Set their values.
SET @FirstNameVariable = N'Amy';
SET @PostalCodeVariable = N'BA5 3HX';

-- Use them in the WHERE clause of a SELECT statement.
SELECT LastName, FirstName, JobTitle, City, StateProvinceName, CountryRegionName
FROM HumanResources.vEmployee
WHERE FirstName = @FirstNameVariable
   OR PostalCode = @PostalCodeVariable;
GO
```

变量也可以通过选择列表中当前所引用的值赋值。 如果在选择列表中引用变量，则它应当被赋以标量值或者 SELECT 语句应仅返回一行。 例如：  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = MAX(EmployeeID)
FROM HumanResources.Employee;
GO
```

> [!WARNING]
> 如果在单个 SELECT 语句中有多个赋值子句，则 SQL Server 不保证表达式求值的顺序。 请注意，只有当赋值之间有引用时才能看到影响。

如果 SELECT 语句返回多个行，且变量引用非标量表达式，则会将变量设置为返回结果集的最后一行中的表达式的值。 例如，在以下批处理 **@EmpIDVariable** 设置为**BusinessEntityID**返回的最后一行的值，它是 1:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = BusinessEntityID
FROM HumanResources.Employee
ORDER BY BusinessEntityID DESC;

SELECT @EmpIDVariable;
GO
```

## <a name="see-also"></a>另请参阅  
 [声明@local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
 [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
  
 [选择@local_variable](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
  
  

