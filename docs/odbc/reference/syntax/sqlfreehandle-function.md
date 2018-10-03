---
title: SQLFreeHandle 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14d883228c17b24f42765c6fbf8484592b5fa117
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820195"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函数
**符合性**  
 版本引入了： ODBC 3.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLFreeHandle**释放与特定的环境、 连接、 语句或描述符句柄关联的资源。  
  
> [!NOTE]  
>  此函数是泛型函数释放句柄。 它取代了 ODBC 2.0 函数**SQLFreeConnect** （适用于释放连接句柄） 和**SQLFreeEnv** （适用于释放环境句柄）。 **SQLFreeConnect**并**SQLFreeEnv**已弃用在 ODBC 3 *.x*。 **SQLFreeHandle**还会替换 ODBC 2.0 函数**SQLFreeStmt** (使用 SQL_DROP*选项*) 释放语句句柄。 有关详细信息，请参阅"注释"。 详细了解驱动程序管理器映射的内容到此函数时 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序，请参阅[用于向后映射替换函数应用程序的兼容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要释放的句柄的类型**SQLFreeHandle**。 必须是以下值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只能由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是下列值之一**SQLFreeHandle**返回 SQL_INVALID_HANDLE。  
  
 *Handle*  
 [输入]要释放句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**返回 SQL_ERROR，句柄是否仍然有效。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFreeHandle**可能从该句柄的诊断数据结构中获取返回 SQL_ERROR，关联的 SQLSTATE 值的**SQLFreeHandle**尝试免费，但没有成功。 下表列出了通常由返回的 SQLSTATE 值**SQLFreeHandle** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） *HandleType*参数为 SQL_HANDLE_ENV，以及至少一个连接处于已分配或已连接状态。 **SQLDisconnect**并**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC 必须为其调用之前，调用每个连接**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_ENV。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_DBC，并在调用之前调用该函数**SQLDisconnect**连接。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_DBC。 调用以异步方式执行的函数时使用*处理*和函数仍在执行时调用此函数。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT。 **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**与语句句柄调用和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT。 语句句柄或关联的连接句柄上调用了异步执行的函数和函数仍在执行时调用此函数。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_DESC。 关联的连接句柄; 上调用异步执行函数和函数仍在执行时调用此函数。<br /><br /> (DM) 所有分公司的句柄和其他资源不之前发布**SQLFreeHandle**调用。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*处理*并*HandleType*已设置为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|*HandleType*参数为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，并且不会处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY017|自动分配的描述符句柄的使用无效。|（数据挖掘）*处理*参数已设置为自动分配的描述符句柄。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|（数据挖掘） *HandleType*自变量为 SQL_HANDLE_DESC，且该驱动程序为 ODBC 2 *.x*驱动程序。<br /><br /> （数据挖掘） *HandleType*参数为 SQL_HANDLE_STMT，，和驱动程序不是有效的 ODBC 驱动程序。|  
  
## <a name="comments"></a>注释  
 **SQLFreeHandle**用于释放句柄的环境、 连接、 语句和描述符，如以下各节中所述。 有关控点的常规信息，请参阅[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 已释放; 之后，应用程序不应使用一个句柄驱动程序管理器不会检查函数调用的句柄的有效性。  
  
## <a name="freeing-an-environment-handle"></a>释放环境句柄  
 在调用之前**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_ENV，应用程序必须调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC 适用于所有环境下分配的连接。 否则为在调用**SQLFreeHandle**返回 SQL_ERROR 和环境，并且任何活动的连接保持有效。 有关详细信息，请参阅[环境处理](../../../odbc/reference/develop-app/environment-handles.md)并[分配环境处理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果环境是一个共享的环境，应用程序的调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_ENV 不再有权访问在调用后，环境而使用环境不一定被释放资源。 在调用**SQLFreeHandle**递减引用计数的环境。 引用计数进行维护的驱动程序管理器。 如果它不会达到零，共享的环境不会释放，因为仍在另一个组件使用。 如果引用计数达到零时，会释放共享环境的资源。  
  
## <a name="freeing-a-connection-handle"></a>释放连接句柄  
 在调用之前**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC，应用程序必须调用**SQLDisconnect**是否存在对此连接的连接处理 *。* 否则为在调用**SQLFreeHandle**返回 SQL_ERROR，并将连接保持有效。  
  
 有关详细信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)并[断开与数据源或驱动程序的连接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="freeing-a-statement-handle"></a>释放语句句柄  
 调用**SQLFreeHandle**与*HandleType*设置为 SQL_HANDLE_STMT，释放所分配的调用的所有资源**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_STMT。 当应用程序调用**SQLFreeHandle**要释放具有挂起的结果的语句，挂起的结果被删除。 当应用程序释放语句句柄时，该驱动程序将释放与该句柄相关联的四个自动分配的描述符。 有关详细信息，请参阅[语句处理](../../../odbc/reference/develop-app/statement-handles.md)并[释放语句句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 请注意， **SQLDisconnect**连接上，将自动删除任何语句和描述符打开。  
  
## <a name="freeing-a-descriptor-handle"></a>释放描述符句柄  
 调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC 的释放描述符句柄*处理*。 在调用**SQLFreeHandle**不会释放分配的应用程序可能会由指针字段 （包括 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 引用的所有任何的内存描述符记录*处理*。 释放该句柄时，会释放不是指针字段的字段的驱动程序分配的内存。 时释放用户分配的描述符句柄，已释放句柄相关联的所有语句都还原为其各自自动分配的描述符句柄。  
  
> [!NOTE]  
>  ODBC 2 *.x*驱动程序不支持释放描述符句柄，就像它们不支持分配的描述符句柄。  
  
 请注意， **SQLDisconnect**连接上，将自动删除任何语句和描述符打开。 当应用程序释放语句句柄时，该驱动程序将释放与该句柄相关联的所有自动生成的描述符。  
  
 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>代码示例  
 有关其他代码示例，请参阅[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)并[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
### <a name="code"></a>代码  
  
```  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消语句处理|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
