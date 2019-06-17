---
title: 编写 ODBC 3.x 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f548e1496ce45d9fdb4677fd9659de349e5c5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636102"
---
# <a name="writing-odbc-3x-drivers"></a>编写 ODBC 3.x 驱动程序
下表显示了在 ODBC 3 函数支持。*x*驱动程序和 ODBC 应用程序，以及针对 ODBC 3 调用函数时执行由驱动程序管理器中的映射。*x*驱动程序。  
  
|函数|支持<br /><br /> 通过<br /><br /> ODBC 3.*x*<br /><br /> 驱动程序？|支持<br /><br /> 通过<br /><br /> ODBC 3.*x*<br /><br /> 应用程序？|映射的/受支持<br /><br /> 通过 ODBC 3 中。*x*<br /><br /> 为驱动程序管理器<br /><br /> ODBC 3。*x*驱动程序？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|否|No[1]|是|  
|**SQLAllocEnv**|否|No[1]|是|  
|**SQLAllocHandle**|是|是|否|  
|**SQLAllocStmt**|否|No[1]|是|  
|**SQLBindCol**|是|是|否|  
|**SQLBindParam**|否|是 [2]|是|  
|**SQLBindParameter**|是|是|否|  
|**SQLBrowseConnect**|是|是|否|  
|**SQLBulkOperations**|是|是|否|  
|**SQLCancel**|是|是|否|  
|**SQLCloseCursor**|是|是|否|  
|**SQLColAttribute**|是|是|否|  
|**SQLColAttributes**|No[3]|否|是|  
|**SQLColumnPrivileges**|是|是|否|  
|**SQLColumns**|是|是|否|  
|**SQLConnect**|是|是|否|  
|**SQLCopyDesc**|是|是|是 [4]|  
|**SQLDataSources**|否|是|是|  
|**SQLDescribeCol**|是|是|否|  
|**SQLDescribeParam**|是|是|否|  
|**SQLDisconnect**|是|是|否|  
|**SQLDriverConnect**|是|是|否|  
|**SQLDrivers**|否|是|是|  
|**SQLEndTran**|是|是|否|  
|**SQLError**|否|No[1]|是|  
|**SQLExecDirect**|是|是|否|  
|**SQLExecute**|是|是|否|  
|**SQLExtendedFetch**|是|否|否|  
|**SQLFetch**|是|是|否|  
|**SQLFetchScroll**|是|是|否|  
|**SQLForeignKeys**|是|是|否|  
|**SQLFreeConnect**|否|是 [1]|是|  
|**SQLFreeEnv**|否|是 [1]|是|  
|**SQLFreeHandle**|是|是|否|  
|**SQLFreeStmt**|是|是|否|  
|**SQLGetConnectAttr**|是|是|否|  
|**SQLGetConnectOption**|No[5]|No[1]|是|  
|**SQLGetCursorName**|是|是|否|  
|**SQLGetData**|是|是|否|  
|**SQLGetDescField**|是|是|否|  
|**SQLGetDescRec**|是|是|否|  
|**SQLGetDiagField**|是|是|否|  
|**SQLGetDiagRec**|是|是|否|  
|**SQLGetEnvAttr**|是|是|否|  
|**SQLGetFunctions**|No[6]|是|是|  
|**SQLGetInfo**|是|是|否|  
|**SQLGetStmtAttr**|是|是|否|  
|**SQLGetStmtOption**|No[5]|No[1]|是|  
|**SQLGetTypeInfo**|是|是|否|  
|**SQLMoreResults**|是|是|否|  
|**SQLNativeSql**|是|是|否|  
|**SQLNumParams**|是|是|否|  
|**SQLNumResultCols**|是|是|否|  
|**SQLParamData**|是|是|否|  
|**SQLParamOptions**|否|否|是|  
|**SQLPrepare**|是|是|否|  
|**SQLPrimaryKeys**|是|是|否|  
|**SQLProcedureColumns**|是|是|否|  
|**SQLProcedures**|是|是|否|  
|**SQLPutData**|是|是|否|  
|**SQLRowCount**|是|是|否|  
|**SQLSetConnectAttr**|是|是|否|  
|**SQLSetConnectOption**|No[5]|No[1]|是|  
|**SQLSetCursorName**|是|是|否|  
|**SQLSetDescField**|是|是|否|  
|**SQLSetDescRec**|是|是|否|  
|**SQLSetEnvAttr**|是|是|否|  
|**SQLSetPos**|是|是|否|  
|**SQLSetParam**|否|否|是|  
|**SQLSetScrollOption**|是|是|否|  
|**SQLSetStmtAttr**|是|是|否|  
|**SQLSetStmtOption**|No[5]|No[1]|是|  
|**SQLSpecialColumns**|是|是|否|  
|**SQLStatistics**|是|是|否|  
|**SQLTablePrivileges**|是|是|否|  
|**SQLTables**|是|是|否|  
|**SQLTransact**|否|No[1]|是|  
  
 [1] 此函数已弃用在 ODBC 3。*x*。 ODBC 3。*x*应用程序不应使用此函数。 但是，Open Group 或符合 ISO CLI 的应用程序可以调用此函数。  
  
 [2] ODBC 3。*x*应用程序应使用**SQLBindParameter**而不是**SQLBindParam**。 但是，Open Group 或符合 ISO CLI 的应用程序可以调用此函数。  
  
 [3] 驱动程序编写人员应该注意，ODBC 2。*x*列属性必须与支持 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH **SQLColAttribute**。  
  
 [4] **SQLCopyDesc**部分实现由驱动程序管理器复制描述符时跨属于不同的驱动程序的连接。 支持所需的驱动程序**SQLCopyDesc**跨两个其自己的连接。 之类的函数**SQLDrivers**，这实现仅由驱动程序管理器，不会显示在此列表上。  
  
 [5] 在某些情况下，驱动程序可能需要支持此函数。 有关详细信息，请参阅此函数的参考页。  
  
 [6]，驱动程序可以选择以支持**SQLGetFunctions**如果的驱动程序支持的函数集各不相同连接连接。
