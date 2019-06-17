---
title: SQLGetTypeInfo Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aef1e90053eba71db84e1fe89aa90684829a4941
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536538"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**返回有关支持的数据源的数据类型的信息。 该驱动程序的 SQL 结果集形式返回的信息。 数据类型适用于在数据定义语言 (DDL) 语句中使用。  
  
> [!IMPORTANT]  
>  应用程序必须使用返回的 TYPE_NAME 列中的类型名称**SQLGetTypeInfo**结果集中**ALTER TABLE**并**CREATE TABLE**语句。 **SQLGetTypeInfo**可能会在 DATA_TYPE 列中返回多个行具有相同值。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]结果集的语句句柄。  
  
 *DataType*  
 [输入]SQL 数据类型。 这必须是中的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)部分的附录 d:数据类型或特定于驱动程序的 SQL 数据类型。 SQL_ALL_TYPES 指定应返回有关所有数据类型的信息。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetTypeInfo**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetTypeInfo** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|指定的语句属性实现运行情况，由于无效，因此已暂时替换一个相近的值。 (调用**SQLGetStmtAttr**来确定暂时被替换的值。)替换值是否为有效*StatementHandle*直到关闭游标。 可以更改的语句属性有：Sql_attr_concurrency 设置 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_KEYSET_SIZE、 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS、 SQL_ATTR_QUERY_TIMEOUT 和 SQL_ATTR_SIMULATE_CURSOR。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|24000|游标状态无效|在打开游标的*StatementHandle，* 并**SQLFetch**或**SQLFetchScroll**已调用一样。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，和如果驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 结果集上打开了*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY004|SQL 数据类型无效|为参数指定的值*数据类型*是既不是有效的 ODBC SQL 数据类型标识符，也不支持驱动程序的特定于驱动程序的数据类型标识符。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*，然后调用该函数，并之前执行完毕**SQLCancel**或**SQLCancelHandle**是在调用*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetTypeInfo**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLGetTypeInfo**作为标准的结果集，由 DATA_TYPE 后按排序紧密程度的数据类型映射到相应 ODBC SQL 数据类型返回结果。 定义数据源的数据类型优先于用户定义数据类型。 因此，排序顺序不一定是一致，但首先通用化 DATA_TYPE 为后, 跟类型 _ 名称，这两个升序。 例如，假设数据源定义整数和计数器的数据类型，其中计数器是自动递增，并且还定义用户定义数据类型 WHOLENUM。 这些将按顺序的整数，WHOLENUM，返回和计数器，因为 WHOLENUM 紧密映射到的 ODBC SQL 数据类型 SQL_INTEGER，虽然自动递增数据类型，即使数据源支持的未映射密切到 ODBC SQL 数据类型。 有关可以如何使用此信息的信息，请参阅[DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*数据类型*参数指定数据类型是有效的 ODBC 驱动程序，支持的版本，但不是受驱动程序，则它将返回空结果集。  
  
> [!NOTE]  
>  有关常规使用、 参数以及 ODBC 目录函数返回的数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 对于 ODBC 3 重命名为以下各列。*x*。 列名称更改不会影响后向兼容性，因为应用程序将绑定的列号。  
  
|ODBC 2.0 列|ODBC 3。*x*列|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 以下各列已添加到返回的结果集**SQLGetTypeInfo** ODBC 3。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出了在结果集中的列。 列 19 (INTERVAL_PRECISION) 之外的其他列可以定义由驱动程序。 应用程序应获得访问驱动程序特定列的结果集末尾的倒计时，而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不会返回所有数据类型。 例如，驱动程序可能不返回用户定义数据类型。 应用程序可以使用任何有效的数据类型，而不考虑是否返回由**SQLGetTypeInfo**。 返回的数据类型**SQLGetTypeInfo**是所支持的数据源。 它们适用于在数据定义语言 (DDL) 语句中使用。 驱动程序可以返回结果集数据使用的数据类型，而不是返回的类型**SQLGetTypeInfo**。 在创建时的目录函数的结果集，该驱动程序可能由数据源使用不受支持的数据类型。  
  
|列名|“列”<br /><br /> number|数据类型|注释|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar 不为 NULL|数据依赖于源的数据类型名称;例如，"char （）"、"VARCHAR()"、"MONEY"、"长 VARBINARY"或者"CHAR FOR BIT DATA （）"。 应用程序必须使用此名称在**CREATE TABLE**并**ALTER TABLE**语句。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint（非 NULL）|SQL 数据类型。 这可以是 ODBC SQL 数据类型或特定于驱动程序的 SQL 数据类型。 对于 datetime 或间隔数据类型，此列返回的简洁数据类型 （如 SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 有关有效的 ODBC SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)中附录 d:数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|服务器支持此数据类型的最大列大小。 对于数值数据，这是最大精度。 对于字符串数据，这是以字符为单位的长度。 对于 datetime 数据类型，这是以字符串表示形式 （假定小数秒元素允许的最大精度） 的字符为单位的长度。 列大小不适用的数据类型则返回 NULL。 间隔数据类型，这是文本的时间间隔的字符表示形式中的字符数 (定义的间隔起始精度; 请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)中附录 d:数据类型）。<br /><br /> 列大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|字符或字符用作前缀文本;例如，可用一个单引号 （'） 的字符数据类型或 binary 数据类型; 0 x文字前缀不适用的数据类型则返回 NULL。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|字符或字符用于终止文字;例如，对于字符数据类型; 可用一个单引号 （'）不适用的文本后缀对于数据类型则返回 NULL。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|关键字，使用类型 _ 名称字段中返回的名称时，应用程序可能在括号中指定每个参数对应的逗号分隔的列表。 在列表中的关键字可以是以下任一： 长度、 精度或小数位数。 它们出现在语法要求他们使用的顺序。 例如，将作为小数点 CREATE_PARAMS"精度、 小数位数";对于 VARCHAR CREATE_PARAMS 就等于"长度"。 如果数据类型定义; 没有参数，则返回 NULL例如，整数。<br /><br /> 驱动程序提供 CREATE_PARAMS 文本中使用该国家/地区的语言。|  
|可以为 NULL (ODBC 2.0)|7|Smallint（非 NULL）|数据类型是否接受 NULL 值：<br /><br /> SQL_NO_NULLS 如果数据类型不接受 NULL 值。<br /><br /> SQL_NULLABLE 如果数据类型接受 NULL 值。<br /><br /> 如果不知道列是否接受 NULL 值，SQL_NULLABLE_UNKNOWN。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint（非 NULL）|字符数据类型是否是区分大小写的排序规则和比较中：<br /><br /> SQL_TRUE 如果数据类型是字符数据类型，区分大小写。<br /><br /> 如果数据类型不是字符数据类型或不区分大小写，SQL_FALSE。|  
|可搜索 (ODBC 2.0)|9|Smallint（非 NULL）|如何在中使用的数据类型**其中**子句：<br /><br /> 如果列不能用于 SQL_PRED_NONE**其中**子句。 （这是 ODBC 2 中的 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> SQL_PRED_CHAR 如果中可以使用该列**其中**子句，但仅**如**谓词。 （这是 ODBC 2 中的 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> SQL_PRED_BASIC 如果中可以使用该列**其中**使用除所有比较运算符的子句**等**(比较、 定量的比较**BETWEEN**， **非重复**， **IN**，**匹配**，并且**UNIQUE**)。 （这是 ODBC 2 中的 SQL_ALL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果列可在 SQL_SEARCHABLE**其中**子句包含任何比较运算符。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|数据类型是无符号：<br /><br /> 如果数据类型为无符号，SQL_TRUE。<br /><br /> 如果数据类型有符号，SQL_FALSE。<br /><br /> 如果该属性不是适用于数据类型或数据类型不是数值，则返回 NULL。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint（非 NULL）|数据类型是否具有预定义固定精度和小数位数 （这些都是特定于源的数据），如 money 数据类型：<br /><br /> SQL_TRUE 如果它有预定义的固定的精度和小数位数。<br /><br /> 如果它不具有预定义的固定的精度和小数位数，SQL_FALSE。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|数据类型是否自动递增：<br /><br /> SQL_TRUE 数据类型是否为自动递增。<br /><br /> 如果数据类型不是自动递增，SQL_FALSE。<br /><br /> 如果该属性不是适用于数据类型或数据类型不是数值，则返回 NULL。<br /><br /> 应用程序可以将值插入到列都有此属性，但通常不能更新列中的值。<br /><br /> Insert 将变成一个自动递增列，唯一值将在插入时插入到列。 增量未定义，但源特定的数据。 应用程序不应假定启动在任何特定点或增量的自动递增列按任何特定值。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|与数据源相关的数据类型名称的本地化版本。 如果是数据源不支持的本地化名称，则返回 NULL。 此名称用于显示唯一，如对话框。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|数据源上的数据类型的最小小数位数。 如果数据类型的小数位数是固定的，则 MINIMUM_SCALE 和 MAXIMUM_SCALE 列将同时包含此值。 例如，对于 SQL_TYPE_TIMESTAMP 列可能会有固定小数位数秒的小数部分。 当小数位数不适用时，将返回 NULL。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|数据源上的数据类型的最大的小数位数。 当小数位数不适用时，将返回 NULL。 如果最大的规模没有单独定义数据源，但改为定义为最大精度相同，则此列包含在 COLUMN_SIZE 列相同的值。 有关详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint NOT NULL|SQL 数据类型，因为它的值出现在描述符的 SQL_DESC_TYPE 字段。 此列是与 DATA_TYPE 列，除了间隔和日期时间数据类型相同。<br /><br /> 对于时间间隔和日期时间数据类型，在结果集中的 SQL_DATA_TYPE 字段将返回 SQL_INTERVAL 或 SQL_DATETIME，和 SQL_DATETIME_SUB 字段将返回特定的时间间隔或日期时间数据类型的子代码。 (请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|如果 SQL_DATA_TYPE 的值为 SQL_DATETIME 或 SQL_INTERVAL，则此列包含 datetime/间隔子代码。 对于日期时间和间隔以外的数据类型，此字段为 NULL。<br /><br /> 对于时间间隔或日期时间数据类型，在结果集中的 SQL_DATA_TYPE 字段将返回 SQL_INTERVAL 或 SQL_DATETIME，和 SQL_DATETIME_SUB 字段将返回特定的时间间隔或日期时间数据类型的子代码。 (请参阅[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|如果数据类型为近似数值类型，此列包含值 2，以指示 COLUMN_SIZE 指定比特数。 对于精确数字类型，此列包含值 10，以指示 COLUMN_SIZE 指定多个十进制数字。 否则，此列为 NULL。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|如果数据类型为时间间隔数据类型，此列包含时间间隔前导精度的值。 (请参阅[间隔数据类型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md)附录 d:数据类型。）否则，此列为 NULL。|  
  
 属性的信息可以应用于结果集中的特定列或为数据类型。 **SQLGetTypeInfo**返回数据类型; 与关联的属性有关的信息**SQLColAttribute**返回有关与结果集中列相关联的属性的信息。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLColAttribute 函数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
