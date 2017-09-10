---
title: "集 QUOTED_IDENTIFIER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 02/03/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c6ba7962a9721dad3c3f043f960c72f718f6062
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遵从关于引号分隔标识符和文字字符串的 ISO 规则。 由双引号分隔的标识符可以是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留关键字，也可以包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符语法约定通常不允许的字符。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET QUOTED_IDENTIFIER { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET QUOTED_IDENTIFIER ON   
```  
  
## <a name="remarks"></a>注释  
 当 SET QUOTED_IDENTIFIER 为 ON 时，标识符可以由双引号分隔，而文字必须由单引号分隔。 当 SET QUOTED_IDENTIFIER 为 OFF 时，标识符不可加引号，且必须符合所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符规则。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。 文字可以由单引号或双引号分隔。  
  
 当 SET QUOTED_IDENTIFIER 为 ON（默认值）时，由双引号分隔的所有字符串都被解释为对象标识符。 因此，加引号的标识符不必符合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符规则。 它们可以是保留关键字，并且可以包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符中通常不允许的字符。 不能使用双引号分隔文字字符串表达式，而必须用单引号括住文字字符串。 如果单引号 () 是一部分的文字字符串，它可以表示由两个单引号 (**"**)。 当对数据库中的对象名使用保留关键字时，SET QUOTED_IDENTIFIER 必须为 ON。  
  
 当 SET QUOTED_IDENTIFIER 为 OFF 时，表达式中的文字字符串可以由单引号或双引号分隔。 如果文字字符串由双引号分隔，则可以在字符串中包含嵌入式单引号，如省略号。  
  
 当在计算列或索引视图上创建或更改索引时，SET QUOTED_IDENTIFIER 必须为 ON。 如果 SET QUOTED_IDENTIFIER 为 OFF，则计算列或索引视图上带索引的表上的 CREATE、UPDATE、INSERT 和 DELETE 语句将失败。 对计算列所需的 SET 选项设置的索引的视图和索引的详细信息，请参阅"当你使用 SET 语句的注意事项"中[SET 语句 &#40;Transact SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 在创建筛选索引，SET QUOTED_IDENTIFIER 必须为 ON。  
  
 在调用 XML 数据类型方法时，SET QUOTED_IDENTIFIER 必须为 ON。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动设置 QUOTED_IDENTIFIER 为 ON 时连接。 这可以在 ODBC 数据源、ODBC 连接特性或 OLE DB 连接属性中进行配置。 对来自 DB-Library 应用程序的连接，SET QUOTED_IDENTIFIER 默认设置为 OFF。  
  
 创建表时，即使此时将 QUOTED IDENTIFIER 选项设置为 OFF，该选项在表的元数据中仍始终存储为 ON。  
  
 创建存储过程时，将捕获 SET QUOTED_IDENTIFIER 和 SET ANSI_NULLS 设置，并用于该存储过程的后续调用。  
  
 在存储过程内执行 SET QUOTED_IDENTIFIER 时，其设置不更改。  
  
 当 SET ANSI_DEFAULTS 为 ON 时，将启用 SET QUOTED_IDENTIFIER。  
  
 SET QUOTED_IDENTIFIER 还与 ALTER DATABASE 的 QUOTED_IDENTIFIER 设置相对应。 有关数据库设置的详细信息，请参阅[ALTER DATABASE &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET QUOTED_IDENTIFIER 是在分析时生效，并且只影响分析过程中，不会执行查询。  
  
 对于顶层的即席批处理分析开始使用适用于 QUOTED_IDENTIFIER 会话的当前设置。  分析批处理 SET QUOTED_IDENTIFIER 任何匹配项将更改从该点的分析行为，并将保存该会话的设置。  因此分析和执行批处理后，将根据批处理中的最后一个匹配的 SET QUOTED_IDENTIFIER 设置会话的 QUOTED_IDENTIFER 设置。  
 静态 SQL 存储过程中的进行分析 QUOTED_IDENTIFIER 设置使用有效的创建或更改存储的过程的批处理。  SET QUOTED_IDENTIFIER 为静态 SQL 存储过程的正文中出现无效。  
  
 使用 sp_executesql 或 exec （） 的嵌套批处理分析开始使用该会话的 QUOTED_IDENTIFIER 设置。  如果在存储过程是嵌套的批处理的分析将使用存储过程的 QUOTED_IDENTIFIER 设置启动。  分析嵌套的批处理 SET QUOTED_IDENTIFIER 的任何匹配项将更改从该点的分析行为，但会话的 QUOTED_IDENTIFIER 设置将不会更新。  
  
 使用方括号， **[**和**]**、 来分隔标识符不受 QUOTED_IDENTIFIER 设置。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';  
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';  
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;  
  
```  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. 使用加引号的标识符设置和保留字对象名  
 以下示例显示 `SET QUOTED_IDENTIFIER` 设置必须为 `ON`，而且表名内的关键字必须在双引号内，才能创建和使用具有保留关键字名称的对象。  
  
```  
SET QUOTED_IDENTIFIER OFF  
GO  
-- An attempt to create a table with a reserved keyword as a name  
-- should fail.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Will succeed.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SELECT "identity","order"   
FROM "select"  
ORDER BY "order";  
GO  
  
DROP TABLE "SELECT";  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. 使用加单引号和双引号的标识符设置  
 以下示例显示将 `SET QUOTED_IDENTIFIER` 设置为 `ON` 和 `OFF` 时，在字符串表达式中使用单引号和双引号的方式。  
  
```  
SET QUOTED_IDENTIFIER OFF;  
GO  
USE AdventureWorks2012;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'Test')  
   DROP TABLE dbo.Test;  
GO  
USE AdventureWorks2012;  
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;  
GO  
  
-- Literal strings can be in single or double quotation marks.  
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");  
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');  
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');  
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');  
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");  
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Strings inside double quotation marks are now treated   
-- as object names, so they cannot be used for literals.  
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');  
GO  
  
-- Object identifiers do not have to be in double quotation marks  
-- if they are not reserved keywords.  
SELECT ID, String   
FROM dbo.Test;  
GO  
  
DROP TABLE dbo.Test;  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `ID          String`  
  
 `----------- ------------------------------`  
  
 `1           'Text in single quotes'`  
  
 `2           'Text in single quotes'`  
  
 `3           Text with 2 '' single quotes`  
  
 `4           "Text in double quotes"`  
  
 `5           "Text in double quotes"`  
  
 `6           Text with 2 "" double quotes`  
  
 `7           Text with a single ' quote`  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE (Transact-SQL)](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [sp_rename &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)  
  
  

