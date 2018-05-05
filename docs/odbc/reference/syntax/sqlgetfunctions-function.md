---
title: SQLGetFunctions 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740742dc80325a26f24effd7e29d808715fd42f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetFunctions**返回有关驱动程序是否支持特定的 ODBC 函数的信息。 此函数被实现在驱动程序管理器中;它可以还在实现驱动程序。 如果驱动程序实现**SQLGetFunctions**，驱动程序管理器驱动程序中调用函数。 否则，它将执行该函数本身。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *FunctionId*  
 [输入]A **#define**值，该值标识相关; ODBC 函数**SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**。 **SQL_API_ODBC3_ALL_FUNCTIONS**由 ODBC 3 *.x*应用程序以确定支持 ODBC 3 *.x*和更早版本的函数。 **SQL_API_ALL_FUNCTIONS**由 ODBC 2 *.x*应用程序以确定支持 ODBC 2 *.x*和更早版本的函数。  
  
 有关的列表 **#define**值，标识 ODBC 函数，请参阅"注释。"中的表  
  
 *SupportedPtr*  
 [输出] 如果*FunctionId*标识单个 ODBC 函数*SupportedPtr*指向单个 SQLUSMALLINT 值，该值是 SQL_TRUE 指定的函数是否支持的驱动程序，以及 SQL_FALSE，如果不是支持。  
  
 如果*FunctionId*是 SQL_API_ODBC3_ALL_FUNCTIONS， *SupportedPtr*指向与大量的元素等于 SQL_API_ODBC3_ALL_FUNCTIONS_SIZE SQLSMALLINT 数组。 此数组被视为由驱动程序管理器可以用于确定是否 ODBC 3 4000 位位图 *.x*或支持更早版本的函数。 SQL_FUNC_EXISTS 宏调用以确定函数的支持。 （请参阅"注释"。）ODBC 3 *.x*应用程序可以调用**SQLGetFunctions**与针对任一 ODBC 3 SQL_API_ODBC3_ALL_FUNCTIONS *.x*或 ODBC 2 *.x*驱动程序。  
  
 如果*FunctionId*是 SQL_API_ALL_FUNCTIONS， *SupportedPtr*指向 SQLUSMALLINT 100 个元素数组。 按索引数组 **#define**使用的值*FunctionId*来标识每个 ODBC 函数; 数组的某些元素是指未使用和保留供将来使用。 元素是 SQL_TRUE，如果它标识 ODBC 2 *.x*或更早版本的驱动程序支持的函数。 如果确定驱动程序不支持 ODBC 函数或没有标识 ODBC 函数，它则 SQL_FALSE。  
  
 在返回的数组 **SupportedPtr*使用从零开始的索引。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetFunctions**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetFunctions**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------|-----|-----------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) **SQLGetFunctions**之前已调用**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**。<br /><br /> (DM) **SQLBrowseConnect**曾为*ConnectionHandle*并返回 SQL_NEED_DATA。 此函数调用之前**SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS 返回。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*ConnectionHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY095|函数类型超出了范围|(DM) 无效*FunctionId*指定的值。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
  
## <a name="comments"></a>注释  
 **SQLGetFunctions**始终返回， **SQLGetFunctions**， **SQLDataSources**，和**SQLDrivers**支持。 它这样做是因为这些函数的实现在驱动程序管理器中。 驱动程序管理器会映射到相应的 Unicode 函数 ANSI 函数，如果 Unicode 函数存在，并将将 Unicode 函数映射到相应的 ANSI 函数，如果存在的 ANSI 函数。 有关如何使用应用程序信息**SQLGetFunctions**，请参阅[界面一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 以下是有效值的列表*FunctionId*符合 ISO 92 标准 – 法规遵从性级别的函数：  
  
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
  
 以下是有效值的列表*FunctionId*符合 Open Group 标准 – 法规遵从性级别的函数：  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 以下是有效值的列表*FunctionId*符合 ODBC 标准 – 法规遵从性级别的函数。  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS [1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] 使用 ODBC 2 时 *.x*驱动程序， **SQLBulkOperations**将返回仅支持下列两个条件，则： ODBC 2 *.x*驱动程序支持**SQLSetPos**，和的信息类型 SQL_POS_OPERATIONS 返回作为组的 SQL_POS_ADD 位。  
  
 以下是有效值的列表*FunctionId*引入 ODBC 3.8 或更高版本的函数：  
  
|FunctionId 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle**将返回这些结果仅受支持的驱动程序支持同时**SQLCancel**和**SQLCancelHandle**。 如果**SQLCancel**支持但**SQLCancelHandle**不是，应用程序仍然可以调用**SQLCancelHandle**在语句句柄，因为它将映射到**SQLCancel**。  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS 宏  
 SQL_FUNC_EXISTS (*SupportedPtr*， *FunctionID*) 宏用于确定支持 ODBC 3 *.x*或之后的早期函数**SQLGetFunctions**已调用与*FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS 自变量。 在应用程序调用与 SQL_FUNC_EXISTS *SupportedPtr*参数设置为*SupportedPtr*传入*SQLGetFunctions*，且*FunctionID*参数设置为 **#define**函数。 SQL_FUNC_EXISTS 否则，返回 SQL_TRUE 如果支持该函数，则和 SQL_FALSE。  
  
> [!NOTE]  
>  使用 ODBC 2 时 *.x*驱动程序，ODBC 3 *.x*驱动程序管理器将返回有关 SQL_TRUE **SQLAllocHandle**和**SQLFreeHandle**因为**SQLAllocHandle**映射到**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**，和因为**SQLFreeHandle**映射到**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**。 **SQLAllocHandle**或**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC 参数不支持，但是，即使 SQL_TRUE 返回对于函数，因为没有任何ODBC 2 *.x*用于在此情况下将映射到函数。  
  
## <a name="code-example"></a>代码示例  
 下面的三个示例演示应用程序如何使用**SQLGetFunctions**确定如果驱动程序支持**SQLTables**， **SQLColumns**，和**SQLStatistics**。 如果该驱动程序不支持这些功能，应用程序断开与该驱动程序连接。 第一个示例调用**SQLGetFunctions**一次针对每个函数。  
  
```  
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
  
 在第二个示例中，ODBC 3.x 应用程序调用**SQLGetFunctions**并将其传递在其中的数组**SQLGetFunctions**返回有关所有 ODBC 信息 3.x 和更早版本的函数。  
  
```  
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
  
 第三个示例是 ODBC 2.x 应用程序调用**SQLGetFunctions**并将其传递顺序的 100 个元素数组**SQLGetFunctions**返回有关所有 ODBC 信息 2.x 和更早版本的函数。  
  
```  
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
|返回有关的驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|返回语句特性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
