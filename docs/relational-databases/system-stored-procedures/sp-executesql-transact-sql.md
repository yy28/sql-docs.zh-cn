---
title: sp_executesql (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_executesql
- sp_executesql_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_executesql
- dynamic SQL
ms.assetid: a8d68d72-0f4d-4ecb-ae86-1235b962f646
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 17dda137d5d3230c5e1ff7270f4af5583fa13fd0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559367"
---
# <a name="spexecutesql-transact-sql"></a>sp_executesql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  执行可多次重复使用或动态生成的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或批处理。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或批处理可以包含嵌入参数。  
  
> [!IMPORTANT]  
>  运行时编译的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可能会使应用程序受到恶意攻击。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_executesql [ @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [ OUT | OUTPUT ][ ,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>参数  
 [ \@stmt =]*语句*  
 是一个 Unicode 字符串，包含[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理。 \@语句必须是 Unicode 常量或 Unicode 变量。 不允许使用更复杂的 Unicode 表达式（例如使用 + 运算符连接两个字符串）。 不允许使用字符常量。 如果指定 Unicode 常量，则它必须带有前缀**N**。例如，Unicode 常量**N 'sp_who'** 有效，但是字符常量 **'sp_who'** 不是。 字符串的大小仅受可用数据库服务器内存限制。 在 64 位服务器上的字符串的大小被限制为 2 GB 的最大大小**nvarchar （max)**。  
  
> [!NOTE]  
>  \@语句可以包含的参数将同一个窗体作为变量名称，例如： `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 包含在每个参数\@stmt 必须具有一个对应的条目，在这种\@params 参数定义列表和参数值列表。  
  
 [ \@params =] N'\@*parameter_name * * data_type* [，...*n* ]  
 是一个字符串，它包含的定义中嵌入的所有参数\@stmt。字符串必须是 Unicode 常量或 Unicode 变量。 每个参数定义由参数名称和数据类型组成。 *n*是表示附加参数定义的占位符。 每个参数中指定\@中定义 stmtmust \@params。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理在\@stmt 不包含参数，\@参数不是必需的。 该参数的默认值为 NULL。  
  
 [ \@param1 =] '*value1*  
 参数字符串中定义的第一个参数的值。 该值可以是 Unicode 常量，也可以是 Unicode 变量。 必须为包含在每个参数提供参数值\@stmt。值不需要[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理在\@stmt 不具有任何参数。  
  
 [ OUT | OUTPUT ]  
 指示参数是输出参数。 **文本**， **ntext**，和**图像**参数可以用作输出参数，除非是公共语言运行时 (CLR) 过程。 使用 OUTPUT 关键字的输出参数可以为游标占位符，CLR 过程除外。  
  
 *n*  
 附加参数值的占位符。 这些值只能为常量或变量， 不能是很复杂的表达式（例如函数）或使用运算符生成的表达式。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零（失败）  
  
## <a name="result-sets"></a>结果集  
 从生成 SQL 字符串的所有 SQL 语句中返回结果集。  
  
## <a name="remarks"></a>Remarks  
 必须按特定顺序输入 sp_executesql 参数，如本主题前面的"语法"部分中所述。 如果这些参数的输入顺序不正确，则会显示一条错误消息。  
  
 在批处理、名称作用域和数据库上下文方面，sp_executesql 与 EXECUTE 的行为相同。 [!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理在 sp_executesql\@直到执行 sp_executesql 语句 stmt 参数时才编译。 内容\@stmt 然后编译并执行作为执行计划独立于调用 sp_executesql 的批处理的执行计划。 sp_executesql 批处理不能引用调用 sp_executesql 的批处理中声明的变量。 sp_executesql 批处理中的本地游标或变量对调用 sp_executesql 的批处理是不可见的。 对数据库上下文所做的更改只在 sp_executesql 语句结束前有效。  
  
 如果只更改了语句中的参数值，则 sp_executesql 可用来代替存储过程多次执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 因为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句本身保持不变，仅参数值发生变化，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器可能重复使用首次执行时所生成的执行计划。  
  
> [!NOTE]  
>  若要提高性能，请在语句字符串中使用完全限定的对象名。  
  
 sp_executesql 支持独立于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 字符串设置参数值，如以下示例所示。  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
  
/* Build the SQL string one time.*/  
SET @SQLString =  
     N'SELECT BusinessEntityID, NationalIDNumber, JobTitle, LoginID  
       FROM AdventureWorks2012.HumanResources.Employee   
       WHERE BusinessEntityID = @BusinessEntityID';  
SET @ParmDefinition = N'@BusinessEntityID tinyint';  
/* Execute the string with the first parameter value. */  
SET @IntVariable = 197;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
/* Execute the same string with the second parameter value. */  
SET @IntVariable = 109;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
```  
  
 输出参数也可用于 sp_executesql。 以下示例从 `AdventureWorks2012.HumanResources.Employee` 表中检索职务，并在输出参数 `@max_title` 中返回结果。  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @max_title varchar(30);  
  
SET @IntVariable = 197;  
SET @SQLString = N'SELECT @max_titleOUT = max(JobTitle)   
   FROM AdventureWorks2012.HumanResources.Employee  
   WHERE BusinessEntityID = @level';  
SET @ParmDefinition = N'@level tinyint, @max_titleOUT varchar(30) OUTPUT';  
  
EXECUTE sp_executesql @SQLString, @ParmDefinition, @level = @IntVariable, @max_titleOUT=@max_title OUTPUT;  
SELECT @max_title;  
```  
  
 替换 sp_executesql 中的参数的能力，与使用 EXECUTE 语句执行字符串相比，有下列优点：  
  
-   因为在 sp_executesql 字符串中，[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的实际文本在两次执行之间并未改变，所以查询优化器应该能将第二次执行中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句与第一次执行时生成的执行计划匹配。 因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不必编译第二条语句。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 字符串只生成一次。  
  
-   整数参数按其本身格式指定。 不需要转换为 Unicode。  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-executing-a-simple-select-statement"></a>A. 执行简单的 SELECT 语句  
 以下示例创建并执行一个简单的 `SELECT` 语句，其中包含名为 `@level` 的嵌入参数。  
  
```  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
          WHERE BusinessEntityID = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
### <a name="b-executing-a-dynamically-built-string"></a>B. 执行动态生成的字符串  
 以下示例显示使用 `sp_executesql` 执行动态生成的字符串。 该示例中的存储过程用于向一组表中插入数据，这些表用于划分一年的销售数据。 一年中的每个月均有一个表，格式如下：  
  
```  
CREATE TABLE May1998Sales  
    (OrderID int PRIMARY KEY,  
    CustomerID int NOT NULL,  
    OrderDate  datetime NULL  
        CHECK (DATEPART(yy, OrderDate) = 1998),  
    OrderMonth int  
        CHECK (OrderMonth = 5),  
    DeliveryDate datetime  NULL,  
        CHECK (DATEPART(mm, OrderDate) = OrderMonth)  
    )  
```  
  
 此示例存储过程将动态生成并执行 `INSERT` 语句，以便向正确的表中插入新订单。 此示例使用订货日期生成应包含数据的表的名称，然后将此名称并入 `INSERT` 语句中。  
  
> [!NOTE]  
>  这是一个简单的 sp_executesql 示例。 此示例不包含错误检查以及业务规则检查，例如，确保订单号在各个表之间不重复。  
  
```  
CREATE PROCEDURE InsertSales @PrmOrderID INT, @PrmCustomerID INT,  
                 @PrmOrderDate DATETIME, @PrmDeliveryDate DATETIME  
AS  
DECLARE @InsertString NVARCHAR(500)  
DECLARE @OrderMonth INT  
  
-- Build the INSERT statement.  
SET @InsertString = 'INSERT INTO ' +  
       /* Build the name of the table. */  
       SUBSTRING( DATENAME(mm, @PrmOrderDate), 1, 3) +  
       CAST(DATEPART(yy, @PrmOrderDate) AS CHAR(4) ) +  
       'Sales' +  
       /* Build a VALUES clause. */  
       ' VALUES (@InsOrderID, @InsCustID, @InsOrdDate,' +  
       ' @InsOrdMonth, @InsDelDate)'  
  
/* Set the value to use for the order month because  
   functions are not allowed in the sp_executesql parameter  
   list. */  
SET @OrderMonth = DATEPART(mm, @PrmOrderDate)  
  
EXEC sp_executesql @InsertString,  
     N'@InsOrderID INT, @InsCustID INT, @InsOrdDate DATETIME,  
       @InsOrdMonth INT, @InsDelDate DATETIME',  
     @PrmOrderID, @PrmCustomerID, @PrmOrderDate,  
     @OrderMonth, @PrmDeliveryDate  
  
GO  
```  
  
 在该过程中使用 sp_executesql 比使用 EXECUTE 执行字符串更有效。 使用 sp_executesql 时，只生成 12 个版本的 INSERT 字符串，每个月的表对应 1 个字符串。 使用 EXECUTE 时，因为参数值不同，每个 INSERT 字符串均是唯一的。 尽管两种方法生成的批处理数相同，但因为 sp_executesql 生成的 INSERT 字符串都相似，所以查询优化器更有可能重复使用执行计划。  
  
### <a name="c-using-the-output-parameter"></a>C. 使用 OUTPUT 参数  
 下面的示例使用`OUTPUT`用于存储生成的结果集参数`SELECT`中的语句`@SQLString`参数。两个`SELECT`使用的值，然后将执行语句`OUTPUT`参数。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @SalesOrderNumber nvarchar(25);  
DECLARE @IntVariable int;  
SET @SQLString = N'SELECT @SalesOrderOUT = MAX(SalesOrderNumber)  
    FROM Sales.SalesOrderHeader  
    WHERE CustomerID = @CustomerID';  
SET @ParmDefinition = N'@CustomerID int,  
    @SalesOrderOUT nvarchar(25) OUTPUT';  
SET @IntVariable = 22276;  
EXECUTE sp_executesql  
    @SQLString  
    ,@ParmDefinition  
    ,@CustomerID = @IntVariable  
    ,@SalesOrderOUT = @SalesOrderNumber OUTPUT;  
-- This SELECT statement returns the value of the OUTPUT parameter.  
SELECT @SalesOrderNumber;  
-- This SELECT statement uses the value of the OUTPUT parameter in  
-- the WHERE clause.  
SELECT OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderNumber = @SalesOrderNumber;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-executing-a-simple-select-statement"></a>D. 执行简单的 SELECT 语句  
 以下示例创建并执行一个简单的 `SELECT` 语句，其中包含名为 `@level` 的嵌入参数。  
  
```  
-- Uses AdventureWorks  
  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorksPDW2012.dbo.DimEmployee   
          WHERE EmployeeKey = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
 有关其他示例，请参阅[sp_executesql (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms188001.aspx)。  
  
## <a name="see-also"></a>请参阅  
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
