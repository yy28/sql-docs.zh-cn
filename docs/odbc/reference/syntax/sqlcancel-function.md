---
title: SQLCancel 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ad701efe914780a74bba3b8f0530b4881d7709
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537631"
---
# <a name="sqlcancel-function"></a>SQLCancel 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLCancel**取消上一个语句的处理。  
  
 若要取消连接或语句的处理，请使用[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCancel**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLCancel** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)参数中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLCancel**调用函数。<br /><br /> (DM) 取消操作失败，因为与之关联的连接句柄上正在执行异步操作*StatementHandle*。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY018|服务器拒绝取消请求|服务器拒绝了取消请求。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 **SQLCancel**可以取消以下类型的一个语句上的处理：  
  
-   在帐单上以异步方式运行的函数。  
  
-   需要数据的语句上一个函数。  
  
-   在另一个线程中的语句上运行的函数。  
  
 在 ODBC 2。*x*，如果应用程序调用**SQLCancel**语句上不执行任何处理，是当**SQLCancel**具有相同的效果**SQLFreeStmt** SQL_CLOSE 选项;仅出于完整性的考虑定义此行为和应用程序应调用**SQLFreeStmt**或**SQLCloseCursor**关闭游标。  
  
 当**SQLCancel**调用来取消异步运行一个语句或函数中，会清除的数据需求，由函数正在取消发布的诊断记录，对语句的函数和**SQLCancel**将发布其自身的诊断记录; 当**SQLCancel**称为若要取消的语句，另一个线程上运行的函数，但是，它不会清除诊断的记录不取消函数而不会发布其自身的诊断记录。  
  
## <a name="canceling-asynchronous-processing"></a>取消异步处理  
 应用程序以异步方式调用一个函数后，它会调用重复用于确定它是否已完成处理的函数。 如果该函数仍在处理，它将返回 SQL_STILL_EXECUTING。 如果该函数已完成处理，则会返回不同的代码。  
  
 任何返回 SQL_STILL_EXECUTING 函数调用后，应用程序可以调用**SQLCancel**取消函数。 如果取消请求成功，驱动程序返回 SQL_SUCCESS。 此消息并不表示，该函数已实际取消;它指示已处理取消请求。 时，或如果实际取消该函数是依赖于驱动程序的代码和数据源决定。 应用程序必须继续调用原始函数，直到返回代码不是 SQL_STILL_EXECUTING。 如果已成功取消该函数，返回代码是 SQL_ERROR 并且 SQLSTATE HY008 （已取消的操作）。 如果该函数完成其正常处理，返回代码是 SQL_SUCCESS 或如果该函数成功，则 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 并且以外 HY008 SQLSTATE （已取消的操作） 如果失败的函数。  
  
> [!NOTE]  
>  在 ODBC 3.5 中，调用**SQLCancel**不会进行处理的语句上完成的时不会视为**SQLFreeStmt**使用 SQL_CLOSE 选项，但具有根本不起作用。 若要关闭游标，应用程序应调用**SQLCloseCursor**，而非**SQLCancel**。  
  
 有关异步处理的详细信息，请参阅[异步执行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。  
  
## <a name="canceling-functions-that-need-data"></a>正在取消需要数据的函数  
 之后**SQLExecute**或**SQLExecDirect**返回 SQL_NEED_DATA 和数据已发送的所有执行时数据参数之前，应用程序可以调用**SQLCancel**取消语句执行。 取消该语句后，应用程序可以调用**SQLExecute**或**SQLExecDirect**试。 有关详细信息，请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 之后**SQLBulkOperations**或**SQLSetPos**返回 SQL_NEED_DATA 和数据已发送的所有执行时数据列之前，应用程序可以调用**SQLCancel**若要取消该操作。 已取消该操作后，应用程序可以调用**SQLBulkOperations**或**SQLSetPos**再次取消不会影响游标状态或当前光标位置。 有关详细信息，请参阅[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>正在取消其他线程上执行的函数  
 在多线程应用程序中，应用程序可以取消在另一个线程运行的函数。 若要取消应用程序调用函数**SQLCancel**与由目标函数中，而另一个线程上使用的相同的语句句柄。 如何取消该函数依赖于驱动程序和操作系统。 如取消以异步方式运行的返回代码的函数中所示**SQLCancel**仅指示驱动程序是否已成功处理该请求。 可以返回仅 SQL_SUCCESS 或 SQL_ERROR;未不返回任何诊断信息。 如果原始函数已取消，它将返回 SQL_ERROR 和 SQLSTATE HY008 （已取消的操作）。  
  
 如果 SQL 语句时执行**SQLCancel**上另一个线程取消语句执行调用，则可能会成功执行和取消时返回 SQL_SUCCESS 也是成功。 在这种情况下，驱动程序管理器假定使应用程序将无法再使用游标通过取消，关闭打开的语句执行游标。  
  
 关于线程处理的详细信息，请参阅[多线程处理](../../../odbc/reference/develop-app/multithreading.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|执行大容量插入或更新操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消异步上运行连接句柄，此外对功能的一个函数**SQLCancel**。|[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|释放语句句柄|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|获取诊断记录的字段或诊断标头的字段|[SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|获取多个字段的诊断数据结构|[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|返回下一个参数将数据发送用于|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|将光标放置在行集中，刷新的行集中的数据或更新或删除结果集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
