---
title: SQLNumResultCols 函数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumResultCols
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLNumResultCols
helpviewer_keywords:
- SQLNumResultCols function [ODBC]
ms.assetid: d863179f-12a9-4b55-ac6b-7d84202d3da3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43c7f72869cf46fa12f942a3d31399cf3e316520
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343546"
---
# <a name="sqlnumresultcols-function"></a>SQLNumResultCols 函数
**度**  
 引入的版本:ODBC 1.0 标准符合性:ISO 92  
  
 **摘要**  
 **SQLNumResultCols**返回结果集中的列数。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLNumResultCols(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ColumnCountPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 送语句句柄。  
  
 *ColumnCountPtr*  
 输出一个指针, 指向要在其中返回结果集中的列数的缓冲区。 此计数不包括绑定书签列。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLNumResultCols**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时, 可以通过使用*SQLGetDiagRec 的 HandleType*和*SQL_HANDLE_STMT*的*句柄*调用**StatementHandle**来获取关联的 SQLSTATE 值。 下表列出了通常由**SQLNumResultCols**返回的 SQLSTATE 值, 并对该函数的上下文中的每个值进行了说明:"(DM)" 表示法位于驱动程序管理器返回的 SQLSTATEs 的说明之前。 除非另有说明, 否则与每个 SQLSTATE 值相关联的返回代码为 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驱动程序特定的信息性消息。 (函数返回 SQL_SUCCESS_WITH_INFO。)|  
|08S01|通信链接失败|在函数完成处理之前, 驱动程序与连接到的数据源之间的通信链接失败。|  
|HY000|一般错误|发生了一个错误, 该错误没有特定的 SQLSTATE, 没有为其定义实现特定的 SQLSTATE。 MessageText 缓冲区中**的 SQLGetDiagRec**返回的错误消息描述了错误及其原因。  *\**|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成此函数所需的内存。|  
|HY008|操作已取消|已为*StatementHandle*启用异步处理。 函数被调用, 在完成执行之前, 在*StatementHandle*上调用了**SQLCancel**或**SQLCancelHandle** ;然后, 在*StatementHandle*上再次调用该函数。<br /><br /> 函数被调用, 在完成执行之前, 从多线程应用程序中的另一个线程调用*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函数序列错误|(DM) 为与*StatementHandle*关联的连接句柄调用了异步执行的函数。 调用**SQLNumResultsCols**函数时, 此异步函数仍在执行。<br /><br /> (DM) 为*StatementHandle*调用了**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 并返回了 SQL_PARAM_DATA_AVAILABLE。 在检索所有流式处理参数的数据之前调用此函数。<br /><br /> (DM) 在为*StatementHandle*调用**SQLPrepare**或**SQLExecDirect**之前调用了函数。<br /><br /> (DM) 为*StatementHandle*调用了异步执行的函数 (而不是此函数), 并且在调用此函数时仍在执行。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSETPOS**调用了*StatementHandle*并返回了 SQL_NEED_DATA。 在为所有执行时数据参数或列发送数据之前, 将调用此函数。<br /><br /> 有关如何释放语句句柄的详细信息, 请参阅[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)。|  
|HY013|内存管理错误|未能处理函数调用, 原因可能是由于内存不足而无法访问基础内存对象。|  
|HY117|由于未知的事务状态, 连接被挂起。 仅允许断开连接和只读函数。|(DM) 有关挂起状态的详细信息, 请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|连接超时期限在数据源响应请求之前过期。 连接超时期限通过**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 设置。|  
|IM001|驱动程序不支持此功能|(DM) 与*StatementHandle*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|无论何时使用通知模型, 都将禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**来完成此句柄上先前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING, 并且如果启用了通知模式, 则必须在句柄上调用**SQLCompleteAsync** , 才能执行后处理并完成操作。|  
  
 **SQLNumResultCols**可以返回**SQLPrepare**或**SQLExecute**在**SQLPrepare**之后调用时可以返回的任何**SQLSTATE, 具体**取决于数据源对 SQL 语句进行计算的时间与语句关联的。  
  
## <a name="comments"></a>注释  
 仅当语句处于准备好的、执行或定位状态时, 才能成功调用**SQLNumResultCols** 。  
  
 如果与*StatementHandle*关联的语句未返回列, 则将**SQLNumResultCols** *ColumnCountPtr*设置为0。  
  
 **SQLNumResultCols**返回的列数与 IRD 的 SQL_DESC_COUNT 字段的值相同。  
  
 有关详细信息, 请参阅是否[创建了结果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)以及[如何使用元数据？](../../../odbc/reference/develop-app/how-is-metadata-used.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|正在取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回有关结果集中的列的信息|[SQLColAttribute 函数](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|返回有关结果集中的列的信息|[SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取数据块或滚动结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|按只进方向提取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取部分或全部数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|准备要执行的 SQL 语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|设置游标滚动选项|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
