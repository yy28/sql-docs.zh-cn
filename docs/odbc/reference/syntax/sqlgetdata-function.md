---
title: SQLGetData 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70ee26274d101d1b18b00c83a89bd0c946da6742
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855807"
---
# <a name="sqlgetdata-function"></a>SQLGetData 函数
**符合性**  
 版本引入了： ODBC 1.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLGetData**检索结果集中的单个列或之后的单个参数数据**SQLParamData**返回 SQL_PARAM_DATA_AVAILABLE。 它可以多次调用来检索部分中的可变长度数据。  
  
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
 [输入]对于检索列数据，它是列的要为其返回数据数。 结果集列在不断增加的列顺序从 1 开始编号。 书签列是列号为 0;这可以是仅在指定是否启用书签。  
  
 用于检索参数数据，它是从 1 开始的参数的序号。  
  
 *TargetType*  
 [输入]C 数据类型的类型标识符 **TargetValuePtr*缓冲区。 有关有效的 C 数据类型和类型标识符的列表，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型中的部分。  
  
 如果*TargetType*是 SQL_ARD_TYPE，驱动程序使用 ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型标识符。 如果*TargetType*是 SQL_APD_TYPE， **SQLGetData**将使用相同的 C 数据类型中指定**SQLBindParameter**。 C 数据类型中的指定，否则**SQLGetData**重写中指定的 C 数据类型**SQLBindParameter**。 如果它为 SQL_C_DEFAULT，驱动程序将选择基于源的 SQL 数据类型的默认 C 数据类型。  
  
 此外可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [输出]指向用于返回数据缓冲区的指针。  
  
 *TargetValuePtr*不能为 NULL。  
  
 *BufferLength*  
 [输入]长度 **TargetValuePtr*以字节为单位的缓冲区。  
  
 驱动程序使用*BufferLength*以免超出末尾的编写\* *TargetValuePtr*缓冲时返回可变长度数据，如字符或二进制数据。 请注意，驱动程序将 null 终止字符，返回字符数据时记\* *TargetValuePtr*。 **TargetValuePtr*因此必须包含 null 终止字符的空间或驱动程序将截断数据。  
  
 当驱动程序返回固定长度的数据，如整数或日期结构时，驱动程序会忽略*BufferLength*并假定缓冲区足够大以保存数据。 因此对于应用程序为固定长度的数据分配足够大的缓冲区或驱动程序将写入缓冲区的结束。  
  
 **SQLGetData**返回 SQLSTATE HY090 （字符串或缓冲区长度无效） 时*BufferLength*是小于 0，但不是在时*BufferLength*为 0。  
  
 *StrLen_or_IndPtr*  
 [输出]要返回的长度或指示器值在其中的缓冲区的指针。 如果这是 null 指针，则返回没有长度或指示器的值。 这将返回错误时要提取的数据为 NULL。  
  
 **SQLGetData**可以返回的长度/指示器缓冲区中的以下值：  
  
-   可用于返回的数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 有关详细信息，请参阅[使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和本主题中的"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetData** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|并非所有指定列的数据*Col_or_Param_Num*，可以在对函数的单个调用中检索。 SQL_NO_TOTAL 或保留在之前的当前调用的指定列中的数据的长度**SQLGetData**中返回\* *StrLen_or_IndPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> 有关详细信息进行多次调用**SQLGetData**单个列，请参阅"注释"。|  
|01S07|截断小数部分|返回一个或多个列的数据已被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳和 interval 数据类型包含时间部分，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|在结果集中的列的数据值不能转换为参数指定的 C 数据类型*TargetType*。|  
|07009|描述符索引无效|为参数指定的值*Col_or_Param_Num*为 0，并将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。<br /><br /> 为参数指定的值*Col_or_Param_Num*大于结果集中的列数。<br /><br /> *Col_or_Param_Num*值不是等于提供的参数的序号。<br /><br /> (DM) 指定的列被绑定。 此说明不适用于返回 SQL_GD_BOUND 位掩码中的 SQL_GETDATA_EXTENSIONS 选项的驱动程序**SQLGetInfo**。<br /><br /> (DM) 指定的列数为小于或等于最大的绑定列数。 此说明不适用于返回 SQL_GD_ANY_COLUMN 位掩码中的 SQL_GETDATA_EXTENSIONS 选项的驱动程序**SQLGetInfo**。<br /><br /> (DM) 已调用应用程序**SQLGetData**当前行; 在当前调用中指定的列数已在前面的调用; 中指定的列数小于和驱动程序不会返回 SQL_GD_ANY_ORDER SQL_GETDATA_EXTENSIONS 选项中的位掩码**SQLGetInfo**。<br /><br /> （数据挖掘） *TargetType*参数为 SQL_ARD_TYPE，并*Col_or_Param_Num* ARD 中的描述符记录未通过一致性检查。<br /><br /> （数据挖掘） *TargetType*参数为 SQL_ARD_TYPE，和 ARD SQL_DESC_COUNT 字段中的值是小于*Col_or_Param_Num*参数。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22002|需要指示器变量，但未提供|*StrLen_or_IndPtr*是空指针，而 NULL 的数据检索。|  
|22003|数值超出范围|为列 （为数字或字符串） 返回的数字值将导致要截断的数字的整个 （而不是小数） 部分。<br /><br /> 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|日期时间格式无效|在结果集中的字符列已绑定到 C 日期、 时间或时间戳结构和列中的值分别是无效的日期、 时间戳。 有关详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|被零除|返回导致被零除的算术表达式中的值。|  
|22015|间隔字段溢出|将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型前导字段中时导致重要数字丢失。<br /><br /> 当数据返回到 C 间隔类型，时没有 C 间隔类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的字符值无效|结果集中的字符列已返回到 C 字符缓冲区，并且该列包含出现没有缓冲区的字符集中的表示形式的字符。<br /><br /> C 类型为精确或近似数值、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;和列中的值不是有效的绑定 C 类型的文本。|  
|24000|游标状态无效|(DM) 而无需第一个调用调用函数**SQLFetch**或**SQLFetchScroll**若要将光标放在所需的数据行。<br /><br /> （数据挖掘） *StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。<br /><br /> 在打开游标的*StatementHandle*并**SQLFetch**或**SQLFetchScroll**已调用一样，但该游标所处的结果集或之后在开始之前结果集的末尾。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY003|超出范围的程序类型|(DM) 参数*TargetType*不是有效的数据类型、 SQL_C_DEFAULT、 SQL_ARD_TYPE （发生时检索列数据） 或 SQL_APD_TYPE （发生时检索参数数据）。<br /><br /> (DM) 参数*Col_or_Param_Num*是 0，并且该参数*TargetType*未 SQL_C_BOOKMARK 定长书签或 SQL_C_VARBOOKMARK 长度可变的书签。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序，然后在函数上调用了再次*StatementHandle*。|  
|HY009|使用空指针无效|(DM) 参数*TargetValuePtr*是空指针。|  
|HY010|函数序列错误|(DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetData**调用函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） *StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。<br /><br /> 调用**SQLExeceute**， **SQLExecDirect**，或**SQLMoreResults**返回 SQL_PARAM_DATA_AVAILABLE，但**SQLGetData**调用而不是**SQLParamData**。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*BufferLength*小于 0。<br /><br /> 为参数指定的值*BufferLength*为小于 4， *Col_or_Param_Num*参数设置为 0，并且司机的 ODBC 2 *.x*驱动程序。|  
|HY109|无效的游标位置|游标被置于 (通过**SQLSetPos**， **SQLFetch**， **SQLFetchScroll**，或者**SQLBulkOperations**) 已删除的行无法提取或。<br /><br /> 游标的只进游标，并且行集大小大于 1。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持使用**SQLGetData**与中的多个行**SQLFetchScroll**。 此说明不适用于返回 SQL_GD_BLOCK 位掩码中的 SQL_GETDATA_EXTENSIONS 选项的驱动程序**SQLGetInfo**。<br /><br /> 驱动程序或数据源不支持指定的组合来转换*TargetType*参数和相应的列的 SQL 数据类型。 此错误仅适用于 SQL 数据类型的列映射到特定于驱动程序的 SQL 数据类型。<br /><br /> 该驱动程序支持 ODBC 2 仅 *.x*，并将参数*TargetType*是以下之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 和中列出的 C 间隔数据类型的任何[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)附录 d： 数据类型。<br /><br /> 该驱动程序仅支持之前需 3.50 和参数的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLGetData**为指定列中返回的数据。 **SQLGetData**仅在已提取从结果集的一个或多个行后，可以调用**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**。 如果长度可变的数据太大，无法对单个调用中返回**SQLGetData** （由于应用程序中的限制）， **SQLGetData**可以检索它的部分。 可以将绑定中的行和调用的某些列**SQLGetData**对于其他操作系统，尽管这会受到某些限制。 有关详细信息，请参阅[获取长整型数据](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 有关使用信息**SQLGetData**使用流式处理的输出参数，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGetData  
 如果该驱动程序不支持的扩展**SQLGetData**，该函数可以返回仅对具有大量未绑定列的数据大于最后一个绑定列。 此外中某行的数据的值, *Col_or_Param_Num*每次调用中的参数**SQLGetData**必须是大于或等于的值*Col_or_Param_Num*中的上一个调用;也就是说，数字列按升序排列必须检索数据。 最后，如果没有扩展支持，则**SQLGetData**如果行集大小大于 1 不能调用。  
  
 驱动程序可以放松任何这些限制。 若要确定驱动程序放松了什么限制，应用程序调用**SQLGetInfo**具有任一以下 SQL_GETDATA_EXTENSIONS 选项：  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以调用以返回输出参数值。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN。 如果返回此选项，则**SQLGetData**可以为任何未绑定列，包括那些在最后一个绑定列之前调用。  
  
-   SQL_GD_ANY_ORDER。 如果返回此选项，则**SQLGetData**可以为未绑定列按任何顺序调用。  
  
-   SQL_GD_BLOCK。 如果返回此选项，那么**SQLGetInfo** SQL_GETDATA_EXTENSIONS 信息类型，该驱动程序支持对调用**SQLGetData**当行集大小是大于 1 时，应用程序可以调用**SQLSetPos** SQL_POSITION 选项将游标定位在正确的行，然后才能调用**SQLGetData。**  
  
-   SQL_GD_BOUND。 如果返回此选项，则**SQLGetData**可以调用对于绑定列，以及未绑定列。  
  
 有两种例外情况这些限制和放宽了它们的驱动程序的能力。 首先， **SQLGetData**时，应永远不会调用对于只进游标行集大小大于 1。 其次，如果驱动程序支持书签，它必须始终支持调用的能力**SQLGetData**列 0，即使它不允许应用程序可以调用**SQLGetData**对于最后一个之前的其他列绑定的列。 (应用程序使用 ODBC 2 *.x*驱动程序， **SQLGetData**成功返回时调用的书签*Col_or_Param_Num*等于 0 后调用**SQLFetch**，因为**SQLFetch** ODBC 3 映射 *.x*到驱动程序管理器**SQLExtendedFetch**与*FetchOrientation*的 SQL_FETCH_NEXT，并**SQLGetData**与*Col_or_Param_Num* 0 的映射由 ODBC 3 *.x*到驱动程序管理器**SQLGetStmtOption**与*fOption*的 SQL_GET_BOOKMARK。)  
  
 **SQLGetData**不能用于检索通过调用刚插入的行的书签将变为**SQLBulkOperations**带有 SQL_ADD 选项，因为该游标未定位在该行上。 应用程序可以通过绑定第 0 列之前调用检索这样的行的书签将变为**SQLBulkOperations** SQL_ADD，这种情况下使用**SQLBulkOperations**返回绑定的缓冲区中的书签。 **SQLFetchScroll**然后可以使用 SQL_FETCH_BOOKMARK 重新光标定位在该行上调用。  
  
 如果*TargetType*参数中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段设置为间隔数据类型，默认时间间隔的前导精度 (2) 和默认时间间隔的秒精度 (6)，ARD，分别用于数据。 如果*TargetType*参数为 SQL_C_NUMERIC 数据类型，默认的精度 （驱动程序定义） 和 ARD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段中设置默认小数位数 (0)，用于数据。 如果任何默认精度或小数位数不适当，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。 它可以将 SQL_DESC_CONCISE_TYPE 字段设置为 SQL_C_NUMERIC 并调用**SQLGetData**与*TargetType* SQL_ARD_TYPE，这将导致在描述符字段的精度和小数位数的值的参数若要使用。  
  
> [!NOTE]  
>  在 ODBC 2 *.x*，应用程序设置*TargetType* SQL_C_DATE、 SQL_C_TIME，或指示 SQL_C_TIMESTAMP \* *TargetValuePtr*是日期、 time、 或时间戳结构。 在 ODBC 3 *.x*，应用程序设置*TargetType* SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，或 SQL_C_TYPE_TIMESTAMP。 驱动程序管理器，可相应映射必要时，基于上的应用程序和驱动程序版本。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>检索在部件中的可变长度数据  
 **SQLGetData**可用于从包含在部分中的可变长度数据的列中检索数据，也就是说，SQL 数据类型的列的标识符时 SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_WCHAR、 SQL_WVARCHAR、 SQL_WLONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY 或可变长度类型的特定于驱动程序的标识符。  
  
 若要从部件中的列检索数据，应用程序调用**SQLGetData**中同一列连续多次。 在每次调用**SQLGetData**返回数据的下一步的一部分。 它是由应用程序以重新组装的部分，注意，要移除的字符数据的中间部分的 null 终止字符。 如果没有更多数据，以返回或不为终止字符分配足够的缓冲区**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （数据被截断）。 当它返回的最后一部分数据， **SQLGetData**返回 SQL_SUCCESS。 因为应用程序然后会有没有办法知道多少应用程序缓冲区中的数据有效，可从某一列，检索数据的最后一个有效调用上返回 SQL_NO_TOTAL 既不为零。 如果**SQLGetData**调用在此之后，其返回 sql_no_data 为止。 有关详细信息，请参阅下一部分中，"使用 SQLGetData 检索数据"。  
  
 可以在部件中返回长度可变的书签**SQLGetData**。 与调用的其他数据一样**SQLGetData**返回中部分的长度可变的书签将返回 SQLSTATE 01004 （字符串数据，右端被截断） 和 SQL_SUCCESS_WITH_INFO 时要返回的更多数据。 通过调用截断长度可变的书签时，这一点不同于用例**SQLFetch**或**SQLFetchScroll**，这会返回 SQL_ERROR 并且 SQLSTATE 22001 （字符串数据，右端被截断）。  
  
 **SQLGetData**不能用于返回部分中的固定长度的数据。 如果**SQLGetData**是为一列以包含固定长度的数据行中调用不止一次，其返回 sql_no_data 为止的所有调用后第一个。  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流的输出参数  
 如果驱动程序支持流的输出参数，应用程序可以调用**SQLGetData**使用一个较小缓冲区多次来检索大型参数值。 有关流式处理的输出参数的详细信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 检索数据  
 返回指定列的数据**SQLGetData**执行以下步骤序列：  
  
1.  如果它已返回所有列的数据，则返回 sql_no_data 为止。  
  
2.  集\* *StrLen_or_IndPtr*为 SQL_NULL_DATA，如果数据为 NULL。 如果数据为 NULL 并且*StrLen_or_IndPtr*是空指针**SQLGetData**返回 SQLSTATE 22002 （指示器变量，但未提供）。  
  
     如果列的数据不为 NULL， **SQLGetData**转到步骤 3。  
  
3.  如果 SQL_ATTR_MAX_LENGTH 语句属性设置为非零值，如果列包含字符或二进制数据，并且如果**SQLGetData**以前尚未调用的列数据被截断为 SQL_ATTR_MAX_LENGTH字节数。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 语句属性旨在减少网络流量。 它通常被实现数据源，返回之前对其通过网络将截断数据。 驱动程序和数据源不需要支持它。 因此，若要确保数据将被截断为特定大小，应用程序应分配该大小的缓冲区，并指定的大小以*BufferLength*参数。  
  
4.  将数据转换中指定的类型为*TargetType*。 数据是为该数据类型提供的默认精度和小数位数。 如果*TargetType*是 SQL_ARD_TYPE，数据使用的 ARD SQL_DESC_CONCISE_TYPE 字段中的类型。 如果*TargetType*是 SQL_ARD_TYPE、 数据中提供了精度和小数位数 SQL_DESC_DATETIME_INTERVAL_PRECISION，SQL_DESC_PRECISION，和 ARD，具体取决于数据的 SQL_DESC_SCALE 字段键入 SQL_DESC_CONCISE类型 （_t） 字段。 如果任何默认精度或小数位数不适当，应用程序显式应通过调用设置适当的描述符字段**SQLSetDescField**或**SQLSetDescRec**。  
  
5.  如果数据已转换为可变长度数据类型，如字符或二进制文件中， **SQLGetData**检查数据的长度是否超过*BufferLength*。 如果字符数据 （包括 null 终止字符） 的长度超过*BufferLength*， **SQLGetData**截断到数据*BufferLength*长度小于null 终止字符。 它然后则以 null 终止的数据。 如果二进制数据的长度超过了数据缓冲区的长度**SQLGetData**将它截断到*BufferLength*字节。  
  
     如果提供的数据缓冲区太小，无法保留 null 终止字符**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004。  
  
     **SQLGetData**永远不会截断数据转换为固定长度的数据类型; 它始终假定的长度 **TargetValuePtr*是数据类型的大小。  
  
6.  将中的已转换 （和可能被截断） 数据放\* *TargetValuePtr*。 请注意， **SQLGetData**不能返回行外的数据。  
  
7.  将放置在数据的长度\* *StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*是空指针**SQLGetData**不返回长度。  
  
    -   对于字符或二进制数据，这是数据的长度转换之后和之前由于截断*BufferLength*。 如果驱动程序无法转换后，确定数据的长度，因为有时是带有长数据的用例，它将返回 SQL_SUCCESS_WITH_INFO 和长度设置为 SQL_NO_TOTAL。 (上次调用**SQLGetData**必须始终返回数据、 不为零或 SQL_NO_TOTAL 的长度。)如果数据已被截断 SQL_ATTR_MAX_LENGTH 语句由于属性，此属性的值，而不是实际长度 — 中放置\* *StrLen_or_IndPtr*。 这是因为此属性设计使该驱动程序不有任何办法来找出实际长度截断的转换之前, 在服务器上的数据。 当**SQLGetData**是连续的多次调用同一列中，这是当前的调用开始处的可用数据的长度; 也就是说，长度还减少了每个后续调用。  
  
    -   对于所有其他数据类型，这是数据的长度后转换，则也就是说，它是类型的到转换数据的大小。  
  
8.  如果在转换期间截断而不会丢失基数的倍数的数据 （例如，实际 1.234 截断数字转换为整数 1） 或由于*BufferLength*太小 （例如，字符串"abcdef"放置4 字节缓冲区） 中**SQLGetData**返回 SQLSTATE 01004 （数据被截断） 和 SQL_SUCCESS_WITH_INFO。 如果数据被截断而不会丢失基数的倍数 SQL_ATTR_MAX_LENGTH 语句属性，由于**SQLGetData**返回 SQL_SUCCESS，且不返回 SQLSTATE 01004 （数据被截断）。  
  
 绑定的数据缓冲区的内容 (如果**SQLGetData**绑定列调用) 的长度/指示器缓冲区是不确定，如果**SQLGetData**不会返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 后续调用**SQLGetData**将从所请求的最后一列中检索数据; 而在以前的偏移量会无效。 例如，执行以下顺序执行：  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData(icol=n) 第二次调用开始处的 n 列检索数据。 任何数据，因为早期调用中的偏移量**SQLGetData**的列将不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述符和 SQLGetData  
 **SQLGetData**不与任何描述符字段的直接交互。  
  
 如果*TargetType*是 SQL_ARD_TYPE，数据使用的 ARD SQL_DESC_CONCISE_TYPE 字段中的类型。 如果*TargetType* SQL_ARD_TYPE 或 SQL_C_DEFAULT，数据中提供了精度和小数位数 SQL_DESC_DATETIME_INTERVAL_PRECISION，SQL_DESC_PRECISION，然后键入 SQL_DESC_SCALE ARD，具体取决于数据字段中的 SQL_DESC_CONCISE_TYPE 字段中。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序执行**选择**语句返回结果集的客户 Id、 名称和电话号码按名称、 ID 和电话号码。 对于每个数据行，它调用**SQLFetch**来定位光标移到下一行。 它将调用**SQLGetData**检索提取的数据; 数据和返回的字节数的缓冲区中指定调用**SQLGetData**。 最后，会输出每个雇员的名称、 ID 和电话号码。  
  
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
|执行块的光标位置不相关的大容量操作|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行 SQL 语句|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在提取单行数据或仅向前方向中的数据块|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在执行时发送参数数据|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位光标，刷新的行集中的数据或更新或删除行集中的数据|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
