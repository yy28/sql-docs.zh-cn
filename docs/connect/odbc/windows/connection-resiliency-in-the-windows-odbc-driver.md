---
title: Windows ODBC 驱动程序中的连接弹性 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a038d146b21660e629c7ba7e44332aa6d2133a2c
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658161"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Windows ODBC 驱动程序中的连接弹性
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  为了确保应用程序能与 [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)] 保持连接，Windows 上的 ODBC 驱动程序可以还原空闲连接。  
  
> [!IMPORTANT]  
>  连接复原功能在 Microsoft Azure SQL Databases 和 SQL Server 2014（以及更高版本）服务器版本上受支持。  
  
 若要详细了解空闲连接复原，请参阅[技术文章 - 空闲连接复原](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Idle%20Connection%20Resiliency.docx)。
  
 为控制重新连接行为，Windows 上 的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 有以下两个选项：  
  
-   连接重试计数。  
  
     连接重试计数可在发生连接失败时，控制重新连接尝试的次数。 有效值范围为 0 到 255。 零 (0) 表示不尝试重新连接。 默认值为一次重新连接尝试。  
  
     在以下情况下可以修改连接重试次数：  
  
    -   定义或修改一个将 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 与“连接重试计数”  控件结合使用的数据源。  
  
    -   使用 **ConnectRetryCount** 连接字符串关键字。  
  
     若要检索连接重试尝试的次数，请使用 SQL_COPT_SS_CONNECT_RETRY_COUNT（只读）连接属性。 如果应用程序连接到的服务器并不支持连接复原，SQL_COPT_SS_CONNECT_RETRY_COUNT 将返回 0。  
  
-   连接重试间隔。  
  
     连接重试间隔指定每次连接重试尝试之间的秒数。 有效值介于 1 和 60 之间。 重新连接的总时间不能超过连接超时（SQLSetStmtAttr 中的 SQL_ATTR_QUERY_TIMEOUT）。 默认值为 10 秒。  
  
     在以下情况下可以修改连接重试间隔：  
  
    -   定义或修改一个将 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 与“连接重试间隔”  控件结合使用的数据源。  
  
    -   使用 **ConnectRetryInterval** 连接字符串关键字。  
  
     若要检索连接重试间隔的时间长度，请使用 SQL_COPT_SS_CONNECT_RETRY_INTERVAL（只读）连接属性。  
  
 如果应用程序建立与 SQL_DRIVER_COMPLETE_REQUIRED 的连接，并稍后尝试通过断开的连接执行语句，ODBC 驱动程序将不再显示该对话框。 此外，在恢复正在进行期间，  
  
-   在恢复期间，任何对 SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD) 的调用都必须返回 SQL_CD_FALSE。  
  
-   如果恢复失败，任何对 SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD) 的调用都必须返回 SQL_CD_TRUE。  
  
 在服务器上执行命令的任何函数都会返回以下状态代码：  
  
|State|消息|  
|-----------|-------------|  
|IMC01|连接已断开，且不能恢复。 客户端驱动程序尝试一次或多次恢复连接，但所有尝试均失败。 增大 ConnectRetryCount 的值以增加恢复尝试的次数。|  
|IMC02|服务器未收到恢复尝试，无法恢复连接。|  
|IMC03|服务器未保留恢复尝试过程中请求的确切客户端 TDS 版本，无法恢复连接。|  
|IMC04|服务器未保留恢复尝试过程中请求的确切服务器主要版本，无法恢复连接。|  
|IMC05|连接已断开，且不能恢复。 服务器将连接标记为不可恢复。 未尝试还原连接。|  
|IMC06|连接已断开，且不能恢复。 客户端驱动程序将连接标记为不可恢复。 未尝试还原连接。|  
  
## <a name="example"></a>示例  
 以下示例包含两个函数。 func1 演示如何通过使用 Windows 上的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的数据源名称 (DSN) 建立连接。 DSN 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，并指定用户 ID。 **func1**然后检索与的连接重试次数**SQL_COPT_SS_CONNECT_RETRY_COUNT**。  
  
 **func2** 使用 **SQLDriverConnect**、 **ConnectRetryCount** 连接字符串关键字和连接属性，检索连接重试和重试间隔的设置。  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
