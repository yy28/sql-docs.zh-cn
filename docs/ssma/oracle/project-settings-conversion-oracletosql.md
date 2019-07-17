---
title: 项目设置 （转换） (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a98a5e07-eb5e-47b9-a6f2-e2cb3a18309c
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 5de646d21ddd9255b1b5bd72794635a1da37ef6c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266624"
---
# <a name="project-settings-conversion-oracletosql"></a>项目设置（转换）(OracleToSQL)
转换页**项目设置**对话框中包含自定义如何 SSMA 将转换到的 Oracle 语法设置的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法。  
  
转换窗格中现已推出**项目设置**并**默认项目设置**对话框：  
  
-   若要指定所有的 SSMA 项目的设置**工具**菜单上，单击**默认项目设置**，选择迁移项目类型设置为其所需查看或更改从**迁移目标版本**下拉列表，然后单击**常规**底部的左窗格中，然后单击**转换**。  
  
-   若要在指定的当前项目中，设置**工具**菜单上，单击**项目设置**，然后单击**常规**底部的左窗格中，然后单击**转换**。  
  
## <a name="conversion-messages"></a>转换消息  
  
|||  
|-|-|  
|术语|定义|  
|**生成有关应用的问题的消息**|指定是否 SSMA 在转换过程将生成信息性消息、 将它们显示在输出窗格中，并将它们添加到转换后的代码。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 否<br /><br />**完整模式：** 否|  
  
## <a name="miscellaneous-options"></a>其他选项  
  
|||  
|-|-|  
|术语|定义|  
|**强制转换为整数 ROWNUM 表达式**|当 SSMA 将转换 ROWNUM 表达式时，它将 TOP 子句后, 跟表达式转换为表达式。 下面的示例演示 ROWNUM Oracle 删除语句中：<br /><br />`DELETE FROM Table1`<br /><br />`WHERE ROWNUM < expression and Field1 >= 2`<br /><br />下面的示例显示了生成[!INCLUDE[tsql](../../includes/tsql-md.md)]:<br /><br />`DELETE TOP (expression-1)`<br /><br />`FROM Table1`<br /><br />`WHERE Field1>=2`<br /><br />顶部需要 TOP 子句表达式计算结果为整数。 如果为负整数，该语句将产生错误。<br /><br />如果选择**是**，SSMA 将强制转换为整数表达式。<br /><br />如果选择**否**，SSMA 会将所有非整数表达式标记为已转换的代码中的错误。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认值或全模式：** 否<br /><br />**乐观模式：** 是|  
|**默认架构映射**|此设置指定如何将 Oracle 架构映射到 SQL Server 架构。 此设置中提供了两个选项：<br /><br />**到数据库的架构：** 在此模式下的 Oracle 架构 sch1 将映射到 SQL Server 数据库 sch1' 中 'dbo' SQL Server 架构的默认情况下。<br /><br />**对架构的架构：** 在此模式下的 Oracle 架构 sch1 将映射到连接对话框中提供的默认 SQL Server 数据库中的 sch1 SQL Server 架构的默认情况下。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 到数据库的架构|  
|**MERGE 语句的转换方法**|如果选择**使用 INSERT、 UPDATE、 DELETE 语句**、 SSMA 合并语句转换为 INSERT、 UPDATE、 DELETE 语句。<br /><br />如果选择**使用 MERGE 语句**，SSMA 将 MERGE 语句中转换为合并语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />**注意：** 此项目设置选项是仅适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014年。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 使用 MERGE 语句|  
|**将调用转换为使用默认自变量的子程序**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函数不支持函数调用中省略的参数。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函数和过程不支持默认参数值的形式的表达式。<br /><br />如果选择**是**和函数调用省略了参数，SSMA 将插入关键字**默认**到函数并在正确的位置的调用。 然后，它会将标记为警告的调用。<br /><br />如果选择**否**，SSMA 会将标记为错误的函数调用。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**将 COUNT 函数转换为 COUNT_BIG**|如果 COUNT 函数可能会返回值大于 2147483647，即 2<sup>31</sup>-1，应将函数转换为 COUNT_BIG。<br /><br />如果选择**是**，SSMA 会将所有使用的计数都转换为 COUNT_BIG。<br /><br />如果选择**否**，函数将保持为计数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果该函数返回一个值大于 2，将返回错误<sup>31</sup>-1。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认值或全模式：** 是<br /><br />**乐观模式：** 否|  
|**FORALL 语句转换为 WHILE 语句**|定义如何 SSMA 将处理 FORALL 循环，对 PL/SQL 集合元素。<br /><br />如果选择**是**，SSMA 创建集合元素是逐个检索到的其中一个 WHILE 循环。<br /><br />如果选择**否**，SSMA 使用 nodes （） 方法从集合中生成行集，并将其用作单个表。 这是更有效，但可以输出代码可读性较差。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 否<br /><br />**完整模式：** 是|  
|**使用 SET NULL 引用操作上的列的转换外键不为 NULL**|Oracle 允许创建外键约束，其中 SET NULL 操作无法可能执行，因为被引用列中不允许 null 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许此类外的密钥配置。<br /><br />如果选择**是**，SSMA 将生成引用操作如下所示 Oracle，但将需要进行手动更改，然后加载到约束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，可以选择 NO ACTION，而不是设置为 NULL。<br /><br />如果选择**否**，该约束将被标记为错误。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 否|  
|**将转换为过程调用的函数调用**|某些 Oracle 函数定义为自治事务或包含不会在中有效的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在这些情况下，SSMA 创建过程和函数，则该过程的包装器。 转换后的函数调用的实现过程。<br /><br />SSMA 可以将对包装函数的调用转换为对该过程的调用。 这将提高代码可读性，并可以提高性能。 但是，上下文不总是允许它;例如，不能将选择列表中的函数调用的过程调用替换为。 SSMA 具有几个选项，以涵盖的常见用例：<br /><br />如果选择**始终为**，SSMA 尝试转换过程的调用包装器函数调用。 如果当前上下文不允许此转换，生成一条错误消息。 这样一来，不包括函数调用会保留在生成的代码。<br /><br />如果选择**尽可能**，SSMA 执行移动到过程调用仅当该函数具有输出参数。 不可能在移动时，会删除参数的输出属性。 在所有其他情况下 SSMA 离开函数调用。<br /><br />如果选择**从不**，SSMA 将保留为函数调用的所有函数调用。 有时选择此选项可能不可接受，由于性能方面的原因。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 在可能的情况|  
|**转换锁 TABLE 语句**|SSMA 可以将多个锁表语句转换为表提示。 SSMA 无法转换包含分区，子分区，任何锁表语句@dblink，和 NOWAIT 子句，并将标记此类语句转换错误消息。<br /><br />如果选择**是**，SSMA 会将受支持的锁表语句转换为表提示。<br /><br />如果选择**否**，SSMA 会将标记与转换错误消息的所有锁表语句。<br /><br />下表显示了 SSMA 将 Oracle 锁模式的转换：<br /><br />**Oracle 锁模式**<br /><br />行共享<br /><br />排他行<br /><br />共享更新 = 行共享<br /><br />共享<br /><br />共享<br /><br />排他<br /><br />**SQL Server 表提示**<br /><br />ROWLOCK HOLDLOCK<br /><br />ROWLOCK，XLOCK，HOLDLOCK<br /><br />ROWLOCK HOLDLOCK<br /><br />TABLOCK HOLDLOCK<br /><br />TABLOCK、 XLOCK，HOLDLOCK<br /><br />TABLOCKX HOLDLOCK<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**将转换为 REF CURSOR OUT 参数打开 FOR 语句**|在 Oracle 中，打开 FOR 语句可用于返回的结果与 OUT 参数类型 REF CURSOR 的子程序集。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，存储的过程直接返回 SELECT 语句的结果。<br /><br />SSMA 可以转换为多个打开 FOR 语句的 SELECT 语句。<br /><br />如果选择**是**，SSMA 将 SELECT 语句结果集返回到客户端转换为开放 FOR 语句。<br /><br />如果选择**否**，SSMA 将生成一条错误消息，在转换后的代码和输出窗格中。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**将记录转换为将变量的列表**|SSMA 可以将 Oracle 记录转换到分隔变量和具有特定结构的 XML 变量。<br /><br />如果选择**是**，SSMA 将记录转换为一系列分隔变量在可能的情况。<br /><br />如果选择**否**，SSMA 将记录转换为具有特定结构的 XML 变量。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**SUBSTR 函数将调用转换为的子字符串函数调用**|SSMA 可以转换到的 Oracle SUBSTR 函数调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**子字符串**函数调用，具体取决于参数的数目。 如果 SSMA 不能转换 SUBSTR 函数调用，或不支持的参数数目，SSMA 将转换为 SUBSTR 函数调用的自定义的 SSMA 函数调用。<br /><br />如果选择**是**，SSMA 会将使用到的三个参数的 SUBSTR 函数调用转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**的子字符串**。 将转换其他 SUBSTR 函数以调用自定义的 SSMA 函数。<br /><br />如果选择**否**，SSMA 将转换为 SUBSTR 函数调用的自定义的 SSMA 函数调用。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 是<br /><br />**完整模式：** 否|  
|**将子类型转换**|SSMA 可以转换在两种方法中的 PL/SQL 子类型：<br /><br />如果选择**是**，将创建 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义类型从子类型，并将其用于此子类型的每个变量。<br /><br />如果选择**否**，SSMA 将替换的子类型与基础类型的所有源声明并将结果转换像往常一样。 在这种情况下，在不创建任何其他类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 否|  
|**将同义词转换**|以下 Oracle 对象的同义词可以迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br />表和对象表<br /><br />视图和对象视图<br /><br />存储的过程和函数<br /><br />具体化的视图<br /><br />**以下的同义词**Oracle 对象可以替换为对对象的直接引用：<br /><br />序列<br /><br />包<br /><br />Java 类架构对象<br /><br />用户定义的对象类型<br /><br />不能迁移其他同义词。 SSMA 将生成同义词和使用该同义词的所有引用的错误消息。<br /><br />如果选择**是**，将创建 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同义词，并根据前面列表中的直接对象引用。<br /><br />如果选择**否**，SSMA 将创建此处列出的所有同义词的直接对象引用。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**转换 TO_CHAR （日期，格式）**|SSMA 可以转换为 Oracle TO_CHAR(date, format) sysdb 数据库中的过程。<br /><br />如果选择**使用 TO_CHAR_DATE 函数**，SSMA 将 TO_CHAR_DATE 函数使用的英语语言的转换转换为 TO_CHAR （日期，格式）。<br /><br />如果选择**使用 TO_CHAR_DATE_LS 函数 （NLS 护理）** ，SSMA 将转换 TO_CHAR_DATE_LS 函数使用的会话语言转换为 TO_CHAR （日期，格式）<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 使用 TO_CHAR_DATE 函数<br /><br />**完整模式：** 使用 TO_CHAR_DATE_LS 函数 （NLS 护理）|  
|**转换事务处理语句**|SSMA 可以转换 Oracle 事务处理语句：<br /><br />如果选择**是**，SSMA 将转换到的 Oracle 事务处理语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句。<br /><br />如果选择**否**，SSMA 将标记的事务处理转换错误的语句。<br /><br />**注意：** Oracle 将隐式打开事务。 若要模拟此行为在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必须 BEGIN TRANSACTION 语句手动添加要在事务启动。 或者，您可以在会话开始时执行 SET IMPLICIT_TRANSACTIONS ON 命令。 转换与自治事务的子例程时，SSMA 会自动添加 SET IMPLICIT_TRANSACTIONS ON。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**模拟在 ORDER BY 子句中的 Oracle null 行为**|NULL 值进行排序以不同的方式在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 Oracle:<br /><br />在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为 NULL 的值为有序列表中的最小值。 在升序的列表中，NULL 值将出现第一个。<br /><br />在 Oracle 中，NULL 值是有序列表中的最高值。 默认情况下，显示按升序顺序列表中最后一个 NULL 值。<br /><br />Oracle 中具有 null 值第一个和最后一个 null 值的子句，这样您就可以更改 Oracle 如何排序 null 值。<br /><br />SSMA 可以模拟 Oracle ORDER BY 行为，通过检查 NULL 值。 它然后首先通过顺序中指定的顺序和订单被其他值的 NULL 值。<br /><br />如果选择**是**，SSMA 将模拟 Oracle ORDER BY 行为的方式的 Oracle 语句转换。<br /><br />如果选择**否**，SSMA 将忽略 Oracle 规则，并生成一条错误消息时遇到的 null 值第一个和最后一个 null 值的子句。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 否<br /><br />**完整模式：** 是|  
|**模拟中选择的行计数异常**|如果带 INTO 子句的 SELECT 语句不返回任何行，Oracle 将引发 NO_DATA_FOUND 异常。 如果该语句返回两个或多个行，将引发 TOO_MANY_ROWS 异常。 中的已转换的语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会引发任何异常，如果从一个不同的行计数。<br /><br />如果选择**是**，SSMA 后每个 SELECT 语句添加到 sysdb 过程 db_error_exact_one_row_check 的调用。 此过程来模拟 NO_DATA_FOUND 和 TOO_MANY_ROWS 异常。 这是默认值，它允许重现 Oracle 行为尽可能接近。 您应始终选择**是**如果源代码具有处理这些错误的异常处理程序。 请注意，是否 SELECT 语句出现在用户定义函数内，此模块将转换为存储过程，因为在执行存储的过程并且引发异常不是与兼容[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函数上下文。<br /><br />如果选择**否**，会生成任何异常。 SSMA 将转换的用户定义函数和你要让其继续中的函数时，可以很有用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**为 DBMS_SQL 生成错误。分析**|如果选择**错误**，SSMA 生成转换 DBMS_SQL 处的错误。分析。<br /><br />如果选择**警告**，SSMA 生成在转换 DBMS_SQL 的警告。分析。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** Error|  
|**生成行 ID 列**|在 SSMA 中创建表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它可以创建行 ID 列。 当迁移数据时，每一行获取由 newid （） 函数生成一个新的唯一标识符值。<br /><br />如果选择**是**，行 ID 列创建的所有表上和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成 Guid，如插入值。 始终选择**是**如果想要使用 SSMA 测试人员。<br /><br />如果选择**否**，ROWID 列不会添加到表。<br /><br />**添加带触发器的表的行 ID 列**ROWID 添加为包含触发器的表。<br /><br />**注意：** 在 SQL Server 2005、 SQL Server 2008 和 SQL Server 2012 和 2014年的情况下的默认设置是**对于带触发器的表添加行 ID 列**。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 添加带触发器的表的行 ID 列<br /><br />**完整模式：** 是|  
|**生成行 ID 列的唯一索引**|指定是否 SSMA 是否生成唯一的索引列上生成的行 ID 列。 如果选项设置为"是"，生成唯一索引和唯一索引如果设置为"否"，不生成行 ID 列上。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**本地模块转换**|定义嵌套的 oracle （在独立存储过程或函数中声明） 的子程序转换的类型。<br /><br />如果选择**内联**，其正文将替换为嵌套的子程序的调用。<br /><br />如果选择**存储过程**、 嵌套的子程序将转换为 SQL Server 存储过程和其调用将替换为在此过程调用。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 内联|  
|**在字符串串联中使用 ISNULL**|Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]串联的字符串包括 NULL 值时返回不同结果。 Oracle 将空字符集等的 NULL 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回 NULL。<br /><br />如果选择**是**，SSMA 替换 Oracle 串联字符 (&#124;&#124;) 与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]串联字符 （+）。 SSMA 还会检查包含 NULL 值串联的两侧的表达式。<br /><br />如果选择**否**，SSMA 替换串联字符，但不会检查 NULL 值。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**在替换函数调用中使用 ISNULL**|替换为函数调用中使用 ISNULL 语句来模拟 Oracle 行为。 以下选项是存在此设置：<br /><br />是<br /><br />是<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 否<br /><br />**完整模式：** 是|  
|**CONCAT 函数调用中使用 ISNULL**|CONCAT 函数调用中使用 ISNULL 语句来模拟 Oracle 行为。 以下选项是存在此设置：<br /><br />是<br /><br />是<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 否<br /><br />**完整模式：** 是|  
|**使用本机的转换函数在可能的情况**|如果选择**是**，SSMA TO_CHAR （日期，格式） 将转换为本机的转换函数在可能的情况。<br /><br />如果选择**否**，SSMA 将 TO_CHAR_DATE 或 TO_CHAR_DATE_LS （由"转换 TO_CHAR(date, format)"选项已定义） 转换为 TO_CHAR （日期，格式）。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观模式：** 是<br /><br />**完整模式：** 否|  
|**使用 SELECT...FOR XML 转换时选择...INTO 记录变量**|指定是否生成 XML 结果集时选择到记录变量。<br /><br />如果选择**是**，SELECT 语句返回的 XML。<br /><br />如果选择**否**，SELECT 语句返回的结果集。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 否|  
  
## <a name="returning-clause-conversion"></a>返回子句转换  
  
|||  
|-|-|  
|术语|定义|  
|**将在 DELETE 语句中的 RETURNING 子句转换为输出**|Oracle 提供的 RETURNING 子句作为一种方法可立即获得已删除的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 OUTPUT 子句提供了此功能。<br /><br />如果选择**是**，SSMA 将转换为 DELETE 语句中的 RETURNING 子句的 OUTPUT 子句。 由于表上的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Oracle 中很多。<br /><br />如果选择**否**，SSMA 将生成 DELETE 语句来检索返回的值之前的 SELECT 语句。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**将在 INSERT 语句中的 RETURNING 子句转换为输出**|Oracle 提供的 RETURNING 子句作为一种方法可立即获得插入的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 OUTPUT 子句提供了此功能。<br /><br />如果选择**是**，SSMA 会将 INSERT 语句中的 RETURNING 子句转换为输出。 由于表上的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Oracle 中很多。<br /><br />如果选择**否**，SSMA 插入，然后从引用表中选择值以模拟 Oracle 功能。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
|**将 UPDATE 语句中的 RETURNING 子句转换为输出**|Oracle 提供的 RETURNING 子句作为一种方法可立即获得更新后的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 OUTPUT 子句提供了此功能。<br /><br />如果选择**是**，SSMA 将转换为的 OUTPUT 子句的 UPDATE 语句中的 RETURNING 子句。 由于表上的触发器可以更改值，返回的值可能会在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Oracle 中很多。<br /><br />如果选择**否**，SSMA 将 UPDATE 语句来检索返回值后生成的 SELECT 语句。<br /><br />当选择中的转换模式**模式下**框，SSMA 适用以下设置：<br /><br />**默认/乐观/Full 模式：** 是|  
  
## <a name="sequence-conversion"></a>序列转换  
  
|||  
|-|-|  
|术语|定义|  
|**转换序列生成器**|在 Oracle 中，可以使用序列生成的唯一标识符。<br /><br />SSMA 可以将序列转换为以下。<br /><br />使用 SQL Server 序列生成器 （此选项才可用时将转换为 SQL Server 2012 和 SQL Server 2014）。<br /><br />使用 SSMA 序列生成器。<br /><br />使用列标识。<br /><br />将转换为 SQL Server 2012 或 SQL Server 2014 时的默认选项是使用 SQL Server 序列生成器。 但是，SQL Server 2012 和 SQL Server 2014 不支持获取当前的序列值 （例如，Oracle 序列 currval 方法）。 请参阅有关迁移的 Oracle 序列 currval 方法的指导的 SSMA 团队博客站点。<br /><br />SSMA 还提供了一个选项以将 Oracle 序列转换为 SSMA 序列仿真程序。 这是默认选项，当您将转换为 SQL Server 2012 之前<br /><br />最后，还可以将转换序列分配给 SQL Server 标识值的表中的列。 必须指定到标识列在 Oracle 上序列之间的映射**表**选项卡|  
|**将 CURRVAL 转换外部触发器**|转换序列生成器设置为时才可见**使用列标识**。 由于 Oracle 序列是独立于表的对象，使用序列的多个表使用触发器生成和插入新的序列值。 SSMA 会注释掉这些语句，或将其标记为错误时注释扩展会生成错误。<br /><br />如果选择**是**，SSMA 会将标记为进行外部触发器已转换序列 CURRVAL 并且出现警告的所有引用。<br /><br />如果选择**否**，SSMA 会将标记为进行外部触发器已转换序列 CURRVAL 并出现错误的所有引用。|  
  
## <a name="see-also"></a>请参阅  
[用户界面参考&#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
