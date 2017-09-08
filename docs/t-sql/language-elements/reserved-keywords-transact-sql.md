---
title: "保留关键字 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efaa21099f422ae812168561351a359fc89f8e0d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="reserved-keywords-transact-sql"></a>保留的关键字的 Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将保留关键字用于定义、操作和访问数据库。 保留关键字是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言语法的一部分，用于分析和理解 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和批处理。 尽管在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留关键字作为标识符和对象名在语法上是可行的，但规定只能使用分隔标识符。  
  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留关键字。  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|和|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|Replication|  
|BACKUP|FROM|RESTORE|  
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
|COLUMN|Insert|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
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
|DATABASE|NULL|TRANSACTION|  
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
|DOUBLE|OPTION|User|  
|DROP|或|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|替换为|  
|在运行 CREATE 语句前执行|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 此外，ISO 标准定义了保留关键字列表。 不要使用 ISO 保留关键字作为对象名和标识符。 ODBC 保留关键字列表（如下表所示）与 ISO 保留关键字列表相同。  
  
> [!NOTE]  
>  ISO 标准保留关键字有时可能比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 限制更多，有时则更少。 例如，ISO 保留的关键字列表包含**INT**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不必将此区分为保留关键字。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留关键字可用作数据库或数据库对象（如表、列、视图等）的标识符或名称。 使用带引号的标识符或分隔标识符。 不限制将保留关键字用作变量和存储过程参数的名称。  
  
## <a name="odbc-reserved-keywords"></a>ODBC 保留关键字  
 保留了下列关键字以用于 ODBC 函数调用。 这些关键字根本不约束 SQL 语法；然而，为确保与支持核心 SQL 语法的驱动程序兼容，应用程序应避免使用这些关键字。  
  
 下面是当前的 ODBC 保留关键字列表。  
  
||||  
|-|-|-|  
|**绝对**|**EXEC**|**重叠**|  
|**操作**|**EXECUTE**|**填充**|  
|**ADA**|**存在**|**部分**|  
|**添加**|EXTERNAL|**PASCAL**|  
|**ALL**|**提取**|**位置**|  
|**分配**|**FALSE**|**精度**|  
|**ALTER**|**提取**|**准备**|  
|**AND**|**第一个**|**保留**|  
|**任何**|**FLOAT**|**PRIMARY**|  
|**是**|**有关**|**之前**|  
|**AS**|**外**|**权限**|  
|**ASC**|**FORTRAN**|**过程**|  
|**断言**|**找到**|**公共**|  
|**在**|**FROM**|**读取**|  
|**授权**|**FULL**|**实际**|  
|**AVG**|**获取**|**引用**|  
|**BEGIN**|**全局**|**相对**|  
|**BETWEEN**|**转到**|**限制**|  
|**位**|**转到**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**同时**|**组**|**回滚**|  
|**通过**|**无**|**行**|  
|**级联**|**小时**|**架构**|  
|**级联**|**标识**|**滚动**|  
|**用例**|**立即**|**第二个**|  
|**强制转换**|**IN**|**部分**|  
|**目录**|**包括**|**SELECT**|  
|**CHAR**|**索引**|**会话**|  
|**CHAR_LENGTH**|**指示器**|**SESSION_USER**|  
|**字符**|**最初**|**设置**|  
|**CHARACTER_LENGTH**|**内部**|**大小**|  
|**检查**|**输入**|**SMALLINT**|  
|**关闭**|**不区分大小写**|**某些**|  
|**将合并**|**INSERT**|**空间**|  
|**逐份打印**|**INT**|**SQL**|  
|**排序规则**|**整数**|**SQLCA**|  
|**列**|**相交**|**SQLCODE**|  
|**提交**|**间隔**|**SQLERROR**|  
|**连接**|**到**|**SQLSTATE**|  
|**连接**|**IS**|**SQLWARNING**|  
|**约束**|**隔离**|**SUBSTRING**|  
|**约束**|**联接**|**总和**|  
|**继续**|**密钥**|**SYSTEM_USER**|  
|**将转换**|**LANGUAGE**|**表**|  
|**相对应**|**最后一个**|**临时**|  
|**计数**|**前导**|**然后**|  
|**创建**|**LEFT**|**时间**|  
|**跨**|**级别**|**时间戳**|  
|**当前**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**本地**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**较低**|**自**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**尾随**|  
|**CURRENT_USER**|**最大值**|**事务**|  
|**光标**|**最小值**|**翻译**|  
|**日期**|**分钟**|**转换**|  
|**一天**|**模块**|**TRIM**|  
|**解除分配**|**月**|**TRUE**|  
|**年 12 月**|**名称**|**联合**|  
|**十进制**|**国家/地区**|**唯一**|  
|**声明**|**自然**|**未知**|  
|**默认值**|**NCHAR**|**UPDATE**|  
|**可以推迟**|**下一步**|**上限**|  
|**延迟**|**不**|**使用情况**|  
|**DELETE**|**NONE**|**用户**|  
|**DESC**|**NOT**|**使用**|  
|**描述**|**NULL**|**VALUE**|  
|**描述符**|**NULLIF**|**值**|  
|**诊断**|**数值**|**VARCHAR**|  
|**断开连接**|**OCTET_LENGTH**|**不同的**|  
|**非重复**|**的**|**视图**|  
|**域**|**ON**|**当**|  
|**双**|**仅**|**每当**|  
|**拖放**|**打开**|**WHERE**|  
|**其他**|**选项**|**与**|  
|**END**|**OR**|**工作**|  
|**结束 EXEC**|**顺序**|**写入**|  
|**转义**|**外部**|**年**|  
|**除非**|**输出**|**区域**|  
|**异常**|||  
  
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
|ASSERTION|整数|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|在|INTERVAL|SEARCH|  
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
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|timestamp|  
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
|DEFERRED|OUTPUT|Value|  
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
|FILTER|REAL|XMLEXISTS|  
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
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>另请参阅  
 [设置 QUOTED_IDENTIFIER &#40;Transact SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
