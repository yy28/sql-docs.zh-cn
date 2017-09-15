---
title: "SQLFetch 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 135ee130d56801c5da3abb47447a1372d29656a5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetch-function"></a>SQLFetch 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFetch**从结果集中提取数据的下一步的行集，并返回所有绑定的列的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetch**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLFetch**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。 如果上一个列中，发生错误时[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)可以使用调用*DiagIdentifier*的 SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 列和**SQLGetDiagField**可以使用调用*DiagIdentifier*的 SQL_DIAG_ROW_NUMBER 以确定包含该列的行。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除外 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果将上一个或多个，但并非所有行的一个多行的操作，发生错误时，如果上发生错误时返回 SQL_ERROR单行更行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制数据的列返回导致非空白字符或非 NULL 二进制数据截断。 如果它是一个字符串值，它是右侧被截断。|  
|01S01|行中的错误|提取一个或多个行时出错。<br /><br /> (如果此 SQLSTATE 返回时 ODBC 3*.x*应用程序使用 ODBC 2*.x*驱动程序，则可以忽略它。)|  
|01S07|小数部分组成的截断|返回的列的数据被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳，和包含时间组件的 interval 数据类型，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法转换的结果集中的列的数据值，由指定的数据类型为*TargetType*中**SQLBindCol**。<br /><br /> 第 0 列被绑定了一个数据类型为 SQL_C_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_VARIABLE。<br /><br /> 第 0 列被绑定了一个数据类型为 SQL_C_VARBOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性未设置为 SQL_UB_VARIABLE。|  
|07009|无效的描述符索引|该驱动程序是 ODBC 2*.x*驱动程序不支持**SQLExtendedFetch**，和一个列的绑定中指定某个列号了 0。<br /><br /> 第 0 列被绑定，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22001|字符串数据，右截断|长度可变的书签的列返回被截断。|  
|22002|需要指示器变量，但未提供|NULL 数据提取了的列中其*StrLen_or_IndPtr*设置**SQLBindCol** (或通过设置 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 是空指针。|  
|22003|数值超出范围|返回数字的数值或字符串的一个或多个绑定的列可能会导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> 有关详细信息，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附录 d： 数据类型中。|  
|22007|无效的日期时间格式|结果集中的字符列已绑定到日期、 时间或时间戳 C 结构，列中的值，分别无效的日期、 时间戳。|  
|22012|被零除|返回一个值算术表达式中的，这会导致除法被零除。|  
|22015|间隔字段溢出|将从精确数字或间隔 SQL 类型分配给间隔 C 类型由前导字段中的重要数字丢失。<br /><br /> 在提取到间隔 C 类型数据, 时没有间隔 C 类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的的无效字符值|结果集中的字符列已绑定到 C 字符缓冲区，并且列包含没有任何表示形式的缓冲区的字符集的字符。<br /><br /> C 类型已准确或近似数字、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;并且列中的值不是有效的文本的绑定的 C 类型。|  
|24000|无效的游标状态|*StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。|  
|40001|序列化失败|在其中执行提取事务已终止，以防止死锁。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 **SQLFetch**调用函数，并且它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*. 则**SQLFetch**函数上调用了再次*StatementHandle*。<br /><br /> 或者， **SQLFetch**调用函数，并且它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*从多线程应用程序中的不同线程。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLFetch**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) **SQLFetch**曾为*StatementHandle*后**SQLExtendedFetch**调用和之前**SQLFreeStmt**与 SQL_调用了关闭选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|SQL_ATTR_USE_BOOKMARK 语句属性已设置为 SQL_UB_VARIABLE，并且第 0 列已绑定到其的长度不等于该结果集的书签的最大长度的缓冲区。 (此长度的 IRD SQL_DESC_OCTET_LENGTH 字段中是否可用，并可以通过调用获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY107|行数值超出范围|指定具有 SQL_ATTR_CURSOR_TYPE 语句属性的值是 SQL_CURSOR_KEYSET_DRIVEN，但具有 SQL_ATTR_KEYSET_SIZE 语句属性指定的值是大于 0 而小于 SQL_ATTR_ROW_ARRAY_ 用指定的值大小语句属性。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过 SQLSetStmtAttr，SQL_ATTR_QUERY_TIMEOUT 设置的超时期限。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLFetch**结果集中返回的下一步的行集。 仅当存在结果集时，可以调用它： 即，调用后创建的结果集并光标结果集的转移已关闭。 如果没有绑定任何列，将在这些列中返回的数据。 如果应用程序指定行状态数组或其返回的行提取，数中的缓冲区的指针**SQLFetch**也会返回此信息。 调用**SQLFetch**可以通过调用混合**SQLFetchScroll**但不能与调用混合**SQLExtendedFetch**。 有关详细信息，请参阅[提取行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3*.x*应用程序处理 ODBC 2*.x*驱动程序，驱动程序管理器映射**SQLFetch**调用**SQLExtendedFetch**为ODBC 2*.x*支持驱动程序**SQLExtendedFetch**。 如果 ODBC 2*.x*驱动程序不支持**SQLExtendedFetch**，驱动程序管理器映射**SQLFetch**调用**SQLFetch** ODBC 2 中*.x*驱动程序，可以提取只有一行。  
  
 有关详细信息，请参阅[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
## <a name="positioning-the-cursor"></a>将光标定位  
 创建结果集时，游标位于结果集的开始之前。 **SQLFetch**提取下一步的行集。 它等效于调用**SQLFetchScroll**与*FetchOrientation*设置为 SQL_FETCH_NEXT。 有关游标的详细信息，请参阅[游标](../../../odbc/reference/develop-app/cursors.md)和[块状游标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行集中的行数。 如果通过提取行集正在**SQLFetch**重叠结果集末尾**SQLFetch**返回部分行集。 也就是说，S + R – 1 大于 L，其中 S 等于正在提取行集 R 的起始行是行集大小和 L 为最后一个行在结果集中，然后仅第一个 L-S + 1 的行集的行有效。 空和状态的 SQL_ROW_NOROW 剩余行。  
  
 后**SQLFetch**返回时，当前行是行集的第一行。  
  
 下表中列出的规则描述光标定位在调用后**SQLFetch**，将根据本节中的第二个表中列出的条件。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|开始之前|1|  
|*CurrRowsetStart* \< =  *LastResultRow – RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow – RowsetSize*[1]|在结束后|  
|在结束后|在结束后|  
  
 [1] 如果提取行集大小发生更改，这是在使用了以前提取的行集大小。  
  
 [2] 如果提取行集大小发生更改，这是在使用了新提取的行集大小。  
  
|表示法|含义|  
|--------------|-------------|  
|开始之前|块状游标位于结果集的开始之前。 如果新的行集的第一个行的结果集，开始之前**SQLFetch**返回 SQL_NO_DATA。|  
|在结束后|块状游标位于结果的一端设置后。 如果在新行集的第一个行后该结果集末尾**SQLFetch**返回 SQL_NO_DATA。|  
|*CurrRowsetStart*|第一个行集中的当前行数。|  
|*LastResultRow*|在结果集中的最后一行的编号。|  
|*RowsetSize*|行集大小。|  
  
 例如，假设结果集有 100 行和行集大小为 5。 下表显示返回的行集和返回代码**SQLFetch**为不同的起始位置。  
  
|当前行集|返回代码|新行集。|# of 提取的行|  
|--------------------|-----------------|----------------|------------------------|  
|开始之前|SQL_SUCCESS|1 到 5|5|  
|1 到 5|SQL_SUCCESS|6 至 10|5|  
|52 到 56|SQL_SUCCESS|57 到 61|5|  
|91 到 95|SQL_SUCCESS|96 到 100|5|  
|93 到 97|SQL_SUCCESS|98 到 100。 行 4 和 5 的行状态数组设置为 SQL_ROW_NOROW。|3|  
|96 到 100|SQL_NO_DATA|无。|0|  
|99 到 100|SQL_NO_DATA|无。|0|  
|在结束后|SQL_NO_DATA|无。|0|  
  
## <a name="returning-data-in-bound-columns"></a>绑定的列中返回数据  
 作为**SQLFetch**返回每个行中，它将为每个绑定的列的数据放在绑定到该列的缓冲区。 如果没有列被绑定， **SQLFetch**不返回任何数据，但未向前移动块状游标。 仍可以使用检索的数据**SQLGetData**。 如果光标位于多行的光标 （即，SQL_ATTR_ROW_ARRAY_SIZE 是大于 1）， **SQLGetData** SQL_GD_BLOCK 返回时，才可以调用**SQLGetInfo**使用调用*信息类型*SQL_GETDATA_EXTENSIONS。 (有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。)  
  
 为在行中，每个绑定列**SQLFetch**执行下列任务：  
  
1.  将长度/指示器缓冲区设置为 SQL_NULL_DATA 而直接进入下一列，如果数据为 NULL。 如果数据为 NULL，而没有长度/指示器缓冲区被绑定， **SQLFetch**行返回 SQLSTATE 22002 （指示器变量需要但未提供），并将继续到下一行。 有关如何确定长度/指示器缓冲区的地址的信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
     如果列的数据不为 NULL， **SQLFetch**继续到步骤 2。  
  
2.  如果 SQL_ATTR_MAX_LENGTH 语句属性设置为非零值，并且该列包含字符或二进制数据，数据将剪裁为 SQL_ATTR_MAX_LENGTH 字节。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 语句属性旨在减少网络流量。 它通常由数据源，然后再返回通过网络将截断数据来实现。 驱动程序和数据源不需要支持它。 因此，若要确保数据将剪裁为特定的大小，应用程序应分配这种大小的缓冲区，并指定的大小以*cbValueMax*中的参数**SQLBindCol**。  
  
3.  将数据转换为指定的类型*TargetType*中**SQLBindCol**。  
  
4.  如果数据已转换为可变长度数据类型，如字符或二进制， **SQLFetch**检查数据的长度是否超出数据缓冲区的长度。 如果字符数据 （包括 null 终止字符） 的长度超过数据缓冲区的长度**SQLFetch**将截断到 null 终止字符的长度小于数据缓冲区的长度的数据。 它然后 null 终止的数据。 如果二进制数据的长度超过了数据缓冲区**SQLFetch**将它截断为数据缓冲区的长度。 使用指定数据缓冲区的长度*BufferLength*中**SQLBindCol**。  
  
     **SQLFetch**永远不会截断数据转换为固定长度的数据类型; 它始终假设数据缓冲区的长度的数据类型的大小。  
  
5.  将放置在数据缓冲区的转换 （和可能截断） 数据。 有关如何确定数据缓冲区的地址的信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
6.  将长度/指示器缓冲区中数据的长度。 如果指示器指针和长度指针已设置为相同的缓冲区 (与调用**SQLBindCol**未)，长度编写有效的数据的缓冲区中，并且 SQL_NULL_DATA 写入 NULL 数据缓冲区中。 如果没有长度/指示器缓冲区被绑定， **SQLFetch**不返回长度。  
  
    -   对于字符或二进制数据，这是数据的长度之后转换和之前截断因为数据缓冲区太小。 如果该驱动程序无法转换后，确定数据的长度，因为有时是长整型数据这种情况，它会设置为 SQL_NO_TOTAL 的长度。 如果由于 SQL_ATTR_MAX_LENGTH 语句特性情况下，数据已被截断，则会将此属性的值放在而不是实际长度长度/指示器缓冲区。 这是因为此属性设计截断转换之前, 在服务器上的数据，以便该驱动程序还了解的实际长度没有方法。  
  
    -   对于所有其他数据类型，这是数据的长度转换后;也就是说，正是数据已转换到的目标类型的大小。  
  
     有关如何确定长度/指示器缓冲区的地址的信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
7.  如果在转换而不会丢失有效位数期间便会截断数据 （例如，实数 1.234 被截断为整数 1 转换时）， **SQLFetch**返回 SQLSTATE 01S07 （小数截断） 和 SQL_SUCCESS_WITH_INFO。 如果数据被截断，因为数据缓冲区的长度是太小 （例如，字符串"abcdef"放在 4 字节缓冲区）， **SQLFetch**返回 SQLSTATE 01004 （截断的数据） 和 SQL_SUCCESS_WITH_INFO。 如果由于 SQL_ATTR_MAX_LENGTH 语句特性，截断数据**SQLFetch**返回 SQL_SUCCESS 且不返回 SQLSTATE 01S07 （小数截断） 或 SQLSTATE 01004 （数据截断）。 如果数据丢失的有效位数 （例如，如果大于 100,000 的 SQL_INTEGER 值已转换为 SQL_C_TINYINT） 的转换过程中会被截断**SQLFetch**返回 SQLSTATE 22003 （超出范围的数字值）和 SQL_ERROR （如果行集大小为 1） 或 SQL_SUCCESS_WITH_INFO （如果行集大小大于 1） 中。  
  
 如果将绑定的数据缓冲区和长度/指示器缓冲区的内容是不确定**SQLFetch**或**SQLFetchScroll**不返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组用于行集合中返回的每个行的状态。 指定了 SQL_ATTR_ROW_STATUS_PTR 语句属性，此数组的地址。 数组由应用程序分配的并且必须具有由 SQL_ATTR_ROW_ARRAY_SIZE 语句特性指定的所有元素。 设置其值**SQLFetch**， **SQLFetchScroll**，和**SQLBulkOperations**或**SQLSetPos** （除外，当它们具有已调用通过具有已定位光标后**SQLExtendedFetch**)。 如果 SQL_ATTR_ROW_STATUS_PTR 语句属性的值为 null 指针，这些函数不返回行的状态。  
  
 如果将行状态数组缓冲区的内容是不确定**SQLFetch**或**SQLFetchScroll**不返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 行状态数组中返回以下值。  
  
|行状态数组值|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行提取了成功，并且后未发生更改它上次提取从该结果集。|  
|SQL_ROW_SUCCESS_WITH_INFO|行提取了成功，并且后未发生更改它上次提取从该结果集。 但是，有关行返回一条警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED [1]，[2] 和 [3]|行提取了成功，并且自上次提取该结果集从以来已更改。 如果从该结果集再次提取或通过刷新行**SQLSetPos**，状态将更改为行的新状态。|  
|SQL_ROW_DELETED [3]|已删除行，因为它上次提取从该结果集。|  
|SQL_ROW_ADDED [4]|插入行时发生**SQLBulkOperations**。 如果从该结果集再次提取或通过刷新行**SQLSetPos**，其状态为 SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|行集占用该结果集的末尾，并且会不返回任何行，对应于此元素的行状态数组。|  
  
 [1] 对于键集游标混合，和动态游标，如果更新密钥的值时，数据的行被视为已被删除且添加新行。  
  
 [2] 某些驱动程序无法检测到对数据的更新，因此无法返回此值。 若要确定驱动程序是否可以检测到对 refetched 行的更新，应用程序调用**SQLGetInfo** SQL_ROW_UPDATES 选项。  
  
 [3] **SQLFetch**可以返回此值，仅当它是混合在一起调用**SQLFetchScroll**。 这是因为**SQLFetch**表示向前移动整个结果集和以独占方式使用它时，重新任何行不提取。 因为任何行不 refetched， **SQLFetch**不会检测对先前获取的行所做的更改。 但是，如果**SQLFetchScroll**将光标置于之前任何以前提取行和**SQLFetch**用于提取这些行， **SQLFetch**可以检测到的任何更改这些行。  
  
 [4] 仅返回由 SQLBulkOperations。 未设置**SQLFetch**或**SQLFetchScroll**。  
  
### <a name="rows-fetched-buffer"></a>行提取缓冲区  
 提取缓冲区的行用于返回的行提取，包括那些为其，因为它们正在提取出错未返回任何数据的行数。 换而言之，它是为其行状态数组中的值不是 SQL_ROW_NOROW 的行数。 指定了 SQL_ATTR_ROWS_FETCHED_PTR 语句属性，此缓冲区的地址。 应用程序分配缓冲区。 设置**SQLFetch**和**SQLFetchScroll**。 如果 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值为 null 指针，这些函数不返回提取的行数。 若要确定在结果集中的当前行号，应用程序可以调用**SQLGetStmtAttr**具有 SQL_ATTR_ROW_NUMBER 属性。  
  
 如果将提取的行缓冲区的内容是不确定**SQLFetch**或**SQLFetchScroll**不除当 SQL_NO_DATA 返回时，在这种情况下返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，在提取缓冲区的行中的值设置为 0。  
  
### <a name="error-handling"></a>错误处理  
 错误和警告可以应用于各个行或整个函数。 有关诊断记录的详细信息，请参阅[诊断](../../../odbc/reference/develop-app/diagnostics.md)和[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>错误和警告的整个函数  
 如果错误适用于整个函数，如 SQLSTATE HYT00 （超时） 或 SQLSTATE 24000 （无效的游标状态）， **SQLFetch**返回 SQL_ERROR 和适用的 SQLSTATE。 是不确定的行集缓冲区的内容，并且光标位置不变。  
  
 如果警告适用于整个函数， **SQLFetch**返回 SQL_SUCCESS_WITH_INFO 和适用的 SQLSTATE。 将应用于整个函数的警告的状态记录返回之前应用于单个行的状态记录。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>错误和警告单个行中  
 如果出现错误 （例如 SQLSTATE 22012 （被零除）) 或警告 （例如 SQLSTATE 01004 （截断的数据）) 将适用于单个行， **SQLFetch**执行下列任务：  
  
-   将设置行状态数组的对应元素为 SQL_ROW_ERROR 了解错误或 SQL_ROW_SUCCESS_WITH_INFO 警告。  
  
-   将添加包含 SQLSTATEs 错误或警告的零个或多个状态记录。  
  
-   设置行和列的数字字段中的状态记录。 如果**SQLFetch**无法确定了行或列号，将该数量设置为 SQL_ROW_NUMBER_UNKNOWN 或 SQL_COLUMN_NUMBER_UNKNOWN，分别。 如果状态记录不适用于特定的列， **SQLFetch** SQL_NO_COLUMN_NUMBER 到设置的列号。  
  
 **SQLFetch**继续提取行，直到它已提取的行集中的所有行。 它将返回 SQL_SUCCESS_WITH_INFO，除非在此情况下它将返回 SQL_ERROR （不包括状态 SQL_ROW_NOROW 行） 的行集，每个行中发生错误。 具体而言，如果行集大小为 1，并且在该行中，出现错误**SQLFetch**返回 SQL_ERROR。  
  
 **SQLFetch**按行编号顺序返回的状态记录。 也就是说，它返回未知行 （如果有的话）; 的所有状态的记录接下来，它返回第一行 （如果有），所有状态记录，然后它都返回的第二行 （如果有），等的所有状态记录。 每个行的状态记录进行排序根据正常规则排序状态记录。有关详细信息，请参见"序列的状态"记录中[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
### <a name="descriptors-and-sqlfetch"></a>说明符和 SQLFetch  
 以下各节描述了如何**SQLFetch**与描述符交互。  
  
#### <a name="argument-mappings"></a>自变量映射  
 该驱动程序不会设置任何基于的自变量的描述符字段**SQLFetch**。  
  
#### <a name="other-descriptor-fields"></a>其他描述符字段  
 使用以下的描述符字段**SQLFetch**。  
  
|描述符字段|Desc。|中的字段|通过设置|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|标头|SQL_ATTR_ROW_ARRAY_SIZE 语句属性|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|标头|SQL_ATTR_ROW_STATUS_PTR 语句属性|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|标头|SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性|  
|SQL_DESC_BIND_TYPE|ARD|标头|SQL_ATTR_ROW_BIND_TYPE 语句属性|  
|SQL_DESC_COUNT|ARD|标头|*ColumnNumber*参数**SQLBindCol**|  
|SQL_DESC_DATA_PTR|ARD|记录|*TargetValuePtr*参数**SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|ARD|记录|*StrLen_or_IndPtr*中的参数**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|ARD|记录|*BufferLength*中的参数**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|记录|*StrLen_or_IndPtr*中的参数**SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|标头|SQL_ATTR_ROWS_FETCHED_PTR 语句属性|  
|SQL_DESC_TYPE|ARD|记录|*TargetType*中的参数**SQLBindCol**|  
  
 此外可以通过设置所有描述符字段**SQLSetDescField**。  
  
#### <a name="separate-length-and-indicator-buffers"></a>单独的长度和指示器缓冲区  
 单个缓冲区或可以用来保存长度和指示器值的两个单独缓冲区，则可以将绑定应用程序。 在应用程序调用**SQLBindCol**，驱动程序将 ARD SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 字段设置为相同的地址，传入*StrLen_or_IndPtr*自变量。 在应用程序调用**SQLSetDescField**或**SQLSetDescRec**，它可以将这两个字段设置为不同的地址。  
  
 **SQLFetch**确定应用程序是否具有指定单独的长度和指示器缓冲区。 在这种情况下，数据不为 NULL，当**SQLFetch**将指示器缓冲区设置为 0 和长度缓冲区中返回的长度。 当数据为 NULL， **SQLFetch**将指示器缓冲区设置为 SQL_NULL_DATA 并不会修改长度缓冲区。  
  
### <a name="code-example"></a>代码示例  
 请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，和[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)。  
  
### <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|关闭的语句上光标|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|提取部分或全部数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回的结果数设置列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
