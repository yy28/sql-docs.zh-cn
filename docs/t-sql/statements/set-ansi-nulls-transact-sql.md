---
title: "设置 ANSI_NULLS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 285803fe112cc0370b8af6049f48846c7ba55cab
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  指定在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中与 Null 值一起使用等于 (=) 和不等于 (<>) 比较运算符时采用符合 ISO 标准的行为。  
  
> [!IMPORTANT]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中，ANSI_NULLS 将始终为 ON，将该选项显式设置为 OFF 的任何应用程序都将产生错误。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_NULLS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_NULLS ON;  
```  
  
## <a name="remarks"></a>注释  
 当 SET ANSI_NULLS 为 ON，可使用 WHERE 的 SELECT 语句*column_name* = **NULL**即使有中的 null 值，则返回零行*column_name*。 使用 WHERE 的 SELECT 语句*column_name* <> **NULL**即使有中的非 null 值，则返回零行*column_name*。  
  
 当 SET ANSI_NULLS 为 OFF 时，等于 (=) 和不等于 (<>) 比较运算符不遵守 ISO 标准。 使用 WHERE 的 SELECT 语句*column_name* = **NULL**返回中有 null 值的行*column_name*。 使用 WHERE 的 SELECT 语句*column_name* <> **NULL**返回的列中具有非 null 值的行。 此外，使用 WHERE 的 SELECT 语句*column_name* <> *XYZ_value*返回所有行不*XYZ_value*和不为 NULL。  
  
 当 SET ANSI_NULLS 为 ON 时，所有对 null 值的比较均取值为 UNKNOWN。 当 SET ANSI_NULLS 为 OFF 时，如果数据值为 NULL，则所有数据对空值的比较将取值为 TRUE。 如果未指定 SET ANSI_NULLS，则应用当前数据库的 ANSI_NULLS 选项设置。 有关 ANSI_NULLS 数据库选项的详细信息，请参阅[ALTER DATABASE &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 仅当某个比较操作数是值为 NULL 的变量或文字 NULL 时，SET ANSI_NULLS ON 才会影响比较。 如果比较双方是列或复合表达式，则该设置不会影响比较。  
  
 为使脚本按预期运行，不管 ANSI_NULLS 数据库选项或 SET ANSI_NULLS 的设置如何，请在可能包含空值的比较中使用 IS NULL 和 IS NOT NULL。  
  
 在执行分布式查询时应将 SET ANSI_NULLS 设置为 ON。  
  
 对计算列或索引视图创建或更改索引时，SET ANSI_NULLS 也必须为 ON。 如果 SET ANSI_NULLS 为 OFF，则针对表（包含计算列或索引视图的索引）的 CREATE、UPDATE、INSERT 和 DELETE 语句将失败。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回一个错误消息，该错误消息会列出所有违反所需值的 SET 选项。 另外，在执行 SELECT 语句时，如果 SET ANSI_NULLS 为 OFF，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将忽略计算列或视图的索引值并解析选择操作，就好像表或视图没有这样的索引一样。  
  
> [!NOTE]  
>  ANSI_NULLS 是在处理计算列或索引视图的索引时必须设置为所需值的七个 SET 选项之一。 还必须将选项 ANSI_PADDING、ANSI_WARNINGS、ARITHABORT、QUOTED_IDENTIFIER 和 CONCAT_NULL_YIELDS_NULL 设置为 ON，而必须将 NUMERIC_ROUNDABORT 设置为 OFF。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动设置 ANSI_NULLS 为 ON 时连接。 该设置可以在 ODBC 数据源、ODBC 连接属性或 OLE DB 连接属性（它们在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之前在应用程序中设置）中进行配置。 SET ANSI_NULLS 的默认值为 OFF。  
  
 当 SET ANSI_DEFAULTS 为 ON 时，将启用 SET ANSI_NULLS。  
  
 SET ANSI_NULLS 的设置是在执行或运行时设置，而不是在分析时设置。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例使用等于 (`=`) 和不等于 (`<>`) 比较运算符对表中的 `NULL` 值和非空值进行比较。 该示例还演示`IS NULL`不受`SET ANSI_NULLS`设置。  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40;等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [如果...其他 &#40;Transact SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60; &#62;&#40;不等于 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE (Transact-SQL)](../../t-sql/language-elements/while-transact-sql.md)  
  
  

