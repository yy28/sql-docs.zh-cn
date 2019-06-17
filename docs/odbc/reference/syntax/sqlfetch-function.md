---
title: SQLFetch 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15074b31b1c147ef78a898dbb8624f3b40358d13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537142"
---
# <a name="sqlfetch-function"></a>SQLFetch 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLFetch**从结果集中提取数据的下一个行集，并返回所有绑定列的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetch**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLFetch** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。 如果在单个列中，出现错误[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)可以使用调用*DiagIdentifier* SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 的列的和**SQLGetDiagField**可以使用调用*DiagIdentifier*的 SQL_DIAG_ROW_NUMBER 以确定包含这一列的行。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果上一个或多个，但并非所有行的多行操作，出现错误，并且如果发生错误，则返回 SQL_ERROR单行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制的列返回的数据时截断了非空白字符或非 NULL 的二进制数据。 如果它是一个字符串值，它是右侧被截断。|  
|01S01|行中的错误|获取一个或多个行时出错。<br /><br /> (如果在 ODBC 3 时返回此 SQLSTATE *.x*应用程序使用 ODBC 2 *.x*驱动程序，则可以忽略它。)|  
|01S07|截断小数部分|返回的列的数据已被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳和包含时间部分的时间间隔数据类型，已截断的小数部分的时间。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法为指定的数据类型转换的结果集中的列的数据值*TargetType*中**SQLBindCol**。<br /><br /> 第 0 列绑定使用的数据类型为 SQL_C_BOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。<br /><br /> 第 0 列绑定使用的数据类型为 SQL_C_VARBOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性未设置为 SQL_UB_VARIABLE。|  
|07009|描述符索引无效|该驱动程序是 ODBC 2 *.x*不支持的驱动程序**SQLExtendedFetch**，和列的绑定中指定列编号为 0。<br /><br /> 第 0 列被绑定，并将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22001|字符串数据，右截断|长度可变的书签的列返回已被截断。|  
|22002|需要指示器变量，但未提供|NULL 已提取数据的列中其*StrLen_or_IndPtr*设置**SQLBindCol** (或通过设置 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 是空指针。|  
|22003|数值超出范围|返回数字的数值或字符串的一个或多个绑定列可能会造成数字被截断的整个 （而不是小数） 部分。<br /><br /> 有关详细信息，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中附录 d:数据类型。|  
|22007|日期时间格式无效|在结果集中的字符列已绑定到日期、 时间或时间戳 C 结构和列中的值时，分别，无效的日期、 时间戳。|  
|22012|被零除|算术表达式中的值返回，这导致除零。|  
|22015|间隔字段溢出|将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型前导字段中时导致重要数字丢失。<br /><br /> 提取数据到 C 间隔类型时，出现没有 C 间隔类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的字符值无效|结果集中的字符列已绑定到 C 字符缓冲区，而该列包含出现没有缓冲区的字符集中的表示形式的字符。<br /><br /> C 类型为精确或近似数值、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;和列中的值不是有效的绑定 C 类型的文本。|  
|24000|游标状态无效|*StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。|  
|40001|序列化失败|在其中执行提取该事务已终止，以防止死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 **SQLFetch**调用函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*. 然后**SQLFetch**上再次调用函数*StatementHandle*。<br /><br /> 或者， **SQLFetch**调用函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*从多线程应用程序中不同的线程。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLFetch**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） **SQLFetch**曾为*StatementHandle*后**SQLExtendedFetch**调用之前**SQLFreeStmt**与 SQL_调用了关闭选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|SQL_ATTR_USE_BOOKMARK 语句属性设置为 SQL_UB_VARIABLE，并且第 0 列绑定到其的长度不等于此结果集的书签的最大长度的缓冲区。 (此长度可在 IRD 的 SQL_DESC_OCTET_LENGTH 字段中，并且可以通过调用来获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY107|行数值超出范围|SQL_ATTR_CURSOR_TYPE 语句属性与指定的值为 SQL_CURSOR_KEYSET_DRIVEN，但使用 SQL_ATTR_KEYSET_SIZE 语句属性指定的值大于 0 且小于 SQL_ATTR_ROW_ARRAY_ 用指定的值大小语句属性。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前请求的结果集返回的数据源。 SQLSetStmtAttr，sql_attr_query_timeout 时，可通过设置超时期限。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLFetch**在结果集中返回的下一步的行集。 结果集中存在时才可以调用它： 即，在调用后，创建结果集和游标结果集中的转移已关闭。 如果任何列的绑定，将这两列中返回的数据。 如果应用程序指定行状态数组或在其中返回读取的行数的缓冲区的指针，则**SQLFetch**也会返回此信息。 调用**SQLFetch**可以通过调用混合**SQLFetchScroll**但不能在其中调用**SQLExtendedFetch**。 有关详细信息，请参阅[提取行数据](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3 *.x*应用程序适用于 ODBC 2 *.x*驱动程序，驱动程序管理器将映射**SQLFetch**调用**SQLExtendedFetch**为ODBC 2 *.x*支持的驱动程序**SQLExtendedFetch**。 如果 ODBC 2 *.x*驱动程序不支持**SQLExtendedFetch**，驱动程序管理器映射**SQLFetch**调用**SQLFetch** ODBC 2 中 *.x*驱动程序，可以提取单个行。  
  
 有关详细信息，请参阅[块状游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附录 g:为了向后兼容的驱动程序指南。  
  
## <a name="positioning-the-cursor"></a>将光标置于  
 创建结果集时，游标位于结果集的开始之前。 **SQLFetch**提取下一个行集。 它相当于调用**SQLFetchScroll**与*FetchOrientation*设置为 SQL_FETCH_NEXT。 有关游标的详细信息，请参阅[游标](../../../odbc/reference/develop-app/cursors.md)并[块状游标](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行集中的行数。 如果行集正在通过提取**SQLFetch**重叠的结果集末尾**SQLFetch**返回的部分行集。 也就是说，S + R-1 大于 L，其中，S 起始行的行集提取，R 是行集大小和 L 是最后一个行在结果集中，然后的第一个 L S + 1 行集的行有效。 剩余的行是空并且具有 SQL_ROW_NOROW 的状态。  
  
 之后**SQLFetch**返回当前行是行集的第一行。  
  
 下表中列出的规则描述游标定位调用之后**SQLFetch**根据本部分中的第二个表中列出的条件。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|在开始之前|1|  
|*CurrRowsetStart* \<= *LastResultRow - RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow - RowsetSize*[1]|后端|  
|后端|后端|  
  
 [1] 如果提取行集大小为发生更改，这是用于上次提取的行集大小。  
  
 [2] 如果提取行集大小为发生更改，这是用于新提取的行集大小。  
  
|表示法|含义|  
|--------------|-------------|  
|在开始之前|块游标位于结果集的开始之前。 如果新的行集的第一行是结果集，在开始之前**SQLFetch**返回 sql_no_data 为止。|  
|后端|块游标位于结果的最终集之后。 如果在新行集的第一个行后的结果集末尾**SQLFetch**返回 sql_no_data 为止。|  
|*CurrRowsetStart*|当前行集中的第一个行数。|  
|*LastResultRow*|在结果集中的最后一个行数。|  
|*RowsetSize*|行集大小。|  
  
 例如，假设一个结果集具有 100 行和行集大小为 5。 下表显示了返回的行集和返回代码**SQLFetch**为不同的起始位置。  
  
|当前行集|返回代码|新行集。|提取的行数|  
|--------------------|-----------------|----------------|------------------------|  
|在开始之前|SQL_SUCCESS|1 到 5|5|  
|1 到 5|SQL_SUCCESS|6 到 10|5|  
|52 到 56|SQL_SUCCESS|57 到 61|5|  
|91 到 95|SQL_SUCCESS|96 到 100|5|  
|93 到 97|SQL_SUCCESS|98 到 100。 行 4 和 5 行状态数组都设置为 SQL_ROW_NOROW。|3|  
|96 到 100|SQL_NO_DATA|无。|0|  
|99 到 100|SQL_NO_DATA|无。|0|  
|后端|SQL_NO_DATA|无。|0|  
  
## <a name="returning-data-in-bound-columns"></a>在绑定列中返回数据  
 作为**SQLFetch**返回每个行中，它将每个绑定列的数据放入缓冲区绑定到该列。 如果绑定没有列， **SQLFetch**不返回任何数据，但 does 向前移动块游标。 仍可以通过使用检索的数据**SQLGetData**。 如果游标是多行的游标 （即，SQL_ATTR_ROW_ARRAY_SIZE 大于 1）， **SQLGetData** SQL_GD_BLOCK 返回时，才可以调用**SQLGetInfo**使用调用*信息类型*SQL_GETDATA_EXTENSIONS。 (有关详细信息，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。)  
  
 为某行中，每个绑定列**SQLFetch**执行以下操作：  
  
1.  长度/指示器缓冲区设置为 SQL_NULL_DATA 并继续执行下一列的数据是否为 NULL。 如果数据为 NULL，并且没有长度/指示器缓冲区已绑定， **SQLFetch**行返回 SQLSTATE 22002 （指示器变量，但未提供），并将继续到下一行。 有关如何确定长度/指示器缓冲区的地址信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
     如果列的数据不为 NULL， **SQLFetch**继续到步骤 2。  
  
2.  如果 SQL_ATTR_MAX_LENGTH 语句属性设置为非零值且列包含字符或二进制数据，数据被截断为 SQL_ATTR_MAX_LENGTH 字节。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 语句属性旨在减少网络流量。 它通常被实现数据源，返回之前对其通过网络将截断数据。 驱动程序和数据源不需要支持它。 因此，若要确保数据将被截断为特定大小，应用程序应分配该大小的缓冲区，并指定的大小以*cbValueMax*中的参数**SQLBindCol**。  
  
3.  将数据转换为指定的类型*TargetType*中**SQLBindCol**。  
  
4.  如果数据已转换为可变长度数据类型，如字符或二进制文件中， **SQLFetch**检查数据的长度是否超过数据缓冲区的长度。 如果字符数据 （包括 null 终止字符） 的长度超过了数据缓冲区的长度**SQLFetch**将截断到的 null 终止字符的长度小于数据缓冲区的长度的数据。 它然后则以 null 终止的数据。 如果二进制数据的长度超过了数据缓冲区的长度**SQLFetch**截断到数据缓冲区的长度。 使用指定数据缓冲区的长度*BufferLength*中**SQLBindCol**。  
  
     **SQLFetch**永远不会截断数据转换为固定长度的数据类型; 它始终假定数据缓冲区的长度是数据类型的大小。  
  
5.  将已转换 （和可能被截断） 数据放入的数据缓冲区。 有关如何确定数据缓冲区的地址信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
6.  将长度/指示器缓冲区中数据的长度。 如果指示器指针和长度指针已设置为同一缓冲区 (与调用**SQLBindCol** does)、 长度为有效的数据缓冲区中写入和 NULL 数据的缓冲区中写入 SQL_NULL_DATA。 如果没有长度/指示器缓冲区已绑定，则**SQLFetch**不返回长度。  
  
    -   对于字符或二进制数据，这是数据的长度之后转换和截断之前由于数据缓冲区过小。 如果驱动程序无法转换后，确定数据的长度，因为有时是带有长数据的用例，但它会将长度设置为 SQL_NO_TOTAL。 如果数据已被截断由于 SQL_ATTR_MAX_LENGTH 语句属性，此属性的值放入而不是实际长度的长度/指示器缓冲区。 这是因为此属性设计要截断的转换之前, 在服务器上的数据，以便该驱动程序有无法找出实际长度。  
  
    -   对于所有其他数据类型，这是数据的长度后转换，则也就是说，它是类型的到转换数据的大小。  
  
     有关如何确定长度/指示器缓冲区的地址信息，请参阅"缓冲区的地址"中[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
7.  如果数据被截断的有效数字不会丢失任何转换过程 （例如，其实数 1.234 被截断为整数 1 转换时）， **SQLFetch**返回 SQLSTATE 01S07 （小数部分截断） 和 SQL_SUCCESS_WITH_INFO。 如果数据被截断，因为数据缓冲区长度太小 （例如，字符串"abcdef"放在 4 字节缓冲区）， **SQLFetch**返回 SQLSTATE 01004 （数据被截断） 和 SQL_SUCCESS_WITH_INFO。 如果数据由于 SQL_ATTR_MAX_LENGTH 语句属性，而被截断**SQLFetch**返回 SQL_SUCCESS，且不返回 SQLSTATE 01S07 （小数部分截断） 或 SQLSTATE 01004 （数据被截断）。 如果数据丢失的有效位数 （例如，如果已将一个 SQL_INTEGER 值大于 100000 转换为 SQL_C_TINYINT），转换过程将被截断**SQLFetch**返回 SQLSTATE 22003 （数值超出范围）和 （如果行集大小为 1） 的 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO （如果行集大小大于 1）。  
  
 如果绑定的数据缓冲区和长度/指示器缓冲区的内容是不确定**SQLFetch**或**SQLFetchScroll**不会返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组用于在行集中返回每行的状态。 此数组的地址是使用 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的。 数组由应用程序分配，并且必须由 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的所有元素。 设置其值**SQLFetch**， **SQLFetchScroll**，并**SQLBulkOperations**或**SQLSetPos** （除非它们已被调用时通过定位游标完后**SQLExtendedFetch**)。 如果将 SQL_ATTR_ROW_STATUS_PTR 语句属性的值为 null 指针，这些函数不会返回行状态。  
  
 行状态数组缓冲区的内容是不确定，如果**SQLFetch**或**SQLFetchScroll**不会返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 行状态数组中返回以下值。  
  
|行状态数组值|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行已成功提取和上一次提取此结果集从之后未发生更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|行已成功提取和上一次提取此结果集从之后未发生更改。 但是，有关行返回一条警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED [1]，[2] 和 [3]|行成功读取，并且此结果集从上次提取后已更改。 如果此结果集从再次提取或刷新的行**SQLSetPos**，状态更改为行的新状态。|  
|SQL_ROW_DELETED[3]|已删除行，因为它上次提取此结果集中。|  
|SQL_ROW_ADDED[4]|通过插入行**SQLBulkOperations**。 如果此结果集从再次提取或刷新的行**SQLSetPos**，其状态是 SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|行集重叠的结果集的末尾并不返回任何行时，对应于此元素的行状态数组。|  
  
 [1] 的由键集游标混合和动态游标，如果更新密钥的值时，数据行被视为已被删除，并添加一个新行。  
  
 [2] 某些驱动程序无法检测到对数据的更新，因此不能返回此值。 若要确定驱动程序是否可以检测到 refetched 行的更新，应用程序调用**SQLGetInfo** SQL_ROW_UPDATES 选项。  
  
 [3] **SQLFetch**可以返回此值仅是混合在一起调用**SQLFetchScroll**。 这是因为**SQLFetch**通过结果集的发展，以独占方式使用它时，不会不重新提取所有行。 不 refetched 任何行，因为**SQLFetch**不会检测到以前提取行所做的更改。 但是，如果**SQLFetchScroll**任何事先提取行之前，将光标置于和**SQLFetch**用于提取这些行**SQLFetch**可以检测到任何更改这些行。  
  
 [4] 仅返回由 SQLBulkOperations。 未设置**SQLFetch**或**SQLFetchScroll**。  
  
### <a name="rows-fetched-buffer"></a>提取的行的缓冲区  
 提取缓冲区行用于返回提取，其中包括那些为其，因为它们正在提取出错未返回任何数据的行的行数。 换而言之，它是为其行状态数组中的值不是 SQL_ROW_NOROW 的行数。 将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性与指定此缓冲区的地址。 由应用程序分配缓冲区。 设置**SQLFetch**并**SQLFetchScroll**。 如果将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值为 null 指针，这些函数不返回提取的行数。 若要确定结果集中的当前行数，应用程序可以调用**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 属性。  
  
 提取行缓冲区的内容是不确定，如果**SQLFetch**或**SQLFetchScroll**除时返回 SQL_NO_DATA，在这种情况下未返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，在提取缓冲区行中的值设置为 0。  
  
### <a name="error-handling"></a>错误处理  
 错误和警告可以应用于整个函数或对单个行。 有关诊断记录的详细信息，请参阅[诊断](../../../odbc/reference/develop-app/diagnostics.md)并[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>错误和警告在整个函数  
 如果错误适用于整个函数，如 SQLSTATE HYT00 （超时已过期） 或 SQLSTATE 24000 （无效的游标状态）， **SQLFetch**返回 SQL_ERROR 和适用的 SQLSTATE。 未定义行集缓冲区的内容和光标位置保持不变。  
  
 警告将应用于整个函数，如果**SQLFetch**返回 SQL_SUCCESS_WITH_INFO 和适用的 SQLSTATE。 将应用于整个函数的警告的状态记录返回之前应用于单个行的状态记录。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>错误和警告中单个行  
 如果出现错误 （例如 SQLSTATE 22012 （被零除）) 或 （如 SQLSTATE 01004 （数据被截断）) 警告适用于单个行**SQLFetch**执行以下操作：  
  
-   设置的相应元素的行状态数组到 SQL_ROW_ERROR 错误或 SQL_ROW_SUCCESS_WITH_INFO 的警告。  
  
-   添加包含 SQLSTATEs 错误或警告的零个或多个状态记录。  
  
-   状态记录中设置行和列的数字字段。 如果**SQLFetch**无法确定一个行或列的数字，将该编号设置为 SQL_ROW_NUMBER_UNKNOWN 或 SQL_COLUMN_NUMBER_UNKNOWN，分别。 状态记录不适用于特定的列，如果**SQLFetch** SQL_NO_COLUMN_NUMBER 到设置的列号。  
  
 **SQLFetch**继续提取行，直到它已提取的行集中的所有行。 除非在这种情况下它将返回 SQL_ERROR （不包括状态 SQL_ROW_NOROW 的行） 的行集，每行中发生错误，否则它将返回 SQL_SUCCESS_WITH_INFO。 具体而言，如果行集大小为 1，在该行中，就会出错**SQLFetch**返回 SQL_ERROR。  
  
 **SQLFetch**按行号顺序返回状态记录。 也就是说，它返回所有状态记录为未知的行 （如果有）;接下来，它返回的第一行 （如果有），所有状态记录，然后都返回所有状态记录 （如果有） 的第二行，等等。 每个行的状态记录按常规的规则来排序状态记录;详细信息，请参阅"序列的状态记录"中[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
### <a name="descriptors-and-sqlfetch"></a>描述符和 SQLFetch  
 以下各节介绍如何**SQLFetch**与描述符进行交互。  
  
#### <a name="argument-mappings"></a>参数映射  
 该驱动程序不会设置的参数的任何描述符字段**SQLFetch**。  
  
#### <a name="other-descriptor-fields"></a>其他的描述符字段  
 使用以下的描述符字段**SQLFetch**。  
  
|描述符字段|Desc。|中的字段|通过设置|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|标头|SQL_ATTR_ROW_ARRAY_SIZE statement attribute|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|标头|SQL_ATTR_ROW_STATUS_PTR 语句属性|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|标头|SQL_ATTR_ROW_BIND_OFFSET_PTR statement attribute|  
|SQL_DESC_BIND_TYPE|ARD|标头|SQL_ATTR_ROW_BIND_TYPE statement attribute|  
|SQL_DESC_COUNT|ARD|标头|*ColumnNumber*自变量的**SQLBindCol**|  
|SQL_DESC_DATA_PTR|ARD|记录|*TargetValuePtr*自变量的**SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|ARD|记录|*StrLen_or_IndPtr*中的参数**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|ARD|记录|*BufferLength*中的参数**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|记录|*StrLen_or_IndPtr*中的参数**SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|标头|SQL_ATTR_ROWS_FETCHED_PTR 语句属性|  
|SQL_DESC_TYPE|ARD|记录|*TargetType*中的参数**SQLBindCol**|  
  
 此外可以通过设置所有描述符字段**SQLSetDescField**。  
  
#### <a name="separate-length-and-indicator-buffers"></a>不同长度和指示器缓冲区  
 应用程序可以绑定一个缓冲区或可用于保存长度和指示器值的两个单独缓冲区。 当应用程序调用**SQLBindCol**，驱动程序将 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 字段设置为相同的地址，在传递*StrLen_or_IndPtr*自变量。 当应用程序调用**SQLSetDescField**或**SQLSetDescRec**，它可以将这两个字段设置为不同的地址。  
  
 **SQLFetch**确定应用程序是否具有指定单独的长度和指示器缓冲区。 在这种情况下，数据不为 NULL，当**SQLFetch**指示器缓冲区设置为 0，并在长度的缓冲区中返回长度。 当数据为 NULL， **SQLFetch**指示器缓冲区设置为 SQL_NULL_DATA，而不修改长度缓冲区。  
  
### <a name="code-example"></a>代码示例  
 请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，以及[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)。  
  
### <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|关闭游标语句|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在提取部分或全部的数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回数的结果集列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
