---
title: SQL执行功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5306567aebc229a8bc9d1d3c91bcbd8e79391752
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286067"
---
# <a name="sqlexecute-function"></a>SQLExecute 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLExecute**执行一个已准备好的语句，使用参数标记变量的当前值（如果语句中存在任何参数标记）。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLExecute**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLExecute**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01001|光标操作冲突|与*语句处理*关联的已准备好的语句包含定位的更新或删除语句，并且没有更新或删除任何行或多行。 （有关对多行的更新的详细信息，请参阅**SQLSetStmtAttr**中的SQL_ATTR_SIMULATE_CURSOR*属性*的说明。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|01003|在设置函数中消除的 NULL 值|与*语句处理*关联的已准备好语句包含一个集函数（如**AVG、MAX、MIN**等），但不包括**COUNT**集函数，在应用函数之前消除了 NULL 参数值。 **MAX** **MIN** （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|为输出参数返回的字符串或二进制数据导致非空白字符或非 NULL 二进制数据的截断。 如果它是一个字符串值，它是右截断的。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01006|未撤消权限|与*语句句柄*关联的已准备好的语句是**REVOKE**语句，用户没有指定的权限。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01007|未授予特权|与*语句句柄*关联的已准备好的语句是**GRANT**语句，无法授予用户指定的权限。|  
|01S02|选项值已更改|由于实现工作条件，指定的语句属性无效，因此临时替换了类似的值。 （可以调用**SQLGetStmtAttr**以确定临时替换的值是什么。替换值对*语句处理*有效，直到游标关闭，此时语句属性将还原到其上一个值。 可以更改的语句属性包括：SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT和SQL_ATTR_SIMULATE_CURSOR。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分数截断|为输入/输出或输出参数返回的数据被截断，因此数字数据类型的小数部分被截断或时间、时间戳或间隔数据类型的时间分量的分数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07002|COUNT 字段不正确|**SQLBind参数**中指定的参数数小于\**语句文本*中包含的 SQL 语句中的参数数。<br /><br /> **SQLBind参数**调用时 *，参数ValuePtr*设置为空指针 *，StrLen_or_IndPtr*未设置为SQL_NULL_DATA或SQL_DATA_AT_EXEC，*并且输入输出类型*未设置为SQL_PARAM_OUTPUT，因此**SQLBind参数**中指定的参数数大于 #*语句文本*中包含的 SQL 语句中的参数数。|  
|07006|受限数据类型属性冲突|绑定参数的**SQLBind 参数**中*的值类型*参数标识的数据值无法转换为**SQLBind 参数**中的*参数类型*参数标识的数据类型。<br /><br /> 返回为SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT绑定的参数的数据值无法转换为**SQLBind 参数**中*ValueType*参数标识的数据类型。<br /><br /> （如果无法转换一个或多个行的数据值，但成功返回一个或多个行，则此函数将返回SQL_SUCCESS_WITH_INFO。|  
|07007|受限参数值冲突|参数类型SQL_PARAM_INPUT_OUTPUT_STREAM仅用于以零件发送和接收数据的参数。 此参数类型不允许输入绑定缓冲区。<br /><br /> 当参数类型SQL_PARAM_INPUT_OUTPUT，并且\***SQLBind 参数**中指定的*StrLen_or_IndPtr*不等于SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_LEN_DATA_AT_EXEC（len）或SQL_DATA_AT_EXEC时，将发生此错误。|  
|07S01|默认参数使用无效|使用**SQLBind参数**设置的参数值SQL_DEFAULT_PARAM，相应的参数不是 ODBC 规范过程调用的参数。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|21S02|派生表的程度与列列表不匹配|与*语句处理*关联的已准备好的语句包含一个**CREATE VIEW**语句，而非限定列列表（SQL 语句的*列标识符*参数中为视图指定的列数）包含的名称数比 SQL 语句*的查询规范*参数定义的派生表中的列数多。|  
|22001|字符串数据，右截断|将字符或二进制值分配给列会导致非空白（字符）或非空（二进制）字符或字节的截断。|  
|22002|需要指标变量，但未提供|NULL 数据绑定到输出参数，其*StrLen_or_IndPtr*由**SQLBind参数**设置为空指针。|  
|22003|数值超范围|与*语句处理*关联的已准备好的语句包含绑定数值参数，并且参数值导致在分配给关联的表列时，将数字的整个（而不是小数）部分被截断。<br /><br /> 为一个或多个输入/输出或输出参数返回数值（作为数字或字符串）将导致数字的整个（而不是小数）部分被截断。|  
|22007|无效日期时间格式|与*语句处理*关联的已准备好的语句包含一个 SQL 语句，该语句包含作为绑定参数的日期、时间或时间戳结构，并且该参数分别是无效的日期、时间或时间戳。<br /><br /> 输入/输出或输出参数绑定到日期、时间或时间戳 C 结构，返回参数中的值分别为无效日期、时间或时间戳。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|22008|日期时间字段溢出|与*语句处理*关联的已准备好的语句包含一个 SQL 语句，其中包含一个日期时间表达式，该表达式在计算时导致日期、时间或时间戳结构无效。<br /><br /> 为输入/输出或输出参数计算的 datetime 表达式会导致日期、时间或时间戳 C 结构无效。|  
|22012|除零|与*语句处理*关联的已准备好的语句包含一个算术表达式，该表达式导致除零。<br /><br /> 为输入/输出或输出参数计算的算术表达式导致除以零。|  
|22015|间隔字段溢出|语句文本包含一个精确的数字或间隔参数，当转换为间隔 SQL 数据类型时，该参数会导致重要数字的损失。 * \**<br /><br /> 语句文本包含一个包含多个字段的间隔参数，当该字段转换为列中的数字数据类型时，数字数据类型中没有表示形式。 * \**<br /><br /> 语句文本包含分配给间隔 SQL 类型的参数数据，并且间隔 SQL 类型中没有 C 类型的值表示形式。 * \**<br /><br /> 将精确数字或间隔 SQL 类型的输入/输出或输出参数分配给间隔 C 类型会导致有效数字丢失。<br /><br /> 当输入/输出参数分配给间隔 C 结构时，间隔数据结构中没有数据的表示形式。|  
|22018|强制转换规范的无效字符值|语句文本包含一个 C 类型，该类型是精确或近似数字、日期时间或间隔数据类型; * \** 列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。<br /><br /> 返回输入/输出或输出参数时，SQL 类型是精确或近似的数字、日期时间或间隔数据类型;C 类型为SQL_C_CHAR;列中的值不是绑定 SQL 类型的有效文本。|  
|22019|无效转义字符|与*语句处理*关联的已准备好的语句包含一个与**WHERE**子**WHERE**句中具有 ESCAPE 的**LIKE**谓词，**并且 ESCAPE**之后的转义字符的长度不等于 1。|  
|22025|无效转义序列|与*语句处理*关联的准备语句在**WHERE**子句中包含 **"LIKE** _模式值_ **ESCAPE** _转义字符_"，模式值中转义字符之后的字符不是"%"或"*"。|  
|23000|完整性约束冲突|与*语句句柄*关联的已准备好的语句包含一个参数。 对于在关联的表列中定义为"非 NULL"的列，参数值为 NULL，为仅包含唯一值的列提供了重复值，或者违反了某些其他完整性约束。|  
|24000|无效的游标状态|**通过 SQLFetch**或**SQLFetchScroll**在*语句处理*上定位了一个光标。 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个光标。<br /><br /> 与*语句处理*关联的已准备好的语句包含定位的更新或删除状态者 t，光标位于结果集开始之前或结果集结束之后。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|42000|语法错误或访问冲突|用户没有执行与*语句句柄*关联的已准备好的语句的权限。|  
|44000|与检查选项冲突|与*语句处理*关联的已准备好的语句包含在已查看的表或从已查看表派生的表上执行的**INSERT**语句，该语句是通过指定 **"与检查选项**"创建的，这样受**INSERT**语句影响的一个或多个行将不再存在于已查看的表中。<br /><br /> 与*语句处理*关联的已准备好的语句包含在已查看的表或从已查看表派生的表上执行**的更新**语句，该语句是通过指定 **"与检查选项**"创建的，这样受**UPDATE**语句影响的一个或多个行将不再存在于已查看的表中。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLExecute**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM）*声明处理*未编制。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|使用**SQLBindParameter**设置的参数值是空指针，参数长度值不是 0、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM或小于或等于SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 使用 SQLBind 参数设置的参数值不是空指针，而使用**SQLBind 参数**设置的参数值不是空指针。C 数据类型为SQL_C_BINARY或SQL_C_CHAR;参数长度值小于 0，但未SQL_NTS、SQL_NULL_DATA、SQL_DEFAULT_PARAM或SQL_DATA_AT_EXEC，或小于或等于SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 由**SQLBind 参数**绑定的参数长度值设置为SQL_DATA_AT_EXEC;SQL 类型要么是SQL_LONGVARCHAR、SQL_LONGVARBINARY，要么是长数据源特定的数据类型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型为"Y"。|  
|HY105|无效参数类型|为**SQLBind 参数**中为参数*InputOutputType*指定的值SQL_PARAM_OUTPUT，该参数为输入参数。|  
|HY109|光标位置无效|准备好的语句是定位的更新或删除语句，光标定位在已删除或无法提取的行上（由**SQLSetPos**或**SQLFetchScroll）。**|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
 **SQLExecute**可以返回**SQLPrepare**可以返回的任何 SQLSTATE，具体取决于数据源何时计算与 语句关联的 SQL 语句。  
  
## <a name="comments"></a>注释  
 **SQLExecute**执行由**SQLPrepare**编写的语句。 在应用程序处理或放弃对**SQLExecute**调用的结果后，应用程序可以使用新的参数值再次调用**SQLExecute。** 有关准备执行的详细信息，请参阅[准备执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
 要多次执行**SELECT**语句，应用程序必须在重新执行**SELECT**语句之前调用**SQLCloseCursor。**  
  
 如果数据源处于手动提交模式（需要显式事务启动），并且尚未启动事务，则驱动程序会在发送 SQL 语句之前启动事务。 有关详细信息，请参阅[事务](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 如果应用程序使用**SQLPrepare**准备和**SQLExecute**提交**COMMIT**或**ROLLBACK**语句，则在 DBMS 产品之间无法互操作。 要提交或回滚事务，请调用**SQLEndTran**。  
  
 如果**SQLExecute**遇到执行时的数据参数，它将返回SQL_NEED_DATA。 应用程序使用**SQLParam 数据和** **SQLPutData**发送数据。 请参阅[SQLBind 参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)[、SQLParamData、SQLPutData](../../../odbc/reference/syntax/sqlparamdata-function.md)和[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
 如果**SQLExecute**执行搜索的更新、插入或删除不影响数据源上任何行的语句，则对**SQLExecute**的调用将返回SQL_NO_DATA。  
  
 如果SQL_ATTR_PARAMSET_SIZE语句属性的值大于 1，并且 SQL 语句至少包含一个参数标记，**则 SQLExecute**将针对数组中参数*\*ValuePtr*参数在调用**SQLBind参数**中指向的每组参数值执行一次 SQL 语句。 有关详细信息，请参阅[参数值数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果启用了书签并执行了不支持书签的查询，驱动程序应尝试通过更改属性值并返回 SQLSTATE 01S02（选项值已更改）来强制环境强制环境为支持书签的环境。 如果无法更改属性，驱动程序应返回 SQLSTATE HY024（无效属性值）。  
  
> [!NOTE]  
>  使用连接池时，应用程序不得执行更改数据库或数据库上下文的 SQL 语句，例如 SQL Server 中的**USE** _数据库_语句，该语句更改数据源使用的目录。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBind 参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)[、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|关闭光标|[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|获取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|释放语句句柄|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回游标名称|[SQLGetCursorName 函数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|获取数据列的一部分或全部|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回下一个参数以发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|准备执行语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
