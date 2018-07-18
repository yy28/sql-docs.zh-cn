---
title: SQLExtendedFetch 函数 |Microsoft 文档
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
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a02b1c2e050b6fc7a0724286c7f023cb376e7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922802"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： 不推荐使用  
  
 **摘要**  
 **SQLExtendedFetch**从结果集中提取数据的指定行集，并返回所有绑定的列的数据。 绝对或相对位置或书签，可以指定行集。  
  
> [!NOTE]  
>  ODBC 3 中 *.x*， **SQLExtendedFetch**已被取代**SQLFetchScroll**。 ODBC 3 *.x*应用程序不应调用**SQLExtendedFetch**; 它们应改为调用**SQLFetchScroll**。 驱动程序管理器映射**SQLFetchScroll**到**SQLExtendedFetch**使用 ODBC 2 时 *.x*驱动程序。 ODBC 3 *.x*驱动程序应支持**SQLExtendedFetch**如果他们想要使用 ODBC 2 *.x*调用它的应用程序。 有关详细信息，请参阅"注释"和[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *FetchOrientation*  
 [输入]提取的类型。 这是与相同*FetchOrientation*中**SQLFetchScroll**。  
  
 *FetchOffset*  
 [输入]要读取的行数。 这是与相同*FetchOffset*中**SQLFetchScroll**，有一个例外。 当*FetchOrientation*是 SQL_FETCH_BOOKMARK， *FetchOffset*是固定长度书签，而不从书签中的偏移量。 换而言之， **SQLExtendedFetch**从该参数，不 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性检索的书签。 它不支持可变长度书签并不支持从书签中提取行集 （0) 以外的某个偏移量上。  
  
 *RowCountPtr*  
 [输出]指向在其返回实际读取的行数的缓冲区的指针。 在 SQL_ATTR_ROWS_FETCHED_PTR 语句属性指定的缓冲区与相同的方式使用此缓冲区。 仅可由使用此缓冲区**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**。  
  
 *RowStatusArray*  
 [输出]指向数组中要返回其每个行的状态。 此数组使用相同的方式与 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的数组中。  
  
 但是，此数组的地址不存储在中 IRD SQL_DESC_STATUS_ARRAY_PTR 字段中。 此外，此数组仅供**SQLExtendedFetch**和**SQLBulkOperations**与*操作*的 SQL_ADD 或**SQLSetPos**之后调用时**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**，而且它不由**SQLBulkOperations**或**SQLSetPos**时之后调用**SQLFetch**或**SQLFetchScroll**。 它还不是时使用**SQLBulkOperations**与*操作*SQL_ADD 的调用之前调用任何提取函数。 换而言之，它仅适用于语句的状态 S7。 在语句状态 S5 或 S6 不使用它。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)附录 b: ODBC 状态转换表中。  
  
 应用程序应提供中的有效指针*RowStatusArray*自变量; 如果没有的行为**SQLExtendedFetch**和对的调用行为**SQLBulkOperations**或**SQLSetPos**游标已通过已定位后**SQLExtendedFetch**是不确定的。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLExtendedFetch**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLError**。 下表列出了通常返回的 SQLSTATE 值**SQLExtendedFetch**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。 如果上一个列中，发生错误时**SQLGetDiagField**可以使用调用*DiagIdentifier*的 SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 列和**SQLGetDiagField**可以使用调用*DiagIdentifier*的 SQL_DIAG_ROW_NUMBER 以确定包含该列的行。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制数据的列返回导致非空白字符或非 NULL 二进制数据截断。 如果它是一个字符串值，它是右侧被截断。 如果它是一个数字值被截断的数字的小数部分。  （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S01|行中的错误|提取一个或多个行时出错。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S06|尝试的结果集返回第一个行集之前提取|请求的行集重叠的结果集中当前位置时超出第一行中，然后开始*FetchOrientation*已 SQL_PRIOR 或*FetchOrientation*已与 SQL_RELATIVE负*FetchOffset*绝对值是小于或等于当前的 SQL_ROWSET_SIZE。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S07|小数部分组成的截断|返回的列的数据被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳，和包含时间组件的 interval 数据类型，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法转换数据值，由指定的 C 数据类型为*TargetType*中**SQLBindCol**。|  
|07009|无效的描述符索引|第 0 列被绑定与**SQLBindCol**，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22002|需要指示器变量，但未提供|NULL 数据提取了的列中其*StrLen_or_IndPtr*设置**SQLBindCol**是空指针。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22003|数值超出范围|返回一个或多个列 （为数字或字符串） 的数字值可能会导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> 有关详细信息，请参阅[间隔和数值数据类型准则](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)附录 d： 数据类型中。|  
|22007|无效的日期时间格式|结果集中的字符列已绑定到日期、 时间或时间戳 C 结构，列中的值，分别无效的日期、 时间戳。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22012|被零除|返回一个值算术表达式中的，这会导致除法被零除。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22015|间隔字段溢出|将从精确数字或间隔 SQL 类型分配给间隔 C 类型由前导字段中的重要数字丢失。<br /><br /> 在提取到间隔 C 类型数据, 时没有间隔 C 类型中的 SQL 类型的值的表示形式。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22018|转换指定的的无效字符值|C 类型已准确或近似数字、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;并且列中的值不是有效的文本的绑定的 C 类型。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|24000|无效的游标状态|*StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLError**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数已在上再次*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLExtendedFetch**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) **SQLExtendedFetch**曾为*StatementHandle*后**SQLFetch**或**SQLFetchScroll**调用和之前**SQLFreeStmt**调用时使用 SQL_CLOSE 选项。<br /><br /> (DM) **SQLBulkOperations**为语句之前调用**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**调用，并然后**SQLExtendedFetch**之前已调用**SQLFreeStmt**调用时使用 SQL_CLOSE 选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY106|提取类型超出了范围|(DM) 值的参数的指定*FetchOrientation*无效。 （请参阅"注释"。）<br /><br /> 自变量*FetchOrientation*已 SQL_FETCH_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 语句属性被设置为 SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE 语句选项的值为 SQL_CURSOR_FORWARD_ONLY 和自变量的值*FetchOrientation*未 SQL_FETCH_NEXT。<br /><br /> 自变量*FetchOrientation*已 SQL_FETCH_RESUME。|  
|HY107|行数值超出范围|用 SQL_CURSOR_TYPE 语句选项指定的值是 SQL_CURSOR_KEYSET_DRIVEN，但具有 SQL_KEYSET_SIZE 语句属性指定的值是大于 0 而小于用 SQL_ROWSET_SIZE 语句属性指定的值.|  
|HY111|无效的书签值|自变量*FetchOrientation*已 SQL_FETCH_BOOKMARK，和书签中指定*FetchOffset*自变量无效。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的提取类型。<br /><br /> 驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。 此错误仅适用于 SQL 数据类型的列已映射到特定于驱动程序的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtOption**，SQL_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 行为**SQLExtendedFetch**等同于的**SQLFetchScroll**，有以下例外：  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同的方法返回的提取的行数。 **SQLExtendedFetch**返回中提取的行数 *\*RowCountPtr*;**SQLFetchScroll**返回提取直接向通过 SQL_ATTR_ROWS_FETCHED_PTR 指向的缓冲区的行数。 有关详细信息，请参阅*RowCountPtr*自变量。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**的不同阵列中返回的每个行的状态。 有关详细信息，请参阅*RowStatusArray*自变量。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同的方法来检索书签时*FetchOrientation*是 SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支持可变长度书签或从书签 0 以外的某个偏移量上提取行集。 有关详细信息，请参阅*FetchOffset*自变量。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同的行集大小。 **SQLExtendedFetch**使用 SQL_ROWSET_SIZE 语句属性的值和**SQLFetchScroll**使用 SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值。  
  
-   **SQLExtendedFetch**出错略有不同的处理与语义**SQLFetchScroll**。 有关详细信息，请参见"错误"中处理的"注释"部分[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
-   **SQLExtendedFetch**不支持绑定偏移量 （SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性）。  
  
-   调用**SQLExtendedFetch**不能与调用混合**SQLFetch**或**SQLFetchScroll**，并且如果**SQLBulkOperations**称为在调用任何提取函数之前， **SQLExtendedFetch**之前关闭并重新打开游标不能调用。 也就是说， **SQLExtendedFetch**可以仅在语句状态 S7 中调用。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)附录 b: ODBC 状态转换表中。  
  
 在应用程序调用**SQLFetchScroll**时使用 ODBC 2 *.x*驱动程序，驱动程序管理器映射到此调用**SQLExtendedFetch**。 有关详细信息，请参阅"SQLFetchScroll 和 ODBC 2 *.x*驱动程序"中[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 在 ODBC 2 *.x*， **SQLExtendedFetch**调用提取多个行和**SQLFetch**调用提取单个行。 ODBC 3 中 *.x*，另一方面， **SQLFetch**可以调用提取多个行。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行大容量插入、 更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回的结果数设置列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|将光标置于、 刷新行集中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
