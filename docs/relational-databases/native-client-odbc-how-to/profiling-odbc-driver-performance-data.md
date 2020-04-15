---
title: 配置文件驱动程序性能数据 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9fa6612f7a9cf0a3e4f26ae4aa42623ec56b268
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282011"
---
# <a name="profiling-odbc-driver-performance-data"></a>分析 ODBC 驱动程序性能数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  此示例显示用于记录性能统计信息的特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驱动程序的选项； 其中创建了一个文件：odbcperf.log。此示例显示如何直接从 SQLPERF 数据结构（SQLPERF 结构在 Odbcss.h 中定义）创建性能数据日志文件和显示性能数据。 此示例是面向 ODBC 3.0 版或更高版本开发的。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果必须保留凭据，则应使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)对其进行加密。  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>使用 ODBC 管理器记录驱动程序性能数据  
  
1.  在**控制面板**中，双击**管理工具**，然后双击**数据源 （ODBC）。** 或者，可以调用 odbcad32.exe。  
  
2.  单击**用户 DSN、****系统 DSN**或**文件 DSN**选项卡。  
  
3.  单击要记录其性能的数据源。  
  
4.  单击 **“配置”**。  
  
5.  在 Microsoft SQL 服务器配置 DSN 向导中，导航到包含**日志 ODBC 驱动程序统计信息的页面到日志文件**。  
  
6.  选择**将 ODBC 驱动程序统计信息记录到日志文件**。 在该框中，放置应记录统计信息的文件的名称。 可选，单击 **"浏览"** 以浏览统计信息日志的文件系统。  
  
### <a name="to-log-driver-performance-data-programmatically"></a>通过编程方式记录驱动程序性能数据  
  
1.  使用SQL_COPT_SS_PERF_DATA_LOG和性能数据日志文件的完整路径和文件名调用[SQLSetConnectAttr。](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 例如：  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  使用SQL_COPT_SS_PERF_DATA和SQL_PERF_START调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)以开始记录性能数据。  
  
3.  或者，使用SQL_COPT_SS_LOG_NOW和 NULL 调用[SQLSetConnectAttr，](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)将性能数据的选项卡分隔记录写入性能数据日志文件。 此操作可以在应用程序运行时执行多次。  
  
4.  使用SQL_COPT_SS_PERF_DATA和SQL_PERF_STOP调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)以停止记录性能数据。  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>将驱动程序性能数据拖到某一应用程序中  
  
1.  使用SQL_COPT_SS_PERF_DATA和SQL_PERF_START调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)以开始分析性能数据。  
  
2.  使用SQL_COPT_SS_PERF_DATA和指向 SQLPERF 结构的指针的地址调用[SQLGetConnectAttr。](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 第一个此类调用将设置一个指针，该指针指向包含当前性能数据的有效 SQLPERF 结构的地址。 驱动程序并不连续刷新该性能结构中的数据。 应用程序必须在需要使用更当前性能数据刷新结构时重复对[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)的调用。  
  
3.  使用SQL_COPT_SS_PERF_DATA和SQL_PERF_STOP调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)以停止记录性能数据。  
  
## <a name="example"></a>示例  
 需要一个名为 AdventureWorks 的 ODBC 数据源，其默认数据库是 AdventureWorks 示例数据库。 （可以从[Microsoft SQL 服务器示例和社区项目](https://go.microsoft.com/fwlink/?LinkID=85384)主页下载 AdventureWorks 示例数据库。此数据源必须基于操作系统提供的 ODBC 驱动程序（驱动程序名称为"SQL Server"）。 如果您要将此示例构建为在 64 位操作系统上运行的 32 位应用程序并运行该示例，则必须使用 %windir%\SysWOW64\odbcad32.exe 中的 ODBC 管理器创建 ODBC 数据源。  
  
 此示例连接到您的计算机上默认的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 若要连接到命名实例，请更改 ODBC 数据源的定义以使用以下格式指定实例：server\namedinstance。 默认情况下，[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 将安装在命名实例中。  
  
 使用 odbc32.lib 进行编译。  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
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
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [分析 ODBC 驱动程序性能执行方式&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)   
 [ODBC 驱动程序性能事件探查](../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
