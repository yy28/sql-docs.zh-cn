---
title: SQL程序列函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306848"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns Function（SQLProcedureColumns 函数）
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLProcessColumns**返回输入和输出参数的列表，以及构成指定过程的结果集的列。 驱动程序将返回信息作为指定语句上的结果集。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]过程目录名称。 如果驱动程序支持某些过程的目录，但不支持其他过程的目录，例如当驱动程序从不同的 DBMS 检索数据时，空字符串（""）表示那些没有目录的过程。 *目录名称*不能包含字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*将被视为标识符，其大小写不重要。 如果SQL_FALSE，目录名称是普通参数;如果为"*目录名称"，则为"目录名称"，* 但为"目录名称"，但为"目录名称"，但它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度在 **目录名称*的字符中。  
  
 *架构名称*  
 [输入]字符串搜索模式的过程架构名称。 如果驱动程序支持某些过程的架构，但不支持其他过程的架构（例如当驱动程序从不同的 DBMS 检索数据时），空字符串（""）表示那些没有架构的过程。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 SchemaName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则 SchemaName 是模式值参数;如果为 SQL_FALSE，则 *"架构名称"* 是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度在 **架构名称*的字符中。  
  
 *ProcName*  
 [输入]字符串搜索模式的过程名称。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 ProcName*被视为标识符，其大小写不重要。 如果*SQL_FALSE，ProcName*是模式值参数;如果为 SQL_FALSE，则 ProcName 是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]长度在 =*ProcName*的字符中。  
  
 *ColumnName*  
 [输入]字符串搜索模式的列名称。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*ColumnName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则"列名"是模式值参数;如果为"*列名称"，* 则为"列名"，即为模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度4*  
 [输入]长度以 =*列名*的字符表示。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQL程序列**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT*Handle*的*句柄类型*和*语句句柄*。 下表列出了**SQLAk**通常返回的 SQLSTATE 值，并解释了此函数上下文中的每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLError**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*目录名称*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*而 SchemaName、ProcName*或*列名*参数是空指针。 *ProcName*|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQLAAK 函数时，此 aynschronous 函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY090|无效的字符串或缓冲区长度|（DM） 其中一个名称长度参数的值小于 0，但不等于SQL_NTS。<br /><br /> 其中一个名称长度参数的值超过相应目录、架构、过程或列名称的最大长度值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了过程目录，驱动程序或数据源不支持目录。<br /><br /> 已指定过程架构，驱动程序或数据源不支持架构。<br /><br /> 为过程架构、过程名称或列名称指定了字符串搜索模式，数据源不支持一个或多个这些参数的搜索模式。<br /><br /> 驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 此函数通常在语句执行之前用于检索有关过程参数以及构成过程返回的结果集或集的列（如果有）的信息。 有关详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  **SQL程序列**可能不会返回过程使用的所有列。 例如，驱动程序可能只返回有关过程使用的参数的信息，而不是返回它生成的结果集中的列的信息。  
  
 *架构名称**、ProcName*和*列名*参数接受搜索模式。 有关有效搜索模式的详细信息，请参阅[模式值参数](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQL程序列**将结果作为标准结果集返回，按PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME和COLUMN_TYPE排序。 按以下顺序为每个过程返回列名称：返回值的名称、过程调用中每个参数的名称（按调用顺序），然后返回过程返回的结果集中每个列的名称（按列顺序排列）。  
  
 应用程序应绑定相对于结果集末尾的特定于驱动程序的列。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
 要确定PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME和COLUMN_NAME列的实际长度，应用程序可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_PROCEDURE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN选项调用**SQLGetInfo。**  
  
 以下列已重命名为 ODBC 3。*x*. . 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC 3.*x*列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程序_OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 以下列已添加到由 ODBC 3 的**SQL 过程列**返回的结果集中。*x*：  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 下表列出了结果集中的列。 驱动程序可以定义第 19 栏（IS_NULLABLE）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT （ODBC 2.0）|1|Varchar|程序目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些过程的目录，但不支持其他过程的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的过程。|  
|PROCEDURE_SCHEM （ODBC 2.0）|2|Varchar|过程架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些过程的架构，但不支持其他过程的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的过程。|  
|PROCEDURE_NAME （ODBC 2.0）|3|瓦尔查尔不是 NULL|过程名。 对于没有名称的过程，将返回一个空字符串。|  
|COLUMN_NAME （ODBC 2.0）|4|瓦尔查尔不是 NULL|过程列名称。 驱动程序返回没有名称的过程列的空字符串。|  
|COLUMN_TYPE （ODBC 2.0）|5|Smallint（非 NULL）|将过程列定义为参数或结果集列：<br /><br /> SQL_PARAM_TYPE_UNKNOWN：过程列是其类型未知参数。 （ODBC 1.0）<br /><br /> SQL_PARAM_INPUT：过程列是输入参数。 （ODBC 1.0）<br /><br /> SQL_PARAM_INPUT_OUTPUT：过程列是输入/输出参数。 （ODBC 1.0）<br /><br /> SQL_PARAM_OUTPUT：过程列是输出参数。 （ODBC 2.0）<br /><br /> SQL_RETURN_VALUE：过程列是过程的返回值。 （ODBC 2.0）<br /><br /> SQL_RESULT_COL：过程列是结果集列。 （ODBC 1.0）|  
|DATA_TYPE （ODBC 2.0）|6|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间和间隔数据类型，此列返回简洁的数据类型（例如，SQL_TYPE_TIME或SQL_INTERVAL_YEAR_TO_MONTH）。 有关有效的 ODBC SQL 数据类型的列表，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|TYPE_NAME （ODBC 2.0）|7|瓦尔查尔不是 NULL|与数据源相关的数据类型名称;例如，"CHAR"，"VARCHAR"，"金钱"，"长VARBINARY"，或"CHAR （ ） BIT 数据"。|  
|COLUMN_SIZE （ODBC 2.0）|8|Integer|数据源上过程列的列大小。 对于不适用的列大小数据类型，将返回 NULL。 有关精度的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|BUFFER_LENGTH （ODBC 2.0）|9|Integer|如果指定了SQL_C_DEFAULT，则在**SQLGetData**或**SQLFetch**操作上传输的数据的长度（以字节为单位）。 对于数字数据，此大小可能与存储在数据源上的数据的大小不同。 有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。"数据类型"。|  
|DECIMAL_DIGITS （ODBC 2.0）|10|Smallint|数据源上过程列的小数位数。 对于不适用十进制数字的数据类型，返回 NULL。 有关十进制数字的详细信息，请参阅[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)，参见附录 D：数据类型。|  
|NUM_PREC_RADIX （ODBC 2.0）|11|Smallint|对于数字数据类型，10 或 2。<br /><br /> 如果为 10，则COLUMN_SIZE和DECIMAL_DIGITS中的值将给出该列允许的十进制数字数。 例如，DECIMAL（12，5）列将返回NUM_PREC_RADIX 10、COLUMN_SIZE 12 和 DECIMAL_DIGITS 5;FLOAT 列可以返回 10 NUM_PREC_RADIX、COLUMN_SIZE 15 和 null DECIMAL_DIGITS。<br /><br /> 如果为 2，则COLUMN_SIZE和DECIMAL_DIGITS中的值给出列中允许的位数。 例如，FLOAT 列可以返回 NUM_PREC_RADIX 2、COLUMN_SIZE 53 和 DECIMAL_DIGITS NULL。<br /><br /> 对于不适用NUM_PREC_RADIX的数据类型，将返回 NULL。|  
|空值 （ODBC 2.0）|12|Smallint（非 NULL）|过程列是否接受 NULL 值：<br /><br /> SQL_NO_NULLS：过程列不接受 NULL 值。<br /><br /> SQL_NULLABLE：过程列接受 NULL 值。<br /><br /> SQL_NULLABLE_UNKNOWN：不知道过程列是否接受 NULL 值。|  
|备注 （ODBC 2.0）|13|Varchar|过程列的说明。|  
|COLUMN_DEF （ODBC 3.0）|14|Varchar|列的默认值。<br /><br /> 如果 NULL 被指定为默认值，则此列是单词 NULL，而不是用引号括起来。 如果不进行截断就无法表示默认值，则此列包含截断，不包含单个引号。 如果未指定默认值，则此列为 NULL。<br /><br /> COLUMN_DEF的值可用于生成新的列定义，除非它包含 TRUNCATED 的值。|  
|SQL_DATA_TYPE （ODBC 3.0）|15|Smallint（非 NULL）|SQL 数据类型的值，如它在描述符的SQL_DESC_TYPE字段中显示的。 此列与DATA_TYPE列相同，但日期时间和间隔数据类型除外。<br /><br /> 对于日期时间和间隔数据类型，结果集中的SQL_DATA_TYPE字段将返回SQL_INTERVAL或SQL_DATETIME，SQL_DATETIME_SUB字段将返回特定间隔或日期时间数据类型的子代码。 （参见[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|SQL_DATETIME_SUB （ODBC 3.0）|16|Smallint|日期时间和间隔数据类型的子类型代码。 对于其他数据类型，此列返回 NULL。|  
|CHAR_OCTET_LENGTH （ODBC 3.0）|17|Integer|字符或二进制数据类型列的最大长度（以字节为单位）。 对于所有其他数据类型，此列返回 NULL。|  
|ORDINAL_POSITION （ODBC 3.0）|18|Integer（非 NULL）|对于输入和输出参数，参数在过程定义中的序形位置（按增加参数顺序，从 1 开始）。 对于返回值（如果有），返回 0。 对于结果集列，在结果集中的列的定位位置，结果集中的第一列为数字 1。 如果存在多个结果集，则以特定于驱动程序的方式返回列序形位置。|  
|IS_NULLABLE （ODBC 3.0）|19|Varchar|如果列不包含 NUL，则为"否"。<br /><br /> 如果列可以包含 NUL，则为"是"。<br /><br /> 如果为 Null 性为未知，该列将返回零长度字符串。<br /><br /> 根据 ISO 规则确定为 Null 性。 遵从 ISO SQL 标准的 DBMS 不能返回空字符串。<br /><br /> 该列返回的值与 NULLABLE 列返回的值不同。 （请参阅 NULLABLE 列的说明。|  
  
## <a name="code-example"></a>代码示例  
 请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回数据源中的过程列表|[SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
