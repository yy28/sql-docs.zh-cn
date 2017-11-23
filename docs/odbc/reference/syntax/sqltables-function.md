---
title: "SQLTables 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLTables
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLTables
helpviewer_keywords: SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be1a2ce0aea9d34ee1fcb8c1f26c5b5147105819
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqltables-function"></a>SQLTables 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： Open Group  
  
 **摘要**  
 **SQLTables**返回的表、 目录或架构名称和表类型，存储在特定数据源的列表。 驱动程序返回信息作为结果集。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄检索结果。  
  
 *CatalogName*  
 [输入]目录名称。 *CatalogName*参数接受搜索模式，如果 SQL_ODBC_VERSION 环境属性是 SQL_OV_ODBC3; 它不接受搜索模式，如果设置 SQL_OV_ODBC2。 如果驱动程序支持目录，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有目录的那些表。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *CatalogName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *CatalogName*是一个模式值参数; 它原义，处理和其大小写很重要。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]以字符为单位的长度 **CatalogName*。  
  
 *SchemaName*  
 [输入]架构名称的字符串的搜索模式。 如果驱动程序支持的架构，对于某些表但没有为其他，如当驱动程序检索数据从不同 Dbms，空字符串 ("") 指示没有架构的那些表。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *SchemaName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *SchemaName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength2*  
 [输入]以字符为单位的长度 **SchemaName*。  
  
 *表名*  
 [输入]表名称的字符串的搜索模式。  
  
 如果 SQL_ATTR_METADATA_ID 语句属性设置为 SQL_TRUE， *TableName*视为标识符和其大小写并不重要。 如果它是 SQL_FALSE， *TableName*是一个模式值参数; 它原义，处理和其大小写很重要。  
  
 *NameLength3*  
 [输入]以字符为单位的长度 **TableName*。  
  
 *TableType*  
 [输入]要匹配的表类型的列表。  
  
 请注意 SQL_ATTR_METADATA_ID 语句属性不影响*TableType*自变量。 *TableType*是值列表自变量，而不考虑 SQL_ATTR_METADATA_ID 的设置。  
  
 *NameLength4*  
 [输入]以字符为单位的长度 **TableType*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLTables**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLTables**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|24000|无效的游标状态|在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。 此错误返回由驱动程序管理器中，如果**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA 和在驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 SQL_NO_DATA。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|40001|序列化失败|事务已回滚，由于资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE， *CatalogName*自变量为 null 指针和 SQL_CATALOG_NAME*信息类型*支持中返回该目录名称。<br /><br /> (DM) SQL_ATTR_METADATA_ID 语句属性已设置为 SQL_TRUE，和*SchemaName*或*TableName*自变量是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 调用 SQLTables 时仍在执行此异步函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 之一的长度参数的值小于 0，但不是等于 sql_nts 以。<br /><br /> 名称长度自变量之一的值超出限制的相应名称的最大长度值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|指定了目录，并且在驱动程序或数据源不支持目录。<br /><br /> 指定了架构，并且在驱动程序或数据源不支持架构。<br /><br /> 为目录名称、 表架构或表名指定字符串的搜索模式和数据源不支持为一个或多个这些自变量的搜索模式。<br /><br /> 驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|查询超时期限过期之前返回请求的结果集的数据源。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 **SQLTables**列出请求的范围中的所有表。 用户可能或可能不具有任何这些表的选择权限。 若要检查可访问性，应用程序可以：  
  
-   调用**SQLGetInfo**和检查 SQL_ACCESSIBLE_TABLES 信息类型。  
  
-   调用**SQLTablePrivileges**检查每个表的特权。  
  
 否则，应用程序必须能够处理的情况下，用户为其选择一个表的其中**选择**不授予特权。  
  
 *SchemaName*和*TableName*参数接受搜索模式。 *CatalogName*参数接受搜索模式，如果 SQL_ODBC_VERSION 环境属性是 SQL_OV_ODBC3; 它不接受搜索模式，如果设置 SQL_OV_ODBC2。 如果设置 SQL_OV_ODBC3，ODBC 3*.x*驱动程序将需要该通配符中*CatalogName*自变量进行转义以原义处理。 有关有效的搜索模式的详细信息，请参阅[模式值自变量](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有关常规使用、 自变量和返回的数据的 ODBC 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 若要支持的目录、 架构和表类型枚举，下面的特殊语义为上定义*CatalogName*， *SchemaName*， *TableName*，和*TableType*的自变量**SQLTables**:  
  
-   如果*CatalogName*是 SQL_ALL_CATALOGS 和*SchemaName*和*TableName*都是空字符串，结果集包含的数据源的有效目录的列表。 （TABLE_CAT 列除外的所有列都包含 null 值）。  
  
-   如果*SchemaName*是 SQL_ALL_SCHEMAS 和*CatalogName*和*TableName*都是空字符串，结果集包含的数据源的有效架构的列表。 （TABLE_SCHEM 列除外的所有列都包含 null 值）。  
  
-   如果*TableType*是 SQL_ALL_TABLE_TYPES 和*CatalogName*， *SchemaName*，和*TableName*都是空字符串，结果集包含的数据源的有效的表类型的列表。 （TABLE_TYPE 列除外的所有列都包含 null 值）。  
  
 如果*TableType*不为空字符串，它必须包含逗号分隔值相关的类型的列表; 可以括在单引号 （'） 或却不加引号，例如，表、 查看或表，查看每个值。 应用程序应始终指定表类型以大写;该驱动程序应将表类型转换为任何用例所需的数据源。 如果数据源不支持指定的表类型**SQLTables**不返回该类型的任何结果。  
  
 **SQLTables**标准的结果集，按 TABLE_TYPE、 TABLE_CAT、 TABLE_SCHEM 和 TABLE_NAME 排序的形式返回结果。 有关如何可能使用此信息的信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要确定 TABLE_CAT、 TABLE_SCHEM 和 TABLE_NAME 列的实际长度，应用程序可以调用**SQLGetInfo**的 SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 信息类型。  
  
 下面的列已重命名为 ODBC 3*.x*。 列名称更改不会影响向后兼容性原因是应用程序绑定的列号。  
  
|ODBC 2.0 列|ODBC 3*.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出在结果集中的列。 可通过该驱动程序定义列 5 （备注) 之外的其他列。 应用程序应访问驱动程序的特定列的倒计时从结尾处的结果集而不是指定显式的序号位置。 有关详细信息，请参阅[目录函数返回数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目录名称;如果不适用于数据源为 NULL。 如果驱动程序支持目录对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有目录这些表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|架构名称;如果不适用于数据源为 NULL。 如果驱动程序支持架构对于某些表，但对于其他操作系统，例如，如果驱动程序从不同 Dbms 检索数据，它将返回空字符串 ("") 不具有架构这些表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|表名。|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|表类型名称;以下项之一:"表"、"视图"、"系统表"、"全局临时"、"本地临时"、"别名"、"同义词"或数据源 – 特定的类型名称。<br /><br /> "别名"和"同义词"的意义进行了特定于驱动程序。|  
|备注 (ODBC 1.0)|5|Varchar|表的说明。|  
  
## <a name="example"></a>示例  
 下面的示例代码不会释放句柄和连接。 请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)和[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)有关代码示例，以释放句柄和语句。  
  
```  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回为一列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|返回一个表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取单个行或只进方向中的数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|返回一个表或表的权限|[SQLTablePrivileges 函数](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
