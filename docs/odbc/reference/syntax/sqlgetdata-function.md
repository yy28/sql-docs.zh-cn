---
title: SQLGetData 功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285503"
---
# <a name="sqlgetdata-function"></a>SQLGetData 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetData**在**SQLParamData**返回SQL_PARAM_DATA_AVAILABLE后检索结果集中的单个列或单个参数的数据。 可以多次调用它来检索零件中的可变长度数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *Col_or_Param_Num*  
 [输入]对于检索列数据，它是要返回数据的列数。 结果集列按从 1 开始的列顺序增加编号。 书签列是列编号 0;书签列为 0。"仅当启用了书签时，才能指定此选项。  
  
 对于检索参数数据，它是参数的元数，从 1 开始。  
  
 *目标类型*  
 [输入]**目标价值Ptr*缓冲区的 C 数据类型的类型标识符。 有关有效的 C 数据类型和类型标识符的列表，请参阅附录 D：数据类型中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)部分。  
  
 如果*TargetType* SQL_ARD_TYPE，则驱动程序使用 ARD SQL_DESC_CONCISE_TYPE 字段中指定的类型标识符。 如果*目标类型***SQL_APD_TYPE，SQLGetData**将使用**SQLBind 参数**中指定的相同 C 数据类型。 否则 **，SQLGetData**中指定的 C 数据类型将覆盖**SQLBind 参数**中指定的 C 数据类型。 如果SQL_C_DEFAULT，驱动程序将基于源的 SQL 数据类型选择默认 C 数据类型。  
  
 您还可以指定扩展的 C 数据类型。 有关详细信息，请参阅[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *目标价值Ptr*  
 [输出]指向要返回数据的缓冲区的指针。  
  
 *目标价值 Ptr*不能为 NULL。  
  
 *缓冲区长度*  
 [输入]**目标ValuePtr*缓冲区的长度（以字节为单位）。  
  
 驱动程序使用*BufferLength*来避免在返回可变长度数据\*（如字符或二进制数据）时写入*TargetValuePtr*缓冲区的末尾。 请注意，当将字符数据返回到\* *TargetValuePtr*时，驱动程序会计算 null 终止字符。 *因此 *，TargetValuePtr*必须包含 null 终止字符的空间，否则驱动程序将截截数据。  
  
 当驱动程序返回固定长度数据（如整数或日期结构）时，驱动程序将忽略*BufferLength*并假定缓冲区足够大以容纳数据。 因此，应用程序为固定长度数据分配足够大的缓冲区非常重要，否则驱动程序将写入缓冲区的末尾。  
  
 当*缓冲区长度*小于 0，但当缓冲区长度为 0 时 **，SQLGetData**返回 SQLSTATE HY090（无效字符串或缓冲区长度），但当*缓冲区长度*为 0 时，则返回 SQLSTATE HY090（无效字符串或缓冲区长度）。  
  
 *StrLen_or_IndPtr*  
 [输出]指向要返回长度或指示器值的缓冲区的指针。 如果这是空指针，则不返回长度或指标值。 当提取的数据为 NULL 时，这将返回一个错误。  
  
 **SQLGetData**可以在长度/指示器缓冲区中返回以下值：  
  
-   可供返回的数据的长度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 有关详细信息，请参阅本主题[中使用长度/指示器值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetData**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT*Handle*的*句柄类型*和*语句句柄*。 下表列出了**SQLGetData**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|并非所有指定列的数据 *（Col_or_Param_Num*）都可以在单个调用函数中检索。 SQL_NO_TOTAL或当前调用**SQLGetData**之前在指定列中剩余数据的长度\**StrLen_or_IndPtr返回。* （函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> 有关对单个列使用多次调用**SQLGetData**的详细信息，请参阅"注释"。|  
|01S07|分数截断|为一个或多个列返回的数据被截断。 对于数字数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|结果集中列的数据值不能转换为参数*TargetType*指定的 C 数据类型。|  
|07009|无效描述符索引|为参数*Col_or_Param_Num*指定的值为 0，并且SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF。<br /><br /> 为参数*Col_or_Param_Num*指定的值大于结果集中的列数。<br /><br /> *Col_or_Param_Num*值不等于可用参数的位数。<br /><br /> （DM） 指定的列已绑定。 此说明不适用于在**SQLGetInfo**中返回 SQL_GETDATA_EXTENSIONSSQL_GD_BOUND位掩码SQL_GD_BOUND的驱动程序。<br /><br /> （DM） 指定列的数量小于或等于最高绑定列的数量。 此说明不适用于在**SQLGetInfo**中返回SQL_GD_ANY_COLUMN位掩码SQL_GETDATA_EXTENSIONS驱动程序。<br /><br /> （DM） 应用程序已为当前行调用**SQLGetData;** 当前调用中指定的列数小于前一个调用中指定的列数;并且驱动程序不返回**SQLGetInfo**中SQL_GETDATA_EXTENSIONS选项的SQL_GD_ANY_ORDER位掩码。<br /><br /> （DM）*目标类型*参数SQL_ARD_TYPE，并且 ARD 中的*Col_or_Param_Num*描述符记录未通过一致性检查。<br /><br /> （DM）*目标类型*参数SQL_ARD_TYPE，ARD SQL_DESC_COUNT字段中的值小于*Col_or_Param_Num*参数。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22002|需要指标变量，但未提供|*StrLen_or_IndPtr*为空指针，并检索 NULL 数据。|  
|22003|数值超范围|返回列的数值（作为数字或字符串）将导致数字的整个部分（而不是小数）被截断。<br /><br /> 有关详细信息，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|无效日期时间格式|结果集中的字符列绑定到 C 日期、时间或时间戳结构，并且列中的值分别为无效的日期、时间或时间戳。 有关详细信息，请参阅附录[D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|除零|返回算术表达式中导致除以零的值。|  
|22015|间隔字段溢出|从精确数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> 将数据返回到间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。|  
|22018|强制转换规范的无效字符值|结果集中的字符列返回到字符 C 缓冲区，该列包含缓冲区的字符集中没有表示的字符。<br /><br /> C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。|  
|24000|无效的游标状态|（DM） 调用函数时，无需首先调用**SQLFetch**或**SQLFetchScroll**即可将光标定位到所需的数据行上。<br /><br /> （DM）*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。<br /><br /> 在*语句句柄*上打开一个游标，并调用**SQLFetch**或**SQLFetchScroll，** 但光标位于结果集开始之前或结果集结束之后。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY003|程序类型范围外|（DM） 参数*TargetType*不是有效的数据类型，SQL_C_DEFAULT、SQL_ARD_TYPE（检索列数据）或SQL_APD_TYPE（在检索参数数据的情况下）。<br /><br /> （DM） 参数*Col_or_Param_Num*为 0，并且参数*TargetType*不SQL_C_BOOKMARK固定长度书签或可变长度书签的SQL_C_VARBOOKMARK。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**在*语句句柄*上调用 ，然后在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**从多线程应用程序中的不同线程调用*了语句句柄*，然后在*语句句柄*上再次调用该函数。|  
|HY009|无效使用空指针|（DM） 参数*TargetValuePtr*是一个空指针。|  
|HY010|函数序列错误|（DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLGetData**函数时，此异步函数仍在执行。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM）*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。<br /><br /> 对**SQLExeceute、SQLExecDirect**或**SQLMore 结果**的调用SQL_PARAM_DATA_AVAILABLE返回，但调用**SQLGetData**而不是**SQLParamData**。 **SQLExecDirect**|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength*指定的值小于 0。<br /><br /> 为参数*BufferLength*指定的值小于*4，Col_or_Param_Num*参数设置为 0，驱动程序为 ODBC 2 *.x*驱动程序。|  
|HY109|光标位置无效|光标被定位在已删除或无法提取的行上（由 SQLSetPos、SQLFetch、SQLFetchScroll 或**SQLBulk 操作）。** **SQLSetPos** **SQLFetch** **SQLFetchScroll**<br /><br /> 光标是仅前进的游标，行集大小大于 1。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持在**SQLFetchScroll**中使用具有多行的**SQLGetData。** 此说明不适用于在**SQLGetInfo**中返回SQL_GETDATA_EXTENSIONS选项的SQL_GD_BLOCK位掩码的驱动程序。<br /><br /> 驱动程序或数据源不支持*由 TargetType*参数和相应列的 SQL 数据类型的组合指定的转换。 仅当列的 SQL 数据类型映射到特定于驱动程序的 SQL 数据类型时，此错误才适用。<br /><br /> 驱动程序仅支持 ODBC 2 *.x*，参数*TargetType*是以下参数之一：<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 和附录 D 中的[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)中列出的任何间隔 C 数据类型：数据类型。<br /><br /> 驱动程序仅支持 3.50 之前的 ODBC 版本，并且参数*TargetType* SQL_C_GUID。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*对应的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **SQLGetData**返回指定列中的数据。 **SQLGetData**只能在从**SQLFetch、SQLFetchScroll**或**SQL 扩展获取**集的结果集中**SQLFetchScroll**获取一个或多个行后才能调用。 如果可变长度数据太大，无法在**SQLGetData**的单个调用中返回（由于应用程序中的限制 **），SQLGetData**可以分部分检索它。 可以绑定一行中的某些列，并为其他列调用**SQLGetData，** 尽管这受一些限制。 有关详细信息，请参阅[获取长数据](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 有关使用具有流式输出参数的**SQLGetData**的信息，请参阅[使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGet 数据  
 如果驱动程序不支持**SQLGetData**的扩展，则函数只能返回数字大于最后一个绑定列的未绑定列的数据。 此外，在一行数据中，对**SQLGetData**的每个调用中*Col_or_Param_Num*参数的值必须大于或等于上一个调用中*Col_or_Param_Num*的值;也就是说，必须按增加列号顺序检索数据。 最后，如果没有支持扩展，则如果行集大小大于 1，则无法调用**SQLGetData。**  
  
 司机可以放宽任何这些限制。 要确定驱动程序放宽的限制，应用程序使用以下任意SQL_GETDATA_EXTENSIONS选项调用**SQLGetInfo：**  
  
-   可以调用 SQL_GD_OUTPUT_PARAMS = **SQLGetData**来返回输出参数值。 有关详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN 如果返回此选项，则可以为任何未绑定列（包括最后一个绑定列之前的列）调用**SQLGetData。**  
  
-   SQL_GD_ANY_ORDER 如果返回此选项，则可以按任意顺序为未绑定列调用**SQLGetData。**  
  
-   SQL_GD_BLOCK 如果**SQLGetInfo**为SQL_GETDATA_EXTENSIONS InfoType 返回此选项，则当行集大小大于 1 时，驱动程序支持对**SQLGetData**的调用，并且应用程序可以使用 SQL_POSITION 选项调用**SQLSetPos，** 在调用**SQLGetData**之前将光标定位在正确的行上。  
  
-   SQL_GD_BOUND 如果返回此选项，则可以为绑定列和无绑定列调用**SQLGetData。**  
  
 这些限制有两个例外，一个司机可以放松这些限制。 首先，当行集大小大于 1 时，不应为仅转发游标调用**SQLGetData。** 其次，如果驱动程序支持书签，它必须始终支持为列 0 调用**SQLGetData**的能力，即使它不允许应用程序在最后一个绑定列之前为其他列调用**SQLGetData。** （当应用程序使用 ODBC 2 *.x*驱动程序时 **，SQLGetData**将在调用**SQLFetch**后*以等于*0 的Col_or_Param_Num调用时成功返回书签，因为**SQLFetch**由 ODBC 3 *.x*驱动程序管理器映射到具有 SQL_FETCH_NEXT 的*提取方向*的**SQLExtendedFetch，** 并且具有*Col_or_Param_Num* 0 的**SQLGetData**由 ODBC 3 *.x*驱动程序管理器映射到**SQLGetStmtOption，** 该驱动程序具有 SQL_GET_BOOKMARK 选项。 *fOption*  
  
 **SQLGetData**不能用于检索刚刚插入的行的书签，该行使用SQL_ADD选项调用**SQLBulk 操作**，因为光标未定位在行上。 应用程序可以通过绑定列 0 检索此类行的书签，然后再使用 SQL_ADD调用**SQLBulk 操作**，在这种情况下**SQLBulk 操作**将返回绑定缓冲区中的书签。 然后，可以使用SQL_FETCH_BOOKMARK调用**SQLFetchScroll，** 以重新定位该行上的光标。  
  
 如果*TargetType*参数是间隔数据类型，则分别用于数据中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 字段中设置的默认间隔前导精度 （2） 和默认间隔秒精度 （6）。 如果*TargetType*参数是SQL_C_NUMERIC数据类型，则数据将使用在 ARD SQL_DESC_PRECISION和SQL_DESC_SCALE字段中设置的默认精度（驱动程序定义）和默认比例 （0）。 如果任何默认精度或比例不合适，应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置相应的描述符字段。 它可以将SQL_DESC_CONCISE_TYPE字段设置为SQL_C_NUMERIC，并将**SQLGetData**与*SQL_ARD_TYPE 的 TargetType*参数调用，这将导致使用描述符字段中的精度和缩放值。  
  
> [!NOTE]
>  在 ODBC 2 *.x*中，应用程序将*TargetType*设置为SQL_C_DATE、SQL_C_TIME或SQL_C_TIMESTAMP，以指示\* *TargetValuePtr*是日期、时间或时间戳结构。 在 ODBC 3 *.x*中，应用程序将*TargetType*设置为SQL_C_TYPE_DATE、SQL_C_TYPE_TIME或SQL_C_TYPE_TIMESTAMP。 驱动程序管理器根据需要根据应用程序和驱动程序版本进行适当的映射。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>检索零件中的可变长度数据  
 **SQLGetData**可用于从包含部分可变长度数据的列中检索数据 ，即当列的 SQL 数据类型的标识符为SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY 或变量长度类型的特定于驱动程序的标识符时。  
  
 若要从部分列中检索数据，应用程序会连续多次为同一列调用**SQLGetData。** 每次调用时 **，SQLGetData**都会返回数据的下一部分。 由应用程序重新组装零件，注意从字符数据的中间部分中删除 null 终止字符。 如果有更多的数据要返回或为终止字符分配了足够的缓冲区 **，SQLGetData**将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004（数据截断）。 当它返回数据的最后一部分时 **，SQLGetData**返回SQL_SUCCESS。 在从列检索数据的最后一个有效调用上，不能返回SQL_NO_TOTAL或零，因为应用程序随后无法知道应用程序缓冲区中有多少数据有效。 如果在此之后调用**SQLGetData，** 它将返回SQL_NO_DATA。 有关详细信息，请参阅下一节"使用 SQLGetData 检索数据"。  
  
 可变长度书签可以通过**SQLGetData**以零件返回。 与其他数据一样，调用**SQLGetData**返回部分中的可变长度书签将返回 SQLSTATE 01004（字符串数据，右截断），并在要返回的数据更多时返回SQL_SUCCESS_WITH_INFO。 这与对**SQLFetch**或**SQLFetchScroll**的调用截断可变长度书签的情况不同，后者返回SQL_ERROR和 SQLSTATE 22001（字符串数据，右截断）。  
  
 **SQLGetData**不能用于返回零件中的固定长度数据。 如果**SQLGetData**在一行中为包含固定长度数据的列调用了多个次，则它将返回第一个长度数据之后的所有调用SQL_NO_DATA。  
  
## <a name="retrieving-streamed-output-parameters"></a>检索流输出参数  
 如果驱动程序支持流式输出参数，应用程序可以多次使用小缓冲区调用**SQLGetData**以检索较大的参数值。 有关流输出参数的详细信息，请参阅使用[SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 检索数据  
 要返回指定列的数据 **，SQLGetData**将执行以下步骤序列：  
  
1.  如果已返回列的所有数据，则返回SQL_NO_DATA。  
  
2.  如果\*数据为 NULL，则将*StrLen_or_IndPtr*集SQL_NULL_DATA。 如果数据为 NULL，并且*StrLen_or_IndPtr*为空指针 **，SQLGetData**将返回 SQLSTATE 22002（需要指标变量，但未提供）。  
  
     如果列的数据不是**NULL，SQLGetData**将继续执行步骤 3。  
  
3.  如果SQL_ATTR_MAX_LENGTH语句属性设置为非零值，则如果列包含字符或二进制数据，并且以前未为列调用**SQLGetData，** 则数据将被截断为SQL_ATTR_MAX_LENGTH字节。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH语句属性旨在减少网络流量。 它通常由数据源实现，数据源在通过网络返回数据之前会截截数据。 驱动程序和数据源不需要支持它。 因此，为了保证数据被截断到特定大小，应用程序应分配该大小的缓冲区，并在*BufferLength 参数*中指定大小。  
  
4.  将数据转换为*TargetType*中指定的类型。 数据为该数据类型的默认精度和缩放。 如果*TargetType* SQL_ARD_TYPE，则使用 ARD SQL_DESC_CONCISE_TYPE字段中的数据类型。 如果*SQL_ARD_TYPE TargetType，* 则根据SQL_DESC_CONCISE_TYPE字段中的数据类型，在 ARD 的SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION和SQL_DESC_SCALE字段中为数据提供精度和缩放。 如果任何默认精度或比例不合适，应用程序应通过调用**SQLSetDescField**或**SQLSetDescRec**显式设置相应的描述符字段。  
  
5.  如果数据转换为可变长度数据类型（如字符或二进制 **），SQLGetData**将检查数据的长度是否超过*BufferLength*。 如果字符数据的长度（包括空终止字符）超过**BufferLength，SQLGetData**会截截到*缓冲区长度*，减去空终止字符的长度。 *BufferLength* 然后，它将终止数据。 如果二进制数据的长度超过数据缓冲区的长度 **，SQLGetData**会将其截截为*缓冲区长度*字节。  
  
     如果提供的数据缓冲区太小，无法容纳 null 终止字符，则**SQLGetData**将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004。  
  
     **SQLGetData**从不截截转换为固定长度数据类型的数据;它总是假定 **目标价值Ptr*的长度是数据类型的大小。  
  
6.  将转换（并可能截断）的数据放在\**TargetValuePtr 中*。 请注意 **，SQLGetData**无法将数据返回行外。  
  
7.  将数据的长度放在\**StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*为空指针 **，SQLGetData**不会返回长度。  
  
    -   对于字符或二进制数据，这是转换后和由于*BufferLength*而截断之前的数据长度。 如果驱动程序无法确定转换后的数据长度（有时与长数据的情况一样），它将返回SQL_SUCCESS_WITH_INFO并将长度设置为SQL_NO_TOTAL。 （对**SQLGetData**的最后一次调用必须始终返回数据的长度，而不是零或SQL_NO_TOTAL。如果数据由于SQL_ATTR_MAX_LENGTH语句属性而被截断，则此属性的值（相对于实际长度）将放在\**StrLen_or_IndPtr*。 这是因为此属性旨在在转换之前截截服务器上的数据，因此驱动程序无法确定实际长度。 当**SQLGetData**连续多次调用同一列时，这是当前调用开始时可用数据的长度;也就是说，每次后续调用的长度都会降低。  
  
    -   对于所有其他数据类型，这是转换后的数据长度;也就是说，它是数据转换到的类型的大小。  
  
8.  如果在转换过程中将数据截断而不丢失显著性（例如，当转换为整数 1 时，实际数字 1.234 被截断），或者由于*BufferLength*太小（例如，字符串"abcdef"放置在 4 字节缓冲区中 **），SQLGetData**返回 SQLSTATE 01004（数据截断）并SQL_SUCCESS_WITH_INFO。 如果数据被截断，而不会因SQL_ATTR_MAX_LENGTH语句属性而丢失显著性 **，SQLGetData**将返回SQL_SUCCESS，并且不返回 SQLSTATE 01004（数据截断）。  
  
 如果**SQLGetData**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则绑定数据缓冲区的内容（如果在绑定列上调用**SQLGetData）** 和长度/指示器缓冲区未定义。  
  
 对**SQLGetData**的连续调用将从请求的最后一列检索数据;以前的偏移量无效。 例如，当执行以下序列时：  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 对 SQLGetData（icol_n） 的第二次调用从 n 列的开头检索数据。 由于以前调用该列的**SQLGetData，** 数据中的任何偏移量都不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述符和 SQLGetData  
 **SQLGetData**不直接与任何描述符字段交互。  
  
 如果*TargetType* SQL_ARD_TYPE，则使用 ARD SQL_DESC_CONCISE_TYPE字段中的数据类型。 如果*TargetType*是SQL_ARD_TYPE或SQL_C_DEFAULT，则根据SQL_DESC_CONCISE_TYPE字段中的数据类型，在 ARD 的SQL_DESC_DATETIME_INTERVAL_PRECISION、SQL_DESC_PRECISION和SQL_DESC_SCALE字段中为数据提供精度和比例。  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序执行**SELECT**语句，以返回按名称、ID 和电话号码排序的客户 ID、名称和电话号码的结果集。 对于每行数据，它会调用**SQLFetch**将光标定位到下一行。 它调用**SQLGetData**来检索提取的数据;在调用**SQLGetData**中指定了数据的缓冲区和返回的字节数。 最后，它打印每个员工的姓名、ID 和电话号码。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|为结果集中的列分配存储|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行与块光标位置无关的批量操作|[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行 SQL 语句|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以仅转发方向获取一行数据或数据块|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在执行时发送参数数据|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位光标、刷新行集中中的数据或更新或删除行集中中的数据|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
