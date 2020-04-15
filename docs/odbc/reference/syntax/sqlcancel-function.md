---
title: SQL取消功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301307"
---
# <a name="sqlcancel-function"></a>SQLCancel 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLCancel**取消语句的处理。  
  
 要取消连接或语句的处理，请使用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCancel**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_STMT的*句柄类型*和*语句句柄*。 下表列出了**SQLCancel**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)在参数*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLCancel**函数时，此异步函数仍在执行。<br /><br /> （DM） 取消操作失败，因为与*语句句柄*关联的连接句柄正在进行异步操作。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY018|服务器拒绝取消请求|服务器拒绝了取消请求。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLCancel**可以取消语句上的以下类型处理：  
  
-   在语句上异步运行的函数。  
  
-   需要数据的语句上的函数。  
  
-   在另一个线程上的语句上运行的函数。  
  
 在 ODBC 2 中。*x，* 如果应用程序在未对语句执行处理时调用**SQLCancel，** 则**SQLCancel**具有与**SQLFreeStmt**与 SQL_CLOSE 选项相同的效果;此行为仅针对完整性而定义，应用程序应调用**SQLFreeStmt**或**SQLCloseCursor**来关闭游标。  
  
 当调用**SQLCancel**以取消在语句或需要数据的语句上异步运行的函数时，将清除被取消的函数发布的诊断记录，并且**SQLCancel**发布自己的诊断记录;但是，当**SQLCancel**调用以取消在另一个线程上的语句上运行的函数时，它不会清除正在取消的函数的诊断记录，也不会发布自己的诊断记录。  
  
## <a name="canceling-asynchronous-processing"></a>取消异步处理  
 应用程序异步调用函数后，它会重复调用该函数以确定它是否已完成处理。 如果函数仍在处理中，它将返回SQL_STILL_EXECUTING。 如果函数已完成处理，它将返回其他代码。  
  
 对返回SQL_STILL_EXECUTING的函数进行任何调用后，应用程序可以调用**SQLCancel**来取消该函数。 如果取消请求成功，驱动程序将返回SQL_SUCCESS。 此消息不指示该函数实际上已取消;因此，该功能未表示该函数已取消。它表示已处理取消请求。 当或如果实际取消该函数时，则与驱动程序相关且与数据源相关。 应用程序必须继续调用原始函数，直到返回代码不SQL_STILL_EXECUTING。 如果已成功取消该功能，则返回代码SQL_ERROR SQLSTATE HY008（操作已取消）。 如果函数完成正常处理，则返回代码将SQL_SUCCESS或SQL_SUCCESS_WITH_INFO如果函数成功或SQL_ERROR，并且如果函数失败，则为 HY008 以外的 SQLSTATE（操作已取消）。  
  
> [!NOTE]  
>  在 ODBC 3.5 中，对**SQLCancel**的调用，当语句未执行任何处理时，不会被视为使用 SQL_CLOSE 选项的**SQLFreeStmt，** 但根本没有效果。 要关闭游标，应用程序应调用**SQLCloseCursor**，而不是**SQLCancel**。  
  
 有关异步处理的详细信息，请参阅[异步执行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。  
  
## <a name="canceling-functions-that-need-data"></a>取消需要数据的函数  
 **在 SQLExecute**或**SQLExecDirect**返回SQL_NEED_DATA并在为所有数据执行参数发送数据之前，应用程序可以调用**SQLCancel**取消语句执行。 取消语句后，应用程序可以再次调用**SQLExecute**或**SQLExecDirect。** 有关详细信息，请参阅[SQLBind参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 **在 SQLBulk 操作**或**SQLSetPos**返回SQL_NEED_DATA后，在为执行时的所有数据发送数据之前，应用程序可以调用**SQLCancel**来取消该操作。 操作取消后，应用程序可以再次调用**SQLBulk 操作**或**SQLSetPos;** 取消不会影响光标状态或当前游标位置。 有关详细信息，请参阅[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>取消在另一个线程上执行的函数  
 在多线程应用程序中，应用程序可以取消在另一个线程上运行的函数。 要取消该函数，应用程序调用**SQLCancel**时，使用与目标函数使用的相同语句句柄，但调用不同的线程。 如何取消功能取决于驱动程序和操作系统。 与取消异步运行的函数一样 **，SQLCancel**的返回代码仅指示驱动程序是否成功处理了请求。 只能返回SQL_SUCCESS或SQL_ERROR;未返回任何诊断信息。 如果原始函数被取消，它将返回SQL_ERROR和 SQLSTATE HY008（操作已取消）。  
  
 如果在调用另一个线程上的**SQLCancel**取消语句执行时正在执行 SQL 语句，则在执行成功并返回SQL_SUCCESS，而取消也成功。 在这种情况下，驱动程序管理器假定语句执行打开的游标被取消关闭，因此应用程序将无法使用游标。  
  
 有关线程的详细信息，请参阅[多线程](../../../odbc/reference/develop-app/multithreading.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|执行批量插入或更新操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|除了**SQLCancel**的功能外，取消在连接句柄上异步运行的函数。|[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放语句句柄|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|获取诊断记录的字段或诊断标头的字段|[SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|获取诊断数据结构的多个字段|[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|返回下一个参数以发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|将光标定位在行集中、刷新行集中中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
