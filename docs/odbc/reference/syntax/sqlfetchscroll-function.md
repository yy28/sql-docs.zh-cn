---
title: SQLFetchScroll 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 439639255cc41fc22f94c5a1605dee8fc68a06ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923302"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll Function（SQLFetchScroll 函数）
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFetchScroll**从结果集中提取数据的指定行集，并返回所有绑定的列的数据。 绝对或相对位置或书签，可以指定行集。  
  
 驱动程序管理器时使用 ODBC 2.x 驱动程序时，将此函数可对映射**SQLExtendedFetch**。 有关详细信息，请参阅[映射用于向后兼容性的应用程序的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *FetchOrientation*  
 [输入]  
  
 提取的类型：  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 有关详细信息，请参阅"备注"部分中的"定位光标"。  
  
 *FetchOffset*  
 [输入]  
  
 要读取的行数。 此自变量的解释依赖于的值*FetchOrientation*自变量。 有关详细信息，请参阅"备注"部分中的"定位光标"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetchScroll**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec** SQL_HANDLE_STMT HandleType 与的句柄StatementHandle。 下表列出了通常返回的 SQLSTATE 值**SQLFetchScroll**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。 如果上一个列中，发生错误时**SQLGetDiagField**可以用 DiagIdentifier 的 SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 列调用和**SQLGetDiagField**可以调用与 DiagIdentifier 的 SQL_DIAG_ROW_NUMBER 以确定包含该列的行。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除外 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果将上一个或多个，但并非所有行的一个多行的操作，发生错误时，如果上发生错误时返回 SQL_ERROR单行更行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制数据的列返回导致非空白字符或非 NULL 二进制数据截断。 如果它是一个字符串值，它是右侧被截断。|  
|01S01|行中的错误|提取一个或多个行时出错。<br /><br /> (如果此 SQLSTATE 返回时 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，则可以忽略它。)|  
|01S06|尝试的结果集返回第一个行集之前提取|请求的行集重叠的结果集时 FetchOrientation 为 SQL_FETCH_PRIOR，当前位置已经超出了第一行中，并且当前行数小于或等于行集大小的开始。<br /><br /> 请求的行集重叠的结果集时 FetchOrientation SQL_FETCH_PRIOR、 当前的位置已超出该结果集的末尾，且行集大小为晚于结果集大小的开始。<br /><br /> 请求的行集重叠的结果集时 FetchOrientation 为 SQL_FETCH_RELATIVE，FetchOffset 是一个负数，并且 FetchOffset 绝对值是小于或等于行集大小的开始。<br /><br /> 请求的行集重叠的结果集时 FetchOrientation SQL_FETCH_ABSOLUTE、 FetchOffset 是一个负数，且 FetchOffset 绝对值为晚于结果集大小开始但小于或等于行集大小。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S07|小数部分组成的截断|返回的列的数据被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳，和包含时间组件的 interval 数据类型，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法转换的结果集中的列的数据值，由指定的数据类型为*TargetType*中**SQLBindCol**。<br /><br /> 第 0 列被绑定了一个数据类型为 SQL_C_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_VARIABLE。<br /><br /> 第 0 列被绑定了一个数据类型为 SQL_C_VARBOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性未设置为 SQL_UB_VARIABLE。|  
|07009|无效的描述符索引|该驱动程序是 ODBC 2 *.x*驱动程序不支持**SQLExtendedFetch**，和一个列的绑定中指定某个列号了 0。<br /><br /> 第 0 列被绑定，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22001|字符串数据，右截断|长度可变的书签的列返回被截断。|  
|22002|需要指示器变量，但未提供|NULL 数据提取了的列中其*StrLen_or_IndPtr*设置**SQLBindCol** (或通过设置 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 是空指针。|  
|22003|数值超出范围|为一个或多个绑定列 （为数字或字符串） 返回数字的值可能会导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> 有关详细信息，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|无效的日期时间格式|结果集中的字符列已绑定到日期、 时间或时间戳 C 结构，列中的值，分别无效的日期、 时间戳。|  
|22012|被零除|返回一个值算术表达式中的，这会导致除法被零除。|  
|22015|间隔字段溢出|将从精确数字或间隔 SQL 类型分配给间隔 C 类型由前导字段中的重要数字丢失。<br /><br /> 在提取到间隔 C 类型数据, 时没有间隔 C 类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的的无效字符值|结果集中的字符列已绑定到 C 字符缓冲区，并且列包含没有任何表示形式的缓冲区的字符集的字符。<br /><br /> C 类型已准确或近似数字、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;并且列中的值不是有效的文本的绑定的 C 类型。|  
|24000|无效的游标状态|*StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。|  
|40001|序列化失败|在其中执行提取事务已终止，以防止死锁。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLFetchScroll**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) **SQLFetch**曾为*StatementHandle*后**SQLExtendedFetch**调用和之前**SQLFreeStmt**与 SQL_调用了关闭选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|SQL_ATTR_USE_BOOKMARK 语句属性已设置为 SQL_UB_VARIABLE，并且第 0 列已绑定到其的长度不等于该结果集的书签的最大长度的缓冲区。 (此长度的 IRD SQL_DESC_OCTET_LENGTH 字段中是否可用，并可以通过调用获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY106|提取类型超出了范围|DM) FetchOrientation 的参数指定的值无效。<br /><br /> (DM) 参数 FetchOrientation 为 SQL_FETCH_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE 语句属性的值是 SQL_CURSOR_FORWARD_ONLY 和 FetchOrientation 未 SQL_FETCH_NEXT 的自变量的值。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 语句属性的值是 SQL_NONSCROLLABLE 和 FetchOrientation 未 SQL_FETCH_NEXT 的自变量的值。|  
|HY107|行数值超出范围|指定具有 SQL_ATTR_CURSOR_TYPE 语句属性的值是 SQL_CURSOR_KEYSET_DRIVEN，但具有 SQL_ATTR_KEYSET_SIZE 语句属性指定的值是大于 0 而小于 SQL_ATTR_ROW_ARRAY_ 用指定的值大小语句属性。|  
|HY111|无效的书签值|自变量 FetchOrientation SQL_FETCH_BOOKMARK，并且书签指向 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性中的值无效或是空指针。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过 SQLSetStmtAttr，SQL_ATTR_QUERY_TIMEOUT 设置的超时期限。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLFetchScroll**从结果集中返回指定的行集。 绝对或相对位置或书签，可以指定行集。 **SQLFetchScroll**仅当存在结果集时，可以调用 — 即，调用后创建的结果集并光标结果集的转移已关闭。 如果没有绑定任何列，将在这些列中返回的数据。 如果应用程序指定行状态数组或其返回的行提取，数中的缓冲区的指针**SQLFetchScroll**返回以及此信息。 调用**SQLFetchScroll**可以通过调用混合**SQLFetch**但不能与调用混合**SQLExtendedFetch**。  
  
 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)和[使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>将光标定位  
 创建结果集时，游标位于结果集的开始之前。 **SQLFetchScroll**的值为基础的块光标置于*FetchOrientation*和*FetchOffset*下表中所示的参数。 用于确定新行集的开始的精确规则下一节所示。  
  
|FetchOrientation|含义|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|返回下一步的行集。 这是等效于调用**SQLFetch**。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_PRIOR|返回之前的行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_RELATIVE|返回行集*FetchOffset*从当前行集的开始。|  
|SQL_FETCH_ABSOLUTE|返回从行开始的行集*FetchOffset*。|  
|SQL_FETCH_FIRST|在结果集中返回第一个行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_LAST|在结果集中返回最后一个的整个行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_BOOKMARK|返回行集 FetchOffset 中的行 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指定的书签。|  
  
 驱动程序不需要支持所有提取方向;应用程序调用**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型来确定哪些提取该驱动程序支持的方向。 应用程序应查看这些信息类型中 SQL_CA1_NEXT、 SQL_CA1_RELATIVE、 SQL_CA1_ABSOLUTE 和 WQL_CA1_BOOKMARK 位掩码。 此外，如果光标位于只进和 FetchOrientation 不 SQL_FETCH_NEXT， **SQLFetchScroll**返回 SQLSTATE HY106 （提取类型超出了范围）。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行集中的行数。 如果通过提取行集正在**SQLFetchScroll**重叠结果集末尾**SQLFetchScroll**返回部分行集。 也就是说，S + R – 1 大于 L，其中 S 等于正在提取行集 R 的起始行是行集大小和 L 为最后一个行在结果集中，然后仅第一个 L-S + 1 的行集的行有效。 空和状态的 SQL_ROW_NOROW 剩余行。  
  
 后**SQLFetchScroll**返回时，当前行是行集的第一行。  
  
## <a name="cursor-positioning-rules"></a>光标定位规则  
 下列各节描述 FetchOrientation 的每个值的精确规则。 这些规则使用的以下表示法。  
  
|表示法|含义|  
|--------------|-------------|  
|*开始之前*|块状游标位于结果集的开始之前。 如果新的行集的第一个行的结果集，开始之前**SQLFetchScroll**返回 SQL_NO_DATA。|  
|*在结束后*|块状游标位于结果的一端设置后。 如果在新行集的第一个行后该结果集末尾**SQLFetchScroll**返回 SQL_NO_DATA。|  
|*CurrRowsetStart*|第一个行集中的当前行数。|  
|*LastResultRow*|在结果集中的最后一行的编号。|  
|*RowsetSize*|行集大小。|  
|*FetchOffset*|值*FetchOffset*自变量。|  
|*BookmarkRow*|对应于 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指定的书签的行。|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*开始之前*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*在结束后*|  
|*在结束后*|*在结束后*|  
  
 [1] 如果提取行的前一个调用后，发生了更改的行集大小，这是与上一个调用一起使用的行集大小。  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*开始之前*|*开始之前*|  
|*CurrRowsetStart = 1*|*开始之前*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2]。</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*后端和 LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*在结束和 LastResultRow 后 > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2]。</sup>|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试的结果集返回第一个行集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*(开始操作之前和 FetchOffset > 0)或者 (后端和 FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 和 FetchOffset < = 0*|*开始之前*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*开始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*开始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*在结束后*|  
|*在结束和 FetchOffset 后 > = 0*|*在结束后*|  
  
 [1] ***SQLFetchScroll***就像它已设置为 SQL_FETCH_ABSOLUTE FetchOrientation 与调用将返回相同的行集。 有关详细信息，请参阅"SQL_FETCH_ABSOLUTE"部分。  
  
 [2] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试的结果集返回第一个行集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*开始之前*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*开始之前*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*在结束后*|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试的结果集返回第一个行集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
 执行对动态游标的绝对读取无法提供所需的结果，因为无法确定在动态游标中的行位置。 此类操作等效于提取第一次跟相对; 提取它不是原子操作，因为是在静态游标的绝对读取。  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 下列规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*开始之前*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*在结束后*|  
  
 有关书签的信息，请参阅[书签 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>生效的已删除、 添加，并且光标移动的错误行  
 静态和键集驱动游标有时将检测添加到的结果的行设置，并且删除从结果集中删除的行。 通过调用**SQLGetInfo** SQL_STATIC_CURSOR_ATTRIBUTES2 与 SQL_KEYSET_CURSOR_ATTRIBUTES2 选项和查看 SQL_CA2_SENSITIVITY_ADDITIONS、 SQL_CA2_SENSITIVITY_DELETIONS 和 SQL_CA2_SENSITIVITY_更新位掩码，应用程序确定实现特定的驱动程序的光标是否执行此操作。 为驱动程序，它可以检测已删除的行并将其删除，以下各段介绍此行为的影响。 驱动程序可以检测到已删除的行，但不能删除它们，删除对产生任何影响光标动作数，并不适用于以下各段。  
  
 如果光标检测添加到结果集的行或删除从结果集中删除的行，它将出现就像它仅在它提取数据时检测这些更改。 这包括这种情况时**SQLFetchScroll**已调用 FetchOrientation 设置为 SQL_FETCH_RELATIVE 和 FetchOffset 设置为 0 以重新提取相同的行集，但不包括这种情况，当设置为 SQL_ fOption SQLSetPos 被调用时刷新。 在后一种情况下，行集缓冲区中的数据被刷新，但不是 refetched 和删除的行不会从结果集。 因此，当从删除或到当前行集中插入行时，光标不会修改的行集缓冲区。 相反，它检测到更改时提取任何行集的以前所包含已删除的行或现在包括插入的行。  
  
 例如：  
  
```  
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
  
 时**SQLFetchScroll**返回新的行集具有相对于当前行集的位置-即 FetchOrientation 是 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR 或 SQL_FETCH_RELATIVE — 它不包括对当前行集的更改在计算新行集的起始位置。 但是，其中包括当前行集之外的更改，如果能够检测它们。 此外，当**SQLFetchScroll**返回新的行集具有独立于当前行集的位置-即 FetchOrientation 是 SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK — 它包括它是能够检测，即使它们是在当前行集中的所有更改。  
  
 在确定新添加的行内部或外部的当前行集时，被视为部分行集的最后一个的有效行; 在结束也就是说，为其行状态不是 SQL_ROW_NOROW 的最后一行。 例如，假设在光标处于能够检测新添加的行、 当前行集是部分行集、 应用程序将添加新行和光标将这些行添加到结果集的末尾。 如果应用程序调用**SQLFetchScroll**与设置为 SQL_FETCH_NEXT，FetchOrientation **SQLFetchScroll**返回开头新添加的第一行的行集。  
  
 例如，假设当前行集包含行 21 到 30、 行集大小为 10、 光标中删除从结果集中删除的行和光标检测添加到结果集的行。 下表显示的行**SQLFetchScroll**在各种情况下返回。  
  
|更改|提取类型|FetchOffset|新行集 [1]|  
|------------|----------------|-----------------|---------------------|  
|删除第 21 行|NEXT|0|31 到 40|  
|删除行 31|NEXT|0|32 到 41|  
|插入行 21 到 22 之间的行|NEXT|0|31 到 40|  
|插入行 30 和 31 之间|NEXT|0|插入的行，31 到 39|  
|删除第 21 行|PRIOR|0|11 到 20|  
|删除行 20|PRIOR|0|10 到 19|  
|插入行 21 到 22 之间的行|PRIOR|0|11 到 20|  
|插入行 20 和 21 之间的行|PRIOR|0|12 到 20 插入的行|  
|删除第 21 行|RELATIVE|0|22 到 31<sup>[2]</sup>|  
|删除第 21 行|RELATIVE|1|22 到 31|  
|插入行 21 到 22 之间的行|RELATIVE|0|21，插入的行，22 到 29 个|  
|插入行 21 到 22 之间的行|RELATIVE|1|22 到 31|  
|删除第 21 行|ABSOLUTE|21|22 到 31<sup>[2]</sup>|  
|删除行 22|ABSOLUTE|21|21，23 到 31|  
|插入行 21 到 22 之间的行|ABSOLUTE|22|插入的行，22 到 29 个|  
  
 [1] 此列使用行号之前已插入或删除任何行。  
  
 [2] 在此情况下，光标将尝试返回开头第 21 行的行。 由于第 21 行已被删除，它将返回第一行是行 22。  
  
 错误行 （即，行状态的 SQL_ROW_ERROR） 不会影响光标移动。 例如，如果当前行集启动含有第 11 行和状态的第 11 行是 SQL_ROW_ERROR，调用**SQLFetchScroll** FetchOrientation 设置为 SQL_FETCH_RELATIVE 和 FetchOffset 设置为 5 将返回行 16，开始的行集就像将第 11 行的状态是否 SQL_SUCCESS。  
  
## <a name="returning-data-in-bound-columns"></a>绑定的列中返回数据  
 **SQLFetchScroll**绑定列中返回数据，方式与**SQLFetch**。 详细信息，请参阅"将数据返回中绑定列"中[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 如果没有列被绑定， **SQLFetchScroll**不返回数据，但未将块光标移动到指定的位置。 是否可以从的块游标的未绑定列检索数据**SQLGetData**取决于该驱动程序。 如果调用，则支持此功能**SQLGetInfo**返回 SQL_GD_BLOCK SQL_GETDATA_EXTENSIONS 信息类型的位。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 **SQLFetchScroll**使用相同的公式来确定为数据和长度/指示器缓冲区的地址**SQLFetch**。 详细信息，请参阅"缓冲区的地址"中[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="row-status-array"></a>行状态数组  
 **SQLFetchScroll** SQLFetch 一样的方法中设置行状态数组中的值。 有关详细信息，请参阅"行状态数组" [SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="rows-fetched-buffer"></a>行提取缓冲区  
 **SQLFetchScroll**返回的行提取缓冲区中提取与相同的方式中的行数**SQLFetch**。 有关详细信息，请参阅"行提取缓冲区" [SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="error-handling"></a>错误处理  
 在应用程序调用**SQLFetchScroll** ODBC 3.x 驱动程序，在驱动程序管理器调用**SQLFetchScroll**驱动程序中。 在应用程序调用**SQLFetchScroll**在 ODBC 2.x 驱动程序，驱动程序管理器调用 SQLExtendedFetch 驱动程序中。 因为**SQLFetchScroll**和 SQLExtendedFetch 句柄错误略有不同的方式，在它调用时应用程序看到略有不同的错误行为**SQLFetchScroll**中 ODBC 2.x 和 ODBC3.x 驱动程序。  
  
 **SQLFetchScroll**中一样的方法返回错误和警告**SQLFetch**; 有关详细信息，请参阅中的"错误处理" **SQLFetch**。 **SQLExtendedFetch**中一样的方法返回错误**SQLFetch**，有以下例外：  
  
 时出现警告时，适用于特定行集中的行，SQLExtendedFetch 将设置到 SQL_ROW_SUCCESS，不 SQL_ROW_SUCCESS_WITH_INFO 行状态数组中的相应条目。  
  
 如果在行集中的每一行中出现错误，SQLExtendedFetch 返回 SQL_SUCCESS_WITH_INFO，不 SQL_ERROR。  
  
 在适用于单个行的状态记录每个组，SQLExtendedFetch 返回的第一个状态记录必须包含 SQLSTATE 01S01 （行中的错误）;**SQLFetchScroll**不返回此 SQLSTATE。 如果无法返回其他 SQLSTATEs SQLExtendedFetch，但它仍必须返回的此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和乐观并发  
 如果游标使用开放式并发 — SQL_ATTR_CONCURRENCY 语句属性，即，具有值为 SQL_CONCUR_VALUES 或 SQL_CONCUR_ROWVER- **SQLFetchScroll**更新使用的数据的开放式并发值若要检测是否已更改行的源。 发生这种情况每当**SQLFetchScroll**提取一个新的行集，包括时它 refetches 当前行集。 （它已调用 FetchOrientation 设置为 SQL_FETCH_RELATIVE 和 FetchOffset 设置为 0。）  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驱动程序  
 在应用程序调用**SQLFetchScroll** ODBC 2.x 驱动程序，在驱动程序管理器将映射到此调用**SQLExtendedFetch**。 它将传递的自变量的以下值**SQLExtendedFetch**。  
  
|SQLExtendedFetch 自变量|“值”|  
|-------------------------------|-----------|  
|StatementHandle|中的 StatementHandle **SQLFetchScroll**。|  
|FetchOrientation|中的 FetchOrientation **SQLFetchScroll**。|  
|FetchOffset|如果 FetchOrientation 不 SQL_FETCH_BOOKMARK 中的 FetchOffset 自变量的值**SQLFetchScroll**使用。<br /><br /> 如果 FetchOrientation 是 SQL_FETCH_BOOKMARK，则使用存储在 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指定的地址的值。|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR 语句属性指定的地址。|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR 语句属性指定的地址。|  
  
 有关详细信息，请参阅[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>说明符和 SQLFetchScroll  
 **SQLFetchScroll**与描述符交互的方式相同**SQLFetch**。 有关详细信息，请参阅中的"描述符和 SQLFetchScroll"一节[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)，[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)，[定位 Update 和 Delete 语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)，和[SQLSetPos使用更新的行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行大容量插入、 更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|关闭的语句上光标|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回的结果数设置列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|将光标置于、 刷新行集中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
