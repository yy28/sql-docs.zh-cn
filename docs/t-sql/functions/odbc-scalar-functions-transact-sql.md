---
title: "ODBC 标量函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
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
- CURDATE ODBC function
- DAYOFMONTH ODBC function
- WEEK ODBC function
- functions, ODBC CONCAT
- SECOND ODBC function
- functions, ODBC CURRENT_TIME
- functions, ODBC HOUR
- functions, ODBC QUARTER
- TRUNCATE ODBC function
- functions, ODBC SECOND
- DAYOFWEEK ODBC function
- CURRENT_DATE ODBC function
- DAYNAME ODBC function
- CURTIME ODBC function
- functions, ODBC CURRENT_DATE
- MINUTE ODBC function
- functions, ODBC BIT_LENGTH
- functions, ODBC OCTET_LENGTH
- CONCAT ODBC function
- MONTHNAME ODBC function
- functions, ODBC DAYOFYEAR
- OCTET_LENGTH ODBC function
- functions [SQL Server], ODBC scalar functions
- BIT_LENGTH ODBC function
- functions, ODBC DAYOFMONTH
- CURRENT_TIME ODBC function
- functions, ODBC CURDATE
- functions, ODBC CURTIME
- functions, ODBC TRUNCATE
- functions, ODBC MONTHNAME
- functions, ODBC DAYNAME
- ODBC scalar functions
- functions, ODBC MINUTE
- functions, ODBC DAYOFWEEK
- QUARTER ODBC function
- DAYOFYEAR ODBC function
- functions, ODBC WEEK
- HOUR ODBC function
ms.assetid: a0df1ac2-6699-4ac0-8f79-f362f23496f1
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b248e52c25e3c4a7cdbb0e52b1df50623e048189
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="odbc-scalar-functions-transact-sql"></a>ODBC 标量函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  你可以使用[ODBC 标量函数](http://go.microsoft.com/fwlink/?LinkID=88579)中[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 这些语句由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 解释。 它们可以用在存储过程和用户定义函数中。 这些函数包括字符串函数、数值函数、时间函数、日期函数、时间间隔函数和系统函数。  
  
## <a name="usage"></a>用法  
 `SELECT {fn <function_name> [ (<argument>,....n) ] }`  
  
## <a name="functions"></a>函数  
 以下各表列出了未在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中重复的 ODBC 标量函数。  
  
### <a name="string-functions"></a>字符串函数  
  
|函数|Description|  
|--------------|-----------------|  
|BIT_LENGTH( string_exp ) (ODBC 3.0)|返回字符串表达式的长度（以位为单位）。<br /><br /> 它不只适用于字符串数据类型， 因此不会将 string_exp 隐式转换为字符串，而是会返回提供给它的任何数据类型的（内部）大小。|  
|CONCAT( string_exp1,string_exp2) (ODBC 1.0)|返回一个表示将 string_exp2 连接到 string_exp1 的结果的字符串。 生成的字符串依赖于 DBMS。 例如，如果 string_exp1 所表示的列包含一个 NULL 值，则 DB2 将返回 NULL，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回非 NULL 的字符串。|  
|OCTET_LENGTH( string_exp ) (ODBC 3.0)|返回字符串表达式的长度（以字节为单位）。 结果为不小于位数除以 8 所得数的最小整数。<br /><br /> 它不只适用于字符串数据类型， 因此不会将 string_exp 隐式转换为字符串，而是会返回提供给它的任何数据类型的（内部）大小。|  
  
### <a name="numeric-function"></a>数值函数  
  
|函数|Description|  
|--------------|-----------------|  
|TRUNCATE( numeric_exp, integer_exp) (ODBC 2.0)|返回截断到小数点右侧 integer_exp 位置的 numeric_exp。 如果 integer_exp 为负，numeric_exp 截断为 &#124; integer_exp &#124;小数点的左侧位置。|  
  
### <a name="time-date-and-interval-functions"></a>时间、日期和时间间隔函数  
  
|函数|Description|  
|--------------|-----------------|  
|CURRENT_DATE( ) (ODBC 3.0)|返回当前日期。|  
|CURDATE( ) (ODBC 3.0)|返回当前日期。|  
|CURRENT_TIME`[( time-precision )]` (ODBC 3.0)|返回当前本地时间。 time-precision 参数确定返回值的秒精度。|  
|CURTIME() (ODBC 3.0)|返回当前本地时间。|  
|DAYNAME( date_exp ) (ODBC 2.0)|返回一个字符串，其中包含 date_exp 的日部分的特定于数据源的日名称（例如，对于使用英语的数据源， 返回 Sunday 到 Saturday 或 Sun. 到 Sat.； 对于使用德语的数据源，返回 Sonntag 到 Samstag）。|  
|DAYOFMONTH( date_exp ) (ODBC 1.0)|根据 date_exp 中的月份字段返回该月的该日，返回值为 1 到 31 范围内的整数。|  
|DAYOFWEEK( date_exp ) (ODBC 1.0)|根据 date_exp 中的周字段返回该周的该日，返回值为 1 到 7 范围内的整数值，其中 1 表示星期天。|  
|HOUR( time_exp ) (ODBC 1.0)|根据 time_exp 中的小时字段返回该小时，返回值为 0 到 23 范围内的整数值。|  
|MINUTE( time_exp ) (ODBC 1.0)|根据 time_exp 中的分钟字段返回该分钟，返回值为 0 到 59 范围内的整数值。|  
|SECOND( time_exp ) (ODBC 1.0)|根据 time_exp 中的秒数字段返回该秒数，返回值为 0 到 59 范围内的整数值。|  
|MONTHNAME( date_exp ) (ODBC 2.0)|返回一个字符串，其中包含 date_exp 的月份部分的特定于数据源的该月份的名称（例如，对于使用英语的数据源，返回 January 到 December 或 Jan. 到 Dec.；对于使用德语的数据源，返回 Januar 到 Dezember）。|  
|QUARTER( date_exp ) (ODBC 1.0)|返回 date_exp 中的该季度，返回值为 1 到 4 范围内的整数值，其中 1 表示 1 月 1 日到 3 月 31 日。|  
|WEEK( date_exp ) (ODBC 1.0)|根据 date_exp 中的星期字段返回该年的该周，返回值为 1 到 53 范围内的整数值。|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-an-odbc-function-in-a-stored-procedure"></a>A. 在存储过程中使用 ODBC 函数  
 下例在存储过程中使用了 ODBC 函数：  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn OCTET_LENGTH( @string_exp )};  
```  
  
### <a name="b-using-an-odbc-function-in-a-user-defined-function"></a>B. 在用户定义函数中使用 ODBC 函数  
 下例在用户定义函数中使用了 ODBC 函数：  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn OCTET_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length.');  
--Returns 38  
  
```  
  
### <a name="c-using-an-odbc-functions-in-select-statements"></a>C. 在 SELECT 语句中使用 ODBC 函数  
 下面的 SELECT 语句使用了 ODBC 函数：  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
SELECT {fn OCTET_LENGTH( @string_exp )};  
-- Returns 38  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn TRUNCATE( 100.123456, 4)};  
-- Returns 100.123400  
SELECT {fn CURRENT_DATE( )};  
-- Returns 2007-04-20  
SELECT {fn CURRENT_TIME(6)};  
-- Returns 10:27:11.973000  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-an-odbc-function-in-a-stored-procedure"></a>D. 在存储过程中使用 ODBC 函数  
 下例在存储过程中使用了 ODBC 函数：  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn BIT_LENGTH( @string_exp )};  
```  
  
### <a name="e-using-an-odbc-function-in-a-user-defined-function"></a>E. 在用户定义函数中使用 ODBC 函数  
 下例在用户定义函数中使用了 ODBC 函数：  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn BIT_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length in bits.');  
--Returns 432  
  
```  
  
### <a name="f-using-an-odbc-functions-in-select-statements"></a>F. 在 SELECT 语句中使用 ODBC 函数  
 下面的 SELECT 语句使用了 ODBC 函数：  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn CURRENT_DATE( )};  
-- Returns todays date  
SELECT {fn CURRENT_TIME(6)};  
-- Returns the time  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  




