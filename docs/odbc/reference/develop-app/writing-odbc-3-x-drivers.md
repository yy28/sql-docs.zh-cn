---
title: "编写 ODBC 3.x 驱动程序 |Microsoft 文档"
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
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ea639a8bde008d657cff558183220d7e68fe568
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="writing-odbc-3x-drivers"></a>编写 ODBC 3.x 驱动程序
下表显示了 ODBC 3 中的函数的支持。*x*驱动程序和 ODBC 应用程序，以及针对 ODBC 3 调用函数时执行的驱动程序管理器中的映射。*x*驱动程序。  
  
|函数|是否支持<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 驱动程序？|是否支持<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 应用程序？|映射支持<br /><br /> 由 ODBC 3 中。*x*<br /><br /> 到的驱动程序管理器<br /><br /> ODBC 3。*x*驱动程序？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|是|没有 [1]|是|  
|**SQLAllocEnv**|是|没有 [1]|是|  
|**SQLAllocHandle**|是|是|是|  
|**SQLAllocStmt**|是|没有 [1]|是|  
|**SQLBindCol**|是|是|是|  
|**SQLBindParam**|是|是 [2]|是|  
|**SQLBindParameter**|是|是|是|  
|**SQLBrowseConnect**|是|是|是|  
|**SQLBulkOperations**|是|是|是|  
|**SQLCancel**|是|是|是|  
|**SQLCloseCursor**|是|是|是|  
|**SQLColAttribute**|是|是|是|  
|**SQLColAttributes**|没有 [3]|是|是|  
|**SQLColumnPrivileges**|是|是|是|  
|**SQLColumns**|是|是|是|  
|**SQLConnect**|是|是|是|  
|**SQLCopyDesc**|是|是|是 [4]|  
|**SQLDataSources**|是|是|是|  
|**SQLDescribeCol**|是|是|是|  
|**SQLDescribeParam**|是|是|是|  
|**SQLDisconnect**|是|是|是|  
|**SQLDriverConnect**|是|是|是|  
|**SQLDrivers**|是|是|是|  
|**SQLEndTran**|是|是|是|  
|**SQLError**|是|没有 [1]|是|  
|**SQLExecDirect**|是|是|是|  
|**SQLExecute**|是|是|是|  
|**SQLExtendedFetch**|是|“否”|是|  
|**SQLFetch**|是|是|是|  
|**SQLFetchScroll**|是|是|是|  
|**SQLForeignKeys**|是|是|是|  
|**SQLFreeConnect**|是|是 [1]|是|  
|**SQLFreeEnv**|是|是 [1]|是|  
|**SQLFreeHandle**|是|是|是|  
|**SQLFreeStmt**|是|是|是|  
|**SQLGetConnectAttr**|是|是|是|  
|**SQLGetConnectOption**|没有 [5]|没有 [1]|是|  
|**SQLGetCursorName**|是|是|是|  
|**SQLGetData**|是|是|是|  
|**SQLGetDescField**|是|是|是|  
|**SQLGetDescRec**|是|是|是|  
|**SQLGetDiagField**|是|是|是|  
|**SQLGetDiagRec**|是|是|是|  
|**SQLGetEnvAttr**|是|是|是|  
|**SQLGetFunctions**|没有 [6]|是|是|  
|**SQLGetInfo**|是|是|是|  
|**SQLGetStmtAttr**|是|是|是|  
|**SQLGetStmtOption**|没有 [5]|没有 [1]|是|  
|**SQLGetTypeInfo**|是|是|是|  
|**SQLMoreResults**|是|是|是|  
|**SQLNativeSql**|是|是|是|  
|**SQLNumParams**|是|是|是|  
|**SQLNumResultCols**|是|是|是|  
|**SQLParamData**|是|是|是|  
|**SQLParamOptions**|是|是|是|  
|**SQLPrepare**|是|是|是|  
|**SQLPrimaryKeys**|是|是|是|  
|**SQLProcedureColumns**|是|是|是|  
|**SQLProcedures**|是|是|是|  
|**SQLPutData**|是|是|是|  
|**SQLRowCount**|是|是|是|  
|**SQLSetConnectAttr**|是|是|是|  
|**SQLSetConnectOption**|没有 [5]|没有 [1]|是|  
|**SQLSetCursorName**|是|是|是|  
|**SQLSetDescField**|是|是|是|  
|**SQLSetDescRec**|是|是|是|  
|**SQLSetEnvAttr**|是|是|是|  
|**SQLSetPos**|是|是|是|  
|**SQLSetParam**|是|是|是|  
|**SQLSetScrollOption**|是|是|是|  
|**SQLSetStmtAttr**|是|是|是|  
|**SQLSetStmtOption**|没有 [5]|没有 [1]|是|  
|**SQLSpecialColumns**|是|是|是|  
|**SQLStatistics**|是|是|是|  
|**SQLTablePrivileges**|是|是|是|  
|**SQLTables**|是|是|是|  
|**SQLTransact**|是|没有 [1]|是|  
  
 [1] 此函数已弃用 ODBC 3 中。*x*。 ODBC 3。*x*应用程序不应使用此函数。 但是，开放组或符合 ISO CLI – 应用程序可以调用此函数。  
  
 [2] ODBC 3。*x*应用程序应使用**SQLBindParameter**而不是**SQLBindParam**。 但是，开放组或符合 ISO CLI – 应用程序可以调用此函数。  
  
 [3] 驱动程序编写器应该注意，ODBC 2。*x*列属性必须为 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH 支持， **SQLColAttribute**。  
  
 [4] **SQLCopyDesc**时描述符正在跨属于不同的驱动程序的连接进行复制的部分实现由驱动程序管理器。 支持所需的驱动程序**SQLCopyDesc**跨两个自己的连接。 函数如**SQLDrivers**，这实现仅由驱动程序管理器，不会显示在此列表。  
  
 [5] 在某些情况下，驱动程序可能需要支持此函数。 有关详细信息，请参阅此函数的引用页。  
  
 [6] 上，驱动程序可以选择支持**SQLGetFunctions**如果的一套驱动程序支持的函数会连接到连接发生变化。
