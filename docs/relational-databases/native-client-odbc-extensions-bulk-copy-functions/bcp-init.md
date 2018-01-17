---
title: bcp_init | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_init
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19e15b0c56bc673bff3bd88bc3b5a639e54ea48c
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2018
---
# <a name="bcpinit"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  初始化大容量复制操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 *szTable*  
 要向内或向外复制的数据库表的名称。 该名称还可以包含数据库名称或所有者名称。 例如， **pubs.gracie.titles**， **pubs...标题**， **gracie.titles**，和**标题**是所有的合法的表名称。  
  
 如果*eDirection*是将， *szTable*也可以是数据库视图的名称。  
  
 如果*eDirection*将，并且使用指定的 SELECT 语句[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)之前[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)调用时， **bcp_init** *szTable*必须设置为 NULL。  
  
 *szDataFile*  
 要向内或向外复制的用户文件的名称。 如果复制数据的变量中直接使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)，将其设置*szDataFile*为 NULL。  
  
 *szErrorFile*  
 使用进度消息、错误消息，以及出于任何原因无法从用户文件复制到表的任何行的副本填充的错误文件的名称。 如果作为传递 NULL *szErrorFile*，不使用任何文件时出错。  
  
 *eDirection*  
 复制方向为 DB_IN 或 DB_OUT。 DB_IN 指示从程序变量或用户文件复制到表中。 DB_OUT 指示从数据库表复制到用户文件中。 必须使用 DB_OUT 指定一个用户文件名。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 调用**bcp_init**之前调用任何其他大容量复制函数。 **在 bcp_init**用于大容量复制工作站之间的数据执行必要的初始化和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **Bcp_init**函数必须提供了用于大容量复制函数启用一个 ODBC 连接句柄。 若要启用该句柄，请使用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)与 SQL_COPT_SS_BCP 上的已分配，但未连接，连接的句柄设置为 SQL_BCP_ON。 尝试对已连接的句柄分配属性将导致错误。  
  
 指定数据文件时， **bcp_init**检查数据库源或目标表，不是数据文件的结构。 **在 bcp_init**指定每个列中的数据库表、 视图或选择结果集所基于的数据文件的数据格式值。 此指定包括每一列的数据类型、数据中是否存在长度或 Null 指示符和终止符字节字符串以及固定长度的数据类型的宽度。 **在 bcp_init**设置这些值，如下所示：  
  
-   指定的数据类型是数据库表、视图或 SELECT 结果集中的列的数据类型。 数据类型由 sqlncli.h 中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机数据类型枚举。 数据自身采用它所在的计算机格式表示。 即，从列中的数据**整数**数据类型由很大的 4 字节序列的或小 endian 基于创建数据文件的计算机上。  
  
-   如果数据库数据类型的长度是固定的，则该数据文件中的数据长度也是固定的。 处理数据的大容量复制函数 (例如， [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)) 分析数据行应为要与数据库表、 视图或所选列列表中指定的数据的长度相同的数据文件中的数据的长度。 例如，为数据库列定义为数据**char （13)**必须由文件中的数据的每一行的 13 个字符来表示。 如果数据库列允许 Null 值，则可以使用 Null 指示符作为固定长度的数据的前缀。  
  
-   定义终止符字节序列时，该终止符字节序列的长度设置为 0。  
  
-   向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制时，数据文件必须包含数据库表中的每列数据。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制时，数据库表、视图或 SELECT 结果集中的所有列的数据均被复制到数据文件中。  
  
-   向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制时，数据文件中的列序号位置必须与数据库表中的列序号位置相同。 当从复制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **bcp_exec**放置在数据库表中的列的序号位置上基于的数据。  
  
-   如果某个数据库数据类型的长度的变量 (例如， **varbinary(22)**) 或数据库列可以包含 null 值，如果数据文件中的数据由长度/null 指示符的前缀。 指示符的宽度因数据类型和大容量复制的版本而异。  
  
 若要更改为数据文件指定的数据格式值，请调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)和[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。  
  
 对于不包含索引的表，通过将数据库恢复模式设置为 SIMPLE 或 BULK_LOGGED 可以优化向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的大容量复制。 有关详细信息，请参阅[Prerequisites for Minimal Logging 中大容量导入](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)和[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)。  
  
 如果使用没有数据文件，则必须调用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)若要在内存中的每个列的数据中指定的格式和位置，然后向其中复制数据行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)。  
  
## <a name="example"></a>示例  
 此示例显示如何将 ODBC bcp_init 函数用于格式化文件。  
  
 编译并运行在 C++ 代码之前，您需要执行以下操作：  
  
-   创建名为 Test 的 ODBC 数据源。 您可以将此数据源与任何数据库相关联。  
  
-   对数据库运行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)]：  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   在您将在其中运行应用程序的目录中，添加名为 Bcpfmt.fmt 的文件，并将以下内容添加到此文件中：  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   在您将在其中运行应用程序的目录中，添加名为 Bcpodbc.bcp 的文件，并将以下内容添加到此文件中：  
  
    ```  
    1  
    2  
    ```  
  
 现在，您可以编译并运行此 C++ 代码了。  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
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
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
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
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
