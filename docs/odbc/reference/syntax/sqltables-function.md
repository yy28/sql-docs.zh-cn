---
title: SQLTables 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae52e6431679ed0f260e6885090ac38363b4ef3d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287127"
---
# <a name="sqltables-function"></a>SQLTables 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 开放组  
  
 **摘要**  
 **SQLTables**返回存储在特定数据源中的表、目录或架构名称以及表类型的列表。 驱动程序将返回结果集。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *语句句柄*  
 [输入]已检索结果的语句句柄。  
  
 *CatalogName*  
 [输入]目录名称。 如果SQL_ODBC_VERSION环境属性SQL_OV_ODBC3，则*目录名称*参数接受搜索模式;如果环境属性SQL_OV_ODBC3，则目录名称参数接受搜索模式。如果设置了SQL_OV_ODBC2，则不接受搜索模式。 如果驱动程序支持某些表的目录，但不支持其他表的目录，例如当驱动程序从不同的 DBMS 检索数据时，空字符串（"）表示那些没有目录的表。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，则*目录名称*将被视为标识符，其大小写不重要。 如果它SQL_FALSE，目录名称是模式值参数;如果为 SQL_FALSE，则 *"目录名称"* 是模式值参数。它被从字面上处理，它的情况很重要。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [输入]长度在 **目录名称*的字符中。  
  
 *架构名称*  
 [输入]架构名称的字符串搜索模式。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），则空字符串（"）表示那些没有架构的表。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则 SchemaName*被视为标识符，其大小写不重要。 如果SQL_FALSE，则 SchemaName 是模式值参数;如果为 SQL_FALSE，则 *"架构名称"* 是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度2*  
 [输入]长度在 **架构名称*的字符中。  
  
 *表名称*  
 [输入]表名称的字符串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*则表Name*被视为标识符，其大小写不重要。 如果SQL_FALSE，*则表名称*是模式值参数;如果为"表名称"，则表名称是模式值参数。它被从字面上处理，它的情况很重要。  
  
 *名称长度3*  
 [输入]=*表名*的字符的长度。  
  
 *表类型*  
 [输入]要匹配的表类型的列表。  
  
 请注意，SQL_ATTR_METADATA_ID 语句属性对*表类型*参数没有影响。 *表类型*是值列表参数，无论SQL_ATTR_METADATA_ID设置如何。  
  
 *名称长度4*  
 [输入]=*表类型*中的字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLTables**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_STMT的*句柄类型*和*语句句柄*。 下表列出了 SQLTables 通常返回的**SQLSTATE**值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|24000|无效的游标状态|语句*处理*上打开了一个游标，并且调用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA，则驱动程序管理器将返回此错误，如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA，则驱动程序将返回此错误。<br /><br /> *语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|40001|序列化失败|由于资源与另一个事务死锁，事务被回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*目录名称*参数为空指针，SQL_CATALOG_NAME *InfoType*返回目录名称受支持。<br /><br /> （DM） SQL_ATTR_METADATA_ID语句属性设置为SQL_TRUE，*而 SchemaName*或*TableName*参数是空指针。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQLTables 时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 长度参数之一的值小于 0，但不等于SQL_NTS。<br /><br /> 其中一个名称长度参数的值超过相应名称的最大长度值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|指定了目录，驱动程序或数据源不支持目录。<br /><br /> 已指定架构，驱动程序或数据源不支持架构。<br /><br /> 为目录名称、表架构或表名称指定了字符串搜索模式，数据源不支持一个或多个这些参数的搜索模式。<br /><br /> 驱动程序或数据源不支持SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE，SQL_ATTR_CURSOR_TYPE语句属性设置为驱动程序不支持书签的游标类型。|  
|HYT00|超时时间已到|查询超时期限在数据源返回请求的结果集之前已过期。 超时期间通过**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT设置。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 **SQLTables**列出了请求范围内的所有表。 用户可能拥有或可能没有对这些表的 SELECT 权限。 要检查辅助功能，应用程序可以：  
  
-   致电**SQLGetInfo**并检查SQL_ACCESSIBLE_TABLES信息类型。  
  
-   调用**SQLTable 特权**以检查每个表的权限。  
  
 否则，应用程序必须能够处理用户选择未为其授予**SELECT**权限的表的情况。  
  
 *架构名称*和*表名称*参数接受搜索模式。 如果SQL_ODBC_VERSION环境属性SQL_OV_ODBC3，则*目录名称*参数接受搜索模式;如果环境属性SQL_OV_ODBC3，则目录名称参数接受搜索模式。如果设置了SQL_OV_ODBC2，则不接受搜索模式。 如果设置了SQL_OV_ODBC3，则 ODBC 3 *.x*驱动程序将要求从*目录名称*参数中的通配符转义才能从字面上处理。 有关有效搜索模式的详细信息，请参阅[模式值参数](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有关 ODBC 目录函数的一般使用、参数和返回数据的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 为了支持对目录、架构和表类型的枚举，为**SQLTable**的*目录名称*、*架构名称*、*表名称*和*表类型*参数定义了以下特殊语义：  
  
-   如果*目录名称*为SQL_ALL_CATALOGS，*并且架构名称*和*表名*为空字符串，则结果集包含数据源的有效目录列表。 （除TABLE_CAT列外的所有列都包含 NUL。  
  
-   如果*SchemaName*是SQL_ALL_SCHEMAS，*目录名称*和*表名*为空字符串，则结果集包含数据源的有效架构列表。 （除TABLE_SCHEM列外的所有列都包含 NUL。  
  
-   如果*表类型*为SQL_ALL_TABLE_TYPES，*目录名称*、*架构名称*和*表名称*为空字符串，则结果集包含数据源的有效表类型列表。 （除TABLE_TYPE列外的所有列都包含 NUL。  
  
 如果*TableType*不是空字符串，它必须包含感兴趣类型的逗号分隔值列表;因此，它必须包含一个逗号分隔的值。每个值可以包含在单个引号 （'） 或未引用，例如，"TABLE"，"视图"或 TABLE，视图。 应用程序应始终以大写指定表类型;因此，应用程序应始终以大写大小表示表类型。驱动程序应将表类型转换为数据源所需的任何情况。 如果数据源不支持指定的表类型 **，SQLTables**不会返回该类型的任何结果。  
  
 **SQLTables**将结果作为标准结果集返回，由TABLE_TYPE、TABLE_CAT、TABLE_SCHEM和TABLE_NAME排序。 有关如何使用此信息的信息，请参阅[目录数据的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 要确定TABLE_CAT、TABLE_SCHEM和TABLE_NAME列的实际长度，应用程序可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN和SQL_MAX_TABLE_NAME_LEN信息类型调用**SQLGetInfo。**  
  
 以下列已重命名为 ODBC 3 *.x*。 列名称更改不会影响向后兼容性，因为应用程序按列号绑定。  
  
|ODBC 2.0 列|ODBC 3 *.x*列|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出了结果集中的列。 驱动程序可以定义第 5 列 （注释） 以外的其他列。 应用程序应通过从结果集的末尾倒计时而不是指定显式单位位置来获得对特定于驱动程序的列的访问权限。 有关详细信息，请参阅[目录函数返回的数据](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|列名称|列号|数据类型|注释|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|目录名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的目录，但不支持其他表的目录（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有目录的表。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|架构名称;如果不适用于数据源，则为 NULL。 如果驱动程序支持某些表的架构，但不支持其他表的架构（例如当驱动程序从不同的 DBMS 检索数据时），它将返回一个空字符串（""），用于那些没有架构的表。|  
|TABLE_NAME （ODBC 1.0）|3|Varchar|表名。|  
|TABLE_TYPE （ODBC 1.0）|4|Varchar|表类型名称;下列："TABLE"、"视图"、"系统表"、"全球临时"、"本地临时"、"ALIAS"、"SYNONYM"或数据源特定类型名称。<br /><br /> "ALIAS"和"SYNONYM"的含义特定于驱动程序。|  
|备注 （ODBC 1.0）|5|Varchar|表的说明。|  
  
## <a name="example"></a>示例  
 以下示例代码不释放句柄和连接。 有关代码示例以释放句柄和语句，请参阅[SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)和[SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|返回列或列的权限|[SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|返回表或表中的列|[SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以仅转发方向获取单个行或数据块|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回表统计信息和索引|[SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|返回表或表的权限|[SQLTablePrivileges Function（SQLTablePrivileges 函数）](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
