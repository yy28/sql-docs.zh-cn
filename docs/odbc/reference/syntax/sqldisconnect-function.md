---
title: SQLDisconnect 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61e32c11aafeaf693188a96b48ddd60728ba5bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061455"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLDisconnect**关闭与特定的连接句柄关联的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDisconnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLDisconnect** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01002|断开连接错误|在断开连接期间出错。 但是，已成功断开连接。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|(DM) 的参数中指定的连接*ConnectionHandle*未打开。|  
|25000|事务状态无效|没有参数所指定的连接上的进程中的事务*ConnectionHandle*。 事务保持活动状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*ConnectionHandle*。 调用该函数，并在它之前已完成执行[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*。 然后在再次调用该函数*ConnectionHandle*。<br /><br /> 调用该函数，和之前完成执行**SQLCancelHandle**上调用了*ConnectionHandle*从多线程应用程序中不同的线程。|  
|HY010|函数序列错误|(DM) 的调用以异步方式执行的函数*StatementHandle*与关联*ConnectionHandle*和仍在执行时**SQLDisconnect**是调用。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *ConnectionHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*与相关联*ConnectionHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求，并且连接仍处于活动状态。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*ConnectionHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 如果应用程序调用**SQLDisconnect**后**SQLBrowseConnect**返回 SQL_NEED_DATA，它将返回不同的返回代码之前，该驱动程序取消浏览进程的连接，并返回与未连接状态的连接。  
  
 如果应用程序调用**SQLDisconnect**虽然没有未完成的事务与连接句柄相关联，但驱动程序将返回 SQLSTATE 25000 （无效的事务状态），该值指示该事务不变并且该连接处于打开状态。 未完成的事务是指尚未提交或回滚与**SQLEndTran**。  
  
 如果应用程序调用**SQLDisconnect**释放与连接关联的所有语句之前，该驱动程序，它已成功断开连接数据源后释放这些语句和已的所有描述符在连接上显式分配。 但是，如果一个或多个与连接相关联的语句仍在执行异步**SQLDisconnect** HY010 的 SQLSTATE 值将返回 SQL_ERROR （函数序列错误）。 此外， **SQLDisconnect**将释放所有关联的语句和已显式分配的连接，如果连接处于挂起状态，或如果的所有描述符**SQLDisconnect**是已成功取消**SQLCancelHandle**。  
  
 有关如何使用应用程序信息**SQLDisconnect**，请参阅[断开与数据源或驱动程序的连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>断开与已入池连接的连接  
 如果共享环境中启用连接池和应用程序调用**SQLDisconnect**上在该环境中的连接，连接将返回到连接池，并且仍可用于使用其他组件同一个共享的环境中。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)，并[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|释放连接句柄|[SQLFreeConnect 函数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
