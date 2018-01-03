---
title: "项目设置 （转换） (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f459472409e9fc85322aca5067d0953bd24831a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-conversion-db2tosql"></a>项目设置 （转换） (DB2ToSQL)
转换页**项目设置**对话框中包含自定义如何 SSMA 将转换到 DB2 语法的设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法。  
  
转换窗格位于**项目设置**和**默认项目设置**对话框：  
  
-   若要对指定的所有的 SSMA 项目设置**工具**菜单上，单击**默认项目设置**，选择为其设置所需查看或更改，不再是迁移项目类型**迁移目标版本**下拉列表，然后单击**常规**中左窗格中，然后单击底部**转换**。  
  
-   若要对指定为当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**常规**中左窗格中，然后单击底部**转换**。  
  
## <a name="conversion-messages"></a>转换消息  
  
### <a name="generate-messages-about-issues-applied"></a>生成有关应用的问题的消息  
指定是否 SSMA 在转换过程将生成信息性消息，将它们显示在输出窗格中，并将它们添加到转换后的代码。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**否  
  
**完整模式：**否  
  
## <a name="miscellaneous-options"></a>其他选项  
  
### <a name="cast-rownum-expressions-as-integers"></a>强制转换为整数的 ROWNUM 表达式  
当 SSMA 转换 ROWNUM 表达式时，它将表达式转换为 TOP 子句，作为表达式的开头。 下面的示例演示 ROWNUM DB2 删除语句中：  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
下面的示例显示得到的[!INCLUDE[tsql](../../includes/tsql_md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
顶部需要 TOP 子句表达式计算结果为整数。 如果为负整数，该语句将产生错误。  
  
-   如果你选择**是**，SSMA 将强制转换为整数表达式。  
  
-   如果你选择**否**，SSMA 会将所有非整数表达式标记为转换后的代码中出现错误。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/完整模式：**否  
  
**开放式模式：**是  
  
### <a name="default-schema-mapping"></a>默认架构映射  
此设置指定如何 DB2 架构映射到 SQL Server 架构。 在此设置中有两个选项：  
  
1.  **到数据库的架构：**在此模式下 DB2 架构 sch1 将映射到 SQL Server 数据库 sch1 中的 dbo SQL Server 架构的默认情况下。  
  
2.  **架构与架构：**在此模式下 DB2 架构 sch1 将映射到连接对话框中提供的默认 SQL Server 数据库中的 sch1 SQL Server 架构的默认情况下。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**到数据库的架构  
  
### <a name="conversion-ways-of-merge-statement"></a>MERGE 语句的转换方法  
  
-   如果你选择**使用插入、 更新 DELETE 语句**、 SSMA 将合并语句转换为 INSERT、 UPDATE、 DELETE 语句。  
  
-   如果你选择**使用 MERGE 语句**，SSMA 将合并语句转换为在 MERGE 语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!WARNING]  
> 此项目设置选项是仅适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014年。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**使用合并语句  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>将使用默认自变量的子程序的调用转换  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函数不支持函数调用中省略的参数。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函数和过程不支持作为默认参数值的表达式。  
  
-   如果你选择**是**和函数调用省略参数，SSMA 将插入关键字**默认**到函数并在正确的位置的调用。 然后，它会将标记调用具有一条警告。  
  
-   如果你选择**否**，SSMA 会将标记为错误的函数调用。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-count-function-to-countbig"></a>将 COUNT 函数转换为 COUNT_BIG  
如果计数函数很可能返回值大于 2147483647，即 2<sup>31</sup>-1，则应将函数转换到 COUNT_BIG。  
  
-   如果你选择**是**，SSMA 会将所有使用计数都转换为 COUNT_BIG。  
  
-   如果你选择**否**，函数将保持为计数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果该函数返回一个值大于 2，将返回错误<sup>31</sup>-1。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/完整模式：**是  
  
**开放式模式：**否  
  
### <a name="convert-forall-statement-to-while-statement"></a>将 FORALL 语句转换为 WHILE 语句  
定义如何 SSMA 将处理 FORALL 循环上 PL/SQL 集合元素。  
  
-   如果你选择**是**，SSMA 创建 WHILE 循环集合元素为逐个检索到的位置。  
  
-   如果你选择**否**，SSMA 使用 nodes （） 方法从集合中生成行集，并将其用作单个表。 这是更高效，但使输出代码可读性较差。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**否  
  
**完整模式：**是  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>使用 SET NULL 引用操作于列的转换外键不为 NULL  
DB2，可以创建外键约束，其中一个设置为 NULL 的操作无法可能执行，因为被引用列中不允许使用 null 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允许此类外的密钥配置。  
  
-   如果你选择**是**，SSMA 将生成如下所示 DB2，引用操作，但你将需要在加载到约束之前进行手动更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 例如，你可以选择 NO ACTION，而不是设置为 NULL。  
  
-   如果你选择**否**，约束将标记为错误。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**否  
  
### <a name="convert-function-calls-to-procedure-calls"></a>将为过程调用的函数调用转换  
某些 DB2 函数定义为自治事务，或包含不会在中有效的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在这些情况下，SSMA 创建过程和函数，则该过程的包装器。 转换后的函数调用的实现过程。  
  
SSMA 可以将对包装函数的调用转换为对该过程的调用。 这将更具可读性的代码，并可以提高性能。 但是，上下文不始终允许它;例如，你不能选择列表中的函数调用的过程调用替换。 SSMA 具有几个选项，以涵盖的常见情况：  
  
-   如果你选择**始终**，SSMA 尝试将包装函数调用转换为过程调用。 如果当前上下文不允许此转换，则生成一条错误消息。 这样一来，不包括函数调用会保留在生成的代码。  
  
-   如果你选择**尽可能**，SSMA 执行移动到过程调用仅当函数具有输出参数。 当不能移动操作时，将删除参数的输出属性。 在所有其他情况下 SSMA 离开函数调用。  
  
-   如果你选择**从不**，SSMA 将保留所有作为函数调用的函数调用。 有时由于性能原因此选择可能是不可接受。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic/完整模式：**尽可能  
  
### <a name="convert-lock-table-statements"></a>转换锁 TABLE 语句  
SSMA 可以将很多锁表语句转换为表提示。 SSMA 不能转换包含分区，分区，任何锁 TABLE 语句@dblink，和 NOWAIT 子句，并将标记此类语句与转换错误消息。  
  
-   如果你选择**是**，SSMA 会将支持的锁定 TABLE 语句转换为表提示。  
  
-   如果你选择**否**，SSMA 会将标记与转换错误消息的所有锁 TABLE 语句。  
  
下表显示如何 SSMA 将转换 DB2 锁定模式：  
  
|||  
|-|-|  
|DB2 的锁模式|SQL Server 表提示|  
|行共享|ROWLOCK HOLDLOCK|  
|独占的行|ROWLOCK，XLOCK，HOLDLOCK|  
|共享更新 = 行共享|ROWLOCK HOLDLOCK|  
|共享|TABLOCK HOLDLOCK|  
|排他共享行|TABLOCK，XLOCK，HOLDLOCK|  
|独占|TABLOCKX HOLDLOCK|  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>将转换为 REF CURSOR OUT 参数打开 FOR 语句  
在 DB2，打开 FOR 语句可用于返回的结果与 OUT 参数类型 REF CURSOR 的子程序集。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，存储的过程直接返回 SELECT 语句的结果。  
  
SSMA 可以将很多打开 FOR 语句转换为 SELECT 语句。  
  
-   如果你选择**是**，SSMA 将打开 FOR 语句转换为的 SELECT 语句，返回的结果集向客户端。  
  
-   如果你选择**否**，SSMA 将生成一条错误消息，在转换后的代码，并在输出窗格中。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>将记录转换为离职变量的列表  
SSMA 可以将 DB2 记录转换到分隔变量和具有特定结构的 XML 变量。  
  
-   如果你选择**是**，SSMA 将记录转换为尽可能离职变量的列表。  
  
-   如果你选择**否**，SSMA 转换到 XML 变量中具有特定结构记录。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTR 函数将调用转换为子字符串函数调用  
SSMA 可以转换到 DB2 SUBSTR 函数调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**子字符串**函数调用，具体取决于参数的数目。 如果 SSMA 不能转换 SUBSTR 函数调用，或不支持参数的数目，SSMA 会将 SUBSTR 函数调用转换为自定义的 SSMA 函数调用。  
  
-   如果你选择**是**，SSMA 会将转换使用三个参数转换的 SUBSTR 函数调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**子字符串**。 其他 SUBSTR 函数将转换为调用自定义的 SSMA 函数。  
  
-   如果你选择**否**，SSMA 会将 SUBSTR 函数调用转换为自定义的 SSMA 函数调用。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**是  
  
**完整模式：**否  
  
### <a name="convert-subtypes"></a>将子类型转换  
SSMA 可以将两种方式的 PL/SQL 子类型转换：  
  
-   如果你选择**是**，将创建 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用户定义类型从子类型，并将其用于此子类型的每个变量。  
  
-   如果你选择**否**，SSMA 将替换的子类型与基础类型的所有源声明并将结果转换像往常一样。 在这种情况下，在中不创建任何其他类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**否  
  
### <a name="convert-synonyms"></a>将同义词转换  
以下的 DB2 对象同义词可以迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
-   表和对象表  
  
-   视图和对象视图  
  
-   存储的过程和函数  
  
-   具体化的视图  
  
可通过对对象的直接引用替换为以下的 DB2 对象的同义词：  
  
-   序列  
  
-   包  
  
-   Java 类架构对象  
  
-   用户定义的对象类型  
  
无法迁移其他同义词。 SSMA 将生成同义词和使用该同义词的所有引用的错误消息。  
  
-   如果你选择**是**，将创建 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同义词和根据上一个列表直接对象引用。  
  
-   如果你选择**否**，SSMA 将创建此处列出的所有同义词的直接对象引用。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-tochardate-format"></a>转换时出现 TO_CHAR （日期，格式）  
SSMA 可以将 DB2 TO_CHAR(date, format) 转换 sysdb 数据库中的过程。  
  
-   如果你选择**使用 TO_CHAR_DATE 函数**，SSMA 转换为 TO_CHAR_DATE 函数使用英语语言的转换时出现 TO_CHAR （日期，格式）。  
  
-   如果你选择**使用 TO_CHAR_DATE_LS 函数 （NLS 小心）**，SSMA 转换为 TO_CHAR_DATE_LS 函数使用的会话语言进行转换时出现 TO_CHAR （日期，格式）  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**使用 TO_CHAR_DATE 函数  
  
**完整模式：**使用 TO_CHAR_DATE_LS 函数 （NLS 小心）  
  
### <a name="convert-transaction-processing-statements"></a>转换事务处理语句  
SSMA 可转换 DB2 事务处理语句：  
  
-   如果你选择**是**，SSMA 将转换到 DB2 事务处理语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语句。  
  
-   如果你选择**否**，SSMA 标记的事务处理视为转换错误的语句。  
  
> [!NOTE]  
> DB2 隐式打开事务。 若要模拟此行为上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必须 BEGIN TRANSACTION 语句手动添加想您启动的事务。 或者，你可以在你的会话开始执行 SET IMPLICIT_TRANSACTIONS ON 命令。 转换与自治事务子例程时，SSMA 将自动添加 SET IMPLICIT_TRANSACTIONS ON。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>模拟 DB2 ORDER BY 子句中的 null 行为  
NULL 值进行排序以不同方式在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和 DB2:  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]为 NULL 的值为顺序列表中的最小的值。 在按升序排列的列表中，NULL 值将出现第一个。  
  
-   在 DB2，NULL 值是经过排序的列表中的最高值。 默认情况下，NULL 值显示升序顺序列表中最后一个。  
  
-   DB2 中具有 null 值第一个和最后一个 NULL 子句，从而使你可以更改如何 DB2 订单 null 值。  
  
通过检查 NULL 值，SSMA 可模拟 DB2 的 ORDER BY 行为。 它然后首先的 NULL 值排序在指定的顺序和订单中的其他值。  
  
-   如果你选择**是**，SSMA 会将转换中一种方法，它们模拟 DB2 的 ORDER BY 行为的 DB2 语句。  
  
-   如果你选择**否**，SSMA 将忽略 DB2 规则并生成一条错误消息，当它遇到 null 值第一个和最后一个 NULL 子句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**否  
  
**完整模式：**是  
  
### <a name="emulate-row-count-exceptions-in-select"></a>模拟中选择的行计数异常  
如果带 INTO 子句的 SELECT 语句不返回任何行，DB2 引发 NO_DATA_FOUND 异常。 如果语句返回两个或多个行，则 TOO_MANY_ROWS 在引发异常。 中的转换后的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不会引发任何异常，如果从一个不同的行计数。  
  
-   如果你选择**是**，SSMA 在每个 SELECT 语句后添加对 sysdb 过程 db_error_exact_one_row_check 调用。 此过程，以模拟 NO_DATA_FOUND 和 TOO_MANY_ROWS 异常。 这是默认值，它允许重现 DB2 行为尽可能接近。 你应始终选择**是**如果源代码处理这些错误的异常处理程序。 请注意，如果 SELECT 语句发生在用户定义函数内，此模块将转换为存储过程，因为执行存储的过程引发异常不是与兼容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函数上下文。  
  
-   如果你选择**否**，将生成任何异常。 SSMA 将转换的用户定义函数，并且你要让其继续中的函数时非常有用的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="generate-error-for-dbmssqlparse"></a>为 DBMS_SQL 生成错误。分析  
  
-   如果你选择**错误**，SSMA 生成转换 DBMS_SQL 错误。分析。  
  
-   如果你选择**警告**，SSMA 生成在转换 DBMS_SQL 的警告。分析。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**错误  
  
### <a name="generate-rowid-column"></a>生成 ROWID 列  
SSMA 创建中的表时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，它可以创建 ROWID 列。 迁移数据时，每个行获取 newid （） 函数生成的一个新的唯一标识符值。  
  
-   如果你选择**是**，在所有表上创建 ROWID 列和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]生成 Guid，如插入值。 始终选择**是**如果你打算使用 SSMA 测试人员。  
  
-   如果你选择**否**，ROWID 列不会添加到表。  
  
-   **添加包含触发器的表的 ROWID 列**为包含触发器的表添加 ROWID。  
  
> [!WARNING]  
> 对于 SQL Server 2005、 SQL Server 2008 和 SQL Server 2012 和 2014年的默认设置是**包含触发器的表的添加 ROWID 列**。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/Optimistic 模式：**添加包含触发器的表的 ROWID 列  
  
**完整模式：**是  
  
### <a name="generate-unique-index-on-rowid-column"></a>生成 ROWID 列上的唯一索引  
指定或不 SSMA 是否生成 ROWID 生成列上的唯一索引列。 如果将选项设置为"是"，生成唯一索引函数，如果设置为"否"，在 ROWID 列上无法生成唯一索引。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="local-modules-conversion"></a>本地模块转换  
定义的嵌套的 DB2 子程序 （在独立存储过程或函数中声明） 转换的类型。  
  
-   如果你选择**内联**，其正文将替换为嵌套的子程序调用。  
  
-   如果你选择**存储过程**、 嵌套的子程序将转换为 SQL Server 存储过程中，和它的调用将被替换为在此过程调用。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**内联  
  
### <a name="use-isnull-in-string-concatenation"></a>在字符串串联中使用 ISNULL  
DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]字符串串联时将包含 NULL 值时返回不同的结果。 DB2 将如空字符集的 NULL 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]返回 NULL。  
  
-   如果你选择**是**，SSMA DB2 串联字符 (|) 替换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]串联字符 （+）。 SSMA 还检查 NULL 值的串联两端的表达式。  
  
-   如果你选择**否**，SSMA 替换串联字符，但不会检查 NULL 值。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
### <a name="use-isnull-in-replace-function-calls"></a>在替换函数调用中使用 ISNULL  
ISNULL 语句替换函数调用中使用，以模拟 DB2 行为。 存在为此设置提供了以下选项：  
  
-   YES  
  
-   是  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**否  
  
**完整模式：**是  
  
### <a name="use-isnull-in-concat-function-calls"></a>在 CONCAT 函数调用中使用 ISNULL  
ISNULL 语句 CONCAT 函数调用中使用，以模拟 DB2 行为。 存在为此设置提供了以下选项：  
  
-   YES  
  
-   是  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**否  
  
**完整模式：**是  
  
### <a name="use-native-convert-function-when-possible"></a>使用本机 convert 函数尽可能  
  
-   如果你选择**是**，SSMA 将时出现 TO_CHAR （日期，格式） 转换为本机的转换函数在可能的情况。  
  
-   如果你选择**否**，SSMA 将时出现 TO_CHAR （日期，格式） 转换成 TO_CHAR_DATE 或 TO_CHAR_DATE_LS （它由定义"将转换 TO_CHAR(date, format)"选项）。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式模式：**是  
  
**完整模式：**否  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>使用选择...对于 XML 转换时选择...INTO 记录变量  
指定是否生成 XML 结果集时选择到记录变量。  
  
-   如果你选择**是**，SELECT 语句将返回 XML。  
  
-   如果你选择**否**，SELECT 语句返回的结果集。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**否  
  
## <a name="returning-clause-conversion"></a>返回子句转换  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>将 DELETE 语句中的 RETURNING 子句转换为输出  
DB2 作为一种方法以立即获取已删除的值提供的 RETURNING 子句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]OUTPUT 子句中提供该功能。  
  
-   如果你选择**是**，SSMA 将转换为输出子句的 DELETE 语句中的 RETURNING 子句。 由于对表的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 DB2。  
  
-   如果你选择**否**，SSMA 将生成 SELECT 语句用于检索返回的值的 DELETE 语句之前。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>将在 INSERT 语句中的 RETURNING 子句转换为输出  
DB2 作为一种方法以立即获取插入的值提供的 RETURNING 子句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]OUTPUT 子句中提供该功能。  
  
-   如果你选择**是**，SSMA 会将 INSERT 语句中的 RETURNING 子句转换为输出。 由于对表的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 DB2。  
  
-   如果你选择**否**，SSMA 它们模拟 DB2 功能插入，然后从引用表中选择值。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>将 UPDATE 语句中的 RETURNING 子句转换为输出  
DB2 作为一种方法以立即获取更新后的值提供的 RETURNING 子句。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]OUTPUT 子句中提供该功能。  
  
-   如果你选择**是**，SSMA 将转换为输出子句的 UPDATE 语句中的 RETURNING 子句。 由于对表的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 DB2。  
  
-   如果你选择**否**，SSMA 将生成更新语句来检索返回值后的 SELECT 语句。  
  
当选择中的转换模式**模式**框，SSMA 适用以下设置：  
  
**默认/开放式/完整模式：**是  
  
## <a name="sequence-conversion"></a>序列转换  
  
### <a name="convert-sequence-generator"></a>转换序列生成器  
在 DB2，可以使用序列生成的唯一标识符。  
  
SSMA 可以将序列转换为以下。  
  
-   使用 SQL Server 序列生成器 （此选项才可用时将转换为 SQL Server 2012 和 SQL Server 2014）。  
  
-   使用 SSMA 序列生成器。  
  
-   使用列标识。  
  
将转换为 SQL Server 2012 或 SQL Server 2014 时的默认选项是使用 SQL Server 序列生成器。 但是，SQL Server 2012 和 SQL Server 2014 不支持获取 （如，DB2 序列 currval 方法） 的当前序列值。 请参阅以获取有关迁移 DB2 序列 currval 方法指导的 SSMA 团队博客网站。  
  
SSMA 还提供了一个选项以将 DB2 序列转换为 SSMA 序列仿真程序。 这是默认选项，当你将转换为 SQL Server 2012 之前  
  
最后，还可以将转换序列分配给 SQL Server 标识值的表中的列。 必须指定到标识列在 DB2 上序列之间的映射**表**选项卡  
  
### <a name="convert-currval-outside-triggers"></a>将 CURRVAL 转换外部触发器  
仅当转换序列生成器设置为时才可见**使用列标识**。 因为 DB2 序列是独立于表的对象，使用序列的多个表使用触发器生成并插入新的序列值。 SSMA 会注释掉这些语句，或将其标记为错误时注释扩展也会生成错误。  
  
-   如果你选择**是**，SSMA 会将标记所有引用以之外上转换后的触发器序列 CURRVAL 伴有警告。  
  
-   如果你选择**否**，SSMA 会将标记为外部上转换后的触发器序列 CURRVAL 出现错误的所有引用。  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考 &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
