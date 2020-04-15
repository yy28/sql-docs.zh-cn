---
title: SQLFreeHandle 功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285768"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFreeHandle**释放与特定环境、连接、语句或描述符句柄关联的资源。  
  
> [!NOTE]
>  此函数是用于释放句柄的泛型函数。 它取代了 ODBC 2.0 函数**SQLFreeConnect（** 用于释放连接句柄）和**SQLFreeEnv（** 用于释放环境句柄）。 **SQLFreeConnect**和**SQLFreeEnv**都在 ODBC 3 *.x*中弃用。 **SQLFreeHandle**还替换了 ODBC 2.0 函数**SQLFreeStmt（** 使用SQL_DROP*选项*），用于释放语句句柄。 有关详细信息，请参阅"注释"。 有关驱动程序管理器将此功能映射到 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序时的详细信息，请参阅[映射应用程序向后兼容性的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]要由**SQLFreeHandle**释放的句柄的类型。 必须是以下值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄仅由驱动程序管理器和驱动程序使用。 应用程序不应使用此句柄类型。 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是这些值之一 **，SQLFreeHandle**将返回SQL_INVALID_HANDLE。  
  
 *Handle*  
 [输入]要释放的句柄。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_ERROR或SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**返回SQL_ERROR，则句柄仍然有效。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFreeHandle**返回SQL_ERROR时，可以从**SQLFreeHandle**尝试释放但无法释放的句柄的诊断数据结构中获取关联的 SQLSTATE 值。 下表列出了**SQLFreeHandle**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） *HandleType*参数SQL_HANDLE_ENV，并且至少有一个连接处于已分配或连接状态。 在使用*SQL_HANDLE_ENV的句柄类型*调用**SQLFreeHandle**之前，必须为每个连接调用具有 SQL_HANDLE_DBC*句柄类型的* **SQLDisconnect**和**SQLFreeHandle。**<br /><br /> （DM） *handleType*参数SQL_HANDLE_DBC，在调用**SQLDisconnect**进行连接之前调用该函数。<br /><br /> （DM）*句柄类型*参数SQL_HANDLE_DBC。 使用*Handle*调用了异步执行函数，并且调用此函数时该函数仍在执行。<br /><br /> （DM）*句柄类型*参数SQL_HANDLE_STMT。 **SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos**被调用语句句柄并返回SQL_NEED_DATA。 **SQLExecute** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM）*句柄类型*参数SQL_HANDLE_STMT。 在语句句柄或关联的连接句柄上调用了异步执行函数，并且在调用此函数时，该函数仍在执行。<br /><br /> （DM）*句柄类型*参数SQL_HANDLE_DESC。 在关联的连接句柄上调用了异步执行函数;调用此函数时，该函数仍在执行。<br /><br /> （DM） 在调用**SQLFreeHandle**之前，未释放所有辅助句柄和其他资源。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用，其中一个语句句柄与*句柄*和*句柄类型*设置为SQL_HANDLE_STMT或SQL_HANDLE_DESC返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|*HandleType*参数SQL_HANDLE_STMT或SQL_HANDLE_DESC，无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY017|自动分配的描述符句柄的使用无效。|（DM） *Handle*参数已设置为自动分配描述符的句柄。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） *handleType*参数SQL_HANDLE_DESC，驱动程序是 ODBC 2 *.x*驱动程序。<br /><br /> （DM） *HandleType*参数SQL_HANDLE_STMT，驱动程序不是有效的 ODBC 驱动程序。|  
  
## <a name="comments"></a>注释  
 **SQLFreeHandle**用于释放环境、连接、语句和描述符的句柄，如以下各节所述。 有关句柄的一般信息，请参阅[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 应用程序在释放句柄后不应使用句柄;驱动程序管理器不检查函数调用中句柄的有效性。  
  
## <a name="freeing-an-environment-handle"></a>释放环境句柄  
 在使用*SQL_HANDLE_ENV的句柄类型*调用**SQLFreeHandle**之前，应用程序必须调用**SQLFreeHandle，** 该*句柄具有*SQL_HANDLE_DBC的句柄类型，用于环境下分配的所有连接。 否则，对**SQLFreeHandle 的**调用将返回SQL_ERROR和环境，并且任何活动连接都仍然有效。 有关详细信息，请参阅[环境句柄](../../../odbc/reference/develop-app/environment-handles.md)和[分配环境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果环境是共享环境，则使用*handletype*调用**SQLFreeHandle**的应用程序SQL_HANDLE_ENV调用后不再有权访问环境，但环境的资源不一定被释放。 对**SQLFreeHandle 的**调用会取消环境的引用计数。 引用计数由驱动程序管理器维护。 如果未达到零，则不会释放共享环境，因为它仍被另一个组件使用。 如果引用计数达到零，则释放共享环境的资源。  
  
## <a name="freeing-a-connection-handle"></a>释放连接句柄  
 在使用*句柄类型*SQL_HANDLE_DBC调用**SQLFreeHandle**之前，如果此句柄上存在连接，则应用程序必须调用**SQLDisconnect**进行连接 *。* 否则，对**SQLFreeHandle 的**调用将返回SQL_ERROR并且连接仍然有效。  
  
 有关详细信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)和[断开与数据源或驱动程序](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="freeing-a-statement-handle"></a>释放语句句柄  
 使用*句柄类型*SQL_HANDLE_STMT对**SQLFreeHandle**的调用会释放通过调用**SQLAllocHandle**分配的具有 SQL_HANDLE_STMT*的句柄类型*的所有资源。 当应用程序调用**SQLFreeHandle**以释放具有挂起结果的语句时，挂起的结果将被删除。 当应用程序释放语句句柄时，驱动程序将释放与该句柄关联的四个自动分配的描述符。 有关详细信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)和[释放语句句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 请注意 **，SQLDisconnect**会自动删除连接上打开的任何语句和描述符。  
  
## <a name="freeing-a-descriptor-handle"></a>释放描述符句柄  
 使用*handle 类型的* **SQLFreeHandle**调用SQL_HANDLE_DESC释放*句柄*中的描述符句柄。 对**SQLFreeHandle 的**调用不会释放应用程序分配的任何内存，这些内存可能由*句柄*的任何描述符记录的指针字段（包括SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR）引用。 释放句柄时，驱动程序为不是指针字段的字段分配的内存将被释放。 释放用户分配的描述符句柄时，释放的句柄与其各自自动分配的描述符句柄关联的所有语句都恢复到其各自的自动分配描述符句柄。  
  
> [!NOTE]
>  ODBC 2 *.x*驱动程序不支持释放描述符句柄，就像它们不支持分配描述符句柄一样。  
  
 请注意 **，SQLDisconnect**会自动删除连接上打开的任何语句和描述符。 当应用程序释放语句句柄时，驱动程序将释放与该句柄关联的所有自动生成的描述符。  
  
 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>代码示例  
 有关其他代码示例，请参阅[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
### <a name="code"></a>代码  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消语句处理|[SQLCance 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 标题文件](../../../odbc/reference/install/odbc-header-files.md)   
 [示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)
