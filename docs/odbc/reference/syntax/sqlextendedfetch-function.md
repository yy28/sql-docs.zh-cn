---
title: SQLExtendedFetch 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63030b34e4b607b850f25a67357d62a7184467c8
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537188"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：不推荐使用  
  
 **摘要**  
 **SQLExtendedFetch**从结果集中提取数据的指定行集，并返回所有绑定列的数据。 绝对或相对位置或书签，可以指定行集。  
  
> [!NOTE]
>  在 ODBC 3 *.x*， **SQLExtendedFetch**已由**SQLFetchScroll**。 ODBC 3 *.x*应用程序不应调用**SQLExtendedFetch**; 它们应改为调用**SQLFetchScroll**。 驱动程序管理器映射**SQLFetchScroll**到**SQLExtendedFetch**时使用的 ODBC 2 *.x*驱动程序。 ODBC 3 *.x*驱动程序应支持**SQLExtendedFetch**如果用户想要使用 ODBC 2 *.x*调用它的应用程序。 有关详细信息，请参阅"注释"和[块状游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附录 g:为了向后兼容的驱动程序指南。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输入]若要提取的行数。 这是与相同*FetchOffset*中**SQLFetchScroll**，有一个例外。 当*FetchOrientation*是 SQL_FETCH_BOOKMARK， *FetchOffset*是一个定长书签，不从书签的偏移量。 换而言之， **SQLExtendedFetch**书签检索此参数，不将 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性。 它不支持长度可变的书签并不支持从书签提取行集 （而不是 0) 的某偏移量处。  
  
 *RowCountPtr*  
 [输出]指向用于返回实际提取的行数的缓冲区。 将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性指定的缓冲区与相同的方式使用此缓冲区。 仅可由使用此缓冲区**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**。  
  
 *RowStatusArray*  
 [输出]指向用于返回每个行状态的数组的指针。 与数组 SQL_ATTR_ROW_STATUS_PTR 语句属性指定相同的方式使用此数组。  
  
 但是，此数组的地址不存储在 IRD 中的 SQL_DESC_STATUS_ARRAY_PTR 字段。 此外，此数组仅供**SQLExtendedFetch**并通过**SQLBulkOperations**与*操作*的 SQL_ADD 或**SQLSetPos**后调用时**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**，并且它不由**SQLBulkOperations**或**SQLSetPos**时后调用**SQLFetch**或**SQLFetchScroll**。 它还不是时，使用**SQLBulkOperations**与*操作*SQL_ADD 的调用之前提取的任何函数调用。 换而言之，它使用仅在语句的状态 S7 中。 在 S5 或 S6 语句状态中不使用它。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)在附录 b:状态转换表。  
  
 应用程序应提供中的有效指针*RowStatusArray*自变量; 如果没有的行为**SQLExtendedFetch**的调用的行为和**SQLBulkOperations**或**SQLSetPos**通过定位游标完后**SQLExtendedFetch**是不确定。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLExtendedFetch**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLError**。 下表列出了通常返回的 SQLSTATE 值**SQLExtendedFetch** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。 如果在单个列中，出现错误**SQLGetDiagField**可以使用调用*DiagIdentifier* SQL_DIAG_COLUMN_NUMBER 来确定该错误出现在; 的列的和**SQLGetDiagField**可以使用调用*DiagIdentifier*的 SQL_DIAG_ROW_NUMBER 以确定包含该列的行。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制的列返回的数据时截断了非空白字符或非 NULL 的二进制数据。 如果它是一个字符串值，它是右侧被截断。 如果它是数字值，已被截断的数字的小数部分。  （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S01|行中的错误|获取一个或多个行时出错。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S06|在尝试提取之前返回的结果集的第一个行集|请求行集重叠的结果集中当前位置的时间超出第一行中，并开始*FetchOrientation*已 SQL_PRIOR 或*FetchOrientation*已与 SQL_RELATIVE负*FetchOffset*其绝对值是小于或等于当前 SQL_ROWSET_SIZE。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S07|截断小数部分|返回的列的数据已被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳和 interval 数据类型包含时间部分，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法为指定的 C 数据类型转换的数据值*TargetType*中**SQLBindCol**。|  
|07009|描述符索引无效|第 0 列已绑定与**SQLBindCol**，SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22002|需要指示器变量，但未提供|NULL 已提取数据的列中其*StrLen_or_IndPtr*设置**SQLBindCol**是空指针。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22003|数值超出范围|返回一个或多个列 （为数字或字符串） 的数字值将导致数字被截断的整个 （而不是小数） 部分。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> 有关详细信息，请参阅[间隔和数值数据类型的准则](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)中附录 d:数据类型。|  
|22007|日期时间格式无效|在结果集中的字符列已绑定到日期、 时间或时间戳 C 结构和列中的值时，分别，无效的日期、 时间戳。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22012|被零除|算术表达式中的值返回，这导致除零。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22015|间隔字段溢出|将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型前导字段中时导致重要数字丢失。<br /><br /> 提取数据到 C 间隔类型时，出现没有 C 间隔类型中的 SQL 类型的值的表示形式。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22018|转换指定的字符值无效|C 类型为精确或近似数值、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;和列中的值不是有效的绑定 C 类型的文本。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|24000|游标状态无效|*StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLError**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLExtendedFetch**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） **SQLExtendedFetch**曾为*StatementHandle*后**SQLFetch**或**SQLFetchScroll**调用之前**SQLFreeStmt**调用时使用的 SQL_CLOSE 选项。<br /><br /> (DM) **SQLBulkOperations**为之前的语句调用**SQLFetch**， **SQLFetchScroll**，或者**SQLExtendedFetch**调用的、 和然后**SQLExtendedFetch**之前已调用**SQLFreeStmt**调用时使用的 SQL_CLOSE 选项。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY106|提取类型超出了范围|(DM) 的参数指定的值*FetchOrientation*无效。 （请参阅"注释"。）<br /><br /> 自变量*FetchOrientation*已 SQL_FETCH_BOOKMARK，和 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE 语句选项的值为 SQL_CURSOR_FORWARD_ONLY 和自变量的值*FetchOrientation*未 SQL_FETCH_NEXT。<br /><br /> 自变量*FetchOrientation*已 SQL_FETCH_RESUME。|  
|HY107|行数值超出范围|指定使用 SQL_CURSOR_TYPE 语句选项的值是 SQL_CURSOR_KEYSET_DRIVEN，但用 SQL_KEYSET_SIZE 语句属性指定的值是大于 0 且小于 SQL_ROWSET_SIZE 语句属性与指定的值.|  
|HY111|书签值无效|自变量*FetchOrientation*已 SQL_FETCH_BOOKMARK，和中指定的书签*FetchOffset*参数无效。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持指定的提取类型。<br /><br /> 驱动程序或数据源不支持指定的组合来转换*TargetType*中**SQLBindCol**和相应的列的 SQL 数据类型。 此错误仅适用于 SQL 数据类型的列映射到特定于驱动程序的 SQL 数据类型。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtOption**，SQL_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 行为**SQLExtendedFetch**等同于**SQLFetchScroll**，但存在以下例外：  
  
-   **SQLExtendedFetch**并**SQLFetchScroll**使用不同的方法以返回提取的行数。 **SQLExtendedFetch**返回在提取的行数 *\*RowCountPtr*;**SQLFetchScroll**返回直接向通过 SQL_ATTR_ROWS_FETCHED_PTR 指向的缓冲区提取的行数。 有关详细信息，请参阅*RowCountPtr*参数。  
  
-   **SQLExtendedFetch**并**SQLFetchScroll**不同数组中返回每行的状态。 有关详细信息，请参阅*RowStatusArray*参数。  
  
-   **SQLExtendedFetch**并**SQLFetchScroll**使用不同的方法来检索该书签时*FetchOrientation*是 SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支持长度可变的书签从 0 以外的某偏移量处提取行集。 有关详细信息，请参阅*FetchOffset*参数。  
  
-   **SQLExtendedFetch**并**SQLFetchScroll**使用不同的行集大小。 **SQLExtendedFetch**使用 SQL_ROWSET_SIZE 语句属性的值和**SQLFetchScroll**使用 SQL_ATTR_ROW_ARRAY_SIZE 语句属性的值。  
  
-   **SQLExtendedFetch**有略有不同的错误处理语义**SQLFetchScroll**。 有关详细信息，请参阅"中的错误处理"的"注释"部分[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
-   **SQLExtendedFetch**不支持绑定的偏移量 （SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性）。  
  
-   调用**SQLExtendedFetch**不能在其中调用**SQLFetch**或**SQLFetchScroll**，并且如果**SQLBulkOperations**称为提取的任何函数调用之前， **SQLExtendedFetch**不能调用，直到关闭并重新打开游标。 即**SQLExtendedFetch**可仅在语句的状态 S7 中调用。 有关详细信息，请参阅[语句转换](../../../odbc/reference/appendixes/statement-transitions.md)在附录 b:状态转换表。  
  
 当应用程序调用**SQLFetchScroll**时使用的 ODBC 2 *.x*驱动程序，驱动程序管理器将映射到此调用**SQLExtendedFetch**。 有关详细信息，请参阅"SQLFetchScroll 和 ODBC 2 *.x*驱动程序"中[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 在 ODBC 2 *.x*， **SQLExtendedFetch**调用提取多个行和**SQLFetch**调用来提取单个行。 在 ODBC 3 *.x*，但是， **SQLFetch**可以调用来提取多行。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行大容量插入、 更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回数的结果集列|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|将光标置于、 在行集中, 刷新数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
