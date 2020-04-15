---
title: 分配句柄并连接到 SQL 服务器 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d26af711c07c4ea296d5351d0fcb0d1f9710706
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294457"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>分配句柄并连接到 SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>分配句柄并连接到 SQL Server  
  
1.  包含 ODBC 头文件 Sql.h、Sqlext.h、Sqltypes.h。  
  
2.  包含特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驱动程序的头文件 Odbcss.h。  
  
3.  使用**处理类型**调用[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) SQL_HANDLE_ENV 以初始化 ODBC 并分配环境句柄。  
  
4.  将[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)设置为SQL_ATTR_ODBC_VERSION，ValuePtr 设置为SQL_OV_ODBC3，以指示应用程序将使用 ODBC 3.x 格式函数调用。 **Attribute** **ValuePtr**  
  
5.  或者，调用[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)来设置其他环境选项，或者调用[SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403)获取环境选项。  
  
6.  使用**句柄类型**SQL_HANDLE_DBC调用[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396)以分配连接句柄。  
  
7.  或者，调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)来设置连接选项，或者调用[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)获取连接选项。  
  
8.  调用 SQLConnect 使用现有数据源连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     Or  
  
     调用[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)使用连接字符串连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     最小的完整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接字符串采用以下两种格式之一：  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     如果连接字符串不完整 **，SQLDriverConnect**可以提示输入所需的信息。 这由为*驱动程序完成*参数指定的值控制。  
  
     \- 或 -  
  
     以迭代方式多次调用[SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)以生成连接字符串并连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
9. 或者，调用[SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)获取数据源的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驱动程序属性和行为。  
  
10. 分配并使用语句。  
  
11. 调用 SQL 断开连接以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]断开连接，并使连接句柄可用于新连接。  
  
12. 使用**SQL_HANDLE_DBC的句柄类型**调用[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)以释放连接句柄。  
  
13. 使用**SQL_HANDLE_ENV的句柄类型**调用**SQLFreeHandle**以释放环境句柄。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果必须保留凭据，则应使用[Win32 加密 API](https://go.microsoft.com/fwlink/?LinkId=64532)对其进行加密。  
  
## <a name="example"></a>示例  
 此示例显示对**SQLDriverConnect**的调用，以连接到 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而无需现有的 ODBC 数据源。 通过将不完整的连接字符串传递到**SQLDriverConnect，** 它会导致 ODBC 驱动程序提示用户输入缺少的信息。  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
