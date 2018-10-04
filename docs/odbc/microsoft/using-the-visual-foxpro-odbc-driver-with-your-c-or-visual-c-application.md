---
title: 使用 Visual FoxPro ODBC 驱动程序与 C 或 Visual c + + 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], C or C++ applications
- C++ applications [ODBC]
- Visual FoxPro ODBC driver [ODBC], C or C++ applications
- Visual FoxPro data [ODBC], C or C++ applications
- C applications [ODBC]
ms.assetid: beb11a68-849e-4fe0-b217-d3722b1b1389
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 751e70345876967a534df0fb234ee8511cc09fe1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612265"
---
# <a name="use-the-visual-foxpro-odbc-driver-with-your-c-or-visual-c-application"></a>使用 Visual FoxPro ODBC 驱动程序与 C 或 Visual c + + 应用程序
在 C 或 c + + 应用程序通过发送 Visual FoxPro 数据与通信[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md) Visual FoxPro 的语句。 此语句可以包含以下信息：  
  
-   SQL 语句本机 Visual FoxPro 语言，如[DROP TABLE](../../odbc/microsoft/drop-table-command.md)命令。  
  
-   [支持 ODBC SQL 语法](../../odbc/microsoft/supported-odbc-sql-grammar-visual-foxpro-odbc-driver.md)。  
  
-   非 SQL Visual FoxPro 语言，如[支持的集命令](../../odbc/microsoft/supported-set-commands-visual-foxpro-odbc-driver.md)。  
  
 Visual FoxPro 的本机 SQL 的详细信息，请参阅 Visual FoxPro 文档。  
  
## <a name="example-using-the-visual-foxpro-odbc-driver-with-your-c-or-c-application"></a>示例： 使用 Visual FoxPro ODBC 驱动程序和 C 或 c + + 应用程序  
 以下示例使用 ODBC C API 来检索存储在名为 TasTrade 的 Microsoft® Visual FoxPro 示例数据库中的 employee 表的 last_name 字段中的数据。 此数据库随 Visual FoxPro 一起提供，默认情况下，在以下位置安装：  
  
 `c:\vfp\samples\mainsamp\data\tastrade.dbc`  
  
 此示例显示一个姓氏一次，您可以单击消息框上的确定以查看下一步的最后一个名称。 假定，名为 Tastrade 的数据源已设置为使用 Tastrade.dbc 数据库。  
  
> [!NOTE]  
>  对所有 ODBC API 调用; 应执行错误检查此示例不包括错误检查，为了简洁起见。  
  
```  
// FoxPro_ODBC_Driver_with_C.cpp  
// compile with: odbc32.lib user32.lib /c  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <stdio.h>  
#include <mbstring.h>  
  
#define MAX_DATA 100  
#define MYSQLSUCCESS(rc) ((rc==SQL_SUCCESS)||(rc==SQL_SUCCESS_WITH_INFO))  
  
class direxec {  
   RETCODE rc;        // ODBC return code  
   HENV henv;         // Environment     
   HDBC hdbc;         // Connection handle  
   HSTMT hstmt;       // Statement handle  
   unsigned char szData[MAX_DATA];   // Returned data storage  
   SDWORD cbData;     // Output length of data  
   unsigned char chr_ds_name[SQL_MAX_DSN_LENGTH];   // Data source name  
  
public:  
   direxec();           // Constructor  
   void sqlconn();      // Allocate env, stat, and conn  
   void sqlexec(unsigned char *);   // Execute SQL statement  
   void sqldisconn();   // Free pointers to env, stat, conn, and disconnect  
   void error_out();    // Displays errors  
};  
  
// Constructor initializes the string chr_ds_name with the data source name.  
direxec::direxec() {  
   _mbscpy_s(chr_ds_name, (const unsigned char *)"tastrade");  
}  
  
// Allocate environment handle, allocate connection handle,  
// connect to data source, and allocate statement handle.  
void direxec::sqlconn() {  
   SQLAllocEnv(&henv);  
   SQLAllocConnect(henv, &hdbc);  
   rc=SQLConnect(hdbc, chr_ds_name, SQL_NTS, NULL, 0, NULL, 0);  
  
   // Deallocate handles, display error message, and exit.  
   if (!MYSQLSUCCESS(rc)) {  
      SQLFreeEnv(henv);  
      SQLFreeConnect(hdbc);  
      error_out();  
      exit(-1);  
   }  
  
   rc = SQLAllocStmt(hdbc, &hstmt);  
}  
  
// Execute SQL command with SQLExecDirect() ODBC API.  
void direxec::sqlexec(unsigned char * cmdstr) {  
   rc = SQLExecDirect(hstmt, cmdstr, SQL_NTS);  
   if (!MYSQLSUCCESS(rc)) {   // Error  
      error_out();  
      // Deallocate handles and disconnect.  
      SQLFreeStmt(hstmt, SQL_DROP);  
      SQLDisconnect(hdbc);  
      SQLFreeConnect(hdbc);  
      SQLFreeEnv(henv);  
      exit(-1);  
   }  
   else {  
      for (rc = SQLFetch(hstmt) ; rc == SQL_SUCCESS; rc=SQLFetch(hstmt)) {  
         SQLGetData(hstmt, 1, SQL_C_CHAR, szData, sizeof(szData), &cbData);  
         // In this example, the data is returned in a messagebox for  
         // simplicity. However, normally the SQLBindCol() ODBC API could  
         // be called to bind individual data rows and assign for a rowset.  
         MessageBox(NULL, (const char *)szData, "ODBC", MB_OK);  
      }  
   }  
}  
  
// Free the statement handle, disconnect, free the connection handle, and  
// free the environment handle.  
void direxec::sqldisconn() {  
   SQLFreeStmt(hstmt, SQL_DROP);  
   SQLDisconnect(hdbc);  
   SQLFreeConnect(hdbc);  
   SQLFreeEnv(henv);  
}  
  
// Display error message in a message box that has an OK button.  
void direxec::error_out() {  
   unsigned char szSQLSTATE[10];  
   SDWORD nErr;  
   unsigned char msg[SQL_MAX_MESSAGE_LENGTH + 1];  
   SWORD cbmsg;  
  
   while(SQLError(0, 0, hstmt, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg) == SQL_SUCCESS) {  
      sprintf_s((char *)szData, MAX_DATA, "Error:\nSQLSTATE=%s, Native error=%ld, msg='%s'",   
         szSQLSTATE, nErr, msg);  
  
      MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
   }  
}  
  
int main (){  
   // Declare an instance of the direxec object.  
   direxec x;  
  
   // Allocate handles and connect.  
   x.sqlconn();  
  
   // Execute SQL command "SELECT last_name FROM employee".  
   x.sqlexec((UCHAR FAR *)"SELECT last_name FROM employee");  
  
   // Free handles, and disconnect.  
   x.sqldisconn();  
  
   // Return success code; example executed successfully.  
   return (TRUE);  
}  
```
