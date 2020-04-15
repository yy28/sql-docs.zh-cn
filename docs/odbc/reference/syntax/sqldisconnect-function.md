---
title: SQL断开功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301147"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLDISCONNECT**将关闭与特定连接句柄关联的连接。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDisconnect**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_DBC的*句柄类型*和*连接句柄*。 下表列出了**SQLDISCONNECT**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01002|断开连接错误|断开连接期间出错。 但是，断开连接成功。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|（DM） 参数*ConnectHandle*中指定的连接未打开。|  
|25000|无效事务状态|在参数*ConnectHandle*指定的连接上存在一个事务。 事务保持活动状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|为*连接句柄*启用了异步处理。 调用该函数，并在它fins执行[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)之前在*ConnectHandle*上调用。 然后在*连接处理*上再次调用该函数。<br /><br /> 调用该函数，并在它执行完**SQLCancelHandle**之前从多线程应用程序中的不同线程调用*了 ConnectHandle。*|  
|HY010|函数序列错误|（DM） 与*ConnectHandle*关联的*语句句柄*调用异步执行函数，并在调用**SQLDISCONNECT**时仍在执行。<br /><br /> （DM） 为*ConnectHandle*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用一个语句句柄，该*语句句柄*与*连接句柄*相关联并返回SQL_NEED_DATA。 **SQLExecute** **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|连接超时期限在数据源响应请求之前过期，并且连接仍然处于活动状态。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*连接句柄*关联的驱动程序不支持该功能。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 如果应用程序在**SQLBrowseConnect**返回SQL_NEED_DATA后调用**SQLDisconnect，** 并在返回其他返回代码之前，驱动程序将取消连接浏览过程，并将连接返回到未连接状态。  
  
 如果应用程序在与连接句柄关联的不完整事务时调用**SQLDisconnect，** 驱动程序将返回 SQLSTATE 25000（无效事务状态），指示事务保持不变，连接处于打开状态。 不完整的事务是尚未提交或回滚**SQLEndTran**的事务。  
  
 如果应用程序在释放与连接关联的所有语句之前调用**SQLDisconnect，** 则驱动程序在成功断开与数据源的连接后，释放这些语句和已在连接上显式分配的所有描述符。 但是，如果与连接关联的一个或多个语句仍在异步执行，**则 SQLDisconnect**返回SQL_ERROR SQLSTATE 值为 HY010（函数序列错误）。 此外，如果连接处于挂起状态，或者**SQLCancelHandle**成功取消了**SQLDisconnect，SQLDisconnect**将释放所有关联的语句和已在连接上显式分配的所有描述符。 **SQLDisconnect**  
  
 有关应用程序如何使用**SQLDisconnect**的信息，请参阅[从数据源或驱动程序断开连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>断开与池连接的连接  
 如果为共享环境启用了连接池，并且应用程序在该环境中的连接上调用**SQLDisconnect，** 则连接将返回到连接池，并且仍然可用于使用相同的共享环境的其他组件。  
  
## <a name="code-example"></a>代码示例  
 请参阅[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)[、SQLBrowse连接函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|连接到数据源|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|释放连接句柄|[SQLFreeConnect 函数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
