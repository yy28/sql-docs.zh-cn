---
title: SQL 扩展获取功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285977"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 **SQLExtendedFetch**从结果集中获取指定的数据行集，并返回所有绑定列的数据。 行集可以在绝对或相对位置或通过书签指定。  
  
> [!NOTE]
>  在 ODBC 3 *.x*中 **，SQL 扩展获取**已被**SQLFetchScroll**替换。 ODBC 3 *.x*应用程序不应调用**SQL 扩展获取**;相反，他们应该调用**SQLFetchScroll。** 使用 ODBC 2 *.x*驱动程序时，驱动程序管理器将**SQLFetchScroll**映射到**SQL 扩展获取**。 如果 ODBC 3 *.x*驱动程序想要与调用它的 ODBC 2 *.x*应用程序配合使用，则应支持**SQLExtendedFetch。** 有关详细信息，请参阅附录 G 中的"注释"和[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)：向后兼容性的驱动程序指南。  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 *提取方向*  
 [输入]提取的类型。 这与**SQLFetchScroll**中的 *"获取方向"* 相同。  
  
 *提取偏移*  
 [输入]要提取的行数。 这与**SQLFetchScroll**中的*提取偏移*相同，但有一个例外。 当*取取方向*SQL_FETCH_BOOKMARK时 *，FetchOffset*是固定长度的书签，而不是书签的偏移量。 换句话说 **，SQLExtendedFetch**从此参数检索书签，而不是SQL_ATTR_FETCH_BOOKMARK_PTR语句属性。 它不支持可变长度书签，不支持从书签的偏移量（0 以外的）提取行集。  
  
 *罗CountPtr*  
 [输出]指向要返回实际提取的行数的缓冲区的指针。 此缓冲区的使用方式与SQL_ATTR_ROWS_FETCHED_PTR语句属性指定的缓冲区相同。 此缓冲区仅由**SQL 扩展获取**使用。 它不被**SQLFetch**或**SQLFetchScroll**使用。  
  
 *行状态数组*  
 [输出]指向要返回每行状态的数组的指针。 此数组的使用方式与SQL_ATTR_ROW_STATUS_PTR语句属性指定的数组相同。  
  
 但是，此数组的地址不会存储在 IRD 中SQL_DESC_STATUS_ARRAY_PTR字段中。 此外，此数组仅在**SQL****扩展获取**后调用时由 SQL 扩展*Operation*获取和**SQLBulk 操作**使用，操作SQL_ADD或**SQLSetPos。** 它不由**SQLFetch**或**SQLFetchScroll**使用 ，并且**SQLBulk 操作**或**SQLSetPos**在**SQLFetch**或**SQLFetchScroll**之后调用时不使用它。 在调用任何提取函数之前调用具有SQL_ADD*操作*的**SQLBulk 操作**时，也不会使用它。 换句话说，它仅在语句状态 S7 中使用。 它不用于语句状态 S5 或 S6。 有关详细信息，请参阅附录 B[中的语句转换](../../../odbc/reference/appendixes/statement-transitions.md)：ODBC 状态转换表。  
  
 应用程序应在*RowStatusArray*参数中提供有效的指针;否则 **，SQL扩展获取**的行为以及**SQL 扩展获取**定位游标后对**SQLBulk 操作**或**SQLSetPos**的调用行为未定义。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLExtendedFetch**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLError**获得关联的 SQLSTATE 值。 下表列出了**SQLAofFetch**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。 如果单个列上发生错误，可以使用 SQL_DIAG_COLUMN_NUMBER*的 Diag标识符*调用**SQLGetDiagField**以确定错误发生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER*的 Diag标识符*调用，以确定包含该列的行。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|为列返回的字符串或二进制数据导致非空白字符或非 NULL 二进制数据的截断。 如果它是一个字符串值，它是右截断的。 如果是数值，则数字的小数部分将被截断。  （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S01|行中的错误|获取一个或多个行时出错。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S06|尝试在结果集返回第一个行集之前提取|当当前位置超出第一行时，请求的行集与结果集的开始重叠，要么*Fetch方向*SQL_PRIOR，要么*Fetch方向*SQL_RELATIVE，其绝对值小于或等于当前SQL_ROWSET_SIZE的负*FetchOffset。* （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分数截断|为列返回的数据被截断。 对于数字数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|数据值无法转换为**SQLBindCol**中*TargetType*指定的 C 数据类型。|  
|07009|无效描述符索引|列 0 与**SQLBindCol**绑定，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22002|需要指标变量，但未提供|NULL 数据被提取到一个列中，该列*的 StrLen_or_IndPtr*由**SQLBindCol**设置为空指针。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|22003|数值超范围|返回一个或多个列的数值（作为数字或字符串）将导致数字的整个部分（而不是小数）被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> 有关详细信息，请参阅附录 D：数据类型中[间隔和数字数据类型的准则](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)。|  
|22007|无效日期时间格式|结果集中的字符列绑定到日期、时间或时间戳 C 结构，并且列中的值分别是无效的日期、时间或时间戳。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|22012|除零|返回算术表达式中的值，结果除以零。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|22015|间隔字段溢出|从精确数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> 将数据提取到间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|22018|强制转换规范的无效字符值|C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|24000|无效的游标状态|*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLError**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**在*语句句柄*上调用 ，然后在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQL 扩展获取**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） SQLExtendedFetch 在调用**SQLFetch**或**SQLFetchScroll**后，在使用SQL_CLOSE选项调用**SQLFreeStmt**之前，为*语句处理*调用了**SQLAa，** 用于语句处理。<br /><br /> （DM） **SQLBulk操作**在调用**SQLFetch、SQLFetchScroll**或 SQL**扩展获取**之前调用了语句，然后在使用SQL_CLOSE选项调用**SQLFreeStmt**之前调用 SQL**扩展获取**。 **SQLFetchScroll**|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY106|提取类型范围外|（DM） 为参数 Fetch*方向*指定的值无效。 （请参阅"注释"。<br /><br /> 参数*Fetch 方向*已SQL_FETCH_BOOKMARK，并且SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE语句选项的值SQL_CURSOR_FORWARD_ONLY，并且参数*Fetch 方向*的值不SQL_FETCH_NEXT。<br /><br /> 争论*Fetch定向*是SQL_FETCH_RESUME。|  
|HY107|行值范围外|使用SQL_CURSOR_TYPE语句选项指定的值SQL_CURSOR_KEYSET_DRIVEN，但使用SQL_KEYSET_SIZE语句属性指定的值大于 0，小于使用 SQL_ROWSET_SIZE 语句属性指定的值。|  
|HY111|无效书签值|SQL_FETCH_BOOKMARK，在*FetchOffset*参数中指定的书签无效。 *FetchOffset*|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持指定的提取类型。<br /><br /> 驱动程序或数据源不支持**SQLBindCol**中的*TargetType*和相应列的 SQL 数据类型的组合指定的转换。 仅当列的 SQL 数据类型映射到特定于驱动程序的 SQL 数据类型时，此错误才适用。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**SQLSetStmtOption**SQL_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLExfetch**的行为与**SQLFetchScroll**的行为相同，但有以下例外：  
  
-   **SQL扩展获取**和**SQLFetch**使用不同的方法来返回提取的行数。 **SQLExtendedFetch**返回*\*在 RowCountPtr*中获取的行数;**SQLFetchScroll**返回直接提取到SQL_ATTR_ROWS_FETCHED_PTR指向的缓冲区的行数。 有关详细信息，请参阅*RowCountPtr*参数。  
  
-   **SQL扩展获取**和**SQLFetchScroll**返回不同数组中每行的状态。 有关详细信息，请参阅*行状态数组*参数。  
  
-   **SQL扩展获取**和**SQLScroll**使用不同的方法来检索书签，当*取取方向*SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支持可变长度书签或从书签中从 0 以外的偏移量提取行集。 有关详细信息，请参阅*提取偏移参数*。  
  
-   **SQL 扩展获取**和**SQLFetch**使用不同的行集大小。 **SQLExtendedFetch**使用SQL_ROWSET_SIZE语句属性的值 **，SQLFetchScroll**使用SQL_ATTR_ROW_ARRAY_SIZE语句属性的值。  
  
-   **SQLExtendedFetch**具有与**SQLFetchScroll**略有不同的错误处理语义。 有关详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)的"注释"部分中的"错误处理"。  
  
-   **SQLExtendedFetch**不支持绑定偏移量（SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性）。  
  
-   对**SQL 扩展提取的**调用不能与**SQLFetch**或**SQLFetchScroll**的调用混合，如果在调用任何提取函数之前调用**SQLBulk 操作，** 则在关闭和重新打开游标之前无法调用**SQLExtendedFetch。** 也就是说 **，SQLExtendedFetch**只能在语句状态 S7 下调用。 有关详细信息，请参阅附录 B[中的语句转换](../../../odbc/reference/appendixes/statement-transitions.md)：ODBC 状态转换表。  
  
 当应用程序使用 ODBC 2 *.x*驱动程序调用**SQLFetchScroll**时，驱动程序管理器将此调用映射到**SQL 扩展获取**。 有关详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)中的"SQLFetchScroll 和 ODBC 2 *.x*驱动程序"。  
  
 在 ODBC 2 *.x*中，调用**SQL 扩展获取**以获取多行，并调用**SQLFetch**来获取一行。 另一方面，在 ODBC 3 *.x*中，可以调用**SQLFetch**来获取多行。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行批量插入、更新或删除操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回结果集列数|[SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位光标、刷新行集中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
