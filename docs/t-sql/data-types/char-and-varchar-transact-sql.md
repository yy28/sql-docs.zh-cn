---
title: "char 和 varchar (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c7bcb0e8ad7f8904703bd6c979b00aa30dd5348
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="char-and-varchar-transact-sql"></a>char 和 varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

这些数据类型是固定的长度或可变长度。  
  
## <a name="arguments"></a>参数  
**char** [(  *n*  )] 固定长度，非 Unicode 字符串数据。 *n*定义的字符串长度，并且必须是介于 1 到 8,000。 存储大小是 *n* 字节。 ISO 同义词**char**是**字符**。
  
**varchar** [(  *n*   |  **max** )] 长度可变，非 Unicode 字符串数据。 *n*定义的字符串长度和可以是一个介于 1 到 8,000。 **最大**指示最大存储大小为 2 ^31-1 个字节 (2 GB)。 存储大小为所输入数据的实际长度 + 2 个字节。 ISO 同义词**varchar**是**charvarying**或**charactervarying**。
  
## <a name="remarks"></a>注释  
当 *n* 未指定数据定义或变量声明语句中的默认长度为 1。 当 *n* 时未指定使用 CAST 和 CONVERT 函数中，默认长度为 30。
  
对象使用**char**或**varchar**分配的默认排序规则的数据库，除非使用 COLLATE 子句分配特定的排序规则。 该排序规则控制用于存储字符数据的代码页。
  
如果你具有支持多种语言的站点，请考虑使用 Unicode **nchar**或**nvarchar**数据类型尽量减少字符转换问题。 如果你使用**char**或**varchar**，我们建议采用以下做法：
- 使用**char**时的列数据条目的大小是一致。  
- 使用**varchar**时的列数据条目的大小相差迥异。  
- 使用**varchar （max)**时的列数据条目的大小相差迥异，和的大小可能超过 8000 个字节。  
  
SET ANSI_PADDING 为 OFF，当执行 CREATE TABLE 或 ALTER TABLE 时，如果**char**被定义为作为处理 NULL 的列**varchar**。
  
当排序规则代码页使用双字节字符时，存储大小仍是 *n* 字节。 具体取决于字符串的存储大小 *n* 字节可以是小于 *n* 字符。

> [!WARNING]
> 每个非 null varchar （max） 或 nvarchar (max) 列需要的其他固定分配期间排序操作计入 8,060 字节行限制的 24 个字节。 这可能会造成的非 null varchar （max） 或 nvarchar (max) 列都可以在表中创建的数字隐式限制。  
在以下情况下不提供特殊错误：创建表格（最大行大小超过允许的最大 8060 字节时出现的一般警告除外）时，或插入数据时。 这一较大的行大小可能会导致在执行某些正常操作（例如聚集索引键更新或完整列集排序）期间出现错误（例如错误 512），使得用户在执行操作前无法预料到此类错误。
  
##  <a name="_character"></a>将字符数据转换  
如果将字符表达式转换为不同大小的字符数据类型，则对于新数据类型而言过长的值将被截断。 **Uniqueidentifier**类型被视为出于从字符表达式，转换的字符类型，并因此受到将转换为字符类型的截断规则。 请参阅后面的“示例”一节。
  
当字符表达式转换为字符表达式的不同的数据类型或大小，如从**char(5)**到**varchar(5)**，或**char(20)**到**char(15)**，输入值的排序规则分配给转换后的值。 如果将非字符表达式转换为字符数据类型，则当前数据库的默认排序规则会被分配给经过转换的值。 在任一情况下，你可以通过使用分配特定的排序规则[COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)子句。
  
> [!NOTE]  
>  支持代码页转换**char**和**varchar**数据类型，但不是能为**文本**数据类型。 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本一样，将不报告代码页转换期间的数据丢失。  
  
字符将被转换为近似的表达式**数值**数据类型可以包括可选指数记数法 (e 小写或大写 E 跟选择性地包含加号 （+） 或减号 （-） 登录，然后号)。
  
字符正在转换为精确的表达式**数值**数据类型必须包括数字、 小数点，和一个可选加号 （+） 或减号 （-）。 将忽略前导空格。 逗号分隔符（例如 123,456.00 中的千位分隔符）在字符串中禁用。
  
字符转换为表达式**money**或**smallmoney**数据类型还可以包含可选小数点和美元符号 （$）。 可以使用逗号分隔符（如在 $123,456.00 中）。
  
## <a name="examples"></a>示例  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. 显示 n 时在变量声明中使用的默认值。  
下面的示例演示的默认值 *n* 对于是 1`char`和`varchar`数据类型时在变量声明中使用它们。
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. 在 CAST 和 CONVERT 中使用 varchar 时，显示 n 的默认值。  
下面的示例演示的默认值 *n* 为 30 时`char`或`varchar`数据类型用于`CAST`和`CONVERT`函数。
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. 转换数据以便于显示  
以下示例将两列转换为字符类型并应用一种样式，该样式将特定格式应用于所显示的数据。 A **money**类型转换为字符数据以及应用了样式 1，其中显示的值用逗号小数点左侧每隔三个数字和两个数字的小数点右侧。 A **datetime**类型转换为字符数据以及应用了样式 3，其格式 dd/mm/yy 中显示的数据。 在 WHERE 子句中， **money**类型被强制转换为要执行的字符串比较运算的字符类型。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. 转换 Uniqueidentifer 数据  
以下示例将 `uniqueidentifier` 值转换为 `char` 数据类型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
以下示例演示在值过长而无法转换数据类型时如何截断数据。 因为**uniqueidentifier**类型仅限于 36 个字符，超过该长度的字符将被截断。
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[nchar 和 nvarchar (Transact-SQL)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[估计数据库的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  

