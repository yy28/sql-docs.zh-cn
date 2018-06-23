---
title: 处理返回代码和输出参数 (ODBC) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- return codes [ODBC]
- output parameters [ODBC]
ms.assetid: 102ae1d0-973d-4e12-992c-d844bf05160d
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1303c15f94dc32e69378c38e5353f8e82bf1214a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025471"
---
# <a name="process-return-codes-and-output-parameters-odbc"></a>处理返回代码和输出参数 (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程可具有整数返回代码和输出参数。 返回代码和输出参数从服务器发送的最后一个数据包中和均不可用于应用程序，直到[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)返回 SQL_NO_DATA。 如果从存储过程返回错误，则调用 SQLMoreResults 以转到下一个结果，直到返回 SQL_NO_DATA。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果必须保存凭据，应当用 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)（Win32 加密 API）加密它们。  
  
### <a name="to-process-return-codes-and-output-parameters"></a>处理返回代码和输出参数  
  
1.  构造的 SQL 语句中使用 ODBC 调用转义序列。 该语句应当对每个输入、输入/输出和输出参数以及过程返回值（如果有）使用参数标记。  
  
2.  调用[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)对于每个输入中，输入/输出和输出参数，和有关该过程返回值 （如果有）。  
  
3.  用 `SQLExecDirect` 执行语句。  
  
4.  直到 `SQLFetch` 或 `SQLFetchScroll` 在处理最后一个结果集时返回 SQL_NO_DATA 或直到 `SQLMoreResults` 返回 SQL_NO_DATA，才处理结果集。 这时，将以返回的数据值填充绑定到返回代码和输出参数的变量。  
  
## <a name="example"></a>示例  
 此示例显示如何处理返回代码和输出参数。 IA64 平台不支持此示例。 此示例是面向 ODBC 3.0 版或更高版本开发的。  
  
 需要一个名为 AdventureWorks 的 ODBC 数据源，其默认数据库是 AdventureWorks 示例数据库。 （可以从 [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384)（Microsoft SQL Server 示例和社区项目）主页下载 AdventureWorks 示例数据库。）此数据源必须基于操作系统提供的 ODBC 驱动程序（该驱动程序的名称为“SQL Server”）。 如果您要将此示例构建为在 64 位操作系统上运行的 32 位应用程序并运行该示例，则必须使用 %windir%\SysWOW64\odbcad32.exe 中的 ODBC 管理器创建 ODBC 数据源。  
  
 此示例连接到您的计算机上默认的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 若要连接到命名实例，请更改 ODBC 数据源的定义以使用以下格式指定实例：server\namedinstance。 默认情况下，[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 将安装在命名实例中。  
  
 第一个 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 代码清单创建此示例使用的存储的过程。  
  
 使用 odbc32.lib 编译第二个 (C++) 代码列表。 然后，执行该程序。  
  
 第三个 ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 代码列表删除此示例使用存储的过程。  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'TestParm')  
   DROP PROCEDURE TestParm  
GO  
  
CREATE PROCEDURE TestParm   
@OutParm int OUTPUT   
AS  
SELECT Name FROM Purchasing.Vendor  
SELECT @OutParm = 88  
RETURN 99  
go  
```  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define MAXBUFLEN 255  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   // SQLBindParameter variables.  
   SWORD sParm1 = 0, sParm2 = 1;  
   SQLLEN cbParm1 = SQL_NTS;  
   SQLLEN cbParm2 = SQL_NTS;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Create the SQL Server DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the return code to variable sParm1.  
   retcode = SQLBindParameter(hstmt1, 1, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm1, 0, &cbParm1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the output parameter to variable sParm2.  
   retcode = SQLBindParameter(hstmt1, 2, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm2, 0, &cbParm2);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.   
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"{? = call TestParm(?)}", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Show parameters are not filled.  
   printf("Before result sets cleared: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA )  
      ;  
  
   // Show parameters are now filled.  
   printf("After result sets drained: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clean up.   
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
DROP PROCEDURE TestParm  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [运行存储的过程操作指南主题&#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)  
  
  