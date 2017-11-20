---
title: "SQLDescribeCol 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a6fcf834f88a1ecc609b56a0f8f493ee5a3c1ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLDescribeCol**返回的结果描述符 — 列名称、 类型、 列大小、 十进制数字和为空性-对于结果中的一个列设置。 此信息也是可用的 IRD 字段中。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ColumnNumber*  
 [输入]结果数据的列数按不断增加的列顺序，从 1 开始按顺序排序。 *ColumnNumber*自变量也可以设置为 0 来描述书签列。  
  
 *列名称*  
 [输出]指向以 null 结尾的缓冲区中要返回的列名称。 从 IRD SQL_DESC_NAME 字段读取此值。 如果列是未命名或无法确定列名称，该驱动程序将返回空字符串。  
  
 如果*ColumnName*为 NULL， *NameLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回指向的缓冲区中*ColumnName*。  
  
 *BufferLength*  
 [输入]长度 **ColumnName*缓冲区，以字符为单位。  
  
 *NameLengthPtr*  
 [输出]指向要返回的字符 （不包括 null 终止） 总数在其中缓冲区的指针可用于返回在\* *ColumnName*。 可用于返回的字符数是否大于或等于*BufferLength*中的列名称\* *ColumnName*截断为*BufferLength*减 null 终止字符的长度。  
  
 *DataTypePtr*  
 [输出]指向在其返回列的 SQL 数据类型的缓冲区的指针。 从 IRD SQL_DESC_CONCISE_TYPE 字段读取此值。 这将是中的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)，或特定于驱动程序的 SQL 数据类型。 如果不确定的数据类型，该驱动程序将返回 SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3。*x*，在中返回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*有关日期、 时间或时间戳数据分别; 在 ODBC 2。*x*，SQL_DATE、 SQL_TIME 或 SQL_TIMESTAMP 返回。 驱动程序管理器执行的所需的映射时 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序或当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序。  
  
 当*ColumnNumber*等于 SQL_BINARY 中为 0 （对于书签列），则返回 *\*DataTypePtr*用于长度可变的书签。 （如果由 ODBC 3 使用书签，则返回 SQL_INTEGER。*x*应用程序使用 ODBC 2。*x*驱动程序或通过 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序。)  
  
 对这些数据类型的详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型中。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。  
  
 *ColumnSizePtr*  
 [输出]指向在其上数据源返回列的大小 （以字符为单位） 的缓冲区的指针。 如果无法确定列大小，该驱动程序将返回 0。 列大小的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。  
  
 *DecimalDigitsPtr*  
 [输出]指向在其上数据源返回的列的十进制位数的缓冲区的指针。 如果的十进制位数无法确定或不适用，则该驱动程序返回 0。 十进制数字的详细信息，请参阅[列大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附录 d： 数据类型中。  
  
 *NullablePtr*  
 [输出]指向在其中以返回一个值，该值指示列是否允许 NULL 值的缓冲区的指针。 从 IRD SQL_DESC_NULLABLE 字段读取此值。 值为下列其中一项：  
  
 SQL_NO_NULLS: 列不允许 NULL 值。  
  
 SQL_NULLABLE: 列允许 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN： 驱动程序无法确定列是否允许 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDescribeCol**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDescribeCol**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *ColumnName*不是否足够大以返回整个列名称，因此，列名称已被截断。 在中返回未截断的列名称的长度 **NameLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07005|不准备语句*光标规范*|与相关的语句*StatementHandle*未返回结果集。 未描述的列。|  
|07009|无效的描述符索引|(DM) 值的参数的指定*ColumnNumber*等于 0，且 SQL_ATTR_USE_BOOKMARKS 语句选项为 SQL_UB_OFF。<br /><br /> 为参数指定的值*ColumnNumber*大于结果集中的列数。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配失败|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLDescribeCol**调用。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) 在调用之前调用该函数**SQLPrepare**， **SQLExecute**，或该语句句柄上的目录函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*BufferLength*小于 0。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
 **SQLDescribeCol**可以返回可以由任何 SQLSTATE **SQLPrepare**或**SQLExecute**时之后调用**SQLPrepare**和之前**SQLExecute**，取决于当数据源的计算结果与语句句柄关联的 SQL 语句。  
  
 出于性能原因，应用程序不应调用**SQLDescribeCol**之前执行语句。  
  
## <a name="comments"></a>注释  
 应用程序通常调用**SQLDescribeCol**后调用**SQLPrepare**和调用之前还是之后关联到**SQLExecute**。 应用程序还可以调用**SQLDescribeCol**后调用**SQLExecDirect**。 有关详细信息，请参阅[结果设置元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**中检索列名称、 类型和长度由生成**选择**语句。 如果列是一个表达式，**ColumnName*是空字符串或驱动程序定义的名称。  
  
> [!NOTE]  
>  ODBC 作为扩展，即使 Open Group 和 SQL 访问组调用级别接口规范中未指定的选项都支持 SQL_NULLABLE_UNKNOWN **SQLDescribeCol**。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回的列的相关信息|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取数据的多个的行|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回的结果数设置列|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行的语句|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

