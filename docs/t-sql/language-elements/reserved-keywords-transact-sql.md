---
title: 保留关键字 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc0390a01bec10b58ed29d1824e8d0b482e78358
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68091776"
---
# <a name="reserved-keywords-transact-sql"></a>保留关键字 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将保留关键字用于定义、操作和访问数据库。 保留关键字是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言语法的一部分，用于分析和理解 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和批处理。 尽管在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留关键字作为标识符和对象名在语法上是可行的，但规定只能使用分隔标识符。  
  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Azure SQL 数据仓库保留关键字。  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|和|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|复制|  
|备份|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|BY|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|关机|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|返回页首|  
|CURSOR|NOT|TRAN|  
|DATABASE|Null|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPTION|USER|  
|DROP|或|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|WITH|  
|在运行 CREATE 语句前执行|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||
  
下表列出了 Azure SQL 数据仓库  专用的保留关键字。

|||
|-|-|
|LABEL ||
  
 此外，ISO 标准定义了保留关键字列表。 不要使用 ISO 保留关键字作为对象名和标识符。 ODBC 保留关键字列表（如下表所示）与 ISO 保留关键字列表相同。  
  
> [!NOTE]  
>  ISO 标准保留关键字有时可能比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 限制更多，有时则更少。 例如，ISO 保留关键字列表包含 **INT**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不必将此区分为保留关键字。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留关键字可用作数据库或数据库对象（如表、列、视图等）的标识符或名称。 使用带引号的标识符或分隔标识符。 不限制将保留关键字用作变量和存储过程参数的名称。  
  
## <a name="odbc-reserved-keywords"></a>ODBC 保留关键字  
 保留了下列关键字以用于 ODBC 函数调用。 这些关键字根本不约束 SQL 语法；然而，为确保与支持核心 SQL 语法的驱动程序兼容，应用程序应避免使用这些关键字。  
  
 下面是当前的 ODBC 保留关键字列表。  
  
||||  
|-|-|-|  
|**ABSOLUTE**|**EXEC**|**OVERLAPS**|  
|**ACTION**|**EXECUTE**|**PAD**|  
|**ADA**|**EXISTS**|**PARTIAL**|  
|**ADD**|EXTERNAL |**PASCAL**|  
|**ALL**|**EXTRACT**|**POSITION**|  
|**ALLOCATE**|**FALSE**|**PRECISION**|  
|**ALTER**|**FETCH**|**PREPARE**|  
|**AND**|**FIRST**|**PRESERVE**|  
|**ANY**|**FLOAT**|**PRIMARY**|  
|**ARE**|**FOR**|**PRIOR**|  
|**AS**|**FOREIGN**|**PRIVILEGES**|  
|**ASC**|**FORTRAN**|**PROCEDURE**|  
|**ASSERTION**|**FOUND**|**PUBLIC**|  
|**AT**|**FROM**|**READ**|  
|**AUTHORIZATION**|**FULL**|**REAL**|  
|**AVG**|**GET**|**REFERENCES**|  
|**BEGIN**|**GLOBAL**|**RELATIVE**|  
|**BETWEEN**|**GO**|**RESTRICT**|  
|**BIT**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**BOTH**|**GROUP**|**ROLLBACK**|  
|**BY**|**HAVING**|**ROWS**|  
|**CASCADE**|HOUR |**SCHEMA**|  
|**CASCADED**|**IDENTITY**|**SCROLL**|  
|**CASE**|**IMMEDIATE**|**SECOND**|  
|**CAST**|**IN**|**SECTION**|  
|**CATALOG**|**INCLUDE**|**SELECT**|  
|**CHAR**|**INDEX**|**SESSION**|  
|**CHAR_LENGTH**|**INDICATOR**|**SESSION_USER**|  
|**CHARACTER**|**INITIALLY**|**SET**|  
|**CHARACTER_LENGTH**|**INNER**|**SIZE**|  
|**CHECK**|**INPUT**|**SMALLINT**|  
|**CLOSE**|**INSENSITIVE**|**SOME**|  
|**COALESCE**|**INSERT**|**SPACE**|  
|**COLLATE**|**INT**|**SQL**|  
|**COLLATION**|**INTEGER**|**SQLCA**|  
|**COLUMN**|**INTERSECT**|**SQLCODE**|  
|**COMMIT**|**INTERVAL**|**SQLERROR**|  
|**CONNECT**|**INTO**|**SQLSTATE**|  
|**CONNECTION**|**IS**|**SQLWARNING**|  
|**CONSTRAINT**|**ISOLATION**|**SUBSTRING**|  
|**CONSTRAINTS**|**JOIN**|**SUM**|  
|**CONTINUE**|**KEY**|**SYSTEM_USER**|  
|**CONVERT**|**LANGUAGE**|**TABLE**|  
|**CORRESPONDING**|**LAST**|**TEMPORARY**|  
|**COUNT**|**LEADING**|**THEN**|  
|**CREATE**|**LEFT**|**TIME**|  
|**CROSS**|**LEVEL**|**TIMESTAMP**|  
|**CURRENT**|**LIKE**|TIMEZONE_HOUR |  
|**CURRENT_DATE**|**LOCAL**|TIMEZONE_MINUTE |  
|**CURRENT_TIME**|**LOWER**|TO |  
|**CURRENT_TIMESTAMP**|**MATCH**|**TRAILING**|  
|**CURRENT_USER**|**MAX**|**TRANSACTION**|  
|**CURSOR**|**MIN**|**TRANSLATE**|  
|**DATE**|MINUTE |**TRANSLATION**|  
|**DAY**|**MODULE**|**TRIM**|  
|**DEALLOCATE**|**MONTH**|**TRUE**|  
|**DEC**|**NAMES**|**UNION**|  
|**DECIMAL**|**NATIONAL**|**UNIQUE**|  
|**DECLARE**|**NATURAL**|UNKNOWN |  
|**DEFAULT**|**NCHAR**|**UPDATE**|  
|**DEFERRABLE**|**NEXT**|**UPPER**|  
|**DEFERRED**|**NO**|**USAGE**|  
|**DELETE**|**NONE**|**USER**|  
|**DESC**|**NOT**|**USING**|  
|**DESCRIBE**|**NULL**|**VALUE**|  
|**DESCRIPTOR**|**NULLIF**|**VALUES**|  
|**DIAGNOSTICS**|**NUMERIC**|**VARCHAR**|  
|**DISCONNECT**|**OCTET_LENGTH**|**VARYING**|  
|**DISTINCT**|**OF**|**VIEW**|  
|**DOMAIN**|**ON**|**WHEN**|  
|**DOUBLE**|**ONLY**|**WHENEVER**|  
|**DROP**|**OPEN**|**WHERE**|  
|**ELSE**|**OPTION**|**WITH**|  
|**END**|**OR**|**WORK**|  
|**END-EXEC**|**ORDER**|**WRITE**|  
|**ESCAPE**|**OUTER**|**YEAR**|  
|**EXCEPT**|**OUTPUT**|**ZONE**|  
|**EXCEPTION**|||  
  
## <a name="future-keywords"></a>将来的关键字  
 下列关键字可能会在将来的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中保留使用，作为将来要实现的新功能。 注意，不要使用这些关键字作为标识符。  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE|  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|SPACE|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|月|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|新增功能|TIMESTAMP|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|是|TIMEZONE_MINUTE|  
|CURRENT_PATH|无|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|值|  
|DEPTH|PAD|VAR_POP|  
|DEREF|参数|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|real|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|FLOAT|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|FREE|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|年|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>另请参阅  
 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
