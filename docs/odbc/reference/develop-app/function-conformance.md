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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069751"
---
# <a name="function-conformance"></a>函数一致性
下表指明了每个 ODBC 函数的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|**SQLAllocHandle**|核心|  
|**SQLBindCol**|核心|  
|**SQLBindParameter**|Core [1]|  
|**SQLBrowseConnect**|级别 1|  
|**SQLBulkOperations**|级别 1|  
|**SQLCancel**|Core [1]|  
|**SQLCloseCursor**|核心|  
|**SQLColAttribute**|Core [1]|  
|**SQLColumnPrivileges**|级别 2|  
|**SQLColumns**|核心|  
|**SQLConnect**|核心|  
|**SQLCopyDesc**|核心|  
|**SQLDataSources**|核心|  
|**SQLDescribeCol**|Core [1]|  
|**SQLDescribeParam**|级别 2|  
|**SQLDisconnect**|核心|  
|**SQLDriverConnect**|核心|  
|**SQLDrivers**|核心|  
|**SQLEndTran**|Core [1]|  
|**SQLExecDirect**|核心|  
|**SQLExecute**|核心|  
|**SQLFetch**|核心|  
|**SQLFetchScroll**|Core [1]|  
|**SQLForeignKeys**|级别 2|  
|**SQLFreeHandle**|核心|  
|**SQLFreeStmt**|核心|  
|**SQLGetConnectAttr**|核心|  
|**SQLGetCursorName**|核心|  
|**SQLGetData**|核心|  
|**SQLGetDescField**|核心|  
|**SQLGetDescRec**|核心|  
|**SQLGetDiagField**|核心|  
|**SQLGetDiagRec**|核心|  
|**SQLGetEnvAttr**|核心|  
|**SQLGetFunctions**|核心|  
|**SQLGetInfo**|核心|  
|**SQLGetStmtAttr**|核心|  
|**SQLGetTypeInfo**|核心|  
|**SQLMoreResults**|级别 1|  
|**SQLNativeSql**|核心|  
|**SQLNumParams**|核心|  
|**SQLNumResultCols**|核心|  
|**SQLParamData**|核心|  
|**SQLPrepare**|核心|  
|**SQLPrimaryKeys**|级别 1|  
|**SQLProcedureColumns**|级别 1|  
|**SQLProcedures**|级别 1|  
|**SQLPutData**|核心|  
|**SQLRowCount**|核心|  
|**SQLSetConnectAttr**|核心 [2]|  
|**SQLSetCursorName**|核心|  
|**SQLSetDescField**|Core [1]|  
|**SQLSetDescRec**|核心|  
|**SQLSetEnvAttr**|核心 [2]|  
|**SQLSetPos**|级别 1 [1]|  
|**SQLSetStmtAttr**|核心 [2]|  
|**SQLSpecialColumns**|Core [1]|  
|**SQLStatistics**|核心|  
|**SQLTablePrivileges**|级别 2|  
|**SQLTables**|核心|  
  
 [1] 此函数的重要功能只能在更高的一致性级别上使用。  
  
 [2] 将某些属性设置为非默认值取决于一致性级别。 有关详细信息，请参阅下一节 "[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)"。
