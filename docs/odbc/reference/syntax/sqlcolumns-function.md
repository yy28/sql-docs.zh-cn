---
title: SQLColumns 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301253"
---
# <a name="sqlcolumns-function"></a>SQLColumns 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 开放组  
  
 **摘要**  
 **SQLColumn**返回指定表中的列名称列表。 驱动程序将返回此信息作为在指定的*语句句柄*上集的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（"）表示那些没有目录的表。 *目录名称*不能包含字符串搜索模式。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*将被视为标识符，其大小写不重要。 如果SQL_FALSE，目录名称是普通参数;如果为"*目录名称"，则为"目录名称"，* 但为"目录名称"，但为"目录名称"，但它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度在 **目录名称*的字符中。  
  
 *架构名称*  
 [输入]架构名称的字符串搜索模式。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（"）表示那些没有架构的表。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 SchemaName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则 SchemaName 是模式值参数;如果为 SQL_FALSE，则 *"架构名称"* 是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度在 **架构名称*的字符中。  
  
 *表名称*  
 [输入]表名称的字符串搜索模式。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则表Name*被视为标识符，其大小写不重要。 如果SQL_FALSE，*则表名称*是模式值参数;如果为"表名称"，则表名称是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]=*表名*的字符的长度。  
  
 *ColumnName*  
 [输入]字符串搜索模式的列名称。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*ColumnName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则"列名"是模式值参数;如果为"*列名称"，* 则为"列名"，即为模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度4*  
 [输入]长度以 =*列名*的字符表示。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLColumns**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了 SQLLists 通常返回的**SQLSTATE**值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但未调用**SQLFetch**或**SQLFetchScroll。**|  
|40001|序列化失败|由于资源与另一个事务死锁，事务被回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*目录名称*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*并且 SchemaName*名称、*表名*或*列名*参数为空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLColumns**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 其中一个名称长度参数的值小于 0，但不等于SQL_NTS。|  
|||其中一个名称长度参数的值超过相应目录或名称的最大长度值。 每个目录或名称的最大长度可以通过使用*InfoType*值调用**SQLGetInfo**获得。 （请参阅"注释"。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了目录名称，并且驱动程序或数据源不支持目录。<br /><br /> 指定了架构名称，驱动程序或数据源不支持架构。<br /><br /> 为架构名称、表名称或列名称指定了字符串搜索模式，数据源不支持一个或多个这些参数的搜索模式。<br /><br /> 驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 此函数通常在语句执行之前用于从数据源的目录中检索有关表或表的列的信息。 **SQLColumns**可用于检索**SQLTables**返回的所有类型的项的数据。 除了基表之外，这可能包括（但不限于）视图、同义词、系统表等。 相反，**函数 SQLColAttribute**和**SQLDescribeCol**描述结果集中的列，函数**SQLNumResultCols**返回结果集中的列数。 有关详细信息，请参阅[目录数据的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLColumns**将结果作为标准结果集返回，按TABLE_CAT、TABLE_SCHEM、TABLE_NAME和ORDINAL_POSITION排序。  
  
> [!NOTE]  
>  当应用程序使用 ODBC 2 时。*x*驱动程序，结果集中不返回ORDINAL_POSITION列。 因此，当使用 ODBC 2 时。*x*驱动程序 **，SQLColumn**返回的列列表中列的顺序不一定与应用程序对该表中的所有列执行 SELECT 语句时返回的列的顺序相同。  
  
> [!NOTE]  
>  **SQLColumns**可能不会返回所有列。 例如，驱动程序可能不会返回有关伪列的信息，例如 Oracle ROWID。 应用程序可以使用任何有效的列，无论它是由**SQLColumn**返回的。  
>   
>  **SQLStatistics**可以返回的某些列不会由**SQLColumns**返回。 例如 **，SQLColumns**不会返回通过表达式或筛选器创建的索引中的列，例如"工资"或"福利"或"DEPT = 0012"。  
  
 VARCHAR 列的长度不显示在表中;因此，VARCHAR 列的长度不显示在表中。实际长度取决于数据源。 要确定TABLE_CAT、TABLE_SCHEM、TABLE_NAME和COLUMN_NAME列的实际长度，应用程序可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN选项调用**SQLGetInfo。**  
  
 以下列已重命名为 ODBC 3。*x*. . 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC 3.*x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 以下列已添加到**SQLColumns**为 ODBC 3 返回的结果集中。*x*：  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 下表列出了结果集中的列。 驱动程序可以定义第 18 列（IS_NULLABLE）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列<br /><br /> 数字|数据类型|注释|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的表。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的表。|  
|TABLE_NAME （ODBC 1.0）|3|瓦尔查尔不是 NULL|表名。|  
|COLUMN_NAME （ODBC 1.0）|4|瓦尔查尔不是 NULL|列名称。 驱动程序返回没有名称的列的空字符串。|  
|DATA_TYPE （ODBC 1.0）|5|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间和间隔数据类型，此列返回简明的数据类型（如SQL_TYPE_DATE或SQL_INTERVAL_YEAR_TO_MONTH，而不是非简洁数据类型（如SQL_DATETIME或SQL_INTERVAL）。 有关有效的 ODBC SQL 数据类型的列表，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。<br /><br /> 为 ODBC 3 返回的数据类型。*x*和 ODBC 2。*x*应用程序可能不同。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|TYPE_NAME （ODBC 1.0）|6|瓦尔查尔不是 NULL|与数据源相关的数据类型名称;例如，"CHAR"，"VARCHAR"，"金钱"，"长VARBINAR"，或"CHAR （ ） BIT 数据"。|  
|COLUMN_SIZE （ODBC 1.0）|7|Integer|如果DATA_TYPE是SQL_CHAR或SQL_VARCHAR，则此列包含列的最大长度（以字符表示）。 对于日期时间数据类型，这是将值转换为字符时显示值所需的字符总数。 对于数字数据类型，根据NUM_PREC_RADIX列，这是数字总数或列中允许的位数总数。 对于间隔数据类型，这是间隔文本的字符表示中的字符数（由间隔前导精度定义，请参阅附录 D 中的[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)：数据类型）。 有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|BUFFER_LENGTH （ODBC 1.0）|8|Integer|如果指定了SQL_C_DEFAULT，则 SQLGetData、SQLFetch 或 SQLFetchScroll 操作上传输的数据的长度（以字节为单位）。 对于数字数据，此大小可能与存储在数据源上的数据的大小不同。 此值可能与字符数据的COLUMN_SIZE列不同。 有关长度的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|DECIMAL_DIGITS （ODBC 1.0）|9|Smallint|小数点右侧的重要数字的总数。 对于SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP，此列包含小数秒组件中的位数。 对于其他数据类型，这是数据源上列的小数位数。 对于包含时间分量的间隔数据类型，此列包含小数点右侧的数字数（分数秒）。 对于不包含时间组件的间隔数据类型，此列为 0。 有关十进制数字的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。 对于不适用DECIMAL_DIGITS的数据类型，将返回 NULL。|  
|NUM_PREC_RADIX （ODBC 1.0）|10|Smallint|对于数字数据类型，10 或 2。 如果为 10，则COLUMN_SIZE和DECIMAL_DIGITS中的值将给出该列允许的十进制数字数。 例如，DECIMAL（12，5）列将返回NUM_PREC_RADIX 10、COLUMN_SIZE 12 和 DECIMAL_DIGITS 5;FLOAT 列可以返回 10 NUM_PREC_RADIX、COLUMN_SIZE 15 和 null DECIMAL_DIGITS。<br /><br /> 如果是 2，则COLUMN_SIZE和DECIMAL_DIGITS中的值给出列中允许的位数。 例如，FLOAT 列可以返回 2 的 RADIX、COLUMN_SIZE 53 和 NULL DECIMAL_DIGITS。<br /><br /> 对于不适用NUM_PREC_RADIX的数据类型，将返回 NULL。|  
|空值（ODBC 1.0）|11|Smallint（非 NULL）|如果列不能包含 NULL 值，则SQL_NO_NULLS。<br /><br /> 如果列接受 NULL 值，则SQL_NULLABLE。<br /><br /> 如果不知道列是否接受 NULL 值，则SQL_NULLABLE_UNKNOWN。<br /><br /> 此列返回的值不同于为IS_NULLABLE列返回的值。 NULLABLE 列明确指示列可以接受 NULL，但无法肯定地指示列不接受 NUL。 IS_NULLABLE列明确指示列不能接受 NUL，但无法肯定地指示列是否接受 NUL。|  
|备注 （ODBC 1.0）|12|Varchar|列的说明。|  
|COLUMN_DEF （ODBC 3.0）|13|Varchar|列的默认值。 如果此列中的值包含在引号中，则应将其解释为字符串。<br /><br /> 如果 NULL 被指定为默认值，则此列是单词 NULL，而不是用引号括起来。 如果不进行截断就无法表示默认值，则此列包含截断，而不包含单个引号。 如果未指定默认值，则此列为 NULL。<br /><br /> COLUMN_DEF的值可用于生成新的列定义，除非它包含 TRUNCATED 的值。|  
|SQL_DATA_TYPE （ODBC 3.0）|14|Smallint（非 NULL）|SQL 数据类型，如 iRD 中SQL_DESC_TYPE记录字段中显示的。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 此列与DATA_TYPE列相同，但日期时间和间隔数据类型除外。 此列返回日期时间和间隔数据类型的非简明数据类型（如SQL_DATETIME或SQL_INTERVAL），而不是简明的数据类型（如SQL_TYPE_DATE或SQL_INTERVAL_YEAR_TO_MONTH）。 如果此列返回SQL_DATETIME或SQL_INTERVAL，则可以从SQL_DATETIME_SUB列确定特定的数据类型。 有关有效的 ODBC SQL 数据类型的列表，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。<br /><br /> 为 ODBC 3 返回的数据类型。*x*和 ODBC 2。*x*应用程序可能不同。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|SQL_DATETIME_SUB （ODBC 3.0）|15|Smallint|日期时间和间隔数据类型的子类型代码。 对于其他数据类型，此列返回 NULL。 有关日期时间和间隔子代码的详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"SQL_DESC_DATETIME_INTERVAL_CODE"。|  
|CHAR_OCTET_LENGTH （ODBC 3.0）|16|Integer|字符或二进制数据类型列的最大长度（以字节为单位）。 对于所有其他数据类型，此列返回 NULL。|  
|ORDINAL_POSITION （ODBC 3.0）|17|Integer（非 NULL）|列在表中的盘位位置。 表中的第一列是数字 1。|  
|IS_NULLABLE （ODBC 3.0）|18|Varchar|如果列不包含 NUL，则为"否"。<br /><br /> 如果列可以包含 NUL，则为"是"。<br /><br /> 如果为 Null 性为未知，该列将返回零长度字符串。<br /><br /> 根据 ISO 规则确定为 Null 性。 遵从 ISO SQL 标准的 DBMS 不能返回空字符串。<br /><br /> 此列返回的值与 NULLABLE 列返回的值不同。 （请参阅 NULLABLE 列的说明。|  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序声明**SQLColumns**返回的结果集的缓冲区。 它调用**SQLColumn**返回描述 EMPLOYER 表中每一列的结果集。 然后，它调用**SQLBindCol**将结果集中的列绑定到缓冲区。 最后，应用程序使用**SQLFetch**获取每一行数据并处理它。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回唯一标识行的列，或由事务自动更新的列|[SQLSpecialColumns 函数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|返回数据源中的表列表|[SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)|  
|返回表或表的权限|[SQLTablePrivileges Function（SQLTablePrivileges 函数）](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
