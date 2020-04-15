---
title: SQLFreeStmt 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285697"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFreeStmt**停止与特定语句关联的处理，关闭与语句关联的任何打开的游标，丢弃挂起的结果，或者，可以选择释放与语句句柄关联的所有资源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄  
  
 *选项*  
 [输入]以下选项之一：  
  
 SQL_关闭：关闭与*语句句柄*关联的游标（如果已定义），并丢弃所有挂起的结果。 应用程序以后可以通过再次使用相同或不同的参数值执行**SELECT**语句来重新打开此游标。 如果没有打开游标，则此选项对应用程序没有影响。 也可以调用**SQLCloseCursor**来关闭游标。 有关详细信息，请参阅[关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP：此选项已弃用。 在驱动程序管理器中映射到**SQLFreeStmt**的调用，选项为[SQL_DROP。](../../../odbc/reference/syntax/sqlfreehandle-function.md) *Option*  
  
 SQL_UNBIND：将 ARD 的SQL_DESC_COUNT字段设置为 0，释放**SQLBindCol**为给定*语句句柄*绑定的所有列缓冲区。 这不会取消绑定书签列;因此，不会取消绑定书签列。为此，书签列的 ARD SQL_DESC_DATA_PTR字段设置为 NULL。 请注意，如果此操作对由多个语句共享的显式分配的描述符执行，则该操作将影响共享描述符的所有语句的绑定。 有关详细信息，请参阅[检索结果概述（基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS：将 APD 的SQL_DESC_COUNT字段设置为 0，释放**SQLBind参数**为给定*语句句柄*设置的所有参数缓冲区。 如果此操作对由多个语句共享的显式分配的描述符执行，则此操作将影响共享描述符的所有语句的绑定。 有关详细信息，请参阅[绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFreeStmt**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_STMT的*句柄类型*和*语句句柄*。 下表列出了**SQLFreeStmt**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLFreeStmt**时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，使用*Option*设置为SQL_RESET_PARAMS调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY092|选项类型范围外|（DM） 为参数*选项*指定的值不是：<br /><br /> SQL_CLOSESQL_DROPSQL_UNBINDSQL_RESET_PARAMS|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 使用SQL_CLOSE选项调用**SQLFreeStmt**等效于调用**SQLCloseCursor，** 只不过，如果语句上未打开游标，则具有SQL_CLOSE的**SQLFreeStmt**不会影响应用程序。 如果未打开游标，则对**SQLCloseCursor 的**调用将返回 SQLSTATE 24000（无效游标状态）。  
  
 应用程序在释放语句句柄后不应使用它;驱动程序管理器不检查函数调用中句柄的有效性。  
  
## <a name="example"></a>示例  
 释放句柄是一种很好的编程实践。 但是，为简单起见，以下示例不包括释放分配的句柄的代码。 有关如何释放句柄的示例，请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|关闭光标|[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|释放手柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
