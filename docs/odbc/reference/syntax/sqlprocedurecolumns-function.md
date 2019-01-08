---
title: SQLProcedureColumns 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b47ef4c2df8a326d993a95e056b27d331dc649f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205596"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns Function（SQLProcedureColumns 函数）
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLProcedureColumns**返回的输入和输出参数，以及组成的指定过程的结果集的列的列表。 该驱动程序返回对指定的语句作为结果集的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]过程目录名称。 如果驱动程序支持目录，对于一些过程，但对于其他操作系统，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示没有目录这些过程。 *CatalogName*不能包含字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*CatalogName*是普通参数; 按字面意思，处理和其大小写很重要。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]过程架构名称的字符串搜索模式。 如果驱动程序支持的架构，对于一些过程，但对于其他操作系统，例如当驱动程序检索数据从不同 Dbms，空字符串 ("") 表示不具有架构的这些过程。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*SchemaName*是模式值自变量; 按字面意思，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *ProcName*  
 [输入]过程名称的字符串搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *ProcName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*ProcName*是模式值自变量; 按字面意思，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **ProcName*。  
  
 *ColumnName*  
 [输入]列名称的字符串搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *ColumnName*视为标识符和其大小写并不重要。 SQL_FALSE，若是*ColumnName*是模式值自变量; 按字面意思，处理和其大小写很重要。  
  
 *NameLength4*  
 [输入]以字符为单位的长度 **ColumnName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLProcedureColumns**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLProcedureColumns** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前的驱动程序返回 SQLSTATEs 说明管理器。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，和如果驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLError**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*参数为 null 指针和 SQL_CATALOG_NAME*信息类型*支持目录名称返回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE，并*SchemaName*， *ProcName*，或*ColumnName*参数是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此 aynschronous 函数仍在执行调用 SQLProcedureColumns 函数时。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度参数值小于 0 但不是等于 SQL_NTS。<br /><br /> 名称长度参数之一的值超出了相应的目录、 架构、 过程或列名称的最大长度值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定过程目录，并在驱动程序或数据源不支持目录。<br /><br /> 指定过程的架构，并在驱动程序或数据源不支持架构。<br /><br /> 过程架构、 过程名称或列名称，为指定的字符串搜索模式和数据源不支持的一个或多个这些参数的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 此函数通常在语句执行之前用于检索过程参数和列组成的结果集的过程，返回的如果任何信息。 有关详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  **SQLProcedureColumns**可能不会返回由过程使用的所有列。 例如，驱动程序可能会返回有关使用的过程，且不会生成结果集中的列的参数的唯一信息。  
  
 *SchemaName*， *ProcName*，并*ColumnName*参数接受搜索模式。 有关有效的搜索模式的详细信息，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLProcedureColumns**以按 PROCEDURE_CAT、 PROCEDURE_SCHEM、 过程名称和 COLUMN_TYPE 标准结果集的形式返回结果。 列名称返回为每个过程按以下顺序： 返回值的名称、 在 （按调用顺序），该过程调用中的每个参数的名称和 （按列顺序） 过程返回的结果集中的每个列的名称。  
  
 应用程序应将相对于结果集末尾的驱动程序特定列绑定。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
 若要确定 PROCEDURE_CAT、 PROCEDURE_SCHEM、 过程名称，而 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**与 SQL_MAX_CATALOG_NAME_LEN，SQL_MAX_SCHEMA_NAME_LEN，SQL_MAX_PROCEDURE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
 对于 ODBC 3 重命名为以下各列。*x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|过程 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 以下各列已添加到返回的结果集**SQLProcedureColumns** ODBC 3。*x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 下表列出了在结果集中的列。 列 19 (IS_NULLABLE) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的结果集末尾的倒计时，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|过程目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录对于一些过程，但对于其他操作系统，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 对于这些没有目录的过程。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|过程架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构对于一些过程，但对于其他操作系统，如当驱动程序检索数据时从不同 Dbms，它返回空字符串 ("") 对于这些没有架构的过程。|  
|过程名称 (ODBC 2.0)|3|Varchar 不为 NULL|过程名。 不具有名称的过程返回空字符串。|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar 不为 NULL|过程列名称。 该驱动程序返回空字符串不具有名称的过程列。|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint（非 NULL）|定义过程列作为参数或结果集列：<br /><br /> SQL_PARAM_TYPE_UNKNOWN:过程列是其类型是未知的参数。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT:过程列是一个输入的参数。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT:过程列是一个输入/输出参数。 (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT:过程列是一个输出参数。 (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE:过程列是该过程的返回值。 (ODBC 2.0)<br /><br /> SQL_RESULT_COL:过程列是结果集列。 (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间和间隔数据类型，此列返回简洁数据类型 （例如，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)中附录 d:数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|TYPE_NAME (ODBC 2.0)|7|Varchar 不为 NULL|数据源相关的数据类型名称;"例如，CHAR"、"VARCHAR"、"MONEY"、"长 VARBINARY"或者"CHAR FOR BIT DATA （）"。|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|过程列上的数据源的列大小。 列大小不适用的数据类型则返回 NULL。 有关精度的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|上传输的数据的字节长度**SQLGetData**或**SQLFetch**如果 SQL_C_DEFAULT 指定的操作。 对于数值数据，此大小可能不同于数据源上存储的数据量。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)，在附录 d:数据类型。|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|过程列的数据源上的十进制数字。 不适用小数位数为数据类型则返回 NULL。 有关十进制数字的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)，在附录 d:数据类型。|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|对于数值数据类型，为 10 或 2。<br /><br /> 如果月 10 日，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值为指定的列允许的十进制位数。 例如，DECIMAL(12,5) 列将返回为 10，12，COLUMN_SIZE 和 5; DECIMAL_DIGITS NUM_PREC_RADIXFLOAT 列可能会返回 10 月 15 日，COLUMN_SIZE 和 DECIMAL_DIGITS 的 NULL NUM_PREC_RADIX。<br /><br /> 如果为 2，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值为提供的列中允许的位数。 例如，FLOAT 列可能返回 2，53，COLUMN_SIZE 和 DECIMAL_DIGITS 的 NULL NUM_PREC_RADIX。<br /><br /> 不适用 NUM_PREC_RADIX 对于数据类型则返回 NULL。|  
|可以为 NULL (ODBC 2.0)|12|Smallint（非 NULL）|是否过程列接受 NULL 值：<br /><br /> SQL_NO_NULLS:过程列不接受 NULL 值。<br /><br /> SQL_NULLABLE:过程列接受 NULL 值。<br /><br /> SQL_NULLABLE_UNKNOWN:并不知道如果过程列接受 NULL 值。|  
|备注 (ODBC 2.0)|13|Varchar|过程列的说明。|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|列的默认值。<br /><br /> 如果指定为默认值为 NULL，此列是词 NULL，不能用引号括起来。 如果默认值不能表示而无需截断，此列包含被截断，加上任何封闭的单个引号。 如果未指定默认值时，此列将为 NULL。<br /><br /> 可在除生成的新列定义，它包含的值被截断时 COLUMN_DEF 的值。|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint（非 NULL）|SQL 数据类型，因为它的值出现在描述符的 SQL_DESC_TYPE 字段。 此列是日期时间和间隔数据类型除外 DATA_TYPE 列相同。<br /><br /> 对于日期时间和间隔数据类型，在结果集中的 SQL_DATA_TYPE 字段将返回 SQL_INTERVAL 或 SQL_DATETIME，和 SQL_DATETIME_SUB 字段将返回特定的时间间隔或日期时间数据类型的子代码。 (请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|日期时间和间隔数据类型的子类型代码。 对于其他数据类型，此列返回 NULL。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|以字节为单位的最大长度的字符或二进制数据类型列。 对于所有其他数据类型，此列返回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer（非 NULL）|对于输入和输出参数，该参数的序号位置 （按不断增加的参数顺序，从 1 开始） 在过程定义中。 对于返回值 （如果有），则返回 0。 对于结果集列，结果中的列的序号位置设置，与结果集中的第一列编号为 1。 如果有多个结果集，以驱动程序特定的方式返回列序号位置。|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"否"如果列不包含 null 值。<br /><br /> "是"如果列可以包含 Null。<br /><br /> 如果为 Null 性为未知，该列将返回零长度字符串。<br /><br /> 根据 ISO 规则确定为 Null 性。 遵从 ISO SQL 标准的 DBMS 不能返回空字符串。<br /><br /> 该列返回的值与 NULLABLE 列返回的值不同。 （请参阅可以为 NULL 的列的说明。）|  
  
## <a name="code-example"></a>代码示例  
 请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|数据源中返回的过程的列表|[SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
