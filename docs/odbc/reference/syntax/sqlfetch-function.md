---
title: SQLFetch 功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285967"
---
# <a name="sqlfetch-function"></a>SQLFetch 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFetch**从结果集中获取下一个数据行集，并返回所有绑定列的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetch**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)来获取关联的 SQLSTATE 值，该函数具有*Handle*SQL_HANDLE_STMT的*句柄类型*和*语句句柄*。 下表列出了**SQLFetch**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。 如果单个列上发生错误，可以使用 SQL_DIAG_COLUMN_NUMBER*的 Diag标识符*调用[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)以确定错误发生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER*的 Diag标识符*调用，以确定包含该列的行。  
  
 对于可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT（01xxx SQLSTATEs 除外），如果多行操作的一个或多个行发生错误（但不是全部）发生错误，则返回SQL_SUCCESS_WITH_INFO，如果单行操作发生错误，则返回SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|为列返回的字符串或二进制数据导致非空白字符或非 NULL 二进制数据的截断。 如果它是一个字符串值，它是右截断的。|  
|01S01|行中的错误|获取一个或多个行时出错。<br /><br /> （如果在 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序时返回此 SQLSTATE，则可以忽略它。|  
|01S07|分数截断|为列返回的数据被截断。 对于数字数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|无法将结果集中列的数据值转换为**SQLBindCol**中*TargetType*指定的数据类型。<br /><br /> 列 0 与SQL_C_BOOKMARK数据类型绑定，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE。<br /><br /> 列 0 与数据类型SQL_C_VARBOOKMARK绑定，并且SQL_ATTR_USE_BOOKMARKS语句属性未设置为SQL_UB_VARIABLE。|  
|07009|无效描述符索引|驱动程序是不支持**SQLExtendedFetch**的 ODBC 2 *.x*驱动程序，在列绑定中指定的列编号为 0。<br /><br /> 列 0 已绑定，SQL_ATTR_USE_BOOKMARKS 语句属性设置为SQL_UB_OFF。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22001|字符串数据，右截断|为列返回的可变长度书签被截断。|  
|22002|需要指标变量，但未提供|NULL 数据被提取到一个列*中，* 该列StrLen_or_IndPtr由**SQLBindCol**设置（或由**SQLSetDescField**或**SQLSetDescRec**设置SQL_DESC_INDICATOR_PTR）为空指针。|  
|22003|数值超范围|将数值作为一个或多个绑定列的数字或字符串返回将导致数字的整个部分（而不是小数）被截断。<br /><br /> 有关详细信息，请参阅在附录 D：数据类型中[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。|  
|22007|无效日期时间格式|结果集中的字符列绑定到日期、时间或时间戳 C 结构，并且列中的值分别是无效的日期、时间或时间戳。|  
|22012|除零|返回算术表达式中的值，结果除以零。|  
|22015|间隔字段溢出|从精确数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> 将数据提取到间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。|  
|22018|强制转换规范的无效字符值|结果集中的字符列绑定到字符 C 缓冲区，该列包含缓冲区的字符集中没有表示的字符。<br /><br /> C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。|  
|24000|无效的游标状态|*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。|  
|40001|序列化失败|执行提取的事务已终止，以防止死锁。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 **SQLFetch**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句句柄*上再次调用**SQLFetch**函数。<br /><br /> 或者 **，SQLFetch**函数被调用，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句处理*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLFetch**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） **SQLFetch**在调用**SQLExtendedFetch**后和在使用SQL_CLOSE选项的**SQLFreeStmt**之前调用了*语句处理*。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|SQL_ATTR_USE_BOOKMARK语句属性设置为SQL_UB_VARIABLE，第 0 列绑定到长度不等于此结果集书签的最大长度的缓冲区。 （此长度在 IRD 的SQL_DESC_OCTET_LENGTH字段中可用，可以通过调用**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**获得。 **SQLColAttribute**|  
|HY107|行值范围外|使用SQL_ATTR_CURSOR_TYPE语句属性指定的值SQL_CURSOR_KEYSET_DRIVEN，但使用SQL_ATTR_KEYSET_SIZE语句属性指定的值大于 0，小于使用SQL_ATTR_ROW_ARRAY_SIZE语句属性指定的值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持**SQLBindCol**中的*TargetType*和相应列的 SQL 数据类型的组合指定的转换。|  
|HYT00|超时时间已到|查询超时期限在数据源返回请求的结果集之前已过期。 超时期间通过 SQL_ATTR_QUERY_TIMEOUT 的 SQLSetStmtAttr 设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **SQLFetch**返回结果集中的下一个行集。 仅当结果集存在时才能调用它：也就是说，在创建结果集的调用之后和在该结果集上的游标关闭之前。 如果绑定任何列，它将返回这些列中的数据。 如果应用程序指定了指向行状态数组的指针或用于返回提取的行数的缓冲区 **，SQLFetch**还会返回此信息。 对**SQLFetch 的**调用可以与**SQLFetchScroll**的调用混合，但不能与**SQLAaFetch 的**调用混合。 有关详细信息，请参阅[获取一行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3 *.x*应用程序与 ODBC 2 *.x*驱动程序一起工作，驱动程序管理器会将**SQLFetch**调用映射到**SQLExtendedFetch，** 用于支持**SQLDb.x 的**ODBC 2 *.x*驱动程序。 如果 ODBC 2 *.x*驱动程序不支持**SQLExtendedFetch，** 驱动程序管理器将**SQLFetch**调用映射到 ODBC 2 *.x*驱动程序中的**SQLFetch，** 该驱动程序只能获取一行。  
  
 有关详细信息，请参阅附录 G 中的[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)：向后兼容性的驱动程序指南。  
  
## <a name="positioning-the-cursor"></a>定位光标  
 创建结果集时，光标位于结果集开始之前。 **SQLFetch**获取下一个行集。 它等效于将*取取定向*设置为SQL_FETCH_NEXT调用**SQLFetchScroll。** 有关游标的详细信息，请参阅[光标](../../../odbc/reference/develop-app/cursors.md)和[块光标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE语句属性指定行集中的行数。 如果**SQLFetch**提取的行集与结果集的末尾重叠，则**SQLFetch**将返回部分行集。 也就是说，如果 S + R - 1 大于 L，其中 S 是要提取的行集的起始行，R 是行集大小，而 L 是结果集中的最后一行，则只有排集的前一行 L - S = 1 行有效。 其余行为空，状态为 SQL_ROW_NOROW。  
  
 **SQLFetch**返回后，当前行是行集的第一行。  
  
 下表中列出的规则基于本节中第二表中列出的条件，描述调用**SQLFetch**后游标定位。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|开始之前|1|  
|*CurrRowset 开始*\<= *上一个结果行 - 行集大小*[1]|*CurrRowset 开始* + *行集大小*[2]|  
|*CurrRowset 开始* > *上一个结果行 - 行集大小*[1]|结束后|  
|结束后|结束后|  
  
 [1] 如果在提取之间更改了行集大小，则这是与上一个提取一起使用的行集大小。  
  
 [2] 如果在提取之间更改了行集大小，则这是与新提取一起使用的行集大小。  
  
|表示法|含义|  
|--------------|-------------|  
|开始之前|块游标位于结果集开始之前。 如果新行集的第一行位于结果集开始之前 **，SQLFetch**将返回SQL_NO_DATA。|  
|结束后|块游标位于结果集结束之后。 如果新行集的第一行位于结果集结束后 **，SQLFetch**将返回SQL_NO_DATA。|  
|*CurrRowset 开始*|当前行集中的第一行的编号。|  
|*最后一个结果行*|结果集中的最后一行的编号。|  
|*行集大小*|行集大小。|  
  
 例如，假设结果集有 100 行，行集大小为 5。 下表显示了**SQLFetch**为不同的起始位置返回的行集和返回代码。  
  
|当前行集|返回代码|新行集|提取的行数|  
|--------------------|-----------------|----------------|------------------------|  
|开始之前|SQL_SUCCESS|1 到 5|5|  
|1 到 5|SQL_SUCCESS|6 到 10|5|  
|52 到 56|SQL_SUCCESS|57 到 61|5|  
|91 到 95|SQL_SUCCESS|96 到 100|5|  
|93 到 97|SQL_SUCCESS|98 到 100。 行状态数组的第 4 行和第 5 行设置为SQL_ROW_NOROW。|3|  
|96 到 100|SQL_NO_DATA|无。|0|  
|99 到 100|SQL_NO_DATA|无。|0|  
|结束后|SQL_NO_DATA|无。|0|  
  
## <a name="returning-data-in-bound-columns"></a>在绑定列中返回数据  
 当**SQLFetch**返回每行时，它将每个绑定列的数据放在绑定到该列的缓冲区中。 如果未绑定列 **，SQLFetch**将返回任何数据，但会向前移动块游标。 仍可以使用**SQLGetData**检索数据。 如果游标是多行游标（即SQL_ATTR_ROW_ARRAY_SIZE大于 1），则仅当使用 SQL_GETDATA_EXTENSIONS*信息类型*调用**SQLGetInfo**时返回SQL_GD_BLOCK才能调用**SQLGetData。** （有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 对于行中的每个绑定列 **，SQLFetch**执行以下操作：  
  
1.  将长度/指示器缓冲区设置为SQL_NULL_DATA，如果数据为 NULL，则继续到下一列。 如果数据为 NULL 且未绑定长度/指示器缓冲区 **，SQLFetch**将返回该行的 SQLSTATE 22002（需要但未提供指标变量），然后继续执行下一行。 有关如何确定长度/指示器缓冲区的地址的信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"缓冲区地址"。  
  
     如果列的数据不是**NULL，SQLFetch**将继续执行步骤 2。  
  
2.  如果SQL_ATTR_MAX_LENGTH语句属性设置为非零值，并且列包含字符或二进制数据，则数据将截断为SQL_ATTR_MAX_LENGTH字节。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH语句属性旨在减少网络流量。 它通常由数据源实现，数据源在通过网络返回数据之前会截截数据。 驱动程序和数据源不需要支持它。 因此，为了保证数据被截断到特定大小，应用程序应分配该大小的缓冲区，并在**SQLBindCol**中指定*cbValueMax*参数中的大小。  
  
3.  将数据转换为**SQLBindCol**中*TargetType*指定的类型。  
  
4.  如果数据转换为可变长度数据类型（如字符或二进制 **），SQLFetch**将检查数据的长度是否超过数据缓冲区的长度。 如果字符数据的长度（包括空终止字符）超过数据缓冲区的长度 **，SQLFetch**会将数据截取到数据缓冲区的长度，而减去空终止字符的长度。 然后，它将终止数据。 如果二进制数据的长度超过数据缓冲区的长度 **，SQLFetch**会将其截截到数据缓冲区的长度。 在**SQLBindCol**中，使用*缓冲区长度*指定数据缓冲区的长度。  
  
     **SQLFetch**从不截取转换为固定长度数据类型的数据;它始终假定数据缓冲区的长度是数据类型的大小。  
  
5.  将转换后的数据（可能截断）数据放入数据缓冲区中。 有关如何确定数据缓冲区地址的信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"缓冲区地址"。  
  
6.  将数据的长度放在长度/指示器缓冲区中。 如果指标指针和长度指针都设置为相同的缓冲区（与**SQLBindCol**的调用相同），则长度将写入缓冲区中，用于有效数据，并在 NULL 数据的缓冲区中写入SQL_NULL_DATA。 如果未绑定长度/指示器缓冲区 **，SQLFetch**不会返回长度。  
  
    -   对于字符或二进制数据，这是转换后和截断前由于数据缓冲区太小而截断之前的数据长度。 如果驱动程序无法确定转换后的数据长度（有时与长数据的情况一样），它将长度设置为SQL_NO_TOTAL。 如果数据由于SQL_ATTR_MAX_LENGTH语句属性而被截断，则此属性的值将放在长度/指示器缓冲区中，而不是实际长度 。 这是因为此属性旨在在转换之前截截服务器上的数据，以便驱动程序无法确定实际长度。  
  
    -   对于所有其他数据类型，这是转换后的数据长度;也就是说，它是数据转换到的类型的大小。  
  
     有关如何确定长度/指示器缓冲区的地址的信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"缓冲区地址"。  
  
7.  如果在转换过程中将数据截断而不丢失有效数字（例如，转换时，实际数字 1.234 被截断到整数**1），SQLFetch**将返回 SQLSTATE 01S07（分数截断）并SQL_SUCCESS_WITH_INFO。 如果数据由于数据缓冲区的长度太小而被截断（例如，字符串"abcdef"放在 4 字节缓冲区中 **），SQLFetch**将返回 SQLSTATE 01004（数据截断）并SQL_SUCCESS_WITH_INFO。 如果数据由于SQL_ATTR_MAX_LENGTH语句属性而截断 **，SQLFetch**将返回SQL_SUCCESS，并且不返回 SQLSTATE 01S07（分数截断）或 SQLSTATE 01004（数据截断）。 如果在转换过程中截断数据，丢失有效数字（例如，如果大于 100，000 的SQL_INTEGER值转换为**SQL_C_TINYINT），SQLFetch**将返回 SQLSTATE 22003（范围外的数字值）和SQL_ERROR（如果行集大小为 1）或SQL_SUCCESS_WITH_INFO（如果行集大小大于 1）。  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则绑定数据缓冲区和长度/指示器缓冲区的内容未定义。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组用于返回行集中每行的状态。 此数组的地址是使用SQL_ATTR_ROW_STATUS_PTR语句属性指定的。 数组由应用程序分配，并且必须具有SQL_ATTR_ROW_ARRAY_SIZE语句属性指定的元素数。 其值由**SQLFetch、SQLFetchScroll**和**SQLBulk 操作**或**SQLSetPos**设置（在**SQLAeFetch**定位后调用它们时除外）。 **SQLFetch** 如果SQL_ATTR_ROW_STATUS_PTR语句属性的值为空指针，则这些函数不会返回行状态。  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则行状态数组缓冲区的内容未定义。  
  
 行状态数组中返回以下值。  
  
|行状态数组值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|该行已成功提取，自上次从此结果集提取以来一直未更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|该行已成功提取，自上次从此结果集提取以来一直未更改。 但是，返回了有关该行的警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED[1]、[2]和[3]|该行已成功提取，自上次从此结果集提取以来已更改。 如果此行再次从此结果集中提取，或者由**SQLSetPos**刷新，则状态将更改为该行的新状态。|  
|SQL_ROW_DELETED[3]|自上次从此结果集中提取行以来，该行已被删除。|  
|SQL_ROW_ADDED[4]|该行由**SQLBulk 操作**插入。 如果再次从此结果集中提取该行，或由**SQLSetPos**刷新，则其状态SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|行集与结果集的末尾重叠，并且不会返回对应于行状态数组的此元素的行。|  
  
 [1] 对于键集、混合游标和动态游标，如果更新了键值，则数据行将被视为已删除并添加新行。  
  
 [2] 某些驱动程序无法检测数据的更新，因此无法返回此值。 要确定驱动程序是否可以检测更新以重新提取行，应用程序使用SQL_ROW_UPDATES选项调用**SQLGetInfo。**  
  
 [3] **SQLFetch**只有在与**SQLFetchScroll**的调用混合时才能返回此值。 这是因为**SQLFetch**在结果集中向前移动，并且当它被独占使用时，不会重新提取任何行。 由于没有重新提取任何行 **，SQLFetch**不会检测以前提取的行所做的更改。 但是，如果**SQLFetchScroll**在以前提取的任何行之前定位游标，并且**SQLFetch**用于获取这些行，**则 SQLFetch**可以检测对这些行的任何更改。  
  
 [4] 仅由 SQLBulk 操作返回。 未由**SQLFetch**或**SQLFetchScroll**设置。  
  
### <a name="rows-fetched-buffer"></a>行提取缓冲区  
 取自缓冲区的行用于返回提取的行数，包括由于在提取行时发生错误而未返回数据的行。 换句话说，它是行状态数组中的值不SQL_ROW_NOROW的行数。 此缓冲区的地址使用SQL_ATTR_ROWS_FETCHED_PTR语句属性指定。 缓冲区由应用程序分配。 它由**SQLFetch**和**SQLFetchScroll**设置。 如果SQL_ATTR_ROWS_FETCHED_PTR语句属性的值为空指针，则这些函数不会返回获取的行数。 要确定结果集中的当前行数，应用程序可以使用 SQL_ATTR_ROW_NUMBER 属性调用**SQLGetStmtAttr。**  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则行提取缓冲区的内容未定义，除非返回SQL_NO_DATA，在这种情况下，行提取缓冲区中的值设置为 0。  
  
### <a name="error-handling"></a>错误处理  
 错误和警告可以应用于单个行或整个函数。 有关诊断记录的详细信息，请参阅[诊断](../../../odbc/reference/develop-app/diagnostics.md)和[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>整个函数上的错误和警告  
 如果错误应用于整个函数，例如 SQLSTATE HYT00（超时已过期）或 SQLSTATE 24000（无效游标状态 **），SQLFetch**将返回SQL_ERROR和适用的 SQLSTATE。 行集缓冲区的内容未定义，光标位置保持不变。  
  
 如果警告应用于整个函数 **，SQLFetch**将返回SQL_SUCCESS_WITH_INFO和适用的 SQLSTATE。 应用于整个函数的警告的状态记录在应用于单个行的状态记录之前返回。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>单个行中的错误和警告  
 如果错误（如 SQLSTATE 22012（除零）））或警告（如 SQLSTATE 01004（数据截断）））应用于单个行 **，SQLFetch**执行以下操作：  
  
-   将行状态数组的相应元素设置为SQL_ROW_ERROR错误或SQL_ROW_SUCCESS_WITH_INFO警告。  
  
-   添加包含 SQLSTAT 的零个或多个状态记录，以查找错误或警告。  
  
-   设置状态记录中的行和列编号字段。 如果**SQLFetch**无法确定行或列号，它将该数字分别设置为SQL_ROW_NUMBER_UNKNOWN或SQL_COLUMN_NUMBER_UNKNOWN。 如果状态记录不适用于特定列 **，SQLFetch**会将列号设置为SQL_NO_COLUMN_NUMBER。  
  
 **SQLFetch**继续提取行，直到它获取行集中的所有行。 除非行集的每一行（不包括状态SQL_ROW_NOROW的行）中发生错误，否则它将返回SQL_SUCCESS_WITH_INFO，在这种情况下，它将返回SQL_ERROR。 特别是，如果行集大小为 1，并且该行中出现错误，则**SQLFetch**将返回SQL_ERROR。  
  
 **SQLFetch**按行号顺序返回状态记录。 也就是说，它返回未知行的所有状态记录（如果有）;接下来，它返回第一行的所有状态记录（如果有），然后返回第二行的所有状态记录（如果有），等等。 每行的状态记录根据常规规则排序状态记录;有关详细信息，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的"状态记录序列"。  
  
### <a name="descriptors-and-sqlfetch"></a>描述符和 SQLFetch  
 以下各节介绍**SQLFetch**如何与描述符进行交互。  
  
#### <a name="argument-mappings"></a>参数映射  
 驱动程序不设置任何描述符字段基于**SQLFetch**的参数。  
  
#### <a name="other-descriptor-fields"></a>其他描述符字段  
 **SQLFetch**使用以下描述符字段。  
  
|描述符字段|德克|字段|设置通过|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|阿尔德|标头的值开始缓存响应|SQL_ATTR_ROW_ARRAY_SIZE语句属性|  
|SQL_DESC_ARRAY_STATUS_PTR|税务局|标头的值开始缓存响应|SQL_ATTR_ROW_STATUS_PTR语句属性|  
|SQL_DESC_BIND_OFFSET_PTR|阿尔德|标头的值开始缓存响应|SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性|  
|SQL_DESC_BIND_TYPE|阿尔德|标头的值开始缓存响应|SQL_ATTR_ROW_BIND_TYPE语句属性|  
|SQL_DESC_COUNT|阿尔德|标头的值开始缓存响应|**SQLBindCol**的*列编号*参数|  
|SQL_DESC_DATA_PTR|阿尔德|records|**SQLBindCol** *的目标值 Ptr*参数|  
|SQL_DESC_INDICATOR_PTR|阿尔德|records|*StrLen_or_IndPtr*在**SQLBindCol**中参数|  
|SQL_DESC_OCTET_LENGTH|阿尔德|records|**SQLBindCol**中的*缓冲区长度*参数|  
|SQL_DESC_OCTET_LENGTH_PTR|阿尔德|records|*StrLen_or_IndPtr*在**SQLBindCol**中参数|  
|SQL_DESC_ROWS_PROCESSED_PTR|税务局|标头的值开始缓存响应|SQL_ATTR_ROWS_FETCHED_PTR语句属性|  
|SQL_DESC_TYPE|阿尔德|records|**SQLBindCol**中*的目标类型*参数|  
  
 所有描述符字段也可以通过**SQLSetDescField 进行**设置。  
  
#### <a name="separate-length-and-indicator-buffers"></a>单独的长度和指示器缓冲区  
 应用程序可以绑定单个缓冲区或两个单独的缓冲区，可用于保存长度和指标值。 当应用程序调用**SQLBindCol**时，驱动程序将 ARD 的SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR字段设置到同一地址，该地址在*StrLen_or_IndPtr*参数中传递。 当应用程序调用**SQLSetDescField**或**SQLSetDescRec**时，它可以将这两个字段设置为不同的地址。  
  
 **SQLFetch**确定应用程序是否指定了单独的长度和指示器缓冲区。 在这种情况下，当数据不是 NULL 时 **，SQLFetch**将指示器缓冲区设置为 0 并返回长度缓冲区中的长度。 当数据为 NULL 时 **，SQLFetch**将指示器缓冲区设置为SQL_NULL_DATA，并且不修改长度缓冲区。  
  
### <a name="code-example"></a>代码示例  
 请参阅[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)SQLBindCol、SQLColumns、SQLGetData 和 SQL 程序。 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
### <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|关闭语句上的光标|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|获取数据列的一部分或全部|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回结果集列数|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
