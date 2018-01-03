---
title: "SQLGetTypeInfo 函数 |Microsoft 文档"
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
apiname: SQLGetTypeInfo
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetTypeInfo
helpviewer_keywords: SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 508b89f5ff60b5cf64a03d167bf1ad4476edb734
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**返回有关支持的数据源的数据类型的信息。 该驱动程序的 SQL 结果集的形式返回的信息。 数据类型用于在数据定义语言 (DDL) 语句中使用。  
  
> [!IMPORTANT]  
>  应用程序必须使用在 TYPE_NAME 列中返回的类型名称**SQLGetTypeInfo**结果集内**ALTER TABLE**和**CREATE TABLE**语句。 **SQLGetTypeInfo**可能返回 DATA_TYPE 列中的多个行具有相同的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]结果集的的语句句柄。  
  
 *数据类型*  
 [输入]SQL 数据类型。 这必须是中的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型或特定于驱动程序的 SQL 数据类型的部分。 SQL_ALL_TYPES 指定应返回有关所有数据类型的信息。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetTypeInfo**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetTypeInfo**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|指定的语句属性由于实现工作条件无效，因此暂时替换类似的值。 (调用**SQLGetStmtAttr**若要确定暂时被替换的值。)替换值可用于*StatementHandle*直到关闭游标。 可以更改这些语句属性包括： SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_KEYSET_SIZE、 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS、 SQL_ATTR_QUERY_TIMEOUT 和 SQL_ATTR_SIMULATE_CURSOR。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle，*和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，并且如果由驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 结果集上打开了*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY004|SQL 数据类型无效|为参数指定的值*DataType*已既不是有效的 ODBC SQL 数据类型标识符，也不支持驱动程序的特定于驱动程序的数据类型标识符。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*，然后调用该函数，并它之前完成执行， **SQLCancel**或**SQLCancelHandle**已对调用*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetTypeInfo**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLGetTypeInfo**标准的结果集，先按 DATA_TYPE 然后按排序的数据类型映射到相应的 ODBC SQL 数据类型的紧密程度的形式返回结果。 定义数据源的数据类型的优先于用户定义的数据类型。 因此，排序顺序不一定一致，但可以是首先为 DATA_TYPE 通用化后, 跟类型 _ 名称，这两个升序。 例如，假设数据源定义整数和计数器的数据类型，其中计数器是自动递增，并且用户定义数据类型 WHOLENUM 也已定义。 这些将返回按顺序整数，WHOLENUM，和计数器，因为 WHOLENUM 紧密映射到 ODBC SQL 数据类型 SQL_INTEGER 时的自动递增数据类型，, 即使支持的数据源，不会不严格地映射到 ODBC SQL 数据类型。 有关如何可能使用此信息的信息，请参阅[DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*DataType*自变量指定为有效的 ODBC 驱动程序，支持的版本的数据类型，但不是支持驱动程序，则它将返回空结果集。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下面的列已重命名为 ODBC 3。*x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 下面的列已添加到返回的结果集**SQLGetTypeInfo** ODBC 3。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 19 (INTERVAL_PRECISION) 之外的其他列。 应用程序应访问驱动程序的特定列按倒计时从结果集的末尾，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不会返回所有数据类型。 例如，驱动程序可能不返回用户定义的数据类型。 应用程序可以使用任何有效的数据类型，而不考虑是否将它返回由**SQLGetTypeInfo**。 通过返回的数据类型**SQLGetTypeInfo**是所支持的数据源。 用于在数据定义语言 (DDL) 语句中使用它们。 驱动程序可以返回使用以外的返回类型的数据类型的结果集数据**SQLGetTypeInfo**。 在创建的目录函数的结果集，该驱动程序可能由数据源使用不支持的数据类型。  
  
|列名|“列”<br /><br /> number|数据类型|注释|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|@shouldalert|Varchar 不为 NULL|数据源 – 依赖于数据类型名称;例如，"char （）"、"VARCHAR()"、"货币"、"长 VARBINARY"或者"CHAR （） FOR BIT DATA"。 应用程序必须使用此名称在**CREATE TABLE**和**ALTER TABLE**语句。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于日期时间或间隔的数据类型，此列返回的简洁数据类型 （例如 SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型中。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|服务器支持此数据类型的最大列大小。 对于数值数据，这是最大精度。 对于字符串数据，这是以字符为单位的长度。 对于 datetime 数据类型，这是以字符串表示形式 （假定小数秒元素允许的最大精度） 的字符为单位的长度。 不适用列大小的数据类型返回 NULL。 对于 interval 数据类型，这是中的字符表示形式的间隔文本的字符数 (由前导精度的间隔定义看到[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)附录 d： 数据类型中)。<br /><br /> 列大小的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|字符或字符用于前缀文本;例如，可用一个单引号 （'） 的字符数据类型或二进制数据类型; 0x不适用的文本的前缀为数据类型返回 NULL。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|字符或字符用于终止文本;例如，对于字符数据类型; 可用一个单引号 （'）不适用的文本的后缀为数据类型返回 NULL。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|关键字，由逗号分隔，使用返回类型 _ 名称字段中的名称时，应用程序可以指定在括号中的每个参数对应的列表。 在列表中的关键字可以是以下任一： 长度、 精度或小数位数。 它们，则语法要求在其可以用于顺序出现。 例如，表示小数点 CREATE_PARAMS 将"精度、 小数位数";对于 VARCHAR CREATE_PARAMS 将等于"长度"。 如果没有为数据类型定义; 参数，则返回 NULL例如，整数。<br /><br /> 驱动程序提供使用它的国家/地区的语言中的 CREATE_PARAMS 文本。|  
|可以为 NULL (ODBC 2.0)|7|Smallint（非 NULL）|是否接受 NULL 值数据类型：<br /><br /> SQL_NO_NULLS 如果数据类型不接受 NULL 值。<br /><br /> SQL_NULLABLE 如果接受 NULL 值的数据类型。<br /><br /> SQL_NULLABLE_UNKNOWN 如果它不已知的列是否接受 NULL 值。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint（非 NULL）|字符数据类型是否区分大小写的排序规则和比较中：<br /><br /> 如果数据类型是字符数据类型，并且区分大小写的 SQL_TRUE。<br /><br /> 如果数据类型不是字符数据类型或不区分大小写的 SQL_FALSE。|  
|可搜索 (ODBC 2.0)|9|Smallint（非 NULL）|如何在中使用的数据类型**其中**子句：<br /><br /> 如果列不能在 SQL_PRED_NONE**其中**子句。 （这是与 ODBC 2 中的 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果列可在 SQL_PRED_CHAR**其中**子句，但仅适合**如**谓词。 （这是与 ODBC 2 中的 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> SQL_PRED_BASIC 如果列可在**其中**子句与除之外的所有比较运算符**如**(比较、 定量的比较**BETWEEN**， **非重复**， **IN**，**匹配**，和**UNIQUE**)。 （这是与 ODBC 2 中的 SQL_ALL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果列可在 SQL_SEARCHABLE**其中**子句的任何比较运算符。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|是否是无符号数据类型：<br /><br /> 如果数据类型是无符号，SQL_TRUE。<br /><br /> SQL_FALSE 如果签名的数据类型。<br /><br /> 如果该属性不是适用于该数据类型或数据类型不是数值，则返回 NULL。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint（非 NULL）|数据类型是否具有预定义固定精度和小数位数 （它们都是数据源 – 特定），如 money 数据类型：<br /><br /> 如果它已预定义的 SQL_TRUE 固定精度和小数位数。<br /><br /> 如果它不具有预定义的固定的精度和小数位数，SQL_FALSE。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|数据类型是否自动增量：<br /><br /> 如果数据类型是自动增量，SQL_TRUE。<br /><br /> 如果数据类型不是自动增量，SQL_FALSE。<br /><br /> 如果该属性不是适用于该数据类型或数据类型不是数值，则返回 NULL。<br /><br /> 应用程序可以将值插入列都有此属性，但通常不能更新列中的值。<br /><br /> 当插入将变成自动递增列时，唯一的值将在插入时，插入到列。 增量未定义，但数据源 – 特定。 应用程序不应假定启动在任何特定点或增量的自动递增列按任何特定值。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|数据类型的数据源 – 依赖名称的本地化的版本。 如果是数据源不支持的本地化名称，则返回 NULL。 此名称用于显示唯一，如所显示对话框。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|数据源上的数据类型最小刻度。 如果数据类型的小数位数是固定的，则 MINIMUM_SCALE 和 MAXIMUM_SCALE 列将同时包含此值。 例如，SQL_TYPE_TIMESTAMP 列可能秒的小数部分具有固定小数位数。 当小数位数不适用时，将返回 NULL。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|数据源上的数据类型最大刻度。 当小数位数不适用时，将返回 NULL。 如果最大刻度上的数据源，未单独定义，但改为定义为最大精度相同，则此列包含 COLUMN_SIZE 列相同的值。 有关详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint 不为 NULL|SQL 数据类型，因为它的值显示在 SQL_DESC_TYPE 字段中的描述符。 此列是 DATA_TYPE 列中的间隔和 datetime 数据类型除外，相同。<br /><br /> 对于间隔和 datetime 数据类型，在结果集中的 SQL_DATA_TYPE 字段将返回 SQL_INTERVAL 或 SQL_DATETIME，和 SQL_DATETIME_SUB 字段将返回特定的间隔或日期时间数据类型的子代码。 (请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|SQL_DATETIME 或 SQL_INTERVAL SQL_DATA_TYPE 的值时，此列包含的 datetime/间隔子代码。 对于日期时间和间隔以外的数据类型，此字段为 NULL。<br /><br /> 对于间隔或日期时间数据类型，在结果集中的 SQL_DATA_TYPE 字段将返回 SQL_INTERVAL 或 SQL_DATETIME，和 SQL_DATETIME_SUB 字段将返回特定的间隔或日期时间数据类型的子代码。 (请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|如果数据类型是近似的数值类型，此列包含值 2 指示 COLUMN_SIZE 指定的位数。 对于精确数字数据类型，此列包含值为 10，指示 COLUMN_SIZE 指定的十进制数字。 否则，此列为 NULL。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|如果数据类型不是间隔数据类型，则此列包含时间间隔前导精度的值。 (请参阅[间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)附录 d： 数据类型中。)否则，此列为 NULL。|  
  
 属性的信息可以应用于数据类型或结果集中的特定列。 **SQLGetTypeInfo**返回有关与数据类型; 关联的属性的信息**SQLColAttribute**返回的结果集中的列关联的属性有关的信息。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLColAttribute 函数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回有关的驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
