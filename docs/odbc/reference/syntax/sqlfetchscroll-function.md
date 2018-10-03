---
title: SQLFetchScroll 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 146967ebc31d5e7d8176d37ee5b8b0b97b6c0674
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769485"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll Function（SQLFetchScroll 函数）
**符合性**  
 版本引入了： ODBC 3.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLFetchScroll**从结果集中提取数据的指定行集，并返回所有绑定列的数据。 绝对或相对位置或书签，可以指定行集。  
  
 在使用 ODBC 2.x 驱动程序，驱动程序管理器将映射到此函数**SQLExtendedFetch**。 有关详细信息，请参阅[用于向后兼容性的应用程序映射替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
  
 有关详细信息，请参阅"注释"部分中的"定位游标"。  
  
 *FetchOffset*  
 [输入]  
  
 若要提取的行数。 此参数的解释取决于的值*FetchOrientation*参数。 有关详细信息，请参阅"注释"部分中的"定位游标"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFetchScroll**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec** SQL_HANDLE_STMT HandleType 和的句柄StatementHandle。 下表列出了通常返回的 SQLSTATE 值**SQLFetchScroll** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。 如果在单个列中，出现错误**SQLGetDiagField**可以使用 DiagIdentifier 的 SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 列调用并**SQLGetDiagField**可以调用使用 DiagIdentifier 的 SQL_DIAG_ROW_NUMBER 以确定包含该列的行。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果上一个或多个，但并非所有行的多行操作，出现错误，并且如果发生错误，则返回 SQL_ERROR单行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制的列返回的数据时截断了非空白字符或非 NULL 的二进制数据。 如果它是一个字符串值，它是右侧被截断。|  
|01S01|行中的错误|获取一个或多个行时出错。<br /><br /> (如果在 ODBC 3 时返回此 SQLSTATE *.x*应用程序使用 ODBC 2 *.x*驱动程序，则可以忽略它。)|  
|01S06|在尝试提取之前返回的结果集的第一个行集|请求行集重叠时 FetchOrientation 已 SQL_FETCH_PRIOR、 第一行中，超出了当前的位置和当前行数小于或等于行集大小的结果集的开头。<br /><br /> 请求行集重叠时 FetchOrientation SQL_FETCH_PRIOR、 当前位置已经超出了结果集的末尾，行集大小大于该结果集大小的结果集的开头。<br /><br /> 请求行集重叠时 FetchOrientation 已 SQL_FETCH_RELATIVE，FetchOffset 为负，和 FetchOffset 绝对值是小于或等于行集大小的结果集的开头。<br /><br /> 请求行集重叠时 FetchOrientation 为 SQL_FETCH_ABSOLUTE、 FetchOffset 为负，且 FetchOffset 绝对值为晚于结果集大小的结果集的开头，但小于或等于行集大小。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S07|截断小数部分|返回的列的数据已被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳和 interval 数据类型包含时间部分，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法为指定的数据类型转换的结果集中的列的数据值*TargetType*中**SQLBindCol**。<br /><br /> 第 0 列绑定使用的数据类型为 SQL_C_BOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。<br /><br /> 第 0 列绑定使用的数据类型为 SQL_C_VARBOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性未设置为 SQL_UB_VARIABLE。|  
|07009|描述符索引无效|该驱动程序是 ODBC 2 *.x*不支持的驱动程序**SQLExtendedFetch**，和列的绑定中指定列编号为 0。<br /><br /> 第 0 列被绑定，并将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22001|字符串数据，右截断|长度可变的书签的列返回已被截断。|  
|22002|需要指示器变量，但未提供|NULL 已提取数据的列中其*StrLen_or_IndPtr*设置**SQLBindCol** (或通过设置 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 是空指针。|  
|22003|数值超出范围|返回一个或多个绑定列 （为数字或字符串） 的数字值将导致要截断的数字的整个 （而不是小数） 部分。<br /><br /> 有关详细信息，请参阅[转换将数据从 SQL 到 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|日期时间格式无效|在结果集中的字符列已绑定到日期、 时间或时间戳 C 结构和列中的值时，分别，无效的日期、 时间戳。|  
|22012|被零除|算术表达式中的值返回，这导致除零。|  
|22015|间隔字段溢出|将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型前导字段中时导致重要数字丢失。<br /><br /> 提取数据到 C 间隔类型时，出现没有 C 间隔类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的字符值无效|结果集中的字符列已绑定到 C 字符缓冲区，而该列包含出现没有缓冲区的字符集中的表示形式的字符。<br /><br /> C 类型为精确或近似数值、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;和列中的值不是有效的绑定 C 类型的文本。|  
|24000|游标状态无效|*StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。|  
|40001|序列化失败|在其中执行提取该事务已终止，以防止死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLFetchScroll**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**或目录函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） **SQLFetch**曾为*StatementHandle*后**SQLExtendedFetch**调用之前**SQLFreeStmt**与 SQL_调用了关闭选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|SQL_ATTR_USE_BOOKMARK 语句属性设置为 SQL_UB_VARIABLE，并且第 0 列绑定到其的长度不等于此结果集的书签的最大长度的缓冲区。 (此长度可在 IRD 的 SQL_DESC_OCTET_LENGTH 字段中，并且可以通过调用来获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY106|提取类型超出了范围|DM) FetchOrientation 的参数指定的值无效。<br /><br /> (DM) 参数 FetchOrientation 为 SQL_FETCH_BOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE 语句属性的值为 SQL_CURSOR_FORWARD_ONLY 和 FetchOrientation 未 SQL_FETCH_NEXT 的自变量的值。<br /><br /> 将 SQL_ATTR_CURSOR_SCROLLABLE 语句属性的值为 SQL_NONSCROLLABLE 和 FetchOrientation 未 SQL_FETCH_NEXT 的自变量的值。|  
|HY107|行数值超出范围|SQL_ATTR_CURSOR_TYPE 语句属性与指定的值为 SQL_CURSOR_KEYSET_DRIVEN，但使用 SQL_ATTR_KEYSET_SIZE 语句属性指定的值大于 0 且小于 SQL_ATTR_ROW_ARRAY_ 用指定的值大小语句属性。|  
|HY111|书签值无效|参数 FetchOrientation 为 SQL_FETCH_BOOKMARK，并通过 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性中的值所指向的书签无效，或者是空指针。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前请求的结果集返回的数据源。 SQLSetStmtAttr，sql_attr_query_timeout 时，可通过设置超时期限。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLFetchScroll**从结果集中返回指定行集。 按绝对或相对位置或书签，可以指定行集。 **SQLFetchScroll**结果集中存在时才可以调用 — 即，在调用后，创建结果集和游标结果集中的转移已关闭。 如果任何列的绑定，将这两列中返回的数据。 如果应用程序指定行状态数组或在其中返回读取的行数的缓冲区的指针，则**SQLFetchScroll**返回此信息。 调用**SQLFetchScroll**可以通过调用混合**SQLFetch**但不能在其中调用**SQLExtendedFetch**。  
  
 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)并[使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>将光标置于  
 创建结果集时，游标位于结果集的开始之前。 **SQLFetchScroll**的值为基础的块光标置于*FetchOrientation*并*FetchOffset*下表中所示的参数。 用于确定新行集的开始的确切规则是下一节中所示。  
  
|FetchOrientation|含义|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|返回下一步的行集。 这相当于调用**SQLFetch**。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_PRIOR|返回之前的行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_RELATIVE|返回行集*FetchOffset*从当前行集的开始。|  
|SQL_FETCH_ABSOLUTE|返回行开始的行集*FetchOffset*。|  
|SQL_FETCH_FIRST|在结果集中返回第一个行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_LAST|在结果集中返回的最后一个完整行集。<br /><br /> **SQLFetchScroll**将忽略的值*FetchOffset*。|  
|SQL_FETCH_BOOKMARK|SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指定的书签 FetchOffset 行返回行集。|  
  
 驱动程序不需要支持所有 fetch 方向;应用程序调用**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型来确定哪些提取驱动程序支持的方向。 应用程序将查看这些信息类型中 SQL_CA1_NEXT、 SQL_CA1_RELATIVE、 SQL_CA1_ABSOLUTE 和 WQL_CA1_BOOKMARK 的位屏蔽。 此外，如果游标是只进和 FetchOrientation 不是 SQL_FETCH_NEXT， **SQLFetchScroll**返回 SQLSTATE HY106 （提取类型超出了范围）。  
  
 将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的行集中的行数。 如果行集正在通过提取**SQLFetchScroll**重叠的结果集末尾**SQLFetchScroll**返回的部分行集。 也就是说，S + R-1 大于 L，其中，S 起始行的行集提取，R 是行集大小和 L 是最后一个行在结果集中，然后仅第一个 L – S + 1 行集的行有效。 剩余的行是空并且具有 SQL_ROW_NOROW 的状态。  
  
 之后**SQLFetchScroll**返回当前行是行集的第一行。  
  
## <a name="cursor-positioning-rules"></a>游标定位规则  
 以下部分介绍 FetchOrientation 每个值的精确的规则。 这些规则使用以下表示法。  
  
|表示法|含义|  
|--------------|-------------|  
|*在开始之前*|块游标位于结果集的开始之前。 如果新的行集的第一行是结果集，在开始之前**SQLFetchScroll**返回 sql_no_data 为止。|  
|*后端*|块游标位于结果的最终集之后。 如果在新行集的第一个行后的结果集末尾**SQLFetchScroll**返回 sql_no_data 为止。|  
|*CurrRowsetStart*|当前行集中的第一个行数。|  
|*LastResultRow*|在结果集中的最后一个行数。|  
|*RowsetSize*|行集大小。|  
|*FetchOffset*|值*FetchOffset*参数。|  
|*BookmarkRow*|SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指定的书签相对应的行。|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*在开始之前*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*后端*|  
|*后端*|*后端*|  
  
 [1] 如果提取行的前一个调用后，发生了更改的行集大小，这是与上一个调用一起使用的行集大小。  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*在开始之前*|*在开始之前*|  
|*CurrRowsetStart = 1*|*在开始之前*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2]。</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*后端和 LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*后端和 LastResultRow > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2]。</sup>|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试提取之前返回的结果集的第一个行集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*(开始操作之前和 FetchOffset > 0)或者 (后端和 FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 和 FetchOffset < = 0*|*在开始之前*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*在开始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 和&#124;FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*在开始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 和&#124;FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*后端*|  
|*后端和 FetchOffset > = 0*|*后端*|  
  
 [1] ***SQLFetchScroll***就像它已设置为 SQL_FETCH_ABSOLUTE FetchOrientation 与调用返回相同的行集。 有关详细信息，请参阅"SQL_FETCH_ABSOLUTE"部分。  
  
 [2] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试提取之前返回的结果集的第一个行集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*FetchOffset < 0 和&#124;FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 和&#124;FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*在开始之前*|  
|*FetchOffset < 0 和&#124;FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*在开始之前*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*后端*|  
  
 [1] **SQLFetchScroll**返回 SQLSTATE 01S06 （尝试提取之前返回的结果集的第一个行集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
 绝对提取执行对动态游标不能提供所需的结果，因为动态游标中的行位置是不确定。 此类操作相当于提取第一次后跟 fetch relative;它不是原子操作，因为是绝对提取对静态游标。  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 如果提取行的前一个调用后，发生了更改的行集大小，这是新的行集大小。  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 以下规则适用。  
  
|条件|第一行的新行集。|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*在开始之前*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*后端*|  
  
 有关书签的信息，请参阅[书签 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>已删除、 添加的效果和错误行的游标移动  
 静态游标和由键集驱动游标有时候检测添加到结果中的行设置和删除从结果集中删除的行。 通过调用**SQLGetInfo** SQL_STATIC_CURSOR_ATTRIBUTES2 和 SQL_KEYSET_CURSOR_ATTRIBUTES2 选项并查看 SQL_CA2_SENSITIVITY_ADDITIONS、 SQL_CA2_SENSITIVITY_DELETIONS 和 SQL_CA2_SENSITIVITY_更新的位屏蔽，应用程序确定由特定的驱动程序实现的游标是否执行此操作。 驱动程序，可以检测已删除的行并将其删除，以下各段介绍此行为的效果。 驱动程序可以检测到已删除的行，但不能删除它们，请删除没有任何影响光标的移动，并不适用于以下各段。  
  
 如果游标检测到已添加到结果集行，或移除从结果集中删除的行，它将显示如如果检测到这些更改仅在提取数据时。 这包括用例时**SQLFetchScroll**称为 FetchOrientation 设置为 SQL_FETCH_RELATIVE，FetchOffset 设置为 0 以重新提取相同的行集，但不包括用例时使用设置为 SQL_ fOption 调用 SQLSetPos刷新。 在后一种情况下，刷新行集缓冲区中的数据，但不是 refetched 和删除的行不会从结果集。 因此，当从已删除或插入到当前行集行时，光标不会修改行集缓冲区。 相反，它检测到更改时提取所有行集的以前所包含已删除的行或现在包括插入的行。  
  
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
  
 时**SQLFetchScroll**返回具有相对于当前行集的位置的新行集 — 即 FetchOrientation 是 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR 或 SQL_FETCH_RELATIVE — 它不包括对当前行集的更改当计算新行集的起始位置。 但是，它包含当前行集外，如果能够将其检测出来。 此外，当**SQLFetchScroll**返回具有独立于当前行集的位置的新行集 — 即 FetchOrientation 是 SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK — 它包括的是能够检测，即使它们是当前行集中的所有更改。  
  
 在确定新添加的行内部或外部的当前行集时，被视为部分行集结束处的最后一个有效行;也就是说，其行状态不是 SQL_ROW_NOROW 的最后一行。 例如，假设在光标位于能够检测新添加的行，当前行集是部分行集、 应用程序添加新行，光标将这些行添加到结果集的末尾。 如果应用程序调用**SQLFetchScroll**与设置为 SQL_FETCH_NEXT，FetchOrientation **SQLFetchScroll**返回从开始新添加的第一行的行集。  
  
 例如，假设当前行集包含 21 到 30 行、 行集大小为 10、 光标移除从结果集中删除的行和光标检测到已添加到结果集行。 下表显示的行**SQLFetchScroll**在各种情况下返回。  
  
|更改|提取类型|FetchOffset|[1] 的新行集|  
|------------|----------------|-----------------|---------------------|  
|删除第 21 行|NEXT|0|31 到 40|  
|删除行 31|NEXT|0|32 到 41|  
|21 和 22 行之间插入行|NEXT|0|31 到 40|  
|插入行 30 和 31 之间的行|NEXT|0|插入的行，31 到 39|  
|删除第 21 行|PRIOR|0|11 到 20|  
|删除第 20 行|PRIOR|0|10 至 19|  
|21 和 22 行之间插入行|PRIOR|0|11 到 20|  
|行 20 和 21 之间插入行|PRIOR|0|12 到 20，插入的行|  
|删除第 21 行|RELATIVE|0|22 到 31<sup>[2]</sup>|  
|删除第 21 行|RELATIVE|1|22 到 31|  
|21 和 22 行之间插入行|RELATIVE|0|21，插入的行，22 到 29|  
|21 和 22 行之间插入行|RELATIVE|1|22 到 31|  
|删除第 21 行|ABSOLUTE|21|22 到 31<sup>[2]</sup>|  
|删除行 22|ABSOLUTE|21|21，23 到 31|  
|21 和 22 行之间插入行|ABSOLUTE|22|插入的行，22 到 29|  
  
 [1] 此列使用行号之前已插入或删除任何行。  
  
 [2] 在这种情况下，光标会尝试返回从开始第 21 行的行。 第 21 行已被删除，因为它将返回第一行是行 22。  
  
 错误行 （即，行状态的 SQL_ROW_ERROR） 不会影响光标的移动。 例如，如果当前行集开头第 11 行和状态的第 11 行是 SQL_ROW_ERROR，调用**SQLFetchScroll** FetchOrientation 设置为 SQL_FETCH_RELATIVE，FetchOffset 设置为 5 将返回从开始第 16，行的行集只需就像第 11 行状态为 SQL_SUCCESS。  
  
## <a name="returning-data-in-bound-columns"></a>在绑定列中返回数据  
 **SQLFetchScroll**在绑定列中返回数据的方式相同**SQLFetch**。 详细信息，请参阅"将数据返回在绑定列"中[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 如果绑定没有列， **SQLFetchScroll**不返回数据，但 does 将块光标移动到指定位置。 是否可以从使用块游标的未绑定列检索数据**SQLGetData**取决于驱动程序。 如果调用，则支持此功能**SQLGetInfo**返回 SQL_GD_BLOCK 位 SQL_GETDATA_EXTENSIONS 信息类型。  
  
## <a name="buffer-addresses"></a>缓冲区地址  
 **SQLFetchScroll**使用相同的公式来确定为数据和长度/指示器缓冲区的地址**SQLFetch**。 详细信息，请参阅"缓冲区的地址"中[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="row-status-array"></a>行状态数组  
 **SQLFetchScroll** SQLFetch 与相同的方式设置行状态数组中的值。 详细信息，请参阅"行状态数组"中[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="rows-fetched-buffer"></a>提取的行的缓冲区  
 **SQLFetchScroll**将返回方式与在提取行的缓冲区中提取的行数**SQLFetch**。 详细信息，请参阅"行提取缓冲区"中[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="error-handling"></a>错误处理  
 当应用程序调用**SQLFetchScroll** ODBC 3.x 驱动程序，在驱动程序管理器调用**SQLFetchScroll**驱动程序中。 当应用程序调用**SQLFetchScroll**在 ODBC 2.x 驱动程序，驱动程序管理器调用 SQLExtendedFetch 驱动程序中。 因为**SQLFetchScroll**和 SQLExtendedFetch 方式略有不同的处理错误、 时它将调用应用程序将略有不同的错误行为**SQLFetchScroll**在 ODBC 2.x 和 ODBC3.x 驱动程序。  
  
 **SQLFetchScroll**返回相同的方式中的错误和警告**SQLFetch**; 有关详细信息，请参阅中的"错误处理" **SQLFetch**。 **SQLExtendedFetch**中一样的方法将返回错误**SQLFetch**，但存在以下例外：  
  
 适用于特定行的行集中出现警告时, SQLExtendedFetch SQL_ROW_SUCCESS，不 SQL_ROW_SUCCESS_WITH_INFO 行状态数组中设置对应的条目。  
  
 如果在行集中的每个行中出现错误，SQLExtendedFetch 返回 SQL_SUCCESS_WITH_INFO，不 SQL_ERROR。  
  
 在适用于单个行的状态记录每个组，返回 SQLExtendedFetch 的第一个状态记录必须包含 SQLSTATE 01S01 （行中的错误）;**SQLFetchScroll**不会返回此 SQLSTATE。 如果无法返回其他 SQLSTATEs SQLExtendedFetch，它仍必须返回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和乐观并发  
 如果游标使用乐观并发，sql_attr_concurrency 设置语句属性，即具有值为 SQL_CONCUR_VALUES 或 SQL_CONCUR_ROWVER — **SQLFetchScroll**更新数据使用的开放式并发值若要检测是否已更改行的源。 发生这种情况每当**SQLFetchScroll**提取的新行集，包括时它 refetches 当前行集。 （它被称为使用 FetchOrientation 设置为 SQL_FETCH_RELATIVE，FetchOffset 设置为 0。）  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驱动程序  
 当应用程序调用**SQLFetchScroll**在 ODBC 2.x 驱动程序，驱动程序管理器将映射到此调用**SQLExtendedFetch**。 它将以下值传递的参数**SQLExtendedFetch**。  
  
|SQLExtendedFetch 参数|ReplTest1|  
|-------------------------------|-----------|  
|StatementHandle|在 StatementHandle **SQLFetchScroll**。|  
|FetchOrientation|在 FetchOrientation **SQLFetchScroll**。|  
|FetchOffset|如果 FetchOrientation 不 SQL_FETCH_BOOKMARK，FetchOffset 参数中的值**SQLFetchScroll**使用。<br /><br /> 如果 FetchOrientation SQL_FETCH_BOOKMARK，使用 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性所指定的地址上存储的值。|  
|RowCountPtr|将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性由指定的地址。|  
|RowStatusArray|将 SQL_ATTR_ROW_STATUS_PTR 语句属性由指定的地址。|  
  
 有关详细信息，请参阅[块状游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中向后兼容性的附录 g： 驱动程序指南。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述符和 SQLFetchScroll  
 **SQLFetchScroll**描述符与交互的方式相同**SQLFetch**。 有关详细信息，请参阅中的"描述符和 SQLFetchScroll"一节[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)，[按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)，[定位 Update 和 Delete 语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)，和[使用 SQLSetPos更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行大容量插入、 更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取单个行或仅向前方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|关闭游标语句|[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|返回数的结果集列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|将光标置于、 在行集中, 刷新数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
