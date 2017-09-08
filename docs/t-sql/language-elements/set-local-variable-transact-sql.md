---
title: "设置@local_variable(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a92fa424de70d1ba9cccf437a2de49ab8432ba1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-localvariable-transact-sql"></a>设置@local_variable(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  设置指定本地创建的变量，以前通过使用 DECLARE @*local_variable*语句，为指定的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET @local_variable {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
  
```  
  
## <a name="arguments"></a>参数  
 **@***local_variable*  
 是除之外的任何类型的变量的名称**光标**，**文本**， **ntext**，**映像**，或**表**。 变量名称必须以一个 at 符号开头 (**@**)。 变量名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 *property_name*  
 用户定义类型的属性。  
  
 *字段名*  
 用户定义类型的公共字段。  
  
 *udt_name*  
 公共语言运行时 (CLR) 用户定义类型的名称。  
  
 { **.** | **::** }  
 指定 CLR 用户定义类型的方法。 对于一个实例 （非静态） 方法，使用句点 (**。**)。 对于静态方法，使用两个冒号 (**::**)。 若要调用 CLR 用户定义类型的方法、属性或字段，必须对类型具有 EXECUTE 权限。  
  
 *method_name* **(** *参数*[ **，**...*n* ] **)**  
 用户定义类型的方法，它带有一个或多个参数以修改类型实例的状态。 静态方法必须是公共的。  
  
 **@***SQLCLR_local_variable*  
 其类型位于程序集内的变量。 有关详细信息，请参阅[公共语言运行时 (CLR) 集成编程概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)。  
  
 *mutator_method*  
 程序集中可更改对象状态的方法。 SQLMethodAttribute.IsMutator 将应用于此方法。  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 复合赋值运算符：  
  
 + = 添加和分配  
  
 -= 减去和分配  
  
 * = Multiply 和分配  
  
 / = 分割和分配  
  
 %= 取模和分配  
  
 & = 按位和分配  
  
 ^ = 按位异或和分配  
  
 | = 按位或和分配  
  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 *cursor_variable*  
 是游标变量的名称。 如果目标游标变量先前引用了不同游标，则删除先前的引用。  
  
 *cursor_name*  
 使用 DECLARE CURSOR 语句声明的游标名称。  
  
 CURSOR  
 指定 SET 语句包含游标的声明。  
  
 SCROLL  
 指定游标支持所有提取选项：FIRST、LAST、NEXT、PRIOR、RELATIVE 和 ABSOLUTE。 如果还指定了 FAST_FORWARD，则不能指定 SCROLL。  
  
 FORWARD_ONLY  
 指定游标仅支持 FETCH NEXT 选项。 只能以一个方向、从第一行到最后一行检索游标。 如果没有使用 STATIC、KEYSET 或 DYNAMIC 关键字指定 FORWARD_ONLY，游标将作为 DYNAMIC 实现。 如果 FORWARD_ONLY 和 SCROLL 均未指定，那么除非指定了 STATIC、KEYSET 或 DYNAMIC 关键字，否则默认值为 FORWARD_ONLY。 对于 STATIC、KEYSET 和 DYNAMIC 游标，SCROLL 为默认值。  
  
 STATIC  
 定义一个游标，以创建将由该游标使用的数据的临时副本。 对游标的所有请求都从 tempdb 中的这一临时表中得到应答；因此，对该游标进行提取操作时返回的数据不反映对基表所做的修改，并且不允许对该游标进行修改。  
  
 KEYSET  
 指定当游标打开时，游标中行的成员身份和顺序已经固定。 唯一标识行的键的一套内置 keysettable tempdb 中。 对基表中的非键值所做的更改（由游标所有者更改或其他用户提交）在游标所有者滚动游标时可见。 其他用户进行的插入不可见，且不能通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标进行插入。  
  
 如果删除了某行，尝试读取的行返回 @@FETCH_STATUS为-2。 在游标外部所的键值的更新都类似于删除旧行后跟新行的插入。 具有新值的行不可见，并且尝试提取具有旧值的行返回 @@FETCH_STATUS为-2。 新值是通过指定 WHERE CURRENT OF 子句通过游标执行更新时可见。  
  
 DYNAMIC  
 定义一个游标，以反映游标所有者滚动游标时对结果集内的行所做的所有数据更改。 行的数据值、顺序和成员身份在每次提取时都会更改。 动态游标不支持绝对和相对提取选项。  
  
 FAST_FORWARD  
 指定启用了优化的 FORWARD_ONLY 和 READ_ONLY 游标。 如果还指定了 SCROLL，则不能指定 FAST_FORWARD。  
  
 READ_ONLY  
 防止通过此游标进行的更新。 在 UPDATE 或 DELETE 语句的 WHERE CURRENT OF 子句中不能引用游标。 该选项优先于要更新的游标的默认功能。  
  
 SCROLL LOCKS  
 指定通过游标进行的定位更新或删除一定会成功。 将行读入游标时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将锁定这些行，以确保随后可对它们进行修改。 如果还指定了 FAST_FORWARD，则不能指定 SCROLL_LOCKS。  
  
 OPTIMISTIC  
 指定如果行自读入游标以来已得到更新，则通过游标进行的定位更新或定位删除不成功。 当将行读入游标时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不锁定行。 相反，它使用 timestamp 列值的比较，或者如果表没有 timestamp 列则使用校验值，以确定将行读入游标后是否已修改该行。 如果已修改该行，尝试进行的定位更新或定位删除将失败。 如果还指定了 FAST_FORWARD，则不能指定 OPTIMISTIC。  
  
 TYPE_WARNING  
 指定如果游标从所请求的类型隐式转换为另一种类型，则向客户端发送警告消息。  
  
 有关*select_statement*  
 定义游标结果集的标准 SELECT 语句。 内不允许使用关键字的浏览和 INTO *select_statement*游标声明。  
  
 如果使用 DISTINCT、 UNION、 GROUP BY 或 HAVING，或中包含的聚合表达式*select_list*，光标将创建为静态。  
  
 如果每个基础表都没有唯一索引，并且请求了 ISO SCROLL 游标或 [!INCLUDE[tsql](../../includes/tsql-md.md)] KEYSET 游标，则游标将自动成为 STATIC 游标。  
  
 如果*select_statement*包含 ORDER BY 子句在其中的列不唯一行标识符，动态游标转换到键集游标，或静态游标如果无法打开键集游标。 这一点同样适用于使用不带 STATIC 关键字的 ISO 语法定义的游标。  
  
 READ ONLY  
 防止通过此游标进行的更新。 在 UPDATE 或 DELETE 语句的 WHERE CURRENT OF 子句中不能引用游标。 该选项优先于要更新的游标的默认功能。 该关键字与早期的 READ_ONLY 关键字的不同之处是 READ 和 ONLY 之间是一个空格，而不是下划线。  
  
 更新 [OF *column_name*[ **，**...*n* ] ]  
 定义游标中可更新的列。 如果的*column_name* [**，**... *n* ] 提供，仅列出的列将允许修改。 如果没有提供列表，则可更新所有列，除非已将游标定义为 READ_ONLY。  
  
## <a name="remarks"></a>注释  
 声明一个变量后，该变量将被初始化为 NULL。 使用 SET 语句将一个不是 NULL 的值赋给声明的变量。 给变量赋值的 SET 语句返回单值。 在初始化多个变量时，为每个局部变量使用单独的 SET 语句。  
  
 变量只能用在表达式中，不能代替对象名或关键字。 若要构造动态 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，请使用 EXECUTE。  
  
 组的语法规则 **@**  *cursor_variable*不包括本地和全局关键字。 当集 **@**  *cursor_variable* = 光标...使用语法，作为全局或本地，具体取决于与局部游标数据库选项的默认设置创建光标。  
  
 即使游标变量引用全局游标，它们也始终是局部变量。 如果游标变量引用全局游标，则该游标既有全局游标引用，也有局部游标引用。 有关详细信息，请参阅示例 C。  
  
 有关详细信息，请参阅[DECLARE CURSOR &#40;Transact SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 复合赋值运算符可以用在存在赋值（在运算符的右侧有一个表达式，包括变量）的任何地方以及 UPDATE、SELECT 和 RECEIVE 语句的 SET 语句中。  
  
 不要在 SELECT 语句中使用变量来连接值（即来计算聚合值）。 可能发生了意外查询结果。 这是因为 SELECT 列表中的所有表达式（包括赋值）不保证对于每个输出行仅执行一次。 有关详细信息，请参阅[此知识库文章](http://support.microsoft.com/kb/287515)。  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。 所有用户都可以都使用组 **@**  *local_variable*。  
  
## <a name="examples"></a>示例  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>A. 输出使用 SET 初始化的变量值  
 下面的示例创建`@myvar`变量，将一个字符串值放入变量，并将的值打印`@myvar`变量。  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>B. 在 SELECT 语句中使用由 SET 赋值的局部变量  
 以下示例创建一个名为 `@state` 的局部变量，并在 `SELECT` 语句中使用该局部变量来查找位于 `Oregon` 州的所有雇员的姓氏与名字。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @state char(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. 为局部变量使用复合赋值  
 以下两个示例将产生相同的结果。 它们创建一个名为 `@NewBalance` 的局部变量，将其乘以 10 并在一个 `SELECT` 语句中显示该局部变量的新值。 第二个示例使用一个复合赋值运算符。  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. 对全局游标使用 SET  
 以下示例创建一个局部变量，然后将游标变量设置为全局游标名。  
  
```  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. 使用 SET 定义游标  
 以下示例使用 `SET` 语句定义游标。  
  
```  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. 通过查询赋值  
 以下示例使用查询为变量赋值。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. 通过修改类型属性为用户定义类型的变量赋值  
 以下示例通过修改类型的 `Point` 属性的值来设置用户定义类型 `X` 的值。  
  
```  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. 通过调用类型的方法为用户定义类型的变量赋值  
 下面的示例设置用户定义类型的值**点**通过调用方法`SetXY`的类型。  
  
```  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>I. 为 CLR 类型创建变量并调用赋值函数方法  
 以下示例为 `Point` 类型创建变量，然后在 `Point` 中执行赋值函数方法。  
  
```  
CREATE ASSEMBLY mytest from 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. 输出使用 SET 初始化的变量值  
 下面的示例创建`@myvar`变量，将一个字符串值放入变量，并将的值打印`@myvar`变量。  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT top 1 @myvar FROM sys.databases;  
  
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>K. 在 SELECT 语句中使用由 SET 赋值的局部变量  
 下面的示例创建一个名为的本地变量`@dept`，并使用在此本地变量`SELECT`语句来查找所有雇员的姓名中的工作的第一个和最后一个名称`Marketing`部门。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @dept char(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>L. 为局部变量使用复合赋值  
 以下两个示例将产生相同的结果。 它们创建一个名为 `@NewBalance` 的局部变量，将其乘以 `10` 并在一个 `SELECT` 语句中显示该局部变量的新值。 第二个示例使用一个复合赋值运算符。  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>M. 通过查询赋值  
 以下示例使用查询为变量赋值。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>另请参阅  
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


