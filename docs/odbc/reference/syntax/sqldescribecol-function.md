---
title: SQLDescribeCol 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d179e7da0b53dbff66c8a3262f68fc4c3fa89df8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537713"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLDescribeCol**为结果集中的一列返回的结果描述符的列名称、 类型、 列大小、 十进制数和为 null 性的。 此信息也是可用的 IRD 字段中。  
  
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
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ColumnNumber*  
 [输入]结果数据的列数在不断增加的列顺序，从 1 开始按顺序排序。 *ColumnNumber*参数还可以将设置为 0 来描述书签列。  
  
 *ColumnName*  
 [输出]指向以 null 结尾的缓冲区中要返回的列名称。 从 IRD 的 SQL_DESC_NAME 字段读取此值。 如果列是未命名或不能确定列名称，该驱动程序将返回空字符串。  
  
 如果*ColumnName*为 NULL， *NameLengthPtr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回通过指向的缓冲区中*ColumnName*。  
  
 *BufferLength*  
 [输入]长度 **ColumnName*缓冲区，以字符为单位。  
  
 *NameLengthPtr*  
 [输出]指向用于返回的字符 （不包括 null 终止） 总数的缓冲区可用于在中返回\* *ColumnName*。 可用于返回的字符数是否大于或等于*BufferLength*中的列名称\* *ColumnName*截断为*BufferLength*减去 null 终止字符的长度。  
  
 *DataTypePtr*  
 [输出]指向用于返回 SQL 数据类型的列的缓冲区的指针。 从 IRD 的 SQL_DESC_CONCISE_TYPE 字段读取此值。 这将是中的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)，或特定于驱动程序的 SQL 数据类型。 如果不确定的数据类型，该驱动程序返回 SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3。*x*，返回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*日期、 时间或时间戳数据的 ODBC 2 中分别;。*x*，则返回 SQL_DATE、 SQL_TIME 或 SQL_TIMESTAMP。 驱动程序管理器执行所需的映射时 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序或当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序。  
  
 当*ColumnNumber*等于 SQL_BINARY 中为 0 （表示书签列），则返回 *\*DataTypePtr*长度可变的书签。 （如果书签由 ODBC 3，则返回 SQL_INTEGER。*x*应用程序使用 ODBC 2。*x*驱动程序或通过 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序。)  
  
 这些数据类型的详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)中附录 d:数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。  
  
 *ColumnSizePtr*  
 [输出]指向在其上数据源返回的列的大小 （以字符为单位） 的缓冲区的指针。 如果无法确定列大小，该驱动程序将返回 0。 列大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。  
  
 *DecimalDigitsPtr*  
 [输出]指向在其上数据源返回的列的小数位数的缓冲区的指针。 如果小数位数不能确定或不适用，则驱动程序将返回 0。 十进制数字的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)中附录 d:数据类型。  
  
 *NullablePtr*  
 [输出]指向用于返回一个值，指示列是否允许 NULL 值的缓冲区。 从 IRD 的 SQL_DESC_NULLABLE 字段读取此值。 值为以下值之一：  
  
 SQL_NO_NULLS:此列不允许 NULL 值。  
  
 SQL_NULLABLE:列允许 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN:该驱动程序无法确定列是否允许 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDescribeCol**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDescribeCol** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *ColumnName*是否不足够大以返回整个列名称，因此列名称已被截断。 在返回未截断的列名称的长度 **NameLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07005|预定义语句不*游标规范*|与相关的语句*StatementHandle*未返回结果集。 没有任何列来描述。|  
|07009|描述符索引无效|(DM) 的参数指定的值*ColumnNumber*等于 0，而 SQL_ATTR_USE_BOOKMARKS 语句选项是 SQL_UB_OFF。<br /><br /> 为参数指定的值*ColumnNumber*大于结果集中的列数。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配失败|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLDescribeCol**调用。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) 在调用之前已调用函数**SQLPrepare**， **SQLExecute**，或该语句句柄上的目录函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*BufferLength*小于 0。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
 **SQLDescribeCol**可以返回任何可由返回的 SQLSTATE **SQLPrepare**或**SQLExecute**时后，调用**SQLPrepare**之前**SQLExecute**，取决于当数据源的计算结果与语句句柄相关联的 SQL 语句。  
  
 出于性能原因，应用程序不应调用**SQLDescribeCol**语句之前执行。  
  
## <a name="comments"></a>注释  
 应用程序通常会调用**SQLDescribeCol**后调用**SQLPrepare**和之前或之后对的关联调用**SQLExecute**。 应用程序还可以调用**SQLDescribeCol**后调用**SQLExecDirect**。 有关详细信息，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**检索的列名称、 类型和长度 パ**选择**语句。 如果列是表达式，**ColumnName*是空字符串或驱动程序定义的名称。  
  
> [!NOTE]  
>  ODBC 作为扩展，即使 Open Group 和 SQL 访问组调用级别接口规范未指定的选项都支持 SQL_NULLABLE_UNKNOWN **SQLDescribeCol**。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在结果集中返回列的相关信息|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|正在提取多行数据|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|返回数的结果集列|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|准备执行的语句|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
