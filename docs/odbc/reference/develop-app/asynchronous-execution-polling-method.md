---
title: 异步执行（轮询方法） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca7b3d5fa16be44bf4c2ef8f8df8953ae081235d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293397"
---
# <a name="asynchronous-execution-polling-method"></a>异步执行（轮询方法）
在 ODBC 3.8 和 Windows 7 SDK 之前，仅允许在语句函数上执行异步操作。 有关详细信息，请参阅本主题后面的**执行语句操作**。  
  
 Windows 7 SDK 中的 ODBC 3.8 引入了连接相关操作的异步执行。 有关详细信息，请参阅本主题后面的 **"同步执行连接操作**"部分。  
  
 在 Windows 7 SDK 中，对于异步语句或连接操作，应用程序确定异步操作是否已完成使用轮询方法。 从 Windows 8 SDK 开始，可以使用通知方法确定异步操作是否已完成。 有关详细信息，请参阅[异步执行（通知方法）。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)  
  
 默认情况下，驱动程序同步执行 ODBC 函数;也就是说，应用程序调用一个函数，驱动程序在完成执行函数之前不会将控件返回到应用程序。 但是，某些函数可以异步执行;也就是说，应用程序调用函数，驱动程序在最少的处理后返回对应用程序的控制。 然后，应用程序可以在第一个函数仍在执行时调用其他函数。  
  
 大多数主要在数据源上执行的函数都支持异步执行，例如建立连接、准备和执行 SQL 语句、检索元数据、提取数据和提交事务的函数。 当在数据源上执行的任务需要很长时间（如登录过程或针对大型数据库的复杂查询）时，它最有用。  
  
 当应用程序执行具有为异步处理启用的语句或连接的函数时，驱动程序执行最少的处理量（例如检查错误参数）、对数据源的句柄处理，以及使用SQL_STILL_EXECUTING返回代码将控制权返回到应用程序。 然后，应用程序执行其他任务。 要确定异步函数何时完成，应用程序通过调用与最初使用的参数相同的参数，定期轮询驱动程序。 如果函数仍在执行，它将返回SQL_STILL_EXECUTING;如果已完成执行，它将返回如果同步执行的代码，例如SQL_SUCCESS、SQL_ERROR或SQL_NEED_DATA。  
  
 函数是同步执行还是异步执行是特定于驱动程序的。 例如，假设结果集元数据缓存在驱动程序中。 在这种情况下，执行**SQLDescribeCol**的时间非常少，驱动程序应该简单地执行该函数，而不是人为地延迟执行。 另一方面，如果驱动程序需要从数据源检索元数据，则应在执行此操作时将控制权返回到应用程序。 因此，应用程序在首次异步执行函数时必须能够处理SQL_STILL_EXECUTING以外的返回代码。  
  
## <a name="executing-statement-operations-asynchronously"></a>异步执行语句操作  
 以下语句函数对数据源运行，可以异步执行：  
  
||||  
|-|-|-|  
|[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 异步语句执行基于每个语句或每个连接进行控制，具体取决于数据源。 也就是说，应用程序指定的不是要异步执行特定函数，而是指定对特定语句执行的任何函数都将异步执行。 要了解支持哪个应用程序，应用程序调用[SQLGetInfo，](../../../odbc/reference/syntax/sqlgetinfo-function.md)选项为 SQL_ASYNC_MODE。 如果支持连接级异步执行（对于语句句柄），则返回SQL_AM_CONNECTION;如果支持语句级异步执行，SQL_AM_STATEMENT。  
  
 要指定使用特定语句执行的函数要异步执行，应用程序使用 SQL_ATTR_ASYNC_ENABLE 属性调用**SQLSetStmtAttr**并将其设置为SQL_ASYNC_ENABLE_ON。 如果支持连接级异步处理，则SQL_ATTR_ASYNC_ENABLE语句属性为只读，其值与分配语句的连接的连接属性相同。 它是特定于驱动程序的，无论语句属性的值是在语句分配时间设置还是更高版本。 尝试设置它将返回SQL_ERROR和 SQLSTATE HYC00（未实现可选功能）。  
  
 要指定使用特定连接执行的函数要异步执行，应用程序使用 SQL_ATTR_ASYNC_ENABLE 属性调用**SQLSetConnectAttr**并将其设置为SQL_ASYNC_ENABLE_ON。 将在连接上分配的所有语句句柄都将启用以进行异步执行;它是驱动程序定义的，是否将此操作启用现有语句句柄。 如果将SQL_ATTR_ASYNC_ENABLE设置为SQL_ASYNC_ENABLE_OFF，则连接上的所有语句都处于同步模式。 如果在连接上有活动语句时启用了异步执行，则返回错误。  
  
 要确定驱动程序在给定连接上可以支持的异步模式下活动并发语句的最大数量，应用程序使用SQL_MAX_ASYNC_CONCURRENT_STATEMENTS选项调用**SQLGetInfo。**  
  
 以下代码演示了轮询模型的工作原理：  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 当函数异步执行时，应用程序可以在任何其他语句上调用函数。 应用程序还可以调用任何连接上的函数，但与异步语句关联的连接除外。 但是，在语句操作返回SQL_STILL_EXECUTING后，应用程序只能调用原始函数和以下函数（具有语句句柄或其关联的连接、环境句柄）：  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle（](../../../odbc/reference/syntax/sqlcancelhandle-function.md)在语句句柄上）  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLData源](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 如果应用程序使用异步语句或与该语句关联的连接调用任何其他函数，则函数将返回 SQLSTATE HY010（函数序列错误）。  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 当应用程序调用函数以确定它是否仍在异步执行时，它必须使用原始语句句柄。 这是因为异步执行是按语句跟踪的。 应用程序还必须为其他参数（原始参数将执行）提供有效值，以在驱动程序管理器中通过错误检查。 但是，在驱动程序检查语句句柄并确定语句以异步方式执行后，它将忽略所有其他参数。  
  
 当函数以异步方式执行时（即，在返回SQL_STILL_EXECUTING后，并在返回其他代码之前，应用程序可以通过使用相同的语句句柄调用**SQLCancel**或**SQLCancelHandle**来取消它。 这不能保证取消函数执行。 例如，函数可能已完成。 此外 **，SQLCancel**或**SQLCancelHandle**返回的代码仅指示取消函数的尝试是否成功，而不是是否实际取消了该函数。 要确定函数是否已取消，应用程序将再次调用该函数。 如果函数已取消，它将返回SQL_ERROR和 SQLSTATE HY008（操作已取消）。 如果未取消该函数，它将返回另一个代码，如SQL_SUCCESS、SQL_STILL_EXECUTING或具有其他 SQLSTATE 的SQL_ERROR。  
  
 要禁用在驱动程序支持语句级异步处理时对特定语句的异步执行，应用程序使用SQL_ATTR_ASYNC_ENABLE属性调用**SQLSetStmtAttr**并将其设置为SQL_ASYNC_ENABLE_OFF。 如果驱动程序支持连接级异步处理，应用程序将调用**SQLSetConnectAttr**将SQL_ATTR_ASYNC_ENABLE设置为SQL_ASYNC_ENABLE_OFF，从而禁用对连接上所有语句的异步执行。  
  
 应用程序应在原始函数的重复循环中处理诊断记录。 如果在执行异步函数时调用**SQLGetDiagField**或**SQLGetDiagRec，** 它将返回当前诊断记录列表。 每次重复原始函数调用时，它都会清除以前的诊断记录。  
  
## <a name="executing-connection-operations-asynchronously"></a>异步执行连接操作  
 在 ODBC 3.8 之前，允许异步执行语句相关操作，如准备、执行和提取，以及目录元数据操作。 从 ODBC 3.8 开始，对于连接相关操作（如连接、断开连接、提交和回滚）也可以执行异步执行。  
  
 有关 ODBC 3.8 的详细信息，请参阅[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 在以下情况下，异步执行连接操作非常有用：  
  
-   当少量线程管理具有极高数据速率的大量设备时。 为了最大限度地提高响应性和可扩展性，所有操作都是异步的。  
  
-   如果要在多个连接上重叠数据库操作以减少已用传输时间。  
  
-   高效的异步 ODBC 调用和取消连接操作的能力使应用程序允许用户取消任何慢速操作，而无需等待超时。  
  
 以下函数在连接句柄上操作，现在可以异步执行：  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQL 断开](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 要确定驱动程序是否支持对这些函数的异步操作，应用程序使用 SQL_ASYNC_DBC_FUNCTIONS调用**SQLGetInfo。** 如果支持异步操作，则返回SQL_ASYNC_DBC_CAPABLE。 如果不支持异步操作，则返回SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 要指定使用特定连接执行的函数要异步执行，应用程序将调用**SQLSetConnectAttr**并将SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE属性设置为SQL_ASYNC_DBC_ENABLE_ON。 在建立连接之前设置连接属性始终同步执行。 此外，使用**SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE连接属性设置的操作始终同步执行。  
  
 应用程序可以在建立连接之前启用异步操作。 由于驱动程序管理器无法确定在建立连接之前要使用的驱动程序，因此驱动程序管理器将始终在**SQLSetConnectAttr**中返回成功。 但是，如果 ODBC 驱动程序不支持异步操作，则可能无法连接。  
  
 通常，最多只能有一个与特定连接句柄或语句句柄关联的异步执行函数。 但是，连接句柄可以有多个关联的语句句柄。 如果连接句柄上没有执行异步操作，则关联的语句句柄可以执行异步操作。 同样，如果任何关联的语句句柄上没有正在进行的异步操作，则可以对连接句柄执行异步操作。 尝试使用当前正在执行异步操作的句柄执行异步操作将返回 HY010，"函数序列错误"。  
  
 如果连接操作返回SQL_STILL_EXECUTING，则应用程序只能调用该连接句柄的原始函数和以下函数：  
  
-   **SQLCancelHandle（** 在连接句柄上）  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle（** 分配ENV/DBC）  
  
-   **SQLAllocHandleStd（** 分配ENV/DBC）  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLData源**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 应用程序应在原始函数的重复循环中处理诊断记录。 如果在执行异步函数时调用 SQLGetDiagField 或 SQLGetDiagRec，它将返回当前诊断记录列表。 每次重复原始函数调用时，它都会清除以前的诊断记录。  
  
 如果以异步方式打开或关闭连接，则当应用程序在原始函数调用中收到SQL_SUCCESS或SQL_SUCCESS_WITH_INFO时，操作将完成。  
  
 一个新的函数已添加到 ODBC **3.8，SQLCancelHandle**。 此函数取消六个连接函数 **（SQLBrowseConnect、SQLConnect、SQL****断开连接****、SQLDriverConnect、SQLEndTran**和**SQLSetConnectAttr）。** **SQLConnect** **SQLEndTran** 应用程序应调用**SQLGet函数**以确定驱动程序是否支持**SQLCancelHandle**。 与**SQLCancel**一样，如果**SQLCancelHandle**返回成功，并不意味着操作已取消。 应用程序应再次调用原始函数以确定操作是否已取消。 **SQLCancelHandle**允许您取消连接句柄或语句句柄上的异步操作。 使用**SQLCancelHandle**取消语句句柄上的操作与调用**SQLCancel**相同。  
  
 不必同时支持**SQLCancelHandle**和异步连接操作。 驱动程序可以支持异步连接操作，但不能支持**SQLCancelHandle，** 反之亦然。  
  
 具有 ODBC 3.8 驱动程序和 ODBC 3.8 驱动程序管理器的 ODBC 3.x 和 ODBC 2.x 应用程序也可以使用异步连接操作和**SQLCancelHandle。** 有关如何启用较旧的应用程序在更高版本的 ODBC 版本中使用新功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>连接池  
 每当启用连接池时，异步操作仅受最小支持，用于建立连接（使用**SQLConnect**和**SQLDriverConnect），** 并关闭与**SQLDisconnect**的连接。 但是，应用程序仍然能够处理来自 SQLConnect、SQLDriverConnect**SQLConnect**和**SQLDisconnect**的SQL_STILL_EXECUTING返回值。 **SQLDriverConnect**  
  
 启用连接池后，异步操作支持**SQLEndTran**和**SQLSetConnectAttr。**  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例演示如何使用**SQLSetConnectAttr**为连接相关的函数启用异步执行。  
  
### <a name="code"></a>代码  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 此示例显示异步提交操作。 回滚操作也可以以这种方式完成。  
  
### <a name="code"></a>代码  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行语句 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
