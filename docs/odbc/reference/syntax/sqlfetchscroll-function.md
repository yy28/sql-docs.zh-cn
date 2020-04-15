---
title: SQLFetchScroll 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285877"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll Function（SQLFetchScroll 函数）
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFetchScroll**从结果集中获取指定的数据行集，并返回所有绑定列的数据。 行集可以在绝对或相对位置或通过书签指定。  
  
 使用 ODBC 2.x 驱动程序时，驱动程序管理器将此函数映射到**SQLExtendedFetch**。 有关详细信息，请参阅[映射应用程序向后兼容性的替代函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *提取方向*  
 [输入]  
  
 提取类型：  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 有关详细信息，请参阅"注释"部分中的"定位光标"。  
  
 *提取偏移*  
 [输入]  
  
 要提取的行数。 此参数的解释取决于*Fetch 方向*参数的值。 有关详细信息，请参阅"注释"部分中的"定位光标"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetchScroll**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的句柄类型和语句句柄。 下表列出了**SQLFetchScroll**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。 如果单个列上发生错误，可以使用 SQL_DIAG_COLUMN_NUMBER的 Diag标识符调用**SQLGetDiagField**以确定错误发生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER的 Diag标识符调用，以确定包含该列的行。  
  
 对于可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT（01xxx SQLSTATEs 除外），如果多行操作的一个或多个行发生错误（但不是全部）发生错误，则返回SQL_SUCCESS_WITH_INFO，如果单行操作发生错误，则返回SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|为列返回的字符串或二进制数据导致非空白字符或非 NULL 二进制数据的截断。 如果它是一个字符串值，它是右截断的。|  
|01S01|行中的错误|获取一个或多个行时出错。<br /><br /> （如果在 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序时返回此 SQLSTATE，则可以忽略它。|  
|01S06|尝试在结果集返回第一个行集之前提取|请求的行集与提取方向时的结果集的开始重叠，当 Fetch 方向SQL_FETCH_PRIOR，当前位置超过第一行，并且当前行的数量小于或等于行集大小。<br /><br /> 请求的行集与结果集的开始重叠，当 Fetch方向SQL_FETCH_PRIOR，当前位置超出结果集的末尾，并且行集大小大于结果集大小。<br /><br /> 请求的行集与结果集的开始重叠，当 Fetch 方向SQL_FETCH_RELATIVE时，FetchOffset 为负值，FetchOffset 的绝对值小于或等于行集大小。<br /><br /> 请求的行集与提取方向 SQL_FETCH_ABSOLUTE时的结果集的开始重叠，FetchOffset 为负，FetchOffset 的绝对值大于结果集大小，但小于或等于行集大小。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分数截断|为列返回的数据被截断。 对于数字数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|无法将结果集中列的数据值转换为**SQLBindCol**中*TargetType*指定的数据类型。<br /><br /> 列 0 与SQL_C_BOOKMARK数据类型绑定，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE。<br /><br /> 列 0 与数据类型SQL_C_VARBOOKMARK绑定，并且SQL_ATTR_USE_BOOKMARKS语句属性未设置为SQL_UB_VARIABLE。|  
|07009|无效描述符索引|驱动程序是不支持**SQLExtendedFetch**的 ODBC 2 *.x*驱动程序，在列绑定中指定的列编号为 0。<br /><br /> 列 0 已绑定，SQL_ATTR_USE_BOOKMARKS 语句属性设置为SQL_UB_OFF。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22001|字符串数据，右截断|为列返回的可变长度书签被截断。|  
|22002|需要指标变量，但未提供|NULL 数据被提取到一个列*中，* 该列StrLen_or_IndPtr由**SQLBindCol**设置（或由**SQLSetDescField**或**SQLSetDescRec**设置SQL_DESC_INDICATOR_PTR）为空指针。|  
|22003|数值超范围|返回一个或多个绑定列的数值（作为数字或字符串）将导致数字的整个部分（而不是小数）被截断。<br /><br /> 有关详细信息，请参阅[在附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)中[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。|  
|22007|无效日期时间格式|结果集中的字符列绑定到日期、时间或时间戳 C 结构，并且列中的值分别是无效的日期、时间或时间戳。|  
|22012|除零|返回算术表达式中的值，结果除以零。|  
|22015|间隔字段溢出|从精确数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> 将数据提取到间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。|  
|22018|强制转换规范的无效字符值|结果集中的字符列绑定到字符 C 缓冲区，该列包含缓冲区的字符集中没有表示的字符。<br /><br /> C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。|  
|24000|无效的游标状态|*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。|  
|40001|序列化失败|执行提取的事务已终止，以防止死锁。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLFetchScroll**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） **SQLFetch**在调用**SQLExtendedFetch**后和在使用SQL_CLOSE选项的**SQLFreeStmt**之前调用了*语句处理*。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|SQL_ATTR_USE_BOOKMARK语句属性设置为SQL_UB_VARIABLE，第 0 列绑定到长度不等于此结果集书签的最大长度的缓冲区。 （此长度在 IRD 的SQL_DESC_OCTET_LENGTH字段中可用，可以通过调用**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**获得。 **SQLColAttribute**|  
|HY106|提取类型范围外|DM） 为参数 Fetch 方向指定的值无效。<br /><br /> （DM） 参数 Fetch 方向SQL_FETCH_BOOKMARK，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE语句属性的值SQL_CURSOR_FORWARD_ONLY，并且参数 Fetch 方向的值不SQL_FETCH_NEXT。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE语句属性的值是SQL_NONSCROLLABLE，并且参数 Fetch 方向的值不SQL_FETCH_NEXT。|  
|HY107|行值范围外|使用SQL_ATTR_CURSOR_TYPE语句属性指定的值SQL_CURSOR_KEYSET_DRIVEN，但使用SQL_ATTR_KEYSET_SIZE语句属性指定的值大于 0，小于使用SQL_ATTR_ROW_ARRAY_SIZE语句属性指定的值。|  
|HY111|无效书签值|参数 FetchOrientation 是SQL_FETCH_BOOKMARK的，并且SQL_ATTR_FETCH_BOOKMARK_PTR语句属性中的值指向的书签无效或为空指针。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持**SQLBindCol**中的*TargetType*和相应列的 SQL 数据类型的组合指定的转换。|  
|HYT00|超时时间已到|查询超时期限在数据源返回请求的结果集之前已过期。 超时期间通过 SQL_ATTR_QUERY_TIMEOUT 的 SQLSetStmtAttr 设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **SQLFetchScroll**从结果集中返回指定的行集。 行集可以由绝对或相对位置或书签指定。 **SQLFetchScroll**只能在存在结果集时调用 ，即在创建结果集的调用之后以及该结果集上的游标关闭之前。 如果绑定任何列，它将返回这些列中的数据。 如果应用程序指定了指向行状态数组的指针或用于返回提取的行数的缓冲区 **，SQLFetchScroll**也返回此信息。 对**SQLFetchScroll 的**调用可以与**SQLFetch**的调用混合，但不能与**SQLAaFetch 的**调用混合。  
  
 有关详细信息，请参阅[使用块光标](../../../odbc/reference/develop-app/using-block-cursors.md)[和使用可滚动光标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>定位光标  
 创建结果集时，光标位于结果集开始之前。 **SQLFetchScroll**基于 *"取取方向"* 和"*提取偏移*"参数的值定位块游标，如下表所示。 确定新行集开始的确切规则将显示在下一节中。  
  
|提取方向|含义|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|返回下一个行集。 这相当于调用**SQLFetch。**<br /><br /> **SQLFetchScroll**忽略*取取偏移*的值。|  
|SQL_FETCH_PRIOR|返回以前的行集。<br /><br /> **SQLFetchScroll**忽略*取取偏移*的值。|  
|SQL_FETCH_RELATIVE|从当前行集的开头返回行集 *"提取偏移*"。|  
|SQL_FETCH_ABSOLUTE|返回从行*提取偏移*开始的行集。|  
|SQL_FETCH_FIRST|返回结果集中的第一个行集。<br /><br /> **SQLFetchScroll**忽略*取取偏移*的值。|  
|SQL_FETCH_LAST|返回结果集中的最后一个完整行集。<br /><br /> **SQLFetchScroll**忽略*取取偏移*的值。|  
|SQL_FETCH_BOOKMARK|从SQL_ATTR_FETCH_BOOKMARK_PTR语句属性指定的书签返回行集 FetchOffset 行。|  
  
 驱动程序不需要支持所有提取方向;应用程序调用**SQLGetInfo**的信息类型为 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或SQL_STATIC_CURSOR_ATTRIBUTES1（取决于游标的类型），以确定驱动程序支持哪些提取方向。 应用程序应查看这些信息类型中SQL_CA1_NEXT、SQL_CA1_RELATIVE、SQL_CA1_ABSOLUTE和WQL_CA1_BOOKMARK位掩码。 此外，如果游标是仅转发的，并且取取方向不是**SQL_FETCH_NEXT，SQLFetchScroll**将返回 SQLSTATE HY106（提取类型不在范围）。  
  
 SQL_ATTR_ROW_ARRAY_SIZE语句属性指定行集中的行数。 如果**SQLFetchScroll**提取的行集与结果集的末尾重叠，则**SQLFetchScroll**返回一个部分行集。 也就是说，如果 S + R - 1 大于 L，其中 S 是要提取的行集的起始行，R 是行集大小，而 L 是结果集中的最后一行，则只有排集的前一行 L - S = 1 行有效。 其余行为空，状态为 SQL_ROW_NOROW。  
  
 **SQLFetchScroll**返回后，当前行是行集的第一行。  
  
## <a name="cursor-positioning-rules"></a>光标定位规则  
 以下各节介绍取取方向的每个值的确切规则。 这些规则使用以下表示法。  
  
|表示法|含义|  
|--------------|-------------|  
|*开始之前*|块游标位于结果集开始之前。 如果新行集的第一行位于结果集开始之前，**则 SQLFetchScroll**返回SQL_NO_DATA。|  
|*结束后*|块游标位于结果集结束之后。 如果新行集的第一行位于结果集结束后，**则 SQLFetchScroll**返回SQL_NO_DATA。|  
|*CurrRowset 开始*|当前行集中的第一行的编号。|  
|*最后一个结果行*|结果集中的最后一行的编号。|  
|*行集大小*|行集大小。|  
|*提取偏移*|*提取偏移*参数的值。|  
|*书签行*|与SQL_ATTR_FETCH_BOOKMARK_PTR语句属性指定的书签对应的行。|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*开始之前*|1|  
|*CurrRowset 开始 = 行集大小*[1] * \<= 最后一个结果行*|*CurrRowset 开始 = 行集大小*[1]|  
|*CurrRowset 开始 = 行集大小*[1]*>最后结果行*|*结束后*|  
|*结束后*|*结束后*|  
  
 {1} 如果自上次调用以提取行以来，行集大小已更改，则这是与上一个调用一起使用的行集大小。  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*开始之前*|*开始之前*|  
|*CurrRowset 开始 = 1*|*开始之前*|  
|*1 < CurrRowset 开始<= 行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowset 开始>行集大小* <sup>[2]</sup>|*CurrRowset 开始 - 行集大小* <sup>[2]</sup>|  
|*结束后和最后一个结果行<行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*结束和最后的结果行>= 行集大小* <sup>[2]</sup>|*上一个结果行 - 行集大小 = 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06（尝试在结果集返回第一个行集之前提取）和SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次调用以提取行以来，行集大小已更改，则这是新的行集大小。  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*（启动前和提取偏移> 0）OR（结束后和提取偏移< 0）*|*--*<sup>[1]</sup>|  
|*启动和提取偏移<= 0*|*开始之前*|  
|*CurrRowset 开始 = 1 和提取偏移量< 0*|*开始之前*|  
|*currRowset 开始> 1 和 Currrowset 开始 = 提取偏移< 1 和&#124;提取偏移量 &#124; > 行集大小* <sup>[3]</sup>|*开始之前*|  
|*currRowset 开始> 1 和 Currrowset 开始 = 提取偏移< 1 和&#124;提取偏移 &#124; <= 行集大小* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowset\<开始 = 提取偏移量 = 上次结果行*|*CurrRowset 开始 + 提取偏移*|  
|*CurrRowset 开始 = 提取偏移>最后结果行*|*结束后*|  
|*结束后和提取偏移量>= 0*|*结束后*|  
  
 [1] ***SQLFetchScroll***返回相同的行集，就好像它被调用时，Fetch方向设置为SQL_FETCH_ABSOLUTE。 有关详细信息，请参阅"SQL_FETCH_ABSOLUTE"部分。  
  
 [2] **SQLFetchScroll**返回 SQLSTATE 01S06（尝试在结果集返回第一个行集之前提取）和SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果自上次调用以提取行以来，行集大小已更改，则这是新的行集大小。  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*提取偏移量< 0 和&#124;提取偏移量 &#124; <= 上一个结果行*|*上一个结果行 = 取取偏移量 = 1*|  
|*提取偏移< 0 和 &#124; 提取偏移量 &#124; > 上一个结果行和&#124;提取偏移量 &#124; > 行集大小* <sup>[2]</sup>|*开始之前*|  
|*提取偏移< 0 和&#124;提取偏移量 &#124; > 最后结果行和&#124;提取偏移量 &#124; <= 行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*提取偏移量 = 0*|*开始之前*|  
|*1 <=\<取取偏移 = 上次结果行*|*提取偏移*|  
|*提取偏移>最后一个结果行*|*结束后*|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06（尝试在结果集返回第一个行集之前提取）和SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次调用以提取行以来，行集大小已更改，则这是新的行集大小。  
  
 对动态游标执行的绝对提取无法提供所需的结果，因为动态游标中的行位置尚未确定。 此类操作等效于先提取，后跟提取相对;它不是原子操作，静态游标上的绝对提取也是原子操作。  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*行集大小* <sup>[1]</sup> <= 上次结果行|*上次结果行 - 行集大小 = 1* <sup>[1]</sup>|  
|*行集大小* <sup>[1]</sup> >最后一个结果行|*1*|  
  
 [1] 如果自上次调用以提取行以来已更改行集大小，则这是新的行集大小。  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 以下规则适用。  
  
|条件|新行集的第一行|  
|---------------|-----------------------------|  
|*书签行 = 取取偏移< 1*|*开始之前*|  
|*1<= 书签行 =\<取取偏移量 = 上一个结果行*|*书签行 = 取取偏移*|  
|*书签行 = 提取偏移>最后结果行*|*结束后*|  
  
 有关书签的信息，请参阅书签[（ODBC）。](../../../odbc/reference/develop-app/bookmarks-odbc.md)  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>删除、添加和错误行对光标移动的影响  
 静态和键集驱动的游标有时检测添加到结果集的行，并删除从结果集中删除的行。 通过使用SQL_STATIC_CURSOR_ATTRIBUTES2和SQL_KEYSET_CURSOR_ATTRIBUTES2选项调用**SQLGetInfo**并查看SQL_CA2_SENSITIVITY_ADDITIONS、SQL_CA2_SENSITIVITY_DELETIONS和SQL_CA2_SENSITIVITY_UPDATES位掩码，应用程序确定由特定驱动程序实现的游标是否执行此操作。 对于可以检测已删除行并删除行的驱动程序，以下段落将描述此行为的效果。 对于可以检测已删除行但无法删除行的驱动程序，删除对游标移动没有影响，并且以下段落不适用。  
  
 如果游标检测到添加到结果集的行或删除从结果集中删除的行，则它看起来好像仅在获取数据时检测到这些更改。 这包括将**SQLFetchScroll**调用时，提取方向设置为SQL_FETCH_RELATIVE，FetchOffset 设置为 0 以重新提取相同的行集，但不包括在使用 fOption 设置为 SQL_REFRESH时调用 SQLSetPos 的情况。 在后一种情况下，将刷新行集缓冲区中的数据，但不会重新提取，并且不会从结果集中删除已删除的行。 因此，当从当前行集中删除行或插入到当前行集时，游标不会修改行集缓冲区。 相反，当它获取以前包含已删除行或现在包含插入的行的任何行集时，它会检测到更改。  
  
 例如：  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 当**SQLFetchScroll**返回具有相对于当前行集的位置的新行集时（即 Fetch方向是SQL_FETCH_NEXT、SQL_FETCH_PRIOR或SQL_FETCH_RELATIVE - 在计算新行集的起始位置时，它不包括对当前行集的更改。 但是，如果能够检测到当前行集之外的更改，它确实包括更改。 此外，当**SQLFetchScroll**返回具有独立于当前行集的位置的新行集时（即 Fetch方向是SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE或SQL_FETCH_BOOKMARK - 它包括它能够检测到的所有更改，即使这些更改位于当前行集中。  
  
 在确定新添加的行是在当前行集内部还是外部时，部分行集被视为在最后一个有效行结束;即行状态未SQL_ROW_NOROW的最后一行。 例如，假设游标能够检测新添加的行，当前行集是部分行集，应用程序添加新行，游标将这些行添加到结果集的末尾。 如果应用程序调用**SQLFetchScroll，** 提取方向设置为**SQL_FETCH_NEXT，SQLFetchScroll**将返回从第一个新添加的行开始的行集。  
  
 例如，假设当前行集包含第 21 行到 30 行，行集大小为 10，游标删除从结果集中删除的行，并且游标检测添加到结果集的行。 下表显示了**SQLFetchScroll**在各种情况下返回的行。  
  
|更改|提取类型|提取偏移|新排集[1]|  
|------------|----------------|-----------------|---------------------|  
|删除行 21|NEXT|0|31 到 40|  
|删除行 31|NEXT|0|32 到 41|  
|在第 21 行和第 22 行之间插入行|NEXT|0|31 到 40|  
|在第 30 行和第 31 行之间插入行|NEXT|0|插入行，31 到 39|  
|删除行 21|PRIOR|0|11 到 20|  
|删除行 20|PRIOR|0|10 到 19|  
|在第 21 行和第 22 行之间插入行|PRIOR|0|11 到 20|  
|在第 20 行和第 21 行之间插入行|PRIOR|0|12 到 20，插入的行|  
|删除行 21|RELATIVE|0|22 到 31<sup>[2]</sup>|  
|删除行 21|RELATIVE|1|22 到 31|  
|在第 21 行和第 22 行之间插入行|RELATIVE|0|21，插入行，22 到 29|  
|在第 21 行和第 22 行之间插入行|RELATIVE|1|22 到 31|  
|删除行 21|ABSOLUTE|21|22 到 31<sup>[2]</sup>|  
|删除行 22|ABSOLUTE|21|21， 23 到 31|  
|在第 21 行和第 22 行之间插入行|ABSOLUTE|22|插入的行，22 到 29|  
  
 [1] 在插入或删除任何行之前，此列使用行号。  
  
 [2] 在这种情况下，游标尝试返回以第 21 行开头的行。 由于第 21 行已被删除，因此返回的第一行是第 22 行。  
  
 错误行（即状态为SQL_ROW_ERROR的行）不会影响光标移动。 例如，如果当前行集以第 11 行开头，并且第 11 行的状态为SQL_ROW_ERROR，则使用 Fetch方向设置为"取向"设置为"SQL_FETCH_RELATIVE"调用**SQLFetchScroll，** 并将 FetchOffset 设置为 5 返回从第 16 行开始的行集，就像该行 11 的状态SQL_SUCCESS一样。  
  
## <a name="returning-data-in-bound-columns"></a>在绑定列中返回数据  
 **SQLFetchScroll**返回绑定列中的数据的方式与**SQLFetch**相同。 有关详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)中的"在绑定列中返回数据"。  
  
 如果未绑定列 **，SQLFetchScroll**不会返回数据，但会将块游标移动到指定位置。 能否使用**SQLGetData**从块游标的未绑定列中检索数据取决于驱动程序。 如果调用**SQLGetInfo**返回SQL_GETDATA_EXTENSIONS信息类型的SQL_GD_BLOCK位，则支持此功能。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 **SQLFetchScroll**使用相同的公式来确定数据和长度/指标缓冲区的地址与**SQLFetch。** 有关详细信息，请参阅[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"缓冲区地址"。  
  
## <a name="row-status-array"></a>行状态数组  
 **SQLFetchScroll**以与 SQLFetch 相同的方式设置行状态数组中的值。 有关详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)中的"行状态数组"。  
  
## <a name="rows-fetched-buffer"></a>行提取缓冲区  
 **SQLFetchScroll**返回行提取缓冲区中的行数，其方式与**SQLFetch**相同。 有关详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)中的"行提取缓冲区"。  
  
## <a name="error-handling"></a>错误处理  
 当应用程序在 ODBC 3.x 驱动程序中调用**SQLFetchScroll**时，驱动程序管理器在驱动程序中调用**SQLFetchScroll。** 当应用程序在 ODBC 2.x 驱动程序中调用**SQLFetchScroll**时，驱动程序管理器在驱动程序中调用 SQLExtendedFetch。 由于**SQLFetchScroll**和 SQLAaFetch 处理错误的方式略有不同，因此应用程序在 ODBC 2.x 和 ODBC 3.x 驱动程序中调用**SQLFetchScroll**时，会看到略有不同的错误行为。  
  
 **SQLFetchScroll**以与**SQLFetch**相同的方式返回错误和警告。有关详细信息，请参阅**SQLFetch**中的"错误处理"。 **SQLExtendedFetch**返回错误的方式与**SQLFetch**相同，但有以下例外情况：  
  
 当发生适用于行集中特定行的警告时，SQLExtendedFetch 将行状态数组中的相应条目设置为SQL_ROW_SUCCESS，而不是SQL_ROW_SUCCESS_WITH_INFO。  
  
 如果行集中的每一行都出现错误，SQLExtendedFetch 将返回SQL_SUCCESS_WITH_INFO，而不是SQL_ERROR。  
  
 在应用于单个行的每个状态记录中，SQLExtendedFetch 返回的第一个状态记录必须包含 SQLSTATE 01S01（行中的错误）;**SQLFetchScroll**不会返回此 SQLSTATE。 如果 SQL 扩展获取无法返回其他 SQLSTATEs，它仍必须返回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和乐观并发  
 如果游标使用乐观并发 （即SQL_ATTR_CONCURRENCY 语句属性的值为 SQL_CONCUR_VALUES 或SQL_CONCUR_ROWVER - **SQLFetchScroll**更新数据源用于检测行是否已更改的乐观并发值。 每当**SQLFetchScroll**获取新的行集时（包括重新提取当前行集时），就会发生这种情况。 （调用它，提取方向设置为SQL_FETCH_RELATIVE和提取偏移设置为 0。  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驱动程序  
 当应用程序在 ODBC 2.x 驱动程序中调用**SQLFetchScroll**时，驱动程序管理器将此调用映射到**SQL 扩展获取**。 它传递 SQL**扩展提取**参数的以下值。  
  
|SQL 扩展获取参数|“值”|  
|-------------------------------|-----------|  
|语句句柄|语句处理在**SQLFetchScroll**中。|  
|提取方向|在**SQLFetchScroll**中获取方向。|  
|提取偏移|如果未SQL_FETCH_BOOKMARK取取方向，则使用**SQLFetchScroll**中提取偏移参数的值。<br /><br /> 如果fetch方向SQL_FETCH_BOOKMARK，则使用存储在SQL_ATTR_FETCH_BOOKMARK_PTR语句属性指定的地址中的值。|  
|罗CountPtr|SQL_ATTR_ROWS_FETCHED_PTR 语句属性指定的地址。|  
|行状态数组|由SQL_ATTR_ROW_STATUS_PTR语句属性指定的地址。|  
  
 有关详细信息，请参阅附录 G 中的[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)：向后兼容性的驱动程序指南。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述符和 SQLFetchScroll  
 **SQLFetchScroll**以与**SQLFetch**相同的方式与描述符进行交互。 有关详细信息，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)中的"描述符和 SQLFetchScroll"部分。  
  
## <a name="code-example"></a>代码示例  
 请参阅[列-Wise 绑定](../../../odbc/reference/develop-app/column-wise-binding.md)、[行-Wise 绑定](../../../odbc/reference/develop-app/row-wise-binding.md)、[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)，以及[使用 SQLSetPos 在行集中更新行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行批量插入、更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|关闭语句上的光标|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回结果集列数|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位光标、刷新行集中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
