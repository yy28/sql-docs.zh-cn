---
title: SQLGetFunctions 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86f888955e6188cd7f90e54f39eeef3723dcfbe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897718"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLGetFunctions**返回有关驱动程序是否支持特定的 ODBC 函数的信息。 执行此函数在驱动程序管理器中;它还可以实现在驱动程序中。 如果驱动程序实现**SQLGetFunctions**，驱动程序管理器驱动程序中调用函数。 否则，它将执行该函数本身。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入] 连接句柄。  
  
 *FunctionId*  
 [输入]一个 **#define**值，该值标识感兴趣; 的 ODBC 函数**SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**。 **SQL_API_ODBC3_ALL_FUNCTIONS**由 ODBC 3 *.x*应用程序以确定是否支持 ODBC 3 *.x*和早期的函数。 **SQL_API_ALL_FUNCTIONS**由 ODBC 2 *.x*应用程序以确定是否支持 ODBC 2 *.x*和早期的函数。  
  
 有关一系列 **#define**标识 ODBC 函数的值，请参阅"注释。"中的表  
  
 *SupportedPtr*  
 [输出] 如果*FunctionId*标识一个单个的 ODBC 函数*SupportedPtr*指向单个 SQLUSMALLINT 值，该值是 SQL_TRUE 指定的函数是否支持驱动程序和 SQL_FALSE 如果不是受支持。  
  
 如果*FunctionId*是 SQL_API_ODBC3_ALL_FUNCTIONS， *SupportedPtr*指向具有大量的元素等于 SQL_API_ODBC3_ALL_FUNCTIONS_SIZE SQLSMALLINT 数组。 此数组由驱动程序管理器视为可用于确定是否 ODBC 3 4000 位位图 *.x*或支持早期的函数。 SQL_FUNC_EXISTS 宏调用以确定函数的支持。 （请参阅"注释"。）ODBC 3 *.x*应用程序可以调用**SQLGetFunctions**与针对任一 ODBC 3 SQL_API_ODBC3_ALL_FUNCTIONS *.x*或 ODBC 2 *.x*驱动程序。  
  
 如果*FunctionId*是 SQL_API_ALL_FUNCTIONS， *SupportedPtr*指向 SQLUSMALLINT 100 个元素数组。 按索引数组 **#define**使用的值*FunctionId*来标识每个 ODBC 函数; 数组的某些元素是未使用和保留供将来使用。 如果标识 ODBC 2，元素为 SQL_TRUE *.x*或早期驱动程序支持的函数。 如果它标识驱动程序不支持 ODBC 函数或不会识别了 ODBC 函数，则 SQL_FALSE。  
  
 在返回的数组 **SupportedPtr*使用从零开始的索引。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetFunctions**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetFunctions** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|Error|描述|  
|--------|-----|-----------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY010|函数序列错误|（数据挖掘） **SQLGetFunctions**之前已调用**SQLConnect**， **SQLBrowseConnect**，或者**SQLDriverConnect**。<br /><br /> （数据挖掘） **SQLBrowseConnect**曾为*ConnectionHandle*和返回 SQL_NEED_DATA。 此函数调用之前**SQLBrowseConnect**返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*ConnectionHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY095|函数类型超出了范围|(DM) 无效*FunctionId*指定的值。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
  
## <a name="comments"></a>注释  
 **SQLGetFunctions**始终返回该**SQLGetFunctions**， **SQLDataSources**，并且**SQLDrivers**支持。 这是因为这些函数的实现是驱动程序管理器中。 驱动程序管理器将映射到相应的 Unicode 函数的 ANSI 函数，如果 Unicode 函数存在，并且如果 ANSI 函数存在，则将映射到相应的 ANSI 函数的 Unicode 函数。 有关如何使用应用程序信息**SQLGetFunctions**，请参阅[接口一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 以下是一系列的有效值*FunctionId*符合 ISO 92 标准符合性级别的函数：  
  
|FunctionId 值|FunctionId 值|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 以下是一系列的有效值*FunctionId*符合 Open Group 标准符合性级别的函数：  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 以下是一系列的有效值*FunctionId*符合 ODBC 标准符合性级别的函数。  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] 时使用的 ODBC 2 *.x*驱动程序， **SQLBulkOperations**将被返回，因为仅支持如果下列两个条件成立： ODBC 2 *.x*驱动程序支持**SQLSetPos**，和的信息类型 SQL_POS_OPERATIONS 返回作为集的 SQL_POS_ADD 位。  
  
 以下是一系列的有效值*FunctionId*引入 ODBC 3.8 或更高版本的函数：  
  
|FunctionId 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle**将返回为仅在受支持的驱动程序支持同时**SQLCancel**并**SQLCancelHandle**。 如果**SQLCancel**支持，但**SQLCancelHandle**不是，应用程序仍然可以调用**SQLCancelHandle**上语句句柄，因为它将映射到**SQLCancel**。  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS 宏  
 SQL_FUNC_EXISTS (*SupportedPtr*， *FunctionID*) 宏用于确定是否支持 ODBC 3 *.x*早期函数后的或**SQLGetFunctions**已使用调用*FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS 参数。 在应用程序调用与 SQL_FUNC_EXISTS *SupportedPtr*参数设置为*SupportedPtr*传入*SQLGetFunctions*，并使用*FunctionID*参数设置为 **#define**函数。 SQL_FUNC_EXISTS 否则返回支持的函数，如果 SQL_TRUE 和 SQL_FALSE。  
  
> [!NOTE]
>  使用 ODBC 2 时 *.x*驱动程序，ODBC 3 *.x*驱动程序管理器将返回为 SQL_TRUE **SQLAllocHandle**和**SQLFreeHandle**因为**SQLAllocHandle**映射到**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**，和因为**SQLFreeHandle**映射到**SQLFreeEnv**， **SQLFreeConnect**，或者**SQLFreeStmt**。 **SQLAllocHandle**或**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC 参数不支持，但是，即使对于函数，返回 SQL_TRUE，因为没有任何ODBC 2 *.x*用于这种情况下将映射函数。  
  
## <a name="code-example"></a>代码示例  
 以下三个示例演示如何使用应用程序**SQLGetFunctions**若要确定驱动程序是否支持**SQLTables**， **SQLColumns**，和**SQLStatistics**。 如果该驱动程序不支持这些函数，该驱动程序从断开连接应用程序。 第一个示例调用**SQLGetFunctions**一次针对每个函数。  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 ODBC 3.x 应用程序在第二个示例中，调用**SQLGetFunctions**并在其中将其传递一个数组**SQLGetFunctions**返回信息所有 ODBC 3.x 和更早的函数。  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 第三个示例是 ODBC 2.x 应用程序调用**SQLGetFunctions**并将其传递在其中的 100 个元素的数组**SQLGetFunctions**返回信息所有 ODBC 2.x 和早期的函数。  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
