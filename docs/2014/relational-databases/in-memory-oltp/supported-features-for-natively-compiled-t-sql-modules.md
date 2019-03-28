---
title: 在本机编译存储过程中受支持的构造 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4fd1a406848006739b83c1b8a0886d5c2d4bdfa
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527139"
---
# <a name="supported-constructs-in-natively-compiled-stored-procedures"></a>本机编译的存储过程中支持的构造
  本主题列出了本机编译存储过程的支持的功能 ([CREATE PROCEDURE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)):  
  
-   [本机编译存储过程中的可编程性](#pncsp)  
  
-   [支持的运算符](#so)  
  
-   [本机编译存储过程中的内置函数](#bfncsp)  
  
-   [在本机编译存储过程的查询外围应用](#qsancsp)  
  
-   [审核](#auditing)  
  
-   [表、 查询和联接提示](#tqh)  
  
-   [排序限制](#los)  
  
 有关本机编译存储过程中支持的数据类型的信息，请参阅 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)。  
  
 有关不支持的构造的完整信息以及有关如何处理本机编译的存储过程中不支持的某些功能的信息，请参阅 [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md)。 有关不支持的功能的详细信息，请参阅 [内存中 OLTP 不支持的 Transact-SQL 构造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
##  <a name="pncsp"></a> 本机编译存储过程中的可编程性  
 支持以下各项：  
  
-   BEGIN ATOMIC（位于存储过程的外层）、LANGUAGE、ISOLATION LEVEL、DATEFORMAT 和 DATEFIRST。  
  
-   将变量声明为 NULL 或 NOT NULL。 如果变量声明为 NOT NULL，则声明必须具有初始值设定项。 如果变量未声明为 NOT NULL，则初始值设定项是可选的。  
  
-   IF 和 WHILE  
  
-   INSERT/UPDATE/DELETE  
  
     不支持子查询。 在 WHERE 或 HAVING 子句中，支持 AND 和 BETWEEN；不支持 OR、NOT 和 IN。  
  
-   内存优化的表类型和表变量。  
  
-   RETURN  
  
-   SELECT  
  
-   SET  
  
-   TRY/CATCH/THROW  
  
     要优化性能，请对整个本机编译存储过程使用单个 TRY/CATCH 块。  
  
##  <a name="so"></a> 支持的运算符  
 支持下列运算符。  
  
-   [比较运算符&#40;TRANSACT-SQL&#41; ](/sql/t-sql/language-elements/comparison-operators-transact-sql) (例如，>， \<，> =、 和 < =) 在条件语句中支持 (如果时)。  
  
-   一元运算符（+、-）。  
  
-   二元运算符（*、/、+、-、%（取模））。  
  
     数字和字符串都支持加号运算符 (+)。  
  
-   逻辑运算符（AND、OR、NOT）。 IF 和 WHILE 语句支持 OR 和 NOT，WHERE 或 HAVING 子句不支持 OR 和 NOT。  
  
-   按位运算符 ~、&、| 和 ^  
  
##  <a name="bfncsp"></a> 本机编译存储过程中的内置函数  
 内存优化表的默认约束中以及本机编译的存储过程中支持以下函数。  
  
-   数学函数：ACOS、ASIN、ATAN、ATN2、COS、COT、DEGREES、EXP、LOG、LOG10、PI、POWER、RADIANS、RAND、SIN、SQRT、SQUARE 和 TAN  
  
-   日期函数：CURRENT_TIMESTAMP、DATEADD、DATEDIFF、DATEFROMPARTS、DATEPART、DATETIME2FROMPARTS、DATETIMEFROMPARTS、DAY、EOMONTH、GETDATE、GETUTCDATE、MONTH、SMALLDATETIMEFROMPARTS、SYSDATETIME、SYSUTCDATETIME 和 YEAR。  
  
-   字符串函数：LEN、LTRIM、RTRIM 和 SUBSTRING  
  
-   恒等函数：SCOPE_IDENTITY  
  
-   NULL 函数说明：ISNULL  
  
-   Uniqueidentifier 函数：NEWID 和 NEWSEQUENTIALID  
  
-   错误函数：ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE  
  
-   转换：CAST 和 CONVERT。 不支持在 Unicode 与非 Unicode 字符串（n(var)char 和 (var)char）之间进行转换。  
  
-   系统函数：@@rowcount。 本机编译存储过程中的语句会更新 @@rowcount，因此，可使用本机编译存储过程中的 @@rowcount 来确定受在该本机编译存储过程中执行的上条语句影响的行数。 但是，@@rowcount 在本机编译存储过程执行开始和结束时会重置为 0。  
  
##  <a name="qsancsp"></a> 在本机编译存储过程的查询外围应用  
 支持以下各项：  
  
-   BETWEEN  
  
-   列名别名（使用 AS 或 = 语法）。  
  
-   CROSS JOIN 和 INNER JOIN 仅支持与 SELECT 查询连用。  
  
-   选择列表中支持表达式和[其中&#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/where-transact-sql)子句，如果他们使用支持的运算符。 有关当前支持的运算符的列表，请参阅 [Supported Operators](#so) 。  
  
-   筛选器谓词 IS [NOT] NULL  
  
-   从\<内存优化表 >  
  
-   [GROUP BY &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql)支持，以及聚合函数 AVG、 COUNT、 COUNT_BIG、 最小值、 最大值和之和。 类型 nvarchar、char、varchar、varchar、varbinary 和 Binary 不支持 MIN 和 MAX。 [ORDER BY 子句&#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-order-by-clause-transact-sql)支持与[GROUP BY &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql)如果 ORDER BY 列表中的表达式逐字出现在 GROUP BY 列表。 例如，支持 GROUP BY a + b ORDER BY a + b，但不支持 GROUP BY a、b ORDER BY a + b。  
  
-   HAVING 具有与 WHERE 子句相同的表达式限制。  
  
-   INSERT VALUES（每条语句一行）和 INSERT SELECT  
  
-   ORDER BY <sup>1</sup>  
  
-   不引用列的谓词。  
  
-   SELECT、UPDATE 和 DELETE  
  
-   顶部<sup>1</sup>  
  
-   SELECT 列表中的变量赋值。  
  
-   WHERE...和  
  
 <sup>1</sup> ORDER BY 和 TOP 支持在本机编译存储过程中，有一些限制：  
  
-   在 `DISTINCT` 或 `SELECT` 子句中不支持 `ORDER BY`。  
  
-   在 `WITH TIES` 子句中不支持 `PERCENT` 或 `TOP`。  
  
-   在 `TOP` 子句中使用常量时，结合使用 `ORDER BY` 与 `TOP` 不支持超过 8,192。 当查询包含联接或聚合函数时，该限制数可能降低。 （例如，对于一个联接（两个表），限制为 4,096 行。 对于两个联接（三个表），限制为 2,730 行。）  
  
     可通过将行数存储在变量中来获得多于 8,192 的结果：  
  
    ```sql  
    DECLARE @v INT = 9000  
    SELECT TOP (@v) ... FROM ... ORDER BY ...  
    ```  
  
 不过，与使用变量相比，在 `TOP` 子句中使用常量将提供更好的性能。  
  
 这些限制不适用于针对内存优化表的解释的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问。  
  
##  <a name="auditing"></a> 审核  
 在本机编译存储过程中支持过程级审核。 不支持语句级审核。  
  
 有关审核的详细信息，请参阅 [Create a Server Audit and Database Audit Specification](../security/auditing/create-a-server-audit-and-database-audit-specification.md)。  
  
##  <a name="tqh"></a> 表、 查询和联接提示  
 支持以下各项：  
  
-   INDEX、FORCESCAN 和 FORCESEEK 提示，位于表提示语法或查询的 [OPTION Clause (Transact-SQL)](/sql/t-sql/queries/option-clause-transact-sql) 中。  
  
-   FORCE ORDER  
  
-   INNER LOOP JOIN  
  
-   OPTIMIZE FOR  
  
 有关详细信息，请参阅[提示&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/hints-transact-sql)。  
  
##  <a name="los"></a>排序限制  
 可以在使用 [TOP (Transact-SQL)](/sql/t-sql/queries/top-transact-sql) 和 [ORDER BY 子句 (Transact-SQL)](/sql/t-sql/queries/select-order-by-clause-transact-sql) 的查询中对 8,000 多行进行排序。 但是，如果没有 [ORDER BY 子句 (Transact-SQL)](/sql/t-sql/queries/select-order-by-clause-transact-sql)，[TOP (Transact-SQL)](/sql/t-sql/queries/top-transact-sql) 最多可对 8,000 行进行排序（如果存在联接，则更少）。  
  
 如果查询同时使用 [TOP (Transact-SQL)](/sql/t-sql/queries/top-transact-sql) 运算符和 [ORDER BY 子句 (Transact-SQL)](/sql/t-sql/queries/select-order-by-clause-transact-sql)，则可以对 TOP 运算符指定多达 8192 行。 如果指定超过 8192 行，系统可能会显示如下错误信息：**消息 41398、 级别 16，状态 1，过程*\<过程名称 >*，行 *\<lineNumber >* ，TOP 运算符可返回最多 8192 行;*\<数 >* 请求。**  
  
 如果您没有 TOP 子句，则可以使用 ORDER BY 对任何数目的行进行排序。  
  
 如果您没有使用 ORDER BY 子句，则可以将任何整数值用于 TOP 运算符。  
  
 使用 TOP N = 8192 的示例：编译  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 使用 TOP N > 8192 的示例：无法编译。  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 该 8192 行限制仅适用于 `TOP N` ，其中 `N` 是常量，如前面的示例中所示。  如果您需要 `N` 大于 8192，则可以将该值分配给一个变量并且将该变量用于 `TOP`。  
  
 使用变量的示例：编译  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 **对返回行的限制：** 有两种情形可减少可由 TOP 运算符返回的行数：  
  
-   在查询中使用 JOIN。  JOIN 对该限制的影响依赖于查询计划。  
  
-   在 ORDER BY 子句中使用聚合函数或对聚合函数的引用。  
  
 用于在 TOP N 中计算最差情形下支持的最大 N 的公式为： `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`。  
  
## <a name="see-also"></a>请参阅  
 [本机编译存储过程](natively-compiled-stored-procedures.md)   
 [本机编译存储过程的迁移问题](migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
