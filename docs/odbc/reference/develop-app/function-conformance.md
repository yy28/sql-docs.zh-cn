---
title: 函数一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45eb427b660496430334633b5d43ee8989211c0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069751"
---
# <a name="function-conformance"></a>函数一致性
下表指示这是定义完善的一致性级别的每个 ODBC 函数。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|**SQLAllocHandle**|Core|  
|**SQLBindCol**|Core|  
|**SQLBindParameter**|Core[1]|  
|**SQLBrowseConnect**|级别 1|  
|**SQLBulkOperations**|级别 1|  
|**SQLCancel**|Core[1]|  
|**SQLCloseCursor**|Core|  
|**SQLColAttribute**|Core[1]|  
|**SQLColumnPrivileges**|级别 2|  
|**SQLColumns**|Core|  
|**SQLConnect**|Core|  
|**SQLCopyDesc**|Core|  
|**SQLDataSources**|Core|  
|**SQLDescribeCol**|Core[1]|  
|**SQLDescribeParam**|级别 2|  
|**SQLDisconnect**|Core|  
|**SQLDriverConnect**|Core|  
|**SQLDrivers**|Core|  
|**SQLEndTran**|Core[1]|  
|**SQLExecDirect**|Core|  
|**SQLExecute**|Core|  
|**SQLFetch**|Core|  
|**SQLFetchScroll**|Core[1]|  
|**SQLForeignKeys**|级别 2|  
|**SQLFreeHandle**|Core|  
|**SQLFreeStmt**|Core|  
|**SQLGetConnectAttr**|Core|  
|**SQLGetCursorName**|Core|  
|**SQLGetData**|Core|  
|**SQLGetDescField**|Core|  
|**SQLGetDescRec**|Core|  
|**SQLGetDiagField**|Core|  
|**SQLGetDiagRec**|Core|  
|**SQLGetEnvAttr**|Core|  
|**SQLGetFunctions**|Core|  
|**SQLGetInfo**|Core|  
|**SQLGetStmtAttr**|Core|  
|**SQLGetTypeInfo**|Core|  
|**SQLMoreResults**|级别 1|  
|**SQLNativeSql**|Core|  
|**SQLNumParams**|Core|  
|**SQLNumResultCols**|Core|  
|**SQLParamData**|Core|  
|**SQLPrepare**|Core|  
|**SQLPrimaryKeys**|级别 1|  
|**SQLProcedureColumns**|级别 1|  
|**SQLProcedures**|级别 1|  
|**SQLPutData**|Core|  
|**SQLRowCount**|Core|  
|**SQLSetConnectAttr**|Core[2]|  
|**SQLSetCursorName**|Core|  
|**SQLSetDescField**|Core[1]|  
|**SQLSetDescRec**|Core|  
|**SQLSetEnvAttr**|Core[2]|  
|**SQLSetPos**|级别 1 [1]|  
|**SQLSetStmtAttr**|Core[2]|  
|**SQLSpecialColumns**|Core[1]|  
|**SQLStatistics**|Core|  
|**SQLTablePrivileges**|级别 2|  
|**SQLTables**|Core|  
  
 [1] 重要的功能，此函数仅在更高的符合性级别均可用。  
  
 [2] 将某些属性设置为非默认值取决于一致性级别。 有关详细信息，请参阅下一部分中，[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)。
