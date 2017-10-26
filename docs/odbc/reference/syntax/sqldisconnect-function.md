---
title: "SQLDisconnect 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af65dee0cfa0efcb4b4daffa55e02dfbebff8473
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLDisconnect**关闭与特定连接句柄关联的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDisconnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDisconnect**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01002|断开连接错误|断开连接期间出错。 但是，已成功断开连接。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) 参数中指定的连接*ConnectionHandle*未打开。|  
|25000|无效的事务状态|没有在自变量所指定的连接上的进程中的事务*ConnectionHandle*。 事务保持活动状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*ConnectionHandle*。 已调用函数，并在它之前完成执行[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*。 然后在再次调用该函数*ConnectionHandle*。<br /><br /> 已调用函数，和之前完成执行**SQLCancelHandle**上调用了*ConnectionHandle*从多线程应用程序中的不同线程。|  
|HY010|函数序列错误|(DM) 以异步方式执行的函数曾为*StatementHandle*与关联*ConnectionHandle*和仍在执行时**SQLDisconnect**已调用。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*ConnectionHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*与关联*ConnectionHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求，而该连接仍处于活动状态。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*ConnectionHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 如果应用程序调用**SQLDisconnect**后**SQLBrowseConnect**返回 SQL_NEED_DATA，它将返回不同的返回代码之前，该驱动程序取消浏览进程的连接，并返回到未连接状态的连接。  
  
 如果应用程序调用**SQLDisconnect**驱动程序时没有与连接句柄关联的未完成事务，返回 SQLSTATE 25000 （无效的事务状态），该值指示事务为不变和的连接已打开。 未完成的事务是指尚未提交或回滚与**SQLEndTran**。  
  
 如果应用程序调用**SQLDisconnect**它已释放与连接关联的所有语句之前，该驱动程序，它已成功断开连接从数据源后将释放这些语句和所有已的描述符显式分配连接上。 但是，如果一个或多个与连接相关联的语句仍在执行异步， **SQLDisconnect** SQLSTATE 值为 HY010 返回 SQL_ERROR （函数序列错误）。 此外， **SQLDisconnect**将释放所有关联的语句和所有已显式分配连接，连接是否处于挂起状态，或如果的描述符**SQLDisconnect**已已成功取消**SQLCancelHandle**。  
  
 有关应用程序如何使用信息**SQLDisconnect**，请参阅[断开与数据源或驱动程序的连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>断开与已入池连接的连接  
 如果共享环境的情况下启用连接池和应用程序调用**SQLDisconnect**在该环境中连接时，该连接返回到连接池，仍可供使用的其他组件相同的共享的环境中。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)，和[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|释放连接句柄|[SQLFreeConnect 函数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

