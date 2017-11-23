---
title: "函数一致性 |Microsoft 文档"
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
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 306dbd7c423a167806b01d0e3f00d1eafbd1a140
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="function-conformance"></a>函数一致性
下表指示这是定义完善的每个 ODBC 函数，一致性级别。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|**SQLAllocHandle**|核心|  
|**SQLBindCol**|核心|  
|**SQLBindParameter**|核心 [1]|  
|**SQLBrowseConnect**|级别 1|  
|**SQLBulkOperations**|级别 1|  
|**SQLCancel**|核心 [1]|  
|**SQLCloseCursor**|核心|  
|**SQLColAttribute**|核心 [1]|  
|**SQLColumnPrivileges**|级别 2|  
|**SQLColumns**|核心|  
|**SQLConnect**|核心|  
|**SQLCopyDesc**|核心|  
|**SQLDataSources**|核心|  
|**SQLDescribeCol**|核心 [1]|  
|**SQLDescribeParam**|级别 2|  
|**SQLDisconnect**|核心|  
|**SQLDriverConnect**|核心|  
|**SQLDrivers**|核心|  
|**SQLEndTran**|核心 [1]|  
|**SQLExecDirect**|核心|  
|**SQLExecute**|核心|  
|**SQLFetch**|核心|  
|**SQLFetchScroll**|核心 [1]|  
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
|**SQLSetDescField**|核心 [1]|  
|**SQLSetDescRec**|核心|  
|**SQLSetEnvAttr**|核心 [2]|  
|**SQLSetPos**|级别 1 [1]|  
|**SQLSetStmtAttr**|核心 [2]|  
|**SQLSpecialColumns**|核心 [1]|  
|**SQLStatistics**|核心|  
|**SQLTablePrivileges**|级别 2|  
|**SQLTables**|核心|  
  
 [此函数 1] 重要的功能功能仅在更高版本的一致性级别均可用。  
  
 [2] 将某些属性设置为非默认值取决于一致性级别。 有关详细信息，请参阅下一部分中，[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)。
