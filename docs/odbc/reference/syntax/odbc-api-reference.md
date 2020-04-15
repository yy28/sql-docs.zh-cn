---
title: ODBC API 参考 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6065db0ea99efaec11190902ec9268db63a6d255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298931"
---
# <a name="odbc-api-reference"></a>ODBC API 参考
本节中的主题按字母顺序描述每个 ODBC 函数。 每个函数被定义为 C 编程语言函数。 描述包括以下内容：  
  
-   目标  
  
-   ODBC 版本  
  
-   标准 CLI 符合性级别  
  
-   语法  
  
-   参数  
  
-   返回值  
  
-   诊断  
  
-   关于使用和实现的评论  
  
-   代码示例  
  
-   对相关函数的引用  
  
 标准 CLI 符合性级别可以是以下级别之一：ISO 92、开放组、ODBC 或已弃用。 标记为 ISO 92 符合项的函数也出现在 Open Group 版本 1 中，因为 Open Group 是 ISO 92 的纯超级集。 在 ODBC 3 中也会显示标记为"符合开放组"的函数。*x*，因为 ODBC 3.*x*是开放组版本 1 的纯超级集。 标记为符合 ODBC 的函数在这两个标准中都显示。 在 ODBC 3 中已弃用标记为弃用的函数。*x*. .  
  
 诊断信息的处理在[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数描述中描述。 包含与 SQLSTATE 值关联的文本是为了提供条件的描述，但不打算规定特定文本。  
  
> [!NOTE]  
>  有关 ODBC 函数的特定于驱动程序的信息，请参阅驱动程序的部分。  
  
 本节包含以下功能的主题：  
  
-   [SQLAllocConnect 函数](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [SQLAllocEnv 函数](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLAllocStmt 函数](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [SQLCloseCursor 函数](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [SQLColAttribute 函数](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [SQLColAttributes 函数](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [SQLColumnPrivileges 函数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [SQLColumns 函数](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [SQLCompleteAsync 函数](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [SQLCopyDesc 函数](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [SQLDataSources 函数](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDescribeCol 函数](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [SQLDescribeParam 函数](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [SQLDrivers 函数](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [SQLError 函数](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [SQLExtendedFetch 函数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys 函数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect 函数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv 函数](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle 函数](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt 函数](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption 函数](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [SQLGetCursorName 函数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [SQLGetDiagField 函数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLGetEnvAttr 函数](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetFunctions 函数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLGetInfo 函数](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [SQLGetStmtOption 函数](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [SQLGetTypeInfo 函数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [SQLMoreResults 函数](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [SQLNativeSql 函数](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [SQLNumParams 函数](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols 函数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [SQLParamOptions 函数](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys 函数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns Function（SQLProcedureColumns 函数）](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount Function（SQLRowCount 函数）](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption 函数](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [SQLSetParam 函数](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [SQLSetScrollOptions 函数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [SQLSetStmtOption 函数](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [SQLSpecialColumns 函数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [SQLStatistics 函数](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [SQLTablePrivileges Function（SQLTablePrivileges 函数）](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact 函数](../../../odbc/reference/syntax/sqltransact-function.md)
