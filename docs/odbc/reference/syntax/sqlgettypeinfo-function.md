---
title: SQLGetTypeInfo 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303258"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**返回有关数据源支持的数据类型的信息。 驱动程序以 SQL 结果集的形式返回信息。 数据类型用于数据定义语言 （DDL） 语句。  
  
> [!IMPORTANT]  
>  应用程序必须使用在**ALTER TABLE**和 CREATE **TABLE**语句中**SQLGetTypeInfo**结果集的TYPE_NAME列中返回的类型名称。 **SQLGetTypeInfo**可能会返回DATA_TYPE列中具有相同值的多行。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]结果集的语句句柄。  
  
 *DataType*  
 [输入]SQL 数据类型。 这必须是附录 D：数据类型或特定于驱动程序的 SQL 数据类型的[SQL 数据类型中的值](../../../odbc/reference/appendixes/sql-data-types.md)之一。 SQL_ALL_TYPES指定应返回有关所有数据类型的信息。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetTypeInfo**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLGetTypeInfo**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|由于实现工作条件，指定的语句属性无效，因此临时替换了类似的值。 （调用**SQLGetStmtAttr**以确定临时替换的值。在光标关闭之前，替换值对*语句处理*有效。 可以更改的语句属性包括：SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT和SQL_ATTR_SIMULATE_CURSOR。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|*语句处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *在语句句柄*上打开了结果集，但未调用**SQLFetch**或**SQLFetchScroll。**|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY004|无效的 SQL 数据类型|为参数*DataType*指定的值既不是有效的 ODBC SQL 数据类型标识符，也不是驱动程序支持的特定于驱动程序的数据类型标识符。|  
|HY008|操作已取消|异步处理为*语句句柄*启用，然后调用函数，并在函数完成执行之前，在语句句柄上调用**SQLCancel**或**SQLCancelHandle。** *StatementHandle* 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，并在它完成执行之前 **，SQLCancel**或**SQLCancelHandle**从多线程应用程序中的不同线程调用*了语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLGetTypeInfo**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*对应的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **SQLGetTypeInfo**将结果作为标准结果集返回，该结果由DATA_TYPE排序，然后按数据类型映射到相应 ODBC SQL 数据类型的紧密程度排序。 数据源定义的数据类型优先于用户定义的数据类型。 因此，排序顺序不一定一致，但可以概括为DATA_TYPE第一，然后是TYPE_NAME，两者都是提升。 例如，假设数据源定义了 INTEGER 和 COUNTER 数据类型，其中 COUNTER 正在自动递增，并且用户定义的数据类型也已定义。 这些数据将按 INTEGER、WHOLENUM 和 COUNTER 的顺序返回，因为 WHOLENUM 与 ODBC SQL 数据类型紧密映射SQL_INTEGER，而自动递增数据类型（即使受数据源支持）也不会紧密映射到 ODBC SQL 数据类型。 有关如何使用此信息的信息，请参阅[DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*DataType*参数指定对驱动程序支持的 ODBC 版本有效的数据类型，但驱动程序不支持该数据类型，则它将返回一个空结果集。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 以下列已重命名为 ODBC 3。*x*. . 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC 3.*x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 以下列已添加到**SQLGetTypeInfo**为 ODBC 3 返回的结果集中。*x*：  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出了结果集中的列。 驱动程序可以定义第 19 列（INTERVAL_PRECISION）以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不会返回所有数据类型。 例如，驱动程序可能不会返回用户定义的数据类型。 应用程序可以使用任何有效的数据类型，而不管它是否由**SQLGetTypeInfo**返回。 **SQLGetTypeInfo**返回的数据类型是数据源支持的数据类型。 它们用于数据定义语言 （DDL） 语句。 驱动程序可以使用**SQLGetTypeInfo**返回的类型以外的数据类型返回结果集数据。 在为目录函数创建结果集时，驱动程序可能使用数据源不支持的数据类型。  
  
|列名称|列<br /><br /> 数字|数据类型|注释|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME （ODBC 2.0）|1|瓦尔查尔不是 NULL|与数据源相关的数据类型名称;例如，"CHAR（）"，"VARCHAR（）"，"金钱"，"长VARBINARY"或"CHAR （ ） BIT 数据"。 应用程序必须在**创建表**和**ALTER TABLE**语句中使用此名称。|  
|DATA_TYPE （ODBC 2.0）|2|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间或间隔数据类型，此列返回简洁的数据类型（如SQL_TYPE_TIME或SQL_INTERVAL_YEAR_TO_MONTH）。 有关有效的 ODBC SQL 数据类型的列表，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|COLUMN_SIZE （ODBC 2.0）|3|Integer|服务器支持此数据类型的最大列大小。 对于数字数据，这是最大精度。 对于字符串数据，这是字符的长度。 对于日期时间数据类型，这是字符串表示的字符长度（假设小数秒组件允许的最大精度）。 对于不适用的列大小数据类型，将返回 NULL。 对于间隔数据类型，这是间隔文本的字符表示中的字符数（由间隔前导精度定义;请参阅附录 D 中的[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)：数据类型）。<br /><br /> 有关列大小的详细信息，请参阅附录 D：数据类型中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|LITERAL_PREFIX （ODBC 2.0）|4|Varchar|用于前缀文本的字符或字符;例如，字符数据类型的单个引号 （'） 或二进制数据类型的 0x;对于不适用文本前缀的数据类型，将返回 NULL。|  
|LITERAL_SUFFIX （ODBC 2.0）|5|Varchar|用于终止文本的字符或字符;例如，字符数据类型的单个引号 （'）;对于不适用于文本后缀的数据类型，将返回 NULL。|  
|CREATE_PARAMS （ODBC 2.0）|6|Varchar|关键字列表，用逗号分隔，对应于应用程序在使用TYPE_NAME字段中返回的名称时在括号中指定的每个参数。 列表中的关键字可以是以下任一关键字：长度、精度或比例。 它们按语法要求使用它们的顺序出现。 例如，DECIMALCREATE_PARAMS是"精度、缩放";VARCHAR 的CREATE_PARAMS等于"长度"。 如果数据类型定义没有参数，则返回 NULL;例如，INTEGER。<br /><br /> 驱动程序以使用该驱动程序的国家/地区的语言提供CREATE_PARAMS文本。|  
|空值 （ODBC 2.0）|7|Smallint（非 NULL）|数据类型是否接受 NULL 值：<br /><br /> 如果数据类型不接受 NULL 值，则SQL_NO_NULLS。<br /><br /> 如果数据类型接受 NULL 值，SQL_NULLABLE。<br /><br /> 如果不知道列是否接受 NULL 值，则SQL_NULLABLE_UNKNOWN。|  
|CASE_SENSITIVE （ODBC 2.0）|8|Smallint（非 NULL）|字符数据类型在排序规则和比较中是否区分大小写：<br /><br /> 如果数据类型为字符数据类型且区分大小写，SQL_TRUE。<br /><br /> 如果数据类型不是字符数据类型或区分大小写，SQL_FALSE。|  
|可搜索 （ODBC 2.0）|9|Smallint（非 NULL）|**在 WHERE**子句中如何使用数据类型：<br /><br /> 如果列不能在**WHERE**子句中使用，则SQL_PRED_NONE。 （这与 ODBC 2 中的SQL_UNSEARCHABLE值相同。*x*.）<br /><br /> SQL_PRED_CHAR列是否可以在**WHERE**子句中使用，但只能与**LIKE**谓词一起使用。 （这与 ODBC 2 中的SQL_LIKE_ONLY值相同。*x*.）<br /><br /> SQL_PRED_BASIC如果该列可以在**WHERE**子句中使用，并且所有比较运算符 **（LIKE、** 量化比较 **、"匹配****"、"差异****"、IN、MATCH**和**UNIQUE）** 除外。 **MATCH** （这与 ODBC 2 中的SQL_ALL_EXCEPT_LIKE值相同。*x*.）<br /><br /> SQL_SEARCHABLE列是否可以在任何比较运算符的**WHERE**子句中使用。|  
|UNSIGNED_ATTRIBUTE （ODBC 2.0）|10|Smallint|数据类型是否未签名：<br /><br /> SQL_TRUE数据类型是否未签名。<br /><br /> 如果数据类型已签名，SQL_FALSE。<br /><br /> 如果属性不适用于数据类型或数据类型不是数字，则返回 NULL。|  
|FIXED_PREC_SCALE （ODBC 2.0）|11|Smallint（非 NULL）|数据类型是否具有预定义的固定精度和缩放（这是特定于数据源的），例如货币数据类型：<br /><br /> SQL_TRUE，如果它具有预定义的固定精度和比例。<br /><br /> SQL_FALSE，如果它没有预定义的固定精度和比例。|  
|AUTO_UNIQUE_VALUE （ODBC 2.0）|12|Smallint|数据类型是否自动递增：<br /><br /> 如果数据类型自动递增，SQL_TRUE。<br /><br /> 如果数据类型不是自动递增，则SQL_FALSE。<br /><br /> 如果属性不适用于数据类型或数据类型不是数字，则返回 NULL。<br /><br /> 应用程序可以将值插入具有此属性的列中，但通常无法更新列中的值。<br /><br /> 当将插入到自动增量列中时，在插入时将一个唯一值插入到列中。 增量未定义，但特定于数据源。 应用程序不应假定自动增量列从任何特定点开始，或由任何特定值增量。|  
|LOCAL_TYPE_NAME （ODBC 2.0）|13|Varchar|与数据源相关的数据类型名称的本地化版本。 如果是数据源不支持的本地化名称，则返回 NULL。 此名称仅用于显示，例如在对话框中。|  
|MINIMUM_SCALE （ODBC 2.0）|14|Smallint|数据源上数据类型的最小比例。 如果数据类型的小数位数是固定的，则 MINIMUM_SCALE 和 MAXIMUM_SCALE 列将同时包含此值。 例如，SQL_TYPE_TIMESTAMP列可能具有小数秒的固定比例。 当小数位数不适用时，将返回 NULL。 有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|MAXIMUM_SCALE （ODBC 2.0）|15|Smallint|数据源上数据类型的最大比例。 当小数位数不适用时，将返回 NULL。 如果在数据源上未单独定义最大比例，而是定义为与最大精度相同，则此列包含与COLUMN_SIZE列相同的值。 有关详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。|  
|SQL_DATA_TYPE （ODBC 3.0）|16|小值不为空|SQL 数据类型的值，如它在描述符的SQL_DESC_TYPE字段中显示的。 此列与DATA_TYPE列相同，间隔和日期时间数据类型除外。<br /><br /> 对于间隔和日期时间数据类型，结果集中的SQL_DATA_TYPE字段将返回SQL_INTERVAL或SQL_DATETIME，SQL_DATETIME_SUB字段将返回特定间隔或日期时间数据类型的子代码。 （参见[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|SQL_DATETIME_SUB （ODBC 3.0）|17|Smallint|当SQL_DATA_TYPE值为SQL_DATETIME或SQL_INTERVAL时，此列包含日期时间/间隔子代码。 对于日期时间和间隔以外的数据类型，此字段为 NULL。<br /><br /> 对于间隔或日期时间数据类型，结果集中的SQL_DATA_TYPE字段将返回SQL_INTERVAL或SQL_DATETIME，SQL_DATETIME_SUB字段将返回特定间隔或日期时间数据类型的子代码。 （参见[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|NUM_PREC_RADIX （ODBC 3.0）|18|Integer|如果数据类型是近似数值类型，则此列包含值 2 以指示COLUMN_SIZE指定多个位。 对于确切的数值类型，此列包含值 10 以指示COLUMN_SIZE指定小数位数。 否则，此列为 NULL。|  
|INTERVAL_PRECISION （ODBC 3.0）|19|Smallint|如果数据类型是间隔数据类型，则此列包含间隔前导精度的值。 （请参阅附录 D 中的[间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)：数据类型。否则，此列为 NULL。|  
  
 属性信息可以应用于数据类型或结果集中的特定列。 **SQLGetTypeInfo**返回有关与数据类型关联的属性的信息;**SQLColAttribute**返回有关与结果集中列关联的属性的信息。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLColAttribute 函数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
