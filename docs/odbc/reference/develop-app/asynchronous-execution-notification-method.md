---
title: 异步执行 （通知方法） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 070ef059855d4c95b4225676ab67eddcd9c16ad1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）
ODBC 允许连接和语句操作的异步的执行。 一个应用程序线程可以在异步模式调用 ODBC 函数，该函数可以返回在操作完成后，允许应用程序线程执行其他任务之前。 在 Windows 7 SDK 中，异步语句或连接操作，将该异步操作已完成使用轮询方法确定应用程序。 有关详细信息，请参阅[异步执行 （轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。 从 Windows 8 SDK 开始，你可以确定异步操作已完成使用通知方法。  
  
 在轮询方法中，应用程序需要调用的异步函数每的次它想要操作的状态。 通知方法是类似于回调和 ADO.NET 中的等待。 ODBC，但是，使用 Win32 事件作为通知对象。  
  
 不能在同一时间使用 ODBC 游标库和 ODBC 异步通知。 将这两个属性将返回错误 SQLSTATE S1119 （游标库异步通知无法启用和在同一时间）。  
  
 请参阅[通知的异步函数完成](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md)驱动程序开发人员有关的信息。  
  
> [!NOTE]  
>  游标库不支持通知方法。 如果它尝试启用通过 SQLSetConnectAttr，光标库，启用通知方法后，应用程序将收到错误消息。  
  
## <a name="overview"></a>概述  
 ODBC 函数调用时在异步模式下，控件就会归还立即，返回代码 SQL_STILL_EXECUTING 调用应用程序。 应用程序必须反复轮询函数，直到它返回 SQL_STILL_EXECUTING 之外的内容。 轮询循环会增加 CPU 使用率，从而导致性能降低，在许多异步方案。  
  
 使用通知模型，则每当轮询模型处于禁用状态。 应用程序不应再次调用原始函数。 调用[SQLCompleteAsync 函数](../../../odbc/reference/syntax/sqlcompleteasync-function.md)以完成异步操作。 如果在异步操作完成之前，应用程序将再次调用原始函数，则调用将返回与 SQLSTATE IM017 SQL_ERROR （异步通知模式中禁用轮询）。  
  
 应用程序使用通知模型时，可以调用**SQLCancel**或**SQLCancelHandle**取消语句或连接的操作。 如果取消请求成功，ODBC 将返回 SQL_SUCCESS。 此消息不表示，该函数已实际取消;它指示程序已被处理取消请求。 是否实际取消该函数是依赖于驱动程序的代码和数据源而定。 取消操作时，驱动程序管理器仍将发信号通知事件。 驱动程序管理器中的返回代码缓冲区返回 SQL_ERROR 并且状态是 SQLSTATE HY008 （已取消的操作） 以指示取消是否成功。 如果该函数完成其正常处理，驱动程序管理器将返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
### <a name="downlevel-behavior"></a>下层行为  
 在完成上支持此通知的 ODBC 驱动程序管理器版本是 ODBC 3.81。  
  
|应用程序的 ODBC 版本|驱动程序管理器版本|驱动程序版本|行为|  
|------------------------------|----------------------------|--------------------|--------------|  
|新的应用程序的任何 ODBC 版本|ODBC 3.81|ODBC 3.80 驱动程序|如果驱动程序支持此功能，应用程序可以使用此功能，否则驱动程序管理器将出错。|  
|新的应用程序的任何 ODBC 版本|ODBC 3.81|Pre ODBC 3.80 驱动程序|如果该驱动程序不支持此功能，则驱动程序管理器将出错。|  
|新的应用程序的任何 ODBC 版本|Pre ODBC 3.81|Any|当应用程序使用此功能时，旧的驱动程序管理器将考虑为特定于驱动程序属性的新特性和驱动程序应出的错误。新的驱动程序管理器将不将这些属性传递给该驱动程序。|  
  
 应用程序应使用此功能之前检查驱动程序管理器版本。 否则，如果驱动程序管理器版本为 pre ODBC 3.81 编写不佳的驱动程序不会出错，，行为是不确定的。  
  
## <a name="use-cases"></a>用例  
 本部分说明异步执行和轮询机制的用例。  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>将来自多个 ODBC 源的数据集成  
 数据集成应用程序以异步方式从多个数据源提取数据。 某些数据是从远程数据源并一些数据从本地文件。 异步操作在完成之前，应用程序无法继续。  
  
 而不是重复轮询一个操作以确定其是否完成，应用程序可以创建一个事件对象，并将其与一个 ODBC 连接句柄或 ODBC 语句句柄关联。 然后，应用程序调用操作系统同步 Api 结合使用以等待一个事件对象或多个事件对象 （ODBC 事件和其他 Windows 事件）。 相应的 ODBC 异步操作完成时，ODBC 将发信号的事件对象。  
  
 在 Windows 上，将使用 Win32 事件对象，并将提供用户的统一编程模型。 在其他平台上的驱动程序管理器可以使用特定于这些平台的事件对象实现。  
  
 下面的代码示例演示如何使用连接和语句的异步通知：  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>确定驱动程序是否支持异步通知  
 ODBC 应用程序可以确定 ODBC 驱动程序是否支持通过调用的异步通知[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。 ODBC 驱动程序管理器将因此调用**SQLGetInfo** SQL_ASYNC_NOTIFICATION 与驱动程序。  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>将 Win32 事件句柄与 ODBC 句柄关联  
 应用程序负责创建 Win32 事件对象使用相应的 Win32 函数。 应用程序可以与一个 ODBC 连接句柄或一个 ODBC 语句句柄关联一个 Win32 事件句柄。  
  
 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 和 SQL_ATTR_ASYNC_DBC_EVENT 连接属性确定 ODBC 在异步模式的执行是否和 ODBC 中是否启用连接句柄的通知模式。 语句特性 SQL_ATTR_ASYNC_ENABLE 和 SQL_ATTR_ASYNC_STMT_EVENT 确定 ODBC 在异步模式的执行是否和 ODBC 中是否启用语句句柄的通知模式。  
  
|SQL_ATTR_ASYNC_ENABLE 或 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT 或 SQL_ATTR_ASYNC_DBC_EVENT|模式|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|启用|非 null|异步通知|  
|启用|null|异步轮询|  
|Disable|any|同步|  
  
 应用程序可以暂时禁用异步操作模式。 如果已禁用的连接级别的异步操作，ODBC 将忽略 SQL_ATTR_ASYNC_DBC_EVENT 的值。 如果已禁用的语句级的异步操作，ODBC 将忽略 SQL_ATTR_ASYNC_STMT_EVENT 的值。  
  
 同步调用**SQLSetStmtAttr**和**SQLSetConnectAttr**  
 -   **SQLSetConnectAttr**支持异步操作，但调用**SQLSetConnectAttr**若要设置 SQL_ATTR_ASYNC_DBC_EVENT 始终是同步。  
  
-   **SQLSetStmtAttr**不支持异步执行。  
  
 错误扩展方案  
 当**SQLSetConnectAttr**进行连接，驱动程序管理器无法确定要使用的驱动程序之前调用。 因此，驱动程序管理器返回的成功**SQLSetConnectAttr**但该属性可能不会准备好设置驱动程序中。 在应用程序调用连接函数时，驱动程序管理器将设置这些属性。 驱动程序管理器可能会错误超时，因为驱动程序不支持异步操作。  
  
 连接属性的继承  
 通常情况下，连接的语句将继承连接属性。 但是，属性 SQL_ATTR_ASYNC_DBC_EVENT 不是可继承，并且只会影响连接操作。  
  
 要将一个事件句柄关联与 ODBC 连接句柄，ODBC 应用程序调用 ODBC API **SQLSetConnectAttr**并指定 SQL_ATTR_ASYNC_DBC_EVENT，如属性和事件处理作为其属性值。 新的 ODBC 属性属于类型 SQL_IS_POINTER SQL_ATTR_ASYNC_DBC_EVENT。  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 通常情况下，应用程序创建自动重置事件对象。 ODBC 时，将不重置事件对象。 应用程序必须确保确认对象未处于终止状态之前调用任何异步的 ODBC 函数。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT 是不会设置驱动程序中的仅限驱动程序管理器的属性。  
  
 SQL_ATTR_ASYNC_DBC_EVENT 的默认值为 NULL。 获取或设置 SQL_ATTR_ASYNC_DBC_EVENT 如果驱动程序不支持异步通知，将返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。  
  
 如果最后一个 SQL_ATTR_ASYNC_DBC_EVENT 值设置上一个 ODBC 连接句柄不为 NULL，并且应用程序启用通过设置属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 与 SQL_ASYNC_DBC_ENABLE_ON，调用任何 ODBC 连接的异步模式支持异步模式的函数将获取完成通知。 如果在一个 ODBC 连接句柄上设置的最后一个 SQL_ATTR_ASYNC_DBC_EVENT 值为 NULL，ODBC 不会发送应用程序任何通知，而不管是否启用异步模式。  
  
 应用程序可以设置 SQL_ATTR_ASYNC_DBC_EVENT 之前或之后将属性 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 设置。  
  
 应用程序可以 SQL_ATTR_ASYNC_DBC_EVENT 属性上设置一个 ODBC 连接句柄调用连接函数之前 (**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**)。 因为 ODBC 驱动程序管理器不知道应用程序将使用哪些 ODBC 驱动程序，它将返回 SQL_SUCCESS。 当应用程序调用连接函数时，ODBC 驱动程序管理器将检查该驱动程序是否支持异步通知。 如果该驱动程序不支持异步通知，ODBC 驱动程序管理器将返回与 SQLSTATE S1_118 SQL_ERROR （驱动程序不支持异步通知）。 如果该驱动程序支持异步通知，ODBC 驱动程序管理器将调用该驱动程序，并设置相应属性 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 和 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT。  
  
 同样，应用程序调用**SQLSetStmtAttr**在 ODBC 语句处理并指定要启用或禁用语句级别异步通知的 SQL_ATTR_ASYNC_STMT_EVENT 特性。 因为后建立连接时，始终调用语句函数**SQLSetStmtAttr**将返回与 SQLSTATE S1_118 SQL_ERROR （驱动程序不支持异步通知） 如果立即相应驱动程序不支持异步操作或驱动程序支持异步操作，但不支持异步通知。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT，可以设置为 NULL，是将不会设置驱动程序中的仅限驱动程序管理器的属性。  
  
 SQL_ATTR_ASYNC_STMT_EVENT 的默认值为 NULL。 如果该驱动程序不支持异步通知，获取或设置 SQL_ATTR_ASYNC_ STMT_EVENT 属性将返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。  
  
 应用程序不应将相同的事件句柄关联与多个 ODBC 句柄。 否则，如果两个异步 ODBC 函数调用完成对两个共享相同的事件句柄的句柄，一个通知将会丢失。 若要避免从连接句柄继承相同的事件句柄的语句句柄，ODBC 返回如果应用程序的连接句柄设置 SQL_ATTR_ASYNC_STMT_EVENT SQL_ERROR 与 SQLSTATE IM016 （不能设置语句属性为连接句柄）。  
  
### <a name="calling-asynchronous-odbc-functions"></a>调用异步 ODBC 函数  
 启用异步通知并开始异步操作后, 应用程序可以调用任何 ODBC 函数。 如果该函数所属的支持异步操作的函数集，应用程序将收到完成通知操作完成后，无论函数是否失败或成功。  唯一的例外是在应用程序调用 ODBC 函数使用无效的连接或语句句柄。 在这种情况下，ODBC 将不获取其事件句柄，并将其设置为终止状态。  
  
 应用程序必须确保关联的事件对象处于是非终止的状态在开始对相应的 ODBC 句柄的异步操作之前。 ODBC 时，将不重置事件对象。  
  
### <a name="getting-notification-from-odbc"></a>从 ODBC 获取通知  
 一个应用程序线程可以调用**WaitForSingleObject**等待上一个事件句柄或调用**WaitForMultipleObjects**等待对事件句柄数组，并被挂起，直到一个或所有事件对象变为终止状态或达到超时间隔。  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
