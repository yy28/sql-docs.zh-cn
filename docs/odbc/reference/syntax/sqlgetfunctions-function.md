---
title: SQLGet 函数功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15537b28ff2bae8a4fcd3e7be82426eb53aa83a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285327"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGet功能**返回有关驱动程序是否支持特定 ODBC 函数的信息。 此功能在驱动程序管理器中实现;也可以在驱动程序中实现。 如果驱动程序实现**SQLGet 函数**，驱动程序管理器将在驱动程序中调用该函数。 否则，它将执行函数本身。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>参数  
 *连接句柄*  
 [输入] 连接句柄。  
  
 *功能 Id*  
 [输入]标识感兴趣的 ODBC 函数**的#define**值;**SQL_API_ODBC3_ALL_FUNCTIONSorSQL_API_ALL_FUNCTIONS。** **SQL_API_ODBC3_ALL_FUNCTIONS**由 ODBC 3 *.x*应用程序用于确定对 ODBC 3 *.x*和早期功能的支持。 **SQL_API_ALL_FUNCTIONS**由 ODBC 2 *.x*应用程序用于确定对 ODBC 2 *.x*和早期功能的支持。  
  
 有关标识 ODBC 函数 **#define**值的列表，请参阅"注释"中的表。  
  
 *支持的 Ptr*  
 [输出] 如果*函数 Id*标识单个 ODBC 函数，*则受支持的 Ptr*指向一个 SQLUSMALLINT 值，该值在驱动程序支持指定函数时SQL_TRUE，如果未支持该函数，则SQL_FALSE。  
  
 如果*函数 Id* SQL_API_ODBC3_ALL_FUNCTIONS，*则受支持的Ptr*指向具有许多元素等于SQL_API_ODBC3_ALL_FUNCTIONS_SIZE的 SQLSMALLINT 数组。 驱动程序管理器将此数组视为 4，000 位图，可用于确定是否支持 ODBC 3 *.x*或更早的功能。 调用SQL_FUNC_EXISTS宏以确定函数支持。 （请参阅"注释"。ODBC 3 *.x*应用程序可以针对 ODBC 3 *.x*或 ODBC 2 *.x*驱动程序使用SQL_API_ODBC3_ALL_FUNCTIONS调用**SQLGet 功能**。  
  
 如果*函数 Id* SQL_API_ALL_FUNCTIONS，*则受支持的Ptr*指向包含 100 个元素的 SQLUSMALLINT 数组。 数组由*函数 Id* **#define**用于标识每个 ODBC 函数的值#define索引;数组的某些元素未使用并保留以供将来使用。 如果元素标识驱动程序支持的 ODBC 2 *.x*或较早的函数，则SQL_TRUE该元素。 如果驱动程序未识别 ODBC 函数或未标识 ODBC 函数，则SQL_FALSE。  
  
 在 [ 支持*Ptr*中返回的数组使用零基索引。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGet 函数**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该*句柄类型*为SQL_HANDLE_DBC和*连接句柄*。 *Handle* 下表列出了**SQLGet 函数**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------|-----|-----------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQLGet函数**是在**SQLConnect、SQLBrowseConnect**或**SQLBrowseConnect****SQLDriverConnect**之前调用的。<br /><br /> （DM） **SQLBrowseConnect**被调用用于*连接句柄*并返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前调用此功能。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用用于*连接处理*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY095|函数类型范围外|（DM） 指定了无效*的函数 Id*值。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
  
## <a name="comments"></a>注释  
 **SQLGet 函数**始终返回**SQLGet 函数** **、SQLDataSources**和**SQLDrivers**受支持。 这样做是因为这些函数在驱动程序管理器中实现。 如果存在 Unicode 函数，驱动程序管理器将 ANSI 函数映射到相应的 Unicode 函数，并且如果存在 ANSI 函数，则将 Unicode 函数映射到相应的 ANSI 函数。 有关应用程序如何使用**SQLGet 函数**的信息，请参阅[接口一致性级别](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 以下是符合 ISO 92 标准合规性级别的*函数的函数 Id*的有效值列表：  
  
|函数 Id 值|函数 Id 值|  
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
  
 以下是符合开放组标准合规性级别的*函数的函数 Id*的有效值列表：  
  
|函数 Id 值|函数 Id 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 以下是符合 ODBC 标准合规性级别的*函数的函数 Id*的有效值列表。  
  
|函数 Id 值|函数 Id 值|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] 使用 ODBC 2 *.x*驱动程序时 **，SQLBulk操作**将返回为支持，仅当以下两个都为 true 时：ODBC 2 *.x*驱动程序支持**SQLSetPos，** 并且信息类型SQL_POS_OPERATIONS按设置返回SQL_POS_ADD位。  
  
 以下是 ODBC 3.8 或更高版本中引入的函数*的函数 Id*的有效值列表：  
  
|函数 Id 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle**将仅作为支持返回，因为驱动程序同时支持**SQLCancel**和**SQLCancelHandle**。 如果**SQLCancel**受支持，但**SQLCancelHandle**不支持，则应用程序仍然可以在语句句柄上调用**SQLCancelHandle，** 因为它将映射到**SQLCancel**。  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS宏  
 SQL_FUNC_EXISTS（*支持Ptr，**函数ID）* 宏用于确定在**SQLGet 函数**使用函数*id*参数SQL_API_ODBC3_ALL_FUNCTIONS调用后对 ODBC 3 *.x*或早期函数的支持。 应用程序调用SQL_FUNC_EXISTS与*支持Ptr*参数设置为在*SQLGet 函数*中传递*的受支持的 Ptr，* 并且*函数 ID*参数设置为函数的 **#define。** 如果支持该函数，SQL_FUNC_EXISTS返回SQL_TRUE，否则SQL_FALSE。  
  
> [!NOTE]
>  使用 ODBC 2 *.x*驱动程序时，ODBC 3 *.x*驱动程序管理器将返回**SQLAllocHandle**和**SQLFreeHandle** SQL_TRUE，因为**SQLAllocHandle**映射到**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt，** 并且因为**SQLFreeHandle**映射到**SQLFreeEnv、SQLFreeConnect**或**SQLFreestmt**。 **SQLAllocConnect** **SQLFreeConnect** 但是，即使为函数返回了SQL_TRUE，但不支持具有SQL_HANDLE_DESC*句柄类型*参数的**SQLAllocHandle**或**SQLFreeHandle，** 因为在这种情况下没有要映射到的 ODBC 2 *.x*函数。  
  
## <a name="code-example"></a>代码示例  
 以下三个示例显示了应用程序如何使用**SQLGet 函数**来确定驱动程序是否支持**SQLTables、SQLColumns**和**SQLStatistics**。 **SQLColumns** 如果驱动程序不支持这些功能，则应用程序将断开与驱动程序的连接。 第一个示例为每个函数调用**SQLGet 函数**一次。  
  
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
  
 在第二个示例中，ODBC 3.x 应用程序调用**SQLGet功能**并传递一个数组，其中**SQLGet 函数**返回有关所有 ODBC 3.x 和早期函数的信息。  
  
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
  
 第三个示例是 ODBC 2.x 应用程序调用**SQLGet功能**，并传递一个包含 100 个元素的数组，其中**SQLGet 函数**返回有关所有 ODBC 2.x 和早期函数的信息。  
  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回有关驱动程序或数据源的信息|[SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
