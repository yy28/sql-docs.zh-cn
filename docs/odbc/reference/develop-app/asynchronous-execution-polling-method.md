---
title: "异步执行 （轮询方法） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
caps.latest.revision: "40"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67943839b7e7425d22ab32251fd1993faf9552eb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="asynchronous-execution-polling-method"></a>异步执行 （轮询方法）
在 ODBC 3.8 和 Windows 7 SDK 之前, 已仅在语句函数上允许异步操作。 有关详细信息，请参阅**异步执行语句操作**，本主题中更高版本。  
  
 在 Windows 7 SDK 中的 ODBC 3.8 引入上与连接相关的操作的异步执行。 有关详细信息，请参阅**异步执行连接操作**本主题后面的部分。  
  
 在 Windows 7 SDK 中，异步语句或连接操作，将该异步操作已完成使用轮询方法确定应用程序。 从 Windows 8 SDK 开始，你可以确定异步操作已完成使用通知方法。 有关详细信息，请参阅[异步执行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
 默认情况下，驱动程序执行 ODBC 函数同步进行;即，应用程序调用一个函数而该驱动程序不会返回控制应用程序完成执行函数前。 但是，可以以异步方式; 执行某些函数也就是说，在应用程序调用该函数，并驱动程序，最小处理之后，将控件返回应用程序。 第一个函数仍在执行时，应用程序然后可以调用其他函数。  
  
 对于很大程度上在数据源执行的大部分函数支持异步执行，如要建立连接、 准备并执行 SQL 语句的函数检索元数据，提取数据，并提交事务。 数据源上当前正在执行的任务需要很长时间，例如登录过程或针对大型数据库的复杂查询时，它是最有用。  
  
 当应用程序执行的函数与语句或启用异步处理的连接时，驱动程序执行最少量的处理 （如检查有错误的自变量），将传递到数据源，处理并返回控制转移到具有 SQL_STILL_EXECUTING 返回代码的应用程序。 然后，应用程序执行其他任务。 若要确定异步函数完成时，应用程序轮询该驱动程序按固定的间隔通过调用具有与它最初使用相同的参数的函数。 如果该函数仍在执行，它将返回 SQL_STILL_EXECUTING;如果它已完成执行，它将返回它具有同步执行它，如 SQL_SUCCESS、 SQL_ERROR 或 SQL_NEED_DATA 返回的代码。  
  
 函数执行同步或异步是特定的驱动程序。 例如，假设在驱动程序中缓存的结果集元数据。 在这种情况下，它用很少的时间来执行**SQLDescribeCol** ，驱动程序应只需执行的函数而不是人为延迟执行。 另一方面，如果该驱动程序必须从数据源中检索元数据，则应给应用程序返回控件时执行此操作。 因此，应用程序必须能够处理非 SQL_STILL_EXECUTING 的返回代码，首先以异步方式执行函数时。  
  
## <a name="executing-statement-operations-asynchronously"></a>以异步方式执行语句操作  
 以下语句函数对数据源进行操作，并且能够以异步方式执行：  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 异步语句执行控制每个语句或每个连接基础，具体取决于数据源上。 即，应用程序不指定将特定的函数是以异步方式执行，但在某一特定语句上执行任何函数是以异步方式执行。 若要查找支持的一个扩展，应用程序调用[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_ASYNC_MODE 的选项。 如果支持连接级别 （适用于语句句柄） 的异步执行，则，返回 SQL_AM_CONNECTION如果支持语句级异步执行，SQL_AM_STATEMENT。  
  
 若要指定与某一特定语句执行的函数是要异步执行，则应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_ASYNC_ENABLE 属性，并将其设置为 SQL_ASYNC_ENABLE_ON。 如果支持连接级别异步处理，则 SQL_ATTR_ASYNC_ENABLE 语句属性是只读的其值为已分配该语句的连接的连接属性相同。 它是特定于驱动程序的语句属性的值是否设置在语句分配时或更高版本。 尝试将其设置将返回 SQL_ERROR 和 SQLSTATE HYC00 （未实现的可选功能）。  
  
 若要指定一个特定连接的情况下执行的函数是要异步执行，则应用程序调用**SQLSetConnectAttr**与 SQL_ATTR_ASYNC_ENABLE 属性，并将其设置为 SQL_ASYNC_ENABLE_ON。 将为异步执行; 启用连接上分配的所有将来的语句句柄它是驱动程序定义的现有语句句柄是否将通过此操作。 如果 SQL_ATTR_ASYNC_ENABLE 设置为 SQL_ASYNC_ENABLE_OFF，连接上的所有语句都是在同步模式下。 如果在连接上的活动语句时启用异步执行，则返回错误。  
  
 若要确定驱动程序可以在给定的连接支持的异步模式中的活动并发语句的最大数，在应用程序调用**SQLGetInfo** SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 选项。  
  
 下面的代码演示轮询模型的工作原理：  
  
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
  
 函数执行时以异步方式，应用程序可以在任何其他语句上调用函数。 应用程序还可以对任何连接，除了与异步语句相关联的一个调用函数。 但应用程序可以仅调用原始函数和 （具有语句句柄或其关联的连接，环境句柄），以下函数语句操作完成后返回 SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) （语句句柄） 上  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 如果在应用程序调用任何其他函数与异步语句或与该语句关联的连接，则函数返回 SQLSTATE HY010 （函数序列错误），例如。  
  
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
  
 当应用程序调用一个函数来确定是否它仍在执行以异步方式时，它必须使用原始语句句柄。 这是因为异步执行跟踪基于每个语句。 应用程序还必须提供有效的其他自变量的值-原始参数将执行-若要获取过去的错误检查驱动程序管理器中。 但是，该驱动程序检查语句句柄，并确定以异步方式执行该语句后，它将忽略所有其他参数。  
  
 以异步方式执行函数时，使用 — 也就是说，它具有返回 SQL_STILL_EXECUTING 之后，并在它返回不同的代码-应用程序可以取消它通过调用**SQLCancel**或**SQLCancelHandle**具有相同的语句句柄。 这是无法保证可以取消函数执行。 例如，函数可能具有已完成。 此外，通过返回的代码**SQLCancel**或**SQLCancelHandle**仅指示尝试取消该函数成功，不是它实际取消函数。 若要确定该函数是否已取消，应用程序再次调用此函数。 如果该函数已取消，它将返回 SQL_ERROR 和 SQLSTATE HY008 （已取消的操作）。 如果未取消函数，则返回另一个代码，如 SQL_SUCCESS、 SQL_STILL_EXECUTING 或使用不同的 SQLSTATE SQL_ERROR。  
  
 若要禁用特定语句的异步执行时的驱动程序支持语句级异步处理，则应用程序调用**SQLSetStmtAttr**与 SQL_ATTR_ASYNC_ENABLE 属性，并将其设置为 SQL_ASYNC_ENABLE_OFF。 如果该驱动程序支持连接级别异步处理，在应用程序调用**SQLSetConnectAttr**将 SQL_ATTR_ASYNC_ENABLE 设置为 SQL_ASYNC_ENABLE_OFF，则计算机禁用异步执行的所有语句连接。  
  
 应用程序应处理的原始函数重复循环中的诊断记录。 如果**SQLGetDiagField**或**SQLGetDiagRec**称为异步函数执行时，它将返回当前诊断记录的列表。 每次重复的原始函数调用，它将清除以前的诊断记录。  
  
## <a name="executing-connection-operations-asynchronously"></a>以异步方式执行连接操作  
 ODBC 3.8 之前异步执行已允许的语句相关的操作如准备、 执行和提取，以及与目录元数据操作。 从 ODBC 3.8 开始，异步执行还有可能的与连接相关的操作，如连接一样，断开连接、 提交和回滚。  
  
 有关 ODBC 3.8 的详细信息，请参阅[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 以异步方式执行连接操作可在以下方案：  
  
-   当线程一小部分管理大量的具有极高的数据速率的设备。 若要最大程度提高响应能力和可伸缩性最好让所有的操作是异步的。  
  
-   如果想要通过多个连接，以减少已用的传输时间重叠数据库操作。  
  
-   高效的异步 ODBC 调用和取消连接操作的功能使应用程序以允许用户取消任何缓慢的操作，而无需等待超时。  
  
 以下函数，对连接句柄进行操作，现在可以以异步方式执行：  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 若要确定驱动程序是否支持对这些函数的异步操作，应用程序调用**SQLGetInfo**与 SQL_ASYNC_DBC_FUNCTIONS。 如果支持异步操作，则返回 SQL_ASYNC_DBC_CAPABLE。 如果不支持异步操作，则返回 SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 若要指定一个特定连接的情况下执行的函数是要异步执行，则应用程序调用**SQLSetConnectAttr**并将 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 属性设置为 SQL_ASYNC_DBC_ENABLE_ON。 在建立的连接始终前设置连接属性以同步方式执行。 此外，设置连接操作属性 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 与**SQLSetConnectAttr**始终以同步方式执行。  
  
 应用程序可以启用异步操作，然后再进行连接。 驱动程序管理器驱动程序管理器无法确定要进行连接之前使用的驱动程序，因为将始终返回成功**SQLSetConnectAttr**。 但是，它可能无法连接如果 ODBC 驱动程序不支持异步操作。  
  
 一般情况下，可以有最多一个以异步方式执行函数与关联的特定连接句柄或语句句柄。 但是，连接句柄可以有多个相关联的语句句柄。 如果没有在连接句柄上执行异步操作，一个关联的语句句柄可以执行异步操作。 同样，你可以对连接句柄的异步操作是否存在任何相关联的语句句柄上无异步操作正在进行。 尝试执行异步操作使用句柄当前正在执行异步操作将返回 HY010，"函数序列错误"。  
  
 如果连接操作返回 SQL_STILL_EXECUTING，应用程序只能调用原始函数，下列功能为该连接句柄：  
  
-   **SQLCancelHandle** （连接句柄） 上  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** （分配 ENV/DBC）  
  
-   **SQLAllocHandleStd** （分配 ENV/DBC）  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 应用程序应处理的原始函数重复循环中的诊断记录。 如果 SQLGetDiagField 或 SQLGetDiagRec 称为异步函数正在执行时，它将返回当前诊断记录的列表。 每次重复的原始函数调用，它将清除以前的诊断记录。  
  
 如果连接正在打开或关闭以异步方式，当应用程序收到 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 原始的函数调用中时，才完成操作。  
  
 新的函数已添加到 ODBC 3.8 **SQLCancelHandle**。 此函数取消六个连接函数 (**SQLBrowseConnect**， **SQLConnect**， **SQLDisconnect**， **SQLDriverConnect**，**SQLEndTran**，和**SQLSetConnectAttr**)。 应用程序应调用**SQLGetFunctions**来判断该驱动程序是否支持**SQLCancelHandle**。 与**SQLCancel**，如果**SQLCancelHandle**返回成功，它并不意味着该操作已取消。 应用程序应调用原始的函数，以确定该操作已取消。 **SQLCancelHandle**使您可以取消连接句柄或语句句柄上的异步操作。 使用**SQLCancelHandle**取消对帐单上的操作句柄是调用相同**SQLCancel**。  
  
 不需要支持这两个**SQLCancelHandle**和同时异步连接操作。 驱动程序可以支持异步连接操作但不是**SQLCancelHandle**，反之亦然。  
  
 异步连接操作和**SQLCancelHandle**还将由 ODBC 3.x 和 ODBC 2.x 应用程序使用 ODBC 3.8 驱动程序和 ODBC 3.8 驱动程序管理器。 有关如何启用较旧的应用程序，以使用更高版本的 ODBC 版本中新功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>连接池  
 每当启用了连接池，仅在最低程度建立的连接支持异步操作 (使用**SQLConnect**和**SQLDriverConnect**) 和关闭与的连接**SQLDisconnect**。 但应用程序应该仍能够处理 SQL_STILL_EXECUTING 返回值从**SQLConnect**， **SQLDriverConnect**，和**SQLDisconnect**。  
  
 启用连接池后， **SQLEndTran**和**SQLSetConnectAttr**支持异步操作。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例演示如何使用**SQLSetConnectAttr**若要启用异步执行与连接相关的函数。  
  
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
  
### <a name="description"></a>Description  
 此示例演示了异步提交操作。 此外可以执行回滚操作这种方式。  
  
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
