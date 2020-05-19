---
title: 内存中 OLTP 不支持的 Transact-SQL 构造 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 95b657064f36045dfd0d916c24097b81c0e44867
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718856"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>内存中 OLTP 不支持的 Transact-SQL 构造
  内存优化的表和本机编译的存储过程不支持基于磁盘的表和解释的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程所支持的完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 外围应用。 尝试使用某个不支持的功能时，服务器返回错误。  
  
 错误消息文本提及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的类型（例如功能、操作、选项）以及功能或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 关键字的名称。 大多数不支持的功能将返回错误 10794，并带有错误消息文本，指示不支持该功能。 下表列出可在错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
 有关针对内存优化表和编辑编译的存储过程的支持的功能的详细信息，请参阅：  
  
-   [本机编译存储过程的迁移问题](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [对内存中 OLTP 的 Transact-SQL 支持](transact-sql-support-for-in-memory-oltp.md)  
  
-   [支持的 SQL Server 功能](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [本机编译的存储过程](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>使用内存中 OLTP 的数据库  
 下表列出了涉及内存中 OLTP 数据库的错误的消息文本中可能出现的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字。  
  
|类型|“属性”|解决方法|  
|----------|----------|----------------|  
|选项|AUTO_CLOSE|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持数据库选项 AUTO_CLOSE=ON。|  
|选项|ATTACH_REBUILD_LOG|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持 CREATE 数据库选项 ATTACH_REBUILD_LOG。|  
|功能|DATABASE SNAPSHOT|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持创建数据库快照。|  
|功能|使用 sync_method“database snapshot”或“database snapshot character”进行复制|具有 MEMORY_OPTIMIZED_DATA 文件组的数据库不支持使用 sync_method“database snapshot”或“database snapshot character”进行复制。|  
|功能|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB 跳过数据库中的内存优化表。<br /><br /> 对内存优化表执行 DBCC CHECKTABLE 将失败。|  
  
## <a name="memory-optimized-tables"></a>内存优化表  
 下表列出可在涉及内存优化表的错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
|类型|“属性”|解决方法|  
|----------|----------|----------------|  
|功能|ON|内存优化的表不能放置在文件组或分区方案上。 从 `CREATE TABLE` 语句删除 ON 子句。|  
|数据类型|数据类型名称**|不支持所示的数据类型。 使用支持的数据类型之一替换该类型。 有关详细信息，请参阅[支持的数据类型](supported-data-types-for-in-memory-oltp.md)。|  
|功能|计算列|内存优化的表不支持计算列。 从 `CREATE TABLE` 语句删除计算列。|  
|功能|复制|内存优化表不支持复制。|  
|功能|FILESTREAM|内存优化的表列不支持 FILESTREAM 存储。 从列定义中删除 `FILESTREAM` 关键字。|  
|功能|SPARSE|内存优化的表列不能定义为 SPARSE。 从列定义中删除 `SPARSE` 关键字。|  
|功能|ROWGUIDCOL|内存优化的表列不支持选项 ROWGUIDCOL。 从列定义中删除 `ROWGUIDCOL` 关键字。|  
|功能|FOREIGN KEY|内存优化的表不支持 FOREIGN KEY 约束。 从表定义中删除该约束。<br /><br /> 有关如何缓解不支持约束的信息，请参阅[迁移 Check 和 Foreign Key 约束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|Feature|CHECK|内存优化的表不支持 CHECK 约束。 从表定义中删除该约束。<br /><br /> 有关如何缓解不支持约束的信息，请参阅[迁移 Check 和 Foreign Key 约束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|功能|UNIQUE|内存优化的表不支持 UNIQUE 约束。 从表定义中删除该约束。<br /><br /> 有关如何缓解不支持约束的信息，请参阅[迁移 Check 和 Foreign Key 约束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。|  
|Feature|COLUMNSTORE|内存优化的表不支持 COLUMNSTORE 索引。 改为指定 NONCLUSTERED 或 NONCLUSTERED HASH 索引。|  
|Feature|聚集索引|指定非聚集索引。 在主键索引的情况下，务必指定 `PRIMARY KEY NONCLUSTERED [HASH]`。|  
|Feature|非 1252 代码页|具有数据类型 `char` 和 `varchar` 的内存优化表中的列必须使用代码页 1252。 请使用 n(var)char 替代 (var)char，或使用具有代码页 1252 的排序规则（例如 Latin1_General_BIN2）。 有关详细信息，请参阅 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|事务中的 DDL|在用户事务的上下文中无法创建或删除内存优化的表和本机编译的存储过程。 在执行 CREATE 或 DROP 语句前不要启动事务并确保会话设置 IMPLICIT_TRANSACTIONS 为 OFF。|  
|功能|DDL 触发器|如果存在该 DDL 操作的服务器或数据库触发器，则无法创建或删除内存优化的表和本机编译的存储过程。 在 CREATE/DROP TABLE 和 CREATE/DROP PROCEDURE 时删除服务器和数据库触发器。|  
|功能|EVENT NOTIFICATION|如果存在该 DDL 操作的服务器或数据库事件通知，则无法创建或删除内存优化的表和本机编译的存储过程。 在 CREATE TABLE 或 DROP TABLE 和 CREATE PROCEDURE 或 DROP PROCEDURE 时删除服务器和数据库事件通知。|  
|功能|FileTable|无法将内存优化的表创建为文件表。 从 `AS FileTable` 语句删除参数 `CREATE TABLE`。|  
|操作|更新主键列|无法更新内存优化的表和表类型中的主键列。 如果需要更新主键，请删除旧的行并插入包含更新的主键的新行。|  
|操作|CREATE INDEX|必须使用 `CREATE TABLE` 语句内联指定内存优化的表的索引。 要将索引添加到内存优化的表，请删除并重新创建该表，包括指定新索引。|  
|操作|ALTER TABLE|不支持更改内存优化的表。 删除表并使用更新的表定义重新创建它。|  
|操作|CREATE FULLTEXT INDEX|内存优化的表不支持全文检索。|  
|操作|架构更改|内存优化的表和本机编译的存储过程不支持架构更改，例如 `sp_rename`。<br /><br /> 尝试作出架构更改（如重命名表）将产生错误 12320。内存优化的表不支持需要更改架构版本的操作（例如，重命名）。<br /><br /> 要更改架构，请删除表或过程并使用更新的定义重新创建它。|  
|操作|CREATE TRIGGER|不支持内存优化的表的触发器。|  
|操作|TRUNCATE TABLE|内存优化的表不支持 TRUNCATE 操作。 若要从表中删除所有行，请使用表删除所有行， `DELETE FROM` *table*或删除并重新创建该表。|  
|操作|ALTER AUTHORIZATION|不支持更改现有内存优化的表或本机编译的存储过程的所有者。 请删除并重新创建该表或过程来更改所有权。|  
|操作|ALTER SCHEMA|不支持更改现有内存优化的表或本机编译的存储过程的架构。 若要更改架构，请删除再重新创建表或过程。|  
|操作|DBCC CHECKTABLE|内存优化的表不支持 DBCC CHECKTABLE。|  
|功能|ANSI_PADDING OFF|创建内存优化的表或本机编译的存储过程时会话选项 `ANSI_PADDING` 必须为 ON。 在运行 CREATE 语句前执行 `SET ANSI_PADDING ON`。|  
|选项|DATA_COMPRESSION|内存优化的表不支持数据压缩。 从表定义中删除该选项。|  
|功能|DTC|不能从分布式事务访问内存优化的表和本机编译的存储过程。 请改用 SQL 事务。|  
|功能|多个活动的结果集 (MARS)|内存优化表不支持多个活动结果集 (MARS)。 此错误还可能指示使用了链接服务器。 链接服务器可以使用 MARS。 内存优化表不支持链接服务器。 请直接连接到内存优化的表所在的服务器和数据库。|  
|操作|内存优化的表作为 MERGE 的目标|内存优化的表不能是 `MERGE` 操作的目标。 请改用 `INSERT`、`UPDATE` 或 `DELETE` 语句。|  
  
## <a name="indexes-on-memory-optimized-tables"></a>内存优化的表的索引  
 下表列出可在涉及内存优化表的索引错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
|类型|“属性”|解决方法|  
|----------|----------|----------------|  
|功能|筛选索引|内存优化的表不支持筛选的索引。 从索引定义中省略 `WHERE` 子句。|  
|功能|UNIQUE|内存优化的表不支持唯一索引。 从索引定义中删除参数 `UNIQUE`。|  
|功能|可为 Null 的列|内存优化表的索引键中的所有列必须指定为 `NOT NULL`。 包含具有索引键中所有列的 `NOT NULL` 约束。|  
|功能|非 bin2 排序规则|必须使用 BIN2 排序规则声明内存优化的索引键中的所有字符列。 使用 `COLLATE` 子句在列定义中设置排序规则。 有关详细信息，请参阅 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|包含列|指定包含列不是内存优化表所必需的。 内存优化表的所有列都隐式包含在每个内存优化索引中。|  
|操作|ALTER INDEX|不支持更改内存优化的表的索引。 请删除该表并使用更新的索引定义重新创建它。|  
|操作|DROP INDEX|不支持删除内存优化的表的索引。 请删除该表并使用所需的索引重新创建它。|  
|索引选项|*索引选项*|内存优化的表的索引不支持所示的索引选项。 从索引定义中删除该选项。|  
  
## <a name="nonclustered-hash-indexes"></a>非聚集哈希索引  
 下表列出可在涉及非聚集哈希索引的错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
|类型|“属性”|解决方法|  
|----------|----------|----------------|  
|选项|ASC/DESC|非聚集哈希索引不排序。 从索引键定义中删除关键字 `ASC` 和 `DESC`。|  
  
## <a name="natively-compiled-stored-procedures"></a>本机编译的存储过程  
 下表列出可在涉及本机编译存储过程的错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
|类型|功能|解决方法|  
|----------|-------------|----------------|  
|功能|内联表变量|不能使用变量声明内联声明表类型。 必须使用 `CREATE TYPE` 语句显式声明表类型。|  
|Feature|游标|本机编译的存储过程不支持游标。<br /><br /> -从客户端执行该过程时，请使用 RPC 而非游标 API。 对于 ODBC，避免 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句 `EXECUTE`，直接指定过程的名称。<br /><br /> -从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理或其他存储过程执行该过程时，请避免将游标用于本机编译的存储过程。<br /><br /> -在创建本机编译的存储过程时，请使用基于集的逻辑或循环来创建本机编译的存储过程，而不是使用游标 `WHILE` 。|  
|Feature|非常量参数默认值|将默认值与本机编译的存储过程参数一起使用时，这些值必须为常量。 从参数声明中删除所有通配符。|  
|功能|EXTERNAL|无法本机编译 CLR 存储过程。 从 CREATE PROCEDURE 语句中删除 AS EXTERNAL 子句或 NATIVE_COMPILATION 选项。|  
|功能|带编号的存储过程|不能对本机编译的存储过程编号。 `;`从语句中删除该*数字* `CREATE PROCEDURE` 。|  
|功能|多行插入 .。。VALUES 语句|在本机编译的存储过程中无法使用同一 `INSERT` 语句插入多行。 为每行创建 `INSERT` 语句。|  
|功能|公用表表达式 (CTE)|本机编译的存储过程中不支持公用表表达式 (CTE)。 重写查询。|  
|功能|子查询|不支持子查询（查询嵌套在另一个查询中）。 重写查询。|  
|功能|COMPUTE|不支持 `COMPUTE` 子句。 从查询中删除它。|  
|Feature|SELECT INTO|`INTO` 语句不支持 `SELECT` 子句。 将查询重写为 `INSERT INTO` *Table* `SELECT` 。|  
|功能|OUTPUT|不支持 `OUTPUT` 子句。 从查询中删除它。|  
|功能|不完整的插入列列表|在 `INSERT` 语句中，必须为表中的所有列指定值。|  
|函数|*Function*|本机编译的存储过程中不支持内置函数。 从存储过程中删除该函数。 有关支持的内置函数的详细信息，请参阅[本机编译的存储过程](../in-memory-oltp/natively-compiled-stored-procedures.md)。|  
|Feature|CASE|本机编译的存储过程内的查询中不支持 `CASE` 语句。 创建每个情况的查询。 有关详细信息，请参阅[实现 CASE 语句](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)。|  
|功能|用户定义的函数|不能在本机编译的存储过程中使用用户定义函数。 从过程定义中删除对该函数的引用。|  
|功能|用户定义聚合|不能在本机编译的存储过程中使用用户定义的聚合函数。 从过程中删除对该函数的引用。|  
|功能|浏览模式元数据|本机编译的存储过程不支持浏览模式元数据。 确保将会话选项 `NO_BROWSETABLE` 设置为 OFF。|  
|功能|带 FROM 子句的 DELETE|表源在本机编译存储过程中的 `FROM` 语句不支持 `DELETE` 子句。<br /><br /> 在指示要执行删除操作的表时，支持带 `DELETE` 子句的 `FROM`。|  
|功能|带 FROM 子句的 UPDATE|本机编译的存储过程中的 `FROM` 语句不支持 `UPDATE` 子句。|  
|功能|临时程序|临时存储过程无法进行本机编译。 请创建永久的本机编译存储过程或临时的解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。|  
|隔离级别|READ UNCOMMITTED|本机编译的存储过程不支持隔离级别 READ UNCOMMITTED。 请使用支持的隔离级别，如 SNAPSHOT。|  
|隔离级别|READ COMMITTED|本机编译的存储过程不支持隔离级别 READ UNCOMMITTED。 请使用支持的隔离级别，如 SNAPSHOT。|  
|功能|临时表|tempdb 中的表不能在本机编译的存储过程中使用。 请使用表变量或 DURABILITY=SCHEMA_ONLY 的内存优化表。|  
|功能|MARS|本机编译的存储过程不支持多个活动结果集 (MARS)。 此错误还可能指示使用了链接服务器。 链接服务器可以使用 MARS。 本机编译的存储过程不支持链接服务器。 请直接连接到本机编译的存储过程所在的服务器和数据库。|  
|功能|DTC|不能从分布式事务访问内存优化的表和本机编译的存储过程。 请改用 SQL 事务。|  
|功能|非 bin2 排序规则|对本机编译的存储过程中的字符串执行比较、排序和其他操作需要使用 BIN2 排序规则。 使用 COLLATE 子句或使用具有合适排序规则的列和变量。 有关详细信息，请参阅 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。|  
|功能|按照 SC 排序规则截断字符串。|采用 `_SC` 排序规则的字符串使用 UTF-16 编码。 将 n(var)char 值转换具有更短长度的 n(var)char 值涉及截断。 这对于本机编译的存储过程中的 UTF-16 值不受支持。 避免 UTF-16 字符串的截断。|  
|功能|EXECUTE WITH RECOMPILE|本机编译的存储过程不支持选项 `WITH RECOMPILE`。|  
|功能|LEN 和 SUBSTRING 的参数采用 SC 排序规则|采用 _SC 排序规则的字符串使用 UTF-16 编码。 在本机编译的存储过程内使用内置函数 LEN 和 SUBSTRING 时，这些函数不支持 UTF-16 编码。 使用其他排序规则或避免使用这些函数。|  
|功能|从专用管理员连接执行。|不能从专用管理员连接 (DAC) 执行本机编译的存储过程。 请改用常规连接。|  
|操作|ALTER PROCEDURE|不能更改本机编译的存储过程。 要更改该过程定义，请删除并重新创建存储过程。|  
|操作|保存点|不能从具有活动保存点的事务调用本机编译的存储过程。 从事务中删除该保存点。|  
|操作|ALTER AUTHORIZATION|不支持更改现有内存优化的表或本机编译的存储过程的所有者。 请删除并重新创建该表或过程来更改所有权。|  
|操作员|OPENROWSET|不支持此运算符。 从本机编译的存储过程中删除 `OPENROWSET`。|  
|操作员|OPENQUERY|不支持此运算符。 从本机编译的存储过程中删除 `OPENQUERY`。|  
|操作员|OPENDATASOURCE|不支持此运算符。 从本机编译的存储过程中删除 `OPENDATASOURCE`。|  
|操作员|OPENXML|不支持此运算符。 从本机编译的存储过程中删除 `OPENXML`。|  
|运算符|CONTAINSTABLE|不支持此运算符。 从本机编译的存储过程中删除 `CONTAINSTABLE`。|  
|运算符|FREETEXTTABLE|不支持此运算符。 从本机编译的存储过程中删除 `FREETEXTTABLE`。|  
|功能|表值函数|不能从本机编译的存储过程引用表值函数。 有可能解决此限制的一种方法是将表值函数中的逻辑添加到过程主体。|  
|运算符|CHANGETABLE|不支持此运算符。 从本机编译的存储过程中删除 `CHANGETABLE`。|  
|运算符|GOTO|不支持此运算符。 使用其他过程构造，如 WHILE。|  
|运算符|EXECUTE, INSERT EXEC|不支持嵌套本机编译的存储过程。 所需的操作可以内联指定作为存储过程定义的一部分。|  
|运算符|OFFSET|不支持此运算符。 从本机编译的存储过程中删除 `OFFSET`。|  
|运算符|UNION|不支持此运算符。 从本机编译的存储过程中删除 `UNION`。 可以使用表变量将几个结果集合并为单个结果集。|  
|运算符|INTERSECT|不支持此运算符。 从本机编译的存储过程中删除 `INTERSECT`。 在某些情况下，可以使用 INNER JOIN 获得相同的结果。|  
|运算符|EXCEPT|不支持此运算符。 从本机编译的存储过程中删除 `EXCEPT`。|  
|运算符|OUTER JOIN|不支持此运算符。 从本机编译的存储过程中删除 `OUTER JOIN`。 有关详细信息，请参阅[实现外部联接](implementing-an-outer-join.md)。|  
|运算符|APPLY|不支持此运算符。 从本机编译的存储过程中删除 `APPLY`。|  
|运算符|PIVOT|不支持此运算符。 从本机编译的存储过程中删除 `PIVOT`。|  
|运算符|UNPIVOT|不支持此运算符。 从本机编译的存储过程中删除 `UNPIVOT`。|  
|运算符|OR, IN|本机编译的存储过程中查询的 WHERE 子句中不支持 Disjunction (OR, IN)。 为每种情况创建查询。|  
|运算符|CONTAINS|不支持此运算符。 从本机编译的存储过程中删除 `CONTAINS`。|  
|运算符|FREETEXT|不支持此运算符。 从本机编译的存储过程中删除 `FREETEXT`。|  
|运算符|NOT|不支持此运算符。 从本机编译的存储过程中删除 `NOT`。 在某些情况下，可以使用不相等替换 `NOT`。 例如，可以使用 `NOT a=b` 替换 `a!=b`。|  
|运算符|TSEQUAL|不支持此运算符。 从本机编译的存储过程中删除 `TSEQUAL`。|  
|运算符|LIKE|不支持此运算符。 从本机编译的存储过程中删除 `LIKE`。|  
|运算符|NEXT VALUE FOR|不能在本机编译的存储过程内引用序列。 使用解释的 [!INCLUDE[tsql](../../includes/tsql-md.md)]获取值，然后将它传递到本机编译的存储过程。 有关详细信息，请参阅 [在内存优化表中实现 IDENTITY](implementing-identity-in-a-memory-optimized-table.md)。|  
|Set 选项|*option*|在本机编译的存储过程内无法更改 SET 选项。 可以使用 BEGIN ATOMIC 语句设置某些选项。 有关详细信息，请参阅 [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)中有关原子块的章节。|  
|操作数|TABLESAMPLE|不支持此运算符。 从本机编译的存储过程中删除 `TABLESAMPLE`。|  
|选项|RECOMPILE|在创建时编译本机编译的存储过程。 要重新编译本机编译的存储过程，请删除并重新创建它。 `RECOMPILE`从过程定义中删除。|  
|选项|ENCRYPTION|不支持此选项。 `ENCRYPTION`从过程定义中删除。|  
|选项|FOR REPLICATION|无法为复制创建本机编译的存储过程。 从过程定义中删除 `FOR REPLICATION`。|  
|选项|FOR XML|不支持此选项。 从本机编译的存储过程中删除 `FOR XML`。|  
|选项|FOR BROWSE|不支持此选项。 从本机编译的存储过程中删除 `FOR BROWSE`。|  
|联接提示|HASH、MERGE|本机编译的存储过程仅支持嵌套的循环联接。 不支持哈希和合并联接。 删除联接提示。|  
|查询提示|*查询提示*|此查询提示不位于本机编译的存储过程内。 有关支持的查询提示，请参阅[查询提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)。|  
|选项|DISTINCT|不支持此选项。 从本机编译的存储过程中的查询删除 `DISTINCT`。|  
|选项|PERCENT|`TOP` 子句不支持此选项。 从本机编译的存储过程中的查询删除 `PERCENT`。|  
|选项|WITH TIES|`TOP` 子句不支持此选项。 从本机编译的存储过程中的查询删除 `WITH TIES`。|  
|聚合函数|*聚合函数*|不支持此子句。 有关本机编译的存储过程中聚合函数的详细信息，请参阅 [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md)。|  
|排名函数|*排名函数*|本机编译的存储过程中不支持排名函数。 从过程定义中删除它们。|  
|函数|*Function*|不支持此函数。 从本机编译的存储过程中删除它。|  
|语句|*损益*|不支持此语句。 从本机编译的存储过程中删除它。|  
|功能|MIN 和 MAX 用于二进制和字符串|聚合函数 `MIN` 和 `MAX` 不能用于本机编译的存储过程中的字符和二进制字符串值。|  
|功能|不带聚合函数的 GROUP BY|在本机编译的存储过程中，当查询具有 `GROUP BY` 子句时，该查询也必须在 SELECT 或 HAVING 子句中使用聚合函数。 向查询中添加聚合函数。|  
|功能|GROUP BY ALL|在本机编译的存储过程中，不能将 ALL 与 GROUP BY 子句一起使用。 从 GROUP BY 子句中删除 ALL。|  
|功能|GROUP BY ()|不支持按空列表分组。 删除 GROUP BY 子句，或在分组列表中加入列。|  
|功能|ROLLUP|在本机编译的存储过程中，`ROLLUP` 不能与 `GROUP BY` 子句一起使用。 `ROLLUP`从过程定义中删除。|  
|功能|CUBE|在本机编译的存储过程中，`CUBE` 不能与 `GROUP BY` 子句一起使用。 `CUBE`从过程定义中删除。|  
|功能|GROUPING SETS|在本机编译的存储过程中，`GROUPING SETS` 不能与 `GROUP BY` 子句一起使用。 `GROUPING SETS`从过程定义中删除。|  
|功能|BEGIN TRANSACTION、COMMIT TRANSACTION 和 ROLLBACK TRANSACTION|使用 ATOMIC 块控制事务和错误处理。 有关详细信息，请参阅 [Atomic Blocks](atomic-blocks-in-native-procedures.md)。|  
|功能|内联表变量声明。|表变量必须引用显式定义的内存优化表类型。 应创建内存优化的表类型并将该类型用于变量声明，而不应在行内指定类型。|  
|功能|sp_recompile|不支持重新编译本机编译的存储过程。 删除并重新创建过程。|  
|功能|EXECUTE AS CALLER|必须有 `EXECUTE AS` 子句。 但不支持 `EXECUTE AS CALLER`。 使用 `EXECUTE AS OWNER` 、 `EXECUTE AS` *用户*或 `EXECUTE AS SELF` 。|  
|功能|基于磁盘的表|无法从本机编译的存储过程中访问基于磁盘的表。 从本机编译的存储过程中删除对基于磁盘的表的引用。 或者，将基于磁盘的表转换为内存优化的表。|  
|功能|视图|无法从本机编译的存储过程中访问视图。 不引用视图，改为引用底层基表。|  
|功能|表值函数|无法从本机编译的存储过程中访问表值函数。 从本机编译的存储过程中删除对表值函数的引用。|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>访问内存优化表的事务  
 下表列出可在涉及访问内存优化表的事务错误消息文本中显示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和关键字，以及用于解决问题的更正操作。  
  
|类型|“属性”|解决方法|  
|----------|----------|----------------|  
|功能|保存点|不支持在访问内存优化的表的事务中创建显式保存点。|  
|功能|绑定的事务|绑定的会话不能参与访问内存优化的表的事务。 在执行过程前不要绑定会话。|  
|功能|DTC|访问内存优化的表的事务不能是分布式事务。|  
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
