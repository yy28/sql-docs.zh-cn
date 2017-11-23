---
title: "ODBC API 参考 |Microsoft 文档"
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
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 348b9a8bead318f99f0ab85f0f961e64a56770f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-api-reference"></a>ODBC API 参考
此部分中的主题描述了每个 ODBC 函数按字母顺序。 每个函数定义为 C 编程语言的函数。 说明如下所示：  
  
-   用途  
  
-   ODBC 版本  
  
-   标准 CLI 一致性级别  
  
-   语法  
  
-   参数  
  
-   返回值  
  
-   诊断  
  
-   有关用法和实现注释  
  
-   代码示例  
  
-   对相关函数的引用  
  
 标准的 CLI 一致性级别可以是以下之一： ISO 92、 Open Group、 ODBC 或已弃用。 标记为符合的 ISO 92 – 也将出现在 Open Group 版本 1，因为 Open Group 是 ISO 92 的纯超集函数。 标记为打开组符合函数也会出现在 ODBC 3。*x*，因为 ODBC 3。*x*为纯 Open Group 版本 1 的超集。 标记为符合 ODBC 的函数显示在既不标准。 ODBC 3 中，标记为已弃用的函数已弃用。*x*。  
  
 中介绍了的诊断信息的处理[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。 SQLSTATE 值与关联的文本包含是为了提供条件的说明，但不是要规定特定文本。  
  
> [!NOTE]  
>  有关 ODBC 函数特定于驱动程序的信息，请参阅驱动程序部分。  
  
 本部分包含有关以下函数的主题：  
  
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
  
-   [SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
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
  
-   [SQLProcedureColumns 函数](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 函数](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount 函数](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
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
  
-   [SQLTablePrivileges 函数](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables 函数](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact 函数](../../../odbc/reference/syntax/sqltransact-function.md)
