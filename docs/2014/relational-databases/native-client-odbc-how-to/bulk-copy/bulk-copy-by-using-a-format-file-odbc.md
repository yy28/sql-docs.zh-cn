---
title: 使用格式化文件进行大容量复制（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy using format file [ODBC]
- ODBC, bulk copy operations
ms.assetid: 970fd3af-f918-4fc3-a5b1-92596515d4de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2dc0ac57b132a0e681337b358a951a0e33f56db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72688907"
---
# <a name="bulk-copy-by-using-a-format-file-odbc"></a>使用格式化文件执行大容量复制 (ODBC)
  此示例显示如何将 ODBC bcp_init 函数用于格式化文件。  
  
### <a name="to-bulk-copy-by-using-a-format-file"></a>使用格式化文件执行大容量复制  
  
1.  分配环境句柄和连接句柄。  
  
2.  设置 SQL_COPT_SS_BCP 和 SQL_BCP_ON 以启用大容量复制操作。  
  
3.  连接到 Microsoft SQL Server。  
  
4.  调用[bcp_init](../../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)以设置以下信息：  
  
    -   作为大容量复制的源或目标的表或视图的名称。  
  
    -   包含要复制到数据库中的数据的数据文件的名称，或者当从数据库中复制时接收数据的数据文件的名称。  
  
    -   接收任何大容量复制错误消息的数据文件的名称（如果您不需要消息文件，请指定 NULL）。  
  
    -   复制方向：DB_IN 表示从文件复制到表或视图。  
  
5.  调用[bcp_readfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)读取用于描述大容量复制操作要使用的数据文件的格式化文件。  
  
6.  调用[bcp_exec](../../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)执行大容量复制操作。  
  
## <a name="example"></a>示例  
 IA64 平台不支持此示例。  
  
 需要一个名为 AdventureWorks 的 ODBC 数据源，其默认数据库是 AdventureWorks 示例数据库。 （您可以从 " [Microsoft SQL Server 示例和社区项目](https://go.microsoft.com/fwlink/?LinkID=85384)" 主页下载 AdventureWorks 示例数据库。）此数据源必须基于操作系统提供的 ODBC 驱动程序（驱动程序名称为 "SQL Server"）。 如果您要将此示例构建为在 64 位操作系统上运行的 32 位应用程序并运行该示例，则必须使用 %windir%\SysWOW64\odbcad32.exe 中的 ODBC 管理器创建 ODBC 数据源。  
  
 此示例连接到您的计算机上默认的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 若要连接到命名实例，请更改 ODBC 数据源的定义以使用以下格式指定实例：server\namedinstance。 默认情况下，[!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] 将安装在命名实例中。  
  
 执行第一个（[!INCLUDE[tsql](../../../includes/tsql-md.md)]）代码列表，以创建此示例将使用的表。  
  
 复制第二个代码列表，并将其粘贴到名为 Bcpfmt.fmt 的文件中。 表中的每一列均由制表符分隔。  
  
 复制第三个代码列表，并将其粘贴到名为 Bcpodbc.bcp 的文件中。 文件中每个回车符之前都有一个制表符。  
  
 使用 odbc32.lib 和 odbcbcp.lib 编译第四个 (C++) 代码列表。 如果用 MSBuild.exe 生成示例，请先将 Bcpfmt.fmt 和 Bcpodbc.bcp 从项目目录复制到 .exe 文件所在的目录，然后调用 .exe。  
  
 执行第五个 ([!INCLUDE[tsql](../../../includes/tsql-md.md)]) 代码列表，以删除该示例使用的表。  
  
```sql
use AdventureWorks  
CREATE TABLE BCPDate (cola int, colb datetime)  
```  
  
```  
8.0  
2  
1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
```  
  
```  
1  
2  
```  
  
```cpp
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
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
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```sql
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server ODBC 驱动程序的大容量复制操作指南主题 &#40;ODBC&#41;](bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [使用数据文件和格式化文件](../../native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
  
