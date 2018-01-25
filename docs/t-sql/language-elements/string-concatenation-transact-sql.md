---
title: "+ （字符串串联）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- concatenation
- +
- string
dev_langs: TSQL
helpviewer_keywords:
- concatenation [SQL Server]
- string concatenation operators
- + (string concatenation)
ms.assetid: 35cb3d7a-48f5-4b13-926c-a9d369e20ed7
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6cc04023e38faa5bce7964fab7aa0b65533a46c6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="-string-concatenation-transact-sql"></a>+（字符串串联）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  字符串表达式中的运算符，它将两个或多个字符串或二进制字符串、列或字符串和列名的组合串联到一个表达式中（字符串运算符）。  例如`SELECT 'book'+'case';`返回`bookcase`。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何数据类型之一的字符和二进制数据类型类别中除**映像**， **ntext**，或**文本**数据类型。 两个表达式必须具有相同的数据类型，或者其中一个表达式必须能够隐式转换为另一个表达式的数据类型。  
  
 在二进制字符串之间串联二进制字符串和任何字符串时，必须显式转换字符数据。 下面的示例演示当`CONVERT`，或`CAST`，必须将用于二进制串联以及何时`CONVERT`，或`CAST`，无需使用。  
  
```  
DECLARE @mybin1 varbinary(5), @mybin2 varbinary(5)  
SET @mybin1 = 0xFF  
SET @mybin2 = 0xA5  
-- No CONVERT or CAST function is required because this example   
-- concatenates two binary strings.  
SELECT @mybin1 + @mybin2  
-- A CONVERT or CAST function is required because this example  
-- concatenates two binary strings plus a space.  
SELECT CONVERT(varchar(5), @mybin1) + ' '   
   + CONVERT(varchar(5), @mybin2)  
-- Here is the same conversion using CAST.  
SELECT CAST(@mybin1 AS varchar(5)) + ' '   
   + CAST(@mybin2 AS varchar(5))  
  
```  
  
## <a name="result-types"></a>结果类型  
 返回优先级最高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 +（字符串串联）运算符在用于长度为零的空字符串时的作用与用于 NULL 或未知值时不同。 长度为零的字符串可以指定为两个引号，引号内没有任何字符。 长度为零的二进制字符串可以指定为不带以十六进制常量指定的任何字节值的 0x。 串联长度为零的字符串始终要串联上述两个指定的字符串。 处理具有空值的字符串时，串联结果取决于会话设置。 与对空值执行的算术运算一样，当将空值添加到已知值时，结果通常是未知值，对空值执行的字符串串联运算也会产生空的结果。 但是，你可以通过更改的设置来更改此行为`CONCAT_NULL_YIELDS_NULL`当前会话。 有关详细信息，请参阅 [SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)。  
  
 如果字符串串联的结果超出 8,000 字节的限值，则结果将被截断。 但是，如果至少其中一个串联的字符串是大值类型，就不会进行截断。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-string-concatenation"></a>A. 使用字符串串联  
 以下示例在列标头 `Name` 下使用多个字符列创建一个列，人员的姓氏后跟随逗号、一个空格，然后是人员的名字。 结果集是按照姓氏，然后按照名字以字母顺序升序排列的。  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM Person.Person  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="b-combining-numeric-and-date-data-types"></a>B. 组合数值和日期数据类型  
 下面的示例使用`CONVERT`函数要串联**数值**和**日期**数据类型。  
  
```  
-- Uses AdventureWorks  
  
SELECT 'The order is due on ' + CONVERT(varchar(12), DueDate, 101)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID = 50001;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------------------------------------------  
 The order is due on 04/23/2007  
 (1 row(s) affected)
 ```  
  
### <a name="c-using-multiple-string-concatenation"></a>C. 使用多个字符串串联  
 以下示例串联多个字符串，形成一个长字符串，显示 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的副总裁的姓氏和名字的首字母。 逗号加在姓氏后，句点加在名字首字母后。  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ',' + SPACE(1) + SUBSTRING(FirstName, 1, 1) + '.') AS Name, e.JobTitle  
FROM Person.Person AS p  
    JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle LIKE 'Vice%'  
ORDER BY LastName ASC;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name               Title  
 -------------      ---------------`  
 Duffy, T.          Vice President of Engineering  
 Hamilton, J.       Vice President of Production  
 Welcker, B.        Vice President of Sales  

 (3 row(s) affected)
 ```  
 
### <a name="d-using-large-strings-in-concatenation"></a>D. 使用串联的大型字符串
下面的示例将多个字符串，以形成一个长字符串连接在一起，然后尝试计算最终的字符串的长度。 结果集中的最后一个长度为 16000，因为表达式计算将开始从左是， @x + @z + @y = > (@x + @z) + @y。 在本例中的结果 (@x + @z) 将被截断为 8000 个字节，然后@y添加到结果集中，这使得最终的字符串长度 16000。 由于@y为较大的值类型字符串时，不会发生截断。

```
DECLARE @x varchar(8000) = replicate('x', 8000)
DECLARE @y varchar(max) = replicate('y', 8000)
DECLARE @z varchar(8000) = replicate('z',8000)
SET @y = @x + @z + @y
-- The result of following select is 16000
SELECT len(@y) AS y
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 y        
 -------  
 16000  
  
 (1 row(s) affected)
 ```  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-multiple-string-concatenation"></a>E. 使用多个字符串串联  
 下面的示例将多个字符串，以形成一个长字符串以显示最后一个名称和副总裁示例数据库中的第一个初始连接在一起。 逗号加在姓氏后，句点加在名字首字母后。  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + SUBSTRING(FirstName, 1, 1) + '.') AS Name, Title  
FROM DimEmployee  
WHERE Title LIKE '%Vice Pres%'  
ORDER BY LastName ASC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name               Title                                           
-------------      ---------------  
Duffy, T.          Vice President of Engineering  
Hamilton, J.       Vice President of Production  
Welcker, B.        Vice President of Sales  
```  
  
## <a name="see-also"></a>另请参阅  
 [+ = &#40;字符串串联分配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
  
  



