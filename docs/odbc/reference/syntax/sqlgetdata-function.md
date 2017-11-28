---
title: "SQLGetData 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetData
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetData
helpviewer_keywords: SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: "46"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: be2121e56cd0fb728c8af0fbb43bcfbf24bd0c57
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetdata-function"></a>SQLGetData 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetData**检索数据以在结果集中的单个列或单个参数后**SQLParamData**返回 SQL_PARAM_DATA_AVAILABLE。 它可以多次调用以检索的部分的长度可变的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *Col_or_Param_Num*  
 [输入]用于检索列数据，它是为其返回数据的列数。 结果集中的列是按从 1 开始的递增列顺序编号。 该书签列为列编号为 0;这可以是仅指定是否启用书签。  
  
 用于检索参数数据，它是从 1 开始的参数的序号。  
  
 *TargetType*  
 [输入]C 数据类型的类型标识符 **TargetValuePtr*缓冲区。 有关有效的 C 数据类型和类型标识符的列表，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中的部分。  
  
 如果*TargetType*是 SQL_ARD_TYPE，ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型标识符的驱动程序使用。 如果*TargetType*是 SQL_APD_TYPE， **SQLGetData**将使用相同的 C 数据类型中指定**SQLBindParameter**。 C 数据类型中指定了其他， **SQLGetData**重写中指定的 C 数据类型**SQLBindParameter**。 如果它 SQL_C_DEFAULT，驱动程序将选择基于的源的 SQL 数据类型的默认 C 数据类型。  
  
 你还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [输出]指向在其中以返回数据缓冲区的指针。  
  
 *TargetValuePtr*不能为 NULL。  
  
 *BufferLength*  
 [输入]长度 **TargetValuePtr*以字节为单位的缓冲区。  
  
 驱动程序使用*BufferLength*为了避免超出末尾的\* *TargetValuePtr*返回可变长度数据，如字符或二进制数据时，会缓冲。 请注意返回到的字符数据时，该驱动程序都将计的 null 终止字符\* *TargetValuePtr*。 **TargetValuePtr*因此必须包含用于 null 终止字符的空间或驱动程序将截断数据。  
  
 在驱动程序返回固定长度的数据，如整数或日期结构，该驱动程序会忽略*BufferLength*并假定缓冲区为大到足以保留数据。 因此，是重要应用程序可以为固定长度的数据分配足够大的缓冲区或驱动程序将写入超过缓冲区的末尾。  
  
 **SQLGetData**返回 SQLSTATE HY090 （无效字符串或缓冲区长度） 时*BufferLength*是小于 0，但不是在*BufferLength*为 0。  
  
 *StrLen_or_IndPtr*  
 [输出]指向要返回的长度或指示器值在其中缓冲区的指针。 如果这是 null 指针，不返回任何长度或指示器的值。 正在提取的数据为 NULL 时，这将返回错误。  
  
 **SQLGetData**可以返回长度/指示器缓冲区中的以下值：  
  
-   可用于返回数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 有关详细信息，请参阅[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和本主题中的"备注"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetData**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|并非所有指定的列中，数据*Col_or_Param_Num*，无法在对函数的单个调用中检索。 SQL_NO_TOTAL 或指定列中之前调用当前剩余数据的长度**SQLGetData**中返回\* *StrLen_or_IndPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> 有关详细信息使用多个调用**SQLGetData**单个列，请参阅"注释"。|  
|01S07|小数部分组成的截断|返回一个或多个列的数据被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳，和包含时间组件的 interval 数据类型，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|结果集中的列的数据值不能转换为自变量所指定的 C 数据类型*TargetType*。|  
|07009|无效的描述符索引|为参数指定的值*Col_or_Param_Num*是 0，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。<br /><br /> 为参数指定的值*Col_or_Param_Num*大于结果集中的列数。<br /><br /> *Col_or_Param_Num*值的不等于提供的参数的序号。<br /><br /> (DM) 指定的列被绑定。 此说明不适用于返回中的 SQL_GETDATA_EXTENSIONS 选项的 SQL_GD_BOUND 位掩码的驱动程序**SQLGetInfo**。<br /><br /> (DM) 指定列的数量为小于或等于最大的绑定列的数目。 此说明不适用于返回中的 SQL_GETDATA_EXTENSIONS 选项的 SQL_GD_ANY_COLUMN 位掩码的驱动程序**SQLGetInfo**。<br /><br /> (DM) 应用程序已调用**SQLGetData**当前行; 的当前调用中指定的列数已在前面的调用; 中指定的列数小于和驱动程序不返回 SQL_中的 SQL_GETDATA_EXTENSIONS 选项 GD_ANY_ORDER 位掩码**SQLGetInfo**。<br /><br /> (DM) *TargetType*自变量为 SQL_ARD_TYPE，和*Col_or_Param_Num*中 ARD 描述符记录未通过一致性检查。<br /><br /> (DM) *TargetType*自变量为 SQL_ARD_TYPE，和 ARD SQL_DESC_COUNT 字段中的值已小于*Col_or_Param_Num*自变量。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22002|需要指示器变量，但未提供|*StrLen_or_IndPtr*是空指针，并且检索数据为空。|  
|22003|数值超出范围|为列 （为数字或字符串） 返回数字的值可能会导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|无效的日期时间格式|在结果集中的字符列已绑定到 C 日期、 时间或时间戳结构，列中的值分别为无效的日期、 时间戳。 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|被零除|返回了导致被零除的算术表达式中的值。|  
|22015|间隔字段溢出|将从精确数字或间隔 SQL 类型分配给间隔 C 类型由前导字段中的重要数字丢失。<br /><br /> 如果将数据还原为间隔 C 类型，存在未没有间隔 C 类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的的无效字符值|指向字符 C 缓冲区，返回结果集中的字符列和列包含没有任何表示形式的缓冲区的字符集的字符。<br /><br /> C 类型已准确或近似数字、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;并且列中的值不是有效的文本的绑定的 C 类型。|  
|24000|无效的游标状态|(DM) 而无需首先调用调用该函数**SQLFetch**或**SQLFetchScroll**以将光标放在所需的数据行。<br /><br /> (DM) *StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。<br /><br /> 在打开游标的*StatementHandle*和**SQLFetch**或**SQLFetchScroll**已调用一样，但光标所处的结果集或之后开始之前结果集末尾。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY003|超出范围的程序类型|(DM) 自变量*TargetType*不是有效的数据类型、 SQL_C_DEFAULT、 SQL_ARD_TYPE （如果检索列数据） 或 SQL_APD_TYPE （如果检索参数数据）。<br /><br /> (DM) 自变量*Col_or_Param_Num* 0，并且参数*TargetType*针对的不是 SQL_C_BOOKMARK 固定长度书签或 SQL_C_VARBOOKMARK 可变长度的书签。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数已在上再次*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序，然后函数上调用了再次*StatementHandle*。|  
|HY009|不允许使用 null 指针|(DM) 自变量*TargetValuePtr*是空指针。|  
|HY010|函数序列错误|(DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetData**调用函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) *StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。<br /><br /> 调用**SQLExeceute**， **SQLExecDirect**，或**SQLMoreResults**返回 SQL_PARAM_DATA_AVAILABLE，但**SQLGetData**调用而不是**SQLParamData**。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*BufferLength*小于 0。<br /><br /> 为参数指定的值*BufferLength*为小于 4， *Col_or_Param_Num*自变量设置为 0，并且驱动程序是 ODBC 2*.x*驱动程序。|  
|HY109|无效的光标位置|光标 (通过**SQLSetPos**， **SQLFetch**， **SQLFetchScroll**，或**SQLBulkOperations**) 删除了某行或无法获取。<br /><br /> 光标只进游标，且行集大小为大于 1。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持使用**SQLGetData**与中的多个行**SQLFetchScroll**。 此说明不适用于返回中的 SQL_GETDATA_EXTENSIONS 选项的 SQL_GD_BLOCK 位掩码的驱动程序**SQLGetInfo**。<br /><br /> 驱动程序或数据源不支持指定的组合来转换*TargetType*自变量和相应的列的 SQL 数据类型。 此错误仅适用于 SQL 数据类型的列已映射到特定于驱动程序的 SQL 数据类型。<br /><br /> 驱动程序还支持仅 ODBC 2*.x*，并将参数*TargetType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 和中的任何间隔 C 数据类型列出[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中。<br /><br /> 该驱动程序仅支持之前售价 3.50 和的自变量的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLGetData**返回指定列中的数据。 **SQLGetData**仅之后从结果集中提取的一个或多个行时，才可以调用**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**. 如果长度可变的数据量太大，对单个调用中返回**SQLGetData** （由于应用程序中的限制）， **SQLGetData**可以检索它在部件中。 可以将绑定中的行和调用的某些列**SQLGetData**对于其他操作系统，尽管这会受到某些限制。 有关详细信息，请参阅[获取长整型数据](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 有关使用信息**SQLGetData**与经过流处理的 output 参数，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGetData  
 如果该驱动程序不支持扩展到**SQLGetData**，函数可以返回仅针对与大量的未绑定列的数据大于最后一绑定列。 此外，在行中的数据的值*Col_or_Param_Num*对每个调用中的参数**SQLGetData**必须大于或等于的值*Col_or_Param_Num*中以前的调用;也就是说，必须以数字升序列检索数据。 最后，如果没有扩展支持， **SQLGetData**不能调用，如果行集大小大于 1。  
  
 驱动程序可以放宽任何这些限制。 若要确定驱动程序会减轻何种限制，应用程序调用**SQLGetInfo**与任意以下 SQL_GETDATA_EXTENSIONS 选项：  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以调用以返回输出参数值。 有关详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN。 如果返回了此选项， **SQLGetData**可以为任何未绑定列，包括上次绑定列之前调用。  
  
-   SQL_GD_ANY_ORDER。 如果返回了此选项， **SQLGetData**可以调用未绑定列采用任何顺序。  
  
-   SQL_GD_BLOCK。 如果此选项未返回**SQLGetInfo** SQL_GETDATA_EXTENSIONS 信息类型，则驱动程序支持对调用**SQLGetData**当行集大小是大于 1 时，应用程序可以调用**SQLSetPos** SQL_POSITION 选项，来将光标置于之前调用正确的行**SQLGetData。**  
  
-   SQL_GD_BOUND。 如果返回了此选项， **SQLGetData**可以调用绑定列，以及未绑定列。  
  
 有两个例外这些限制和驱动程序的能力放宽了它们。 首先， **SQLGetData**应永远不会在对于只进游标时调用的行集大小大于 1。 其次，如果驱动程序支持书签，它必须始终支持调用的能力**SQLGetData**列 0，即使它不允许应用程序调用**SQLGetData**早于最后其他列绑定的列。 (应用程序使用 ODBC 2*.x*驱动程序， **SQLGetData**将成功返回时使用调用的书签*Col_or_Param_Num*等于 0 后调用**SQLFetch**，这是因为**SQLFetch**映射由 ODBC 3*.x*到驱动程序管理器**SQLExtendedFetch**与*FetchOrientation*的 SQL_FETCH_NEXT，和**SQLGetData**与*Col_or_Param_Num* 0 的映射由 ODBC 3*.x*到驱动程序管理器**SQLGetStmtOption**与*fOption*的 SQL_GET_BOOKMARK。)  
  
 **SQLGetData**不能用于检索通过调用刚插入的行的书签**SQLBulkOperations**使用 SQL_ADD 选项，因为未将光标放置在该行上。 应用程序可以通过绑定第 0 列之前调用检索这样的行的书签**SQLBulkOperations** SQL_ADD，这种情况下与**SQLBulkOperations**返回绑定的缓冲区中的书签。 **SQLFetchScroll**然后可以使用 SQL_FETCH_BOOKMARK 重新光标定位在该行上调用。  
  
 如果*TargetType*自变量不是间隔数据类型，默认时间间隔前导精度 (2) 和默认间隔秒精度 (6) 中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段设置ARD，分别用于数据。 如果*TargetType*参数不是 SQL_C_NUMERIC 数据类型 （驱动程序定义） 的默认精度和 ARD SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置默认小数位数 (0) 时，用于的数据。 如果任何默认精度或小数位数不合适，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。 它可以将 SQL_DESC_CONCISE_TYPE 字段设置为 SQL_C_NUMERIC 并调用**SQLGetData**与*TargetType* SQL_ARD_TYPE，这将导致描述符字段中的精度和小数位数的值的自变量要使用。  
  
> [!NOTE]  
>  在 ODBC 2*.x*，应用程序集*TargetType*到 SQL_C_DATE、 SQL_C_TIME 或 SQL_C_TIMESTAMP，则指示\* *TargetValuePtr*为日期、 time、 或时间戳结构。 ODBC 3 中*.x*，应用程序集*TargetType*到 SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME 或 SQL_C_TYPE_TIMESTAMP。 驱动程序管理器对相应映射如果有必要，基于应用程序和驱动程序版本。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>检索部分的长度可变的数据  
 **SQLGetData**可以用于从包含部件中的可变长度数据的列中检索数据-即，SQL 数据类型的列的标识符时 SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_WCHAR、 SQL_WVARCHAR、 SQL_WLONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或可变长度类型的特定于驱动程序的标识符。  
  
 若要从部分中的列中检索数据，在应用程序调用**SQLGetData**中针对同一列的连续多次。 在每次调用**SQLGetData**返回数据的下一部分。 它是由应用程序将部分，但注意要移除的字符数据的中间部分的 null 终止字符集合。 如果没有更多的数据，以返回或不足够的缓冲区已终止字符，为分配**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （数据截断）。 当此方法返回的数据的最后一部分**SQLGetData**返回 SQL_SUCCESS。 因为应用程序将必须无法知道应用程序缓冲区中的数据中有多少有效，可以在列中检索数据上一次有效调用返回既不 SQL_NO_TOTAL，也不为零。 如果**SQLGetData**称为此后，它将返回 SQL_NO_DATA。 有关详细信息，请参阅下一部分中，"检索数据，SQLGetData。"  
  
 可以在部件中返回可变长度书签**SQLGetData**。 其他数据，对的调用与**SQLGetData**返回部分中的变量长度书签将返回 SQLSTATE 01004 （字符串数据，右截断） 和 SQL_SUCCESS_WITH_INFO 时要返回的更多数据。 通过调用截断长度可变的书签时，此函数不同于这种情况**SQLFetch**或**SQLFetchScroll**，它返回 SQL_ERROR 和 SQLSTATE 22001 （字符串数据，右截断）。  
  
 **SQLGetData**不能用于在中，部件返回固定长度的数据。 如果**SQLGetData**是为一列以包含固定长度的数据，请在行中调用不止一次，它将返回 SQL_NO_DATA 所有调用后第一个。  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流式处理的输出参数  
 如果驱动程序支持流式处理的输出参数，应用程序可以调用**SQLGetData**带小缓冲次数多，若要检索的大型参数值。 有关流式处理的输出参数的详细信息，请参阅[检索输出参数使用 SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>用 SQLGetData 检索数据  
 返回为指定的列中，数据**SQLGetData**执行下面的步骤序列：  
  
1.  如果它已具有返回所有列的数据，则返回 SQL_NO_DATA。  
  
2.  集\* *StrLen_or_IndPtr*到 SQL_NULL_DATA 如果数据为 NULL。 如果数据为 NULL 和*StrLen_or_IndPtr*是空指针， **SQLGetData**返回 SQLSTATE 22002 （指示器变量需要但未提供）。  
  
     如果列的数据不为 NULL， **SQLGetData**继续到步骤 3。  
  
3.  如果 SQL_ATTR_MAX_LENGTH 语句属性设置为非零值，如果列包含字符或二进制数据，并且**SQLGetData**以前尚未调用的列，数据将剪裁为 SQL_ATTR_MAX_LENGTH字节数。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 语句属性旨在减少网络流量。 它通常由数据源，然后再返回跨网络将截断数据来实现。 驱动程序和数据源不需要支持它。 因此，若要确保数据将剪裁为特定的大小，应用程序应分配这种大小的缓冲区，并指定的大小以*BufferLength*自变量。  
  
4.  将数据转换中指定的类型为*TargetType*。 数据中，针对该数据类型都是给定的默认精度和小数位数。 如果*TargetType*是 SQL_ARD_TYPE，数据使用的 ARD SQL_DESC_CONCISE_TYPE 字段中的类型。 如果*TargetType*是 SQL_ARD_TYPE、 数据中提供了精度和小数位数 SQL_DESC_DATETIME_INTERVAL_PRECISION，SQL_DESC_PRECISION，和 ARD，具体取决于数据的 SQL_DESC_SCALE 字段键入 SQL_DESC_CONCISE（_t） 字段。 如果任何默认精度或小数位数不合适，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
5.  如果数据已转换为可变长度数据类型，如字符或二进制， **SQLGetData**检查数据的长度是否超出*BufferLength*。 如果字符数据 （包括 null 终止字符） 的长度超过*BufferLength*， **SQLGetData**将截断到数据*BufferLength*长度小于null 终止字符。 它然后 null 终止的数据。 如果二进制数据的长度超过了数据缓冲区**SQLGetData**将它截断到*BufferLength*字节。  
  
     如果所提供的数据缓冲区太小，保留 null 终止字符**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004。  
  
     **SQLGetData**永远不会截断数据转换为固定长度的数据类型; 它始终假定的长度 **TargetValuePtr*是数据类型的大小。  
  
6.  将中的转换 （和可能截断） 数据\* *TargetValuePtr*。 请注意， **SQLGetData**不能返回外部的数据。  
  
7.  将中的数据的长度\* *StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*是空指针， **SQLGetData**不返回长度。  
  
    -   对于字符或二进制数据，这是数据的长度之后转换和之前截断由于*BufferLength*。 如果该驱动程序无法转换后，确定数据的长度，因为有时是长整型数据这种情况，它返回 SQL_SUCCESS_WITH_INFO，并将长度设置为 SQL_NO_TOTAL。 (上次调用**SQLGetData**必须始终返回数据，不是零或 SQL_NO_TOTAL 的长度。)如果数据已被截断由于 SQL_ATTR_MAX_LENGTH 语句的属性，此属性的值，而不是实际的长度-放入\* *StrLen_or_IndPtr*。 这是因为此属性设计截断转换之前, 在服务器上的数据，因此驱动程序还找出哪些的实际长度是没有方法。 当**SQLGetData**是连续的多次调用相同的列中，这是与当前调用开始时的可用数据的长度; 即，长度还减少了每个后续调用。  
  
    -   对于所有其他数据类型，这是数据的长度转换后;也就是说，正是数据已转换到的目标类型的大小。  
  
8.  如果在转换期间截断而不会丢失的基数的倍数数据 （例如，实数 1.234 将截断时转换为整数 1） 或者是因为*BufferLength*太小 （例如，字符串"abcdef"放置4 字节缓冲区） 中, **SQLGetData**返回 SQLSTATE 01004 （截断的数据） 和 SQL_SUCCESS_WITH_INFO。 如果数据截断而不会丢失的基数的倍数由于 SQL_ATTR_MAX_LENGTH 语句属性， **SQLGetData**返回 SQL_SUCCESS 且不返回 SQLSTATE 01004 （数据截断）。  
  
 绑定的数据缓冲区的内容 (如果**SQLGetData**调用在绑定的列上) 的长度/指示器缓冲区是不确定的如果**SQLGetData**不返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 对连续调用**SQLGetData**将从请求的最后一列中检索数据; 以前的偏移量会变得无效。 例如，执行以下顺序执行：  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData(icol=n) 第二次调用从开始处的 n 列中检索数据。 任何源于到早期调用数据中的偏移量**SQLGetData**为列不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>说明符和 SQLGetData  
 **SQLGetData**不直接与任何描述符字段不进行交互。  
  
 如果*TargetType*是 SQL_ARD_TYPE，数据使用的 ARD SQL_DESC_CONCISE_TYPE 字段中的类型。 如果*TargetType* SQL_ARD_TYPE 或 SQL_C_DEFAULT、 数据中提供了精度和小数位数 SQL_DESC_DATETIME_INTERVAL_PRECISION，SQL_DESC_PRECISION，和 SQL_DESC_SCALE 字段的 ARD，根据数据输入中的 SQL_DESC_CONCISE_TYPE 字段中。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序执行**选择**语句以返回结果集的客户 Id，名称，并电话号码按名称、 ID 和电话号码。 对于每行数据，它调用**SQLFetch**到下一行将光标定位。 它调用**SQLGetData**若要检索提取的数据; 的缓冲区的数据和返回的字节数指定的调用中**SQLGetData**。 最后，它将打印每个员工的名称、 ID 和电话号码。  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配结果集中的列的存储|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行不与块光标位置的大容量操作|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行 SQL 语句|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取数据的单个行或只进方向中的数据块|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在执行时发送的参数数据|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|将光标置于、 刷新数据集中的行，或更新或删除行集中的数据|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
