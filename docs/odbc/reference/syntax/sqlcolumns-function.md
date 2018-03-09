---
title: "SQLColumns 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLColumns
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLColumns
helpviewer_keywords: SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cb9d78a2ee194779f9e01dfd313ae4846d5a804
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcolumns-function"></a>SQLColumns 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： Open Group  
  
 **摘要**  
 **SQLColumns**返回指定的表中的列名称的列表。 驱动程序返回作为结果集上指定此信息*StatementHandle*。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有目录的那些表。 *CatalogName*不能包含字符串的搜索模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是的普通自变量; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]架构名称的字符串的搜索模式。 如果驱动程序支持的架构，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有架构的那些表。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *表名*  
 [输入]表名称的字符串的搜索模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *TableName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *列名称*  
 [输入]列名称的字符串的搜索模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *ColumnName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *ColumnName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength4*  
 [输入]以字符为单位的长度 **ColumnName*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColumns**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLColumns**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，并且如果由驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，由于资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*， *TableName*，或*ColumnName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLColumns**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的名称长度自变量的值小于 0，但不是等于 sql_nts 以。|  
|||名称长度自变量之一的值超出限制的相应目录或名称的最大长度值。 可以通过调用获取每个目录或名称的最大长度**SQLGetInfo**与*信息类型*值。 （请参阅"注释"。）|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定的目录名称，并在驱动程序或数据源不支持目录。<br /><br /> 指定的架构名称，并在驱动程序或数据源不支持架构。<br /><br /> 架构名称、 表名或列名，为指定字符串的搜索模式和数据源不支持为一个或多个这些自变量的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 此函数通常用于在语句执行之前从数据源的目录中检索表或表的列的信息。 **SQLColumns**可以用于检索返回项的所有类型的数据**SQLTables**。 除了基表，这可能包括 （但不限于） 视图、 同义词、 系统表和等等。 相比之下，函数**SQLColAttribute**和**SQLDescribeCol**描述结果集和该函数中的列**SQLNumResultCols**返回的数目在结果集中的列。 有关详细信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLColumns**标准的结果集，按 TABLE_CAT、 TABLE_SCHEM、 TABLE_NAME 和 ORDINAL_POSITION 排序的形式返回结果。  
  
> [!NOTE]  
>  当应用程序适用于 ODBC 2。*x*驱动程序，没有 ORDINAL_POSITION 列在结果集中返回。 因此，当使用 ODBC 2。*x*驱动程序，返回的列列表中的列的顺序**SQLColumns**不一定与列的顺序相同时，返回应用程序对所有执行 SELECT 语句此表中的列。  
  
> [!NOTE]  
>  **SQLColumns**可能不会返回所有列。 例如，驱动程序可能不返回伪列，例如 Oracle ROWID 的信息。 应用程序可以使用任何有效的列，是否通过返回**SQLColumns**。  
>   
>  可以返回的某些列**SQLStatistics**不会返回**SQLColumns**。 例如， **SQLColumns**不通过表达式或筛选器，如薪金 + 优势或部门创建索引中返回列 = 0012。  
  
 VARCHAR 列的长度不表所示;实际长度依赖于数据源。 若要确定 TABLE_CAT、 TABLE_SCHEM、 TABLE_NAME 和 COLUMN_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**使用 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN，和 SQL_MAX_COLUMN_NAME_LEN 选项。  
  
 下面的列已重命名为 ODBC 3。*x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 下面的列已添加到返回的结果集**SQLColumns** ODBC 3。*x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 18 (IS_NULLABLE) 之外的其他列。 应用程序应访问驱动程序的特定列的倒计时从结尾处的结果集而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|“列”<br /><br /> number|数据类型|注释|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|@shouldalert|Varchar|目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有目录这些表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有架构这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar 不为 NULL|表名。|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar 不为 NULL|列名称。 该驱动程序返回的列没有名称为空字符串。|  
|DATA_TYPE (ODBC 1.0)|5|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间和间隔的数据类型，此列返回的简洁数据类型 （例如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH，而不是如 SQL_DATETIME 或 SQL_INTERVAL nonconcise 数据类型）。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型中。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。<br /><br /> 对于 ODBC 3 返回的数据类型。*x*和 ODBC 2。*x*应用程序可能会不同。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|TYPE_NAME (ODBC 1.0)|6|Varchar 不为 NULL|数据源 – 依赖于数据类型名称;例如，"CHAR"、"VARCHAR"、"货币"、"长 VARBINAR"或者"CHAR （） FOR BIT DATA"。|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|如果 DATA_TYPE SQL_CHAR 或 SQL_VARCHAR，此列将包含以字符为单位的列的最大长度。 对于 datetime 数据类型，这是所需的值转换为字符时显示的字符总数。 对于数值数据类型，这根据 NUM_PREC_RADIX 列是的位数总数，或者在列中，允许的位的总数。 对于 interval 数据类型，这是中的字符表示形式的间隔文本的字符数 (由前导精度的间隔的定义，请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)附录 d： 数据类型中)。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|如果指定 SQL_C_DEFAULT，以字节为单位的数据的长度对 SQLGetData、 SQLFetch 或 SQLFetchScroll 操作传输。 对于数值数据，此大小可能与数据源上存储的数据的大小不同。 此值可能会与为字符数据的 COLUMN_SIZE 列不同。 有关长度的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|小数点右侧的位数总数。 对于 SQL_TYPE_TIME SQL_TYPE_TIMESTAMP，此列包含秒的小数部分组件中的数字个数。 对于其他数据类型，这是对数据源列的十进制数字。 对于包含时间组件的 interval 数据类型，此列包含小数点 （秒的小数部分） 右侧的数字个数。 对于不包含时间组件的 interval 数据类型，此列将为 0。 有关十进制数字的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。 不适用 DECIMAL_DIGITS 为数据类型返回 NULL。|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|对于数值数据类型，为 10 或 2。 如果它为 10，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值为提供的允许的列的十进制位数。 例如，DECIMAL(12,5) 列将返回 10，12，COLUMN_SIZE 和 5; DECIMAL_DIGITS NUM_PREC_RADIXFLOAT 列可能会返回为 10，15，COLUMN_SIZE 和 DECIMAL_DIGITS 的 NULL NUM_PREC_RADIX。<br /><br /> 如果该值为 2，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值为列中允许的比特数。 例如，FLOAT 列可能会返回一个基数为 2，53，COLUMN_SIZE 和 DECIMAL_DIGITS 的 NULL。<br /><br /> 不适用 NUM_PREC_RADIX 为数据类型返回 NULL。|  
|可以为 NULL (ODBC 1.0)|11|Smallint（非 NULL）|SQL_NO_NULLS 如果列不可包含 NULL 值。<br /><br /> SQL_NULLABLE 如果列接受 NULL 值。<br /><br /> SQL_NULLABLE_UNKNOWN 如果它不已知的列是否接受 NULL 值。<br /><br /> 此列返回的值不同于 IS_NULLABLE 列返回的值。 列可以接受 null 值，但不能指示某一列不接受 null 值的明确地明确地指示可以为 NULL 的列。 列不能接受 null 值，但不能指示列接受 null 值的明确地明确地指示 IS_NULLABLE 列。|  
|备注 (ODBC 1.0)|12|Varchar|列的说明。|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|列的默认值。 如果它用引号引起来，应将此列中的值视为字符串。<br /><br /> 如果指定 NULL 为默认值，此列将是未用引号引起来的单词 NULL。 如果默认值不能表示而不发生截断，则此列包含截断，没有用单引号引起来。 如果未不指定任何默认值，此列将为 NULL。<br /><br /> 可以在包含值截断时除外生成新的列定义，使用 COLUMN_DEF 的值。|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint（非 NULL）|SQL 数据类型，在 IRD 的 SQL_DESC_TYPE 记录字段中所示。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 此列是 DATA_TYPE 列中的日期时间和间隔数据类型除外，相同。 此列返回的 nonconcise 数据类型 （例如 SQL_DATETIME 或 SQL_INTERVAL），而不是简洁数据类型 （如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH） 对于 datetime 和 interval 数据类型。 如果此列返回 SQL_DATETIME 或 SQL_INTERVAL，可以从 SQL_DATETIME_SUB 列来确定特定的数据类型。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型中。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。<br /><br /> 对于 ODBC 3 返回的数据类型。*x*和 ODBC 2。*x*应用程序可能会不同。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|日期时间和间隔数据类型的子类型代码。 对于其他数据类型，此列返回 NULL。 有关日期时间和间隔子代码的详细信息，请参阅"SQL_DESC_DATETIME_INTERVAL_CODE"中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|以字节为单位的最大长度的字符或二进制数据类型列。 对于所有其他数据类型，此列返回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer（非 NULL）|表中列的序号位置。 表中的第一列是数字 1。|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"否"如果列不包括 null 值。<br /><br /> "是"如果列无法包含 null 值。<br /><br /> 如果为 Null 性为未知，该列将返回零长度字符串。<br /><br /> 根据 ISO 规则确定为 Null 性。 符合 ISO SQL – DBMS 不能返回一个空字符串。<br /><br /> 此列返回的值可以为 NULL 的列返回的值不同。 （请参阅为 NULL 的列的说明。）|  
  
## <a name="code-example"></a>代码示例  
 应用程序在以下示例中，声明为返回的结果集的缓冲区**SQLColumns**。 它调用**SQLColumns**以返回员工表中的每个列的说明结果集。 然后，它调用**SQLBindCol**将列绑定中的结果集的缓冲区。 最后，应用程序，则提取的数据与每个行**SQLFetch**然后处理该请求。  
  
```  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回为一列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取数据的多个的行|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回唯一标识一行的列或列自动更新的事务|[SQLSpecialColumns 函数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|数据源中返回表的列表|[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)|  
|返回一个表或表的权限|[SQLTablePrivileges 函数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
