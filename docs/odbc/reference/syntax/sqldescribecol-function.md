---
title: SQLDescribeCol 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301167"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLDescribeCol**返回结果集中一列的结果描述符 - 列名、类型、列大小、十进制数字和空度。 此信息也可在税务局的字段中查阅。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]语句句柄。  
  
 ColumnNumber   
 [输入]按增加列顺序按顺序排序的结果数据的列编号，从 1 开始。 列*数*参数也可以设置为 0 来描述书签列。  
  
 *ColumnName*  
 [输出]指向用于返回列名称的 null 端结束的缓冲区的指针。 此值从 IRD 的SQL_DESC_NAME字段中读取。 如果列未命名或无法确定列名称，则驱动程序将返回一个空字符串。  
  
 如果*列名*为*NULL，NameLengthPtr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可在*列名*指向的缓冲区中返回。  
  
 *缓冲区长度*  
 [输入]**列名*缓冲区的长度（以字符表示）。  
  
 *名称长度 Ptr*  
 [输出]指向要返回\**列名*中返回的字符总数（不包括空终止）的缓冲区的指针。 如果可返回的字符数大于或等于*BufferLength，* 则\**列名中的列*名称将截断为 *"缓冲区长度*"减去空终止字符的长度。  
  
 *数据类型Ptr*  
 [输出]指向要返回列的 SQL 数据类型的缓冲区的指针。 此值从 IRD 的SQL_DESC_CONCISE_TYPE字段中读取。 这将是[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)或特定于驱动程序的 SQL 数据类型中的值之一。 如果无法确定数据类型，驱动程序将返回SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3 中。*x*x、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP分别在*\*DataTypePtr*中返回日期、时间或时间戳数据;在 ODBC 2 中。*x*返回 SQL_DATE、SQL_TIME 或SQL_TIMESTAMP。 当 ODBC 2 时，驱动程序管理器执行所需的映射。*x*应用程序使用 ODBC 3。*x*驱动程序或当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序。  
  
 当*列数*等于 0（对于书签列），SQL_BINARY在*\*DataTypePtr*中返回，用于可变长度书签。 （如果 ODBC 3 使用书签，则返回SQL_INTEGER。*x*应用程序使用 ODBC 2。*x*驱动程序或 ODBC 2。*x*使用 ODBC 3 的应用程序。*x*驱动程序。  
  
 有关这些数据类型的详细信息，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。  
  
 *列大小器*  
 [输出]指向要在数据源上返回列大小（以字符）的缓冲区的指针。 如果无法确定列大小，驱动程序返回 0。 有关列大小的详细信息，请参阅附录 D：数据类型中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *十进制数字Ptr*  
 [输出]指向要返回数据源上列的小数位数的缓冲区的指针。 如果无法确定或不适用小数位数，则驱动程序返回 0。 有关十进制数字的详细信息，请参阅附录 D 中的[列大小、十进制数字、传输八字长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)：数据类型。  
  
 *空可点*  
 [输出]指向要返回指示列是否允许 NULL 值的值的缓冲区的指针。 此值从 IRD 的SQL_DESC_NULLABLE字段中读取。 该值为以下值之一：  
  
 SQL_NO_NULLS：该列不允许 NULL 值。  
  
 SQL_NULLABLE：该列允许 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN：驱动程序无法确定列是否允许 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDescribeCol**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT*Handle*的*句柄类型*和*语句句柄*。 下表列出了**SQLDescribeCol**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\**列名*不够大，无法返回整个列名称，因此列名称被截断。 未压缩的列名称的长度在 #*NameLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07005|已准备好的语句不是*游标规范*|与*语句句柄*关联的语句未返回结果集。 没有要描述的列。|  
|07009|无效描述符索引|（DM） 为参数*列编号*指定的值等于 0，SQL_ATTR_USE_BOOKMARKS 语句选项SQL_UB_OFF。<br /><br /> 为参数*ColumnNumber*指定的值大于结果集中的列数。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配失败|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLDescribeCol**时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） 在调用**SQLPrepare、SQLExecute****SQLExecute**或语句句柄上的目录函数之前调用函数。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*BufferLength*指定的值小于 0。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
 **SQLDescribeCol**可以返回**SQLPrepare**或**SQLExecute**可在**SQLPrepare**之后和**SQLExecute**之前调用时返回的任何 SQLSTATE，具体取决于数据源何时计算与语句句柄关联的 SQL 语句。  
  
 出于性能原因，应用程序在执行语句之前不应调用**SQLDescribeCol。**  
  
## <a name="comments"></a>注释  
 应用程序通常在调用**SQLPrepare**后以及关联调用 SQLExecute 之前或之后调用**SQLDescribeCol。** **SQLExecute** 应用程序也可以调用**SQLExecDirect**后调用**SQLDescribeCol。** 有关详细信息，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**检索**SELECT**语句生成的列名称、类型和长度。 如果列是表达式，则 **列名*是空字符串或驱动程序定义的名称。  
  
> [!NOTE]  
>  ODBC 支持SQL_NULLABLE_UNKNOWN作为扩展，即使开放组和 SQL 访问组调用级别接口规范未指定**SQLDescribeCol**的选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中列的信息|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|获取多行数据|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回结果集列数|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行语句|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
