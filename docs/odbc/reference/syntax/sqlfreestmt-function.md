---
title: "SQLFreeStmt 函数 |Microsoft 文档"
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
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 929fc50091c914936b5bedfb58bd42c1d07d99ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLFreeStmt**停止与特定报表关联的处理、 关闭任何打开的游标语句，放弃挂起的结果，与关联，或 （可选） 释放与该语句句柄关联的所有资源。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄  
  
 *选项*  
 [输入]以下选项之一：  
  
 SQL_ 关闭： 关闭与关联的光标*StatementHandle* （如果已定义） 并放弃所有挂起结果。 应用程序可以通过重新打开此光标更高版本执行**选择**再次使用相同或不同的参数值的语句。 如果任何光标不处于打开状态，此选项不起该应用程序。 **SQLCloseCursor**还可以调用以进行时关闭游标。 有关详细信息，请参阅[关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP： 此选项已弃用。 调用**SQLFreeStmt**与*选项*SQL_DROP 的映射在驱动程序管理器到[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
 SQL_UNBIND： 设置为 0，释放所有列缓冲区 ARD SQL_DESC_COUNT 字段绑定通过**SQLBindCol**为给定*StatementHandle*。 这不会解除绑定书签列中。若要做到这一点，书签列 ARD SQL_DESC_DATA_PTR 字段设置为 NULL。 请注意，是否上显式分配的描述符所共享的多个语句执行此操作，则该操作将影响所有共享描述符的语句的绑定。 有关详细信息，请参阅[概述的检索结果 (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS： 将 APD SQL_DESC_COUNT 字段设置为 0，释放所有参数缓冲区设置**SQLBindParameter**为给定*StatementHandle*。 如果显式分配的描述符所共享的多个语句上执行此操作，则此操作将影响所有共享描述符的语句的绑定。 有关详细信息，请参阅[绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLFreeStmt**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLFreeStmt**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLFreeStmt**调用。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 此函数调用时使用*选项*之前数据已检索到的所有流的参数设置为 SQL_RESET_PARAMS。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY092|选项类型超出了范围|(DM) 值的参数的指定*选项*不：<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 调用**SQLFreeStmt**对于 SQL_CLOSE 选项是等效于调用**SQLCloseCursor**，只不过**SQLFreeStmt**与 SQL_CLOSE 不会影响应用程序如果在语句上打开任何光标。 如果没有光标位于打开，请调用**SQLCloseCursor**返回 SQLSTATE 24000 （无效的游标状态）。  
  
 已释放; 之后，应用程序不应使用的语句句柄驱动程序管理器不检查函数调用中的句柄的有效性。  
  
## <a name="example"></a>示例  
 很好的编程做法释放句柄。 但是，为了简单起见，下面的示例不包括释放分配的句柄的代码。 有关如何释放句柄的示例，请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```  
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
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|关闭游标|[SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|释放句柄|[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

