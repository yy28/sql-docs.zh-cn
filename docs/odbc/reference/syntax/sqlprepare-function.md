---
title: SQL准备功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306878"
---
# <a name="sqlprepare-function"></a>SQLPrepare 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLPrepare**准备一个 SQL 字符串进行执行。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *语句文本*  
 [输入]SQL 文本字符串。  
  
 *TextLength*  
 [输入]长度 =*字符语句文本*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPrepare**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了 SQLPrepare 通常返回的**SQLSTATE**值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|由于实现工作条件，指定的语句属性无效，因此临时替换了类似的值。 （可以调用**SQLGetStmtAttr**以确定临时替换的值是什么。在光标关闭之前，替换值对*语句处理*有效。 可以更改的语句属性是：SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPESQL_ATTR_KEYSET_SIZESQL_ATTR_QUERY_TIMEOUTSQL_ATTR_QUERY_TIMEOUT SQL_ATTR_MAX_ROWSSQL_ATTR_KEYSET_SIZESQL_ATTR_MAX_LENGTH SQL_ATTR_SIMULATE_CURSORSQL_ATTR_CONCURRENCY<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|21S01|插入值列表与列列表不匹配|\**语句文本*包含一个**INSERT**语句，要插入的值数与派生表的程度不匹配。|  
|21S02|派生表的程度与列列表不匹配|\**语句文本*包含一个**CREATE VIEW**语句，并且指定的名称数与查询规范定义的派生表的程度不同。|  
|22018|强制转换规范的无效字符值|**语句文本*包含包含文本或参数的 SQL 语句，并且该值与关联的表列的数据类型不兼容。|  
|22019|无效转义字符|参数*语句文本*包含一个**LIKE**谓词，其中包含**WHERE**子句中的**ESCAPE，** 并且**ESCAPE**之后的转义字符的长度不等于 1。|  
|22025|无效转义序列|参数*语句文本*在**WHERE**子句中包含 **"LIKE** _模式值_ **ESCAPE** _转义字符_"，模式值中转义字符之后的字符既不是"%"也不是"*"。|  
|24000|无效的游标状态|（DM）*语句处理*上打开一个游标，并且调用**了 SQLFetch**或**SQLFetchScroll。**<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|34000|无效的游标名称|\**语句文本*包含定位的**DELETE**或定位**的更新**，并且准备语句引用的光标未打开。|  
|3D000|无效目录名称|*语句文本*中指定的目录名称无效。|  
|3F000|无效的架构名称|*语句文本*中指定的架构名称无效。|  
|42000|语法错误或访问冲突|\**语句文本*包含一个不可预备的 SQL 语句或包含语法错误。<br /><br /> **语句文本*包含一个声明，用户没有所需的权限。|  
|42S01|基本表或视图已存在|\**语句文本*包含 **"创建表"** 或 **"创建视图**"语句，指定的表名称或视图名称已存在。|  
|42S02|找不到基本表或视图|\**语句文本*包含**DROP TABLE**或**DROP VIEW**语句，并且指定的表名称或视图名称不存在。<br /><br /> \**语句文本*包含**ALTER TABLE**语句，并且指定的表名称不存在。<br /><br /> \**语句文本*包含一个**CREATE VIEW**语句，查询规范定义的表名称或视图名称不存在。<br /><br /> \**语句文本*包含一个**CREATE INDEX**语句，并且指定的表名称不存在。<br /><br /> \**语句文本*包含一个**GRANT**或**REVOKE**语句，并且指定的表名称或视图名称不存在。<br /><br /> \**语句文本*包含**SELECT**语句，并且指定的表名称或视图名称不存在。<br /><br /> \**语句文本*包含**DELETE、INSERT**或**UPDATE**语句，并且指定的表名称不存在。 **INSERT**<br /><br /> \**语句文本*包含一个**CREATE TABLE**语句，并且约束中指定的表（引用正在创建的表以外的表）不存在。|  
|42S11|索引已存在|\**语句文本*包含一个**CREATE INDEX**语句，并且指定的索引名称已经存在。|  
|42S12|未找到索引|\**语句文本*包含**DROP INDEX**语句，并且指定的索引名称不存在。|  
|42S21|列已存在|\**语句文本*包含**ALTER TABLE**语句 **，ADD**子句中指定的列不是唯一的，或标识基表中的现有列。|  
|42S22|未找到列|\**语句文本*包含**CREATE INDEX**语句，列列表中指定的一个或多个列名称不存在。<br /><br /> \**语句文本*包含**GRANT**或**REVOKE**语句，并且指定的列名称不存在。<br /><br /> \**语句文本*包含**SELECT、DELETE、****插入**或**更新**语句，并且指定的列名称不存在。 **SELECT**<br /><br /> \**语句文本*包含一个**CREATE TABLE**语句，并且约束中指定的列（引用正在创建的表以外的表）不存在。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**在*语句句柄*上调用 ，然后在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|（DM）*语句文本*是一个空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLPrepare**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 参数*文本长度*小于或等于 0，但不等于SQL_NTS。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|对于定义的游标类型，并发设置无效。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLPrepare**将 SQL 语句发送到数据源进行准备。 有关准备执行的详细信息，请参阅[准备执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。 应用程序可以在 SQL 语句中包含一个或多个参数标记。 要包含参数标记，应用程序在适当的位置将问号 （？） 嵌入到 SQL 字符串中。 有关参数的信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
> [!NOTE]  
>  如果应用程序使用**SQLPrepare**准备和**SQLExecute**提交**COMMIT**或**ROLLBACK**语句，则在 DBMS 产品之间无法互操作。 要提交或回滚事务，请调用**SQLEndTran**。  
  
 驱动程序可以修改语句以使用数据源使用的 SQL 形式，然后将其提交到数据源进行准备。 特别是，驱动程序修改用于定义某些功能的 SQL 语法的转义序列。 （有关 SQL 语句语法的说明，请参阅 ODBC 和附录 C[中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)[：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。对于驱动程序，语句句柄类似于嵌入 SQL 代码中的语句标识符。 如果数据源支持语句标识符，驱动程序可以将语句标识符和参数值发送到数据源。  
  
 准备语句后，应用程序使用 语句句柄在以后的函数调用中引用语句。 通过调用**SQLExecute**可以重新执行与语句句柄关联的准备语句，直到应用程序使用 SQL_DROP 选项释放对**SQLFreeStmt**的调用语句，或者直到语句句柄用于调用**SQLPrepare、SQLExecDirect**或**SQLExecDirect**目录函数之一 **（SQLColumns、SQLTables**等） **SQLTables** 应用程序准备语句后，可以请求有关结果集格式的信息。 对于某些实现，在**SQLPrepare**之后调用**SQLDescribeCol**或**SQLDescribeParam**可能不如在**SQLExecute**或**SQLExecDirect**之后调用函数更有效。  
  
 当应用程序调用**SQLPrepare**时，某些驱动程序无法返回语法错误或访问冲突。 驱动程序可以处理语法错误和访问冲突，只能处理语法错误，或者语法错误和访问冲突。 因此，应用程序在调用后续相关函数（如 SQLNumCols、SQLDescribeCol、SQLCol**属性**和**SQLExecute）** 时必须能够处理这些条件。 **SQLNumResultCols** **SQLDescribeCol**  
  
 根据驱动程序和数据源的功能，在编写语句（如果所有参数都已绑定）或执行语句（如果所有参数尚未绑定）时，可能会检查参数信息（如数据类型）。 为了达到最大互操作性，应用程序应在对同一语句上准备新的 SQL 语句之前取消绑定应用于旧 SQL 语句的所有参数。 这样可以防止由于旧参数信息应用于新语句而导致的错误。  
  
> [!IMPORTANT]  
>  通过显式调用**SQLEndTran**或以自动提交模式工作来提交事务，可能会导致数据源删除连接上所有语句的访问计划。 有关详细信息，请参阅[SQLGetInfo 中](../../../odbc/reference/syntax/sqlgetinfo-function.md)SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型以及[事务对游标和准备语句的影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBind 参数](../../../odbc/reference/syntax/sqlbindparameter-function.md) [、SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配语句句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|将缓冲区绑定到参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回受语句影响的行数|[SQLRowCount Function（SQLRowCount 函数）](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
