---
title: 编写 ODBC 3.x 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4d281ce0c0bcf50525daaf337577bdf0dd1ba26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="writing-odbc-3x-drivers"></a>编写 ODBC 3.x 驱动程序
下表显示了 ODBC 3 中的函数的支持。*x*驱动程序和 ODBC 应用程序，以及针对 ODBC 3 调用函数时执行的驱动程序管理器中的映射。*x*驱动程序。  
  
|函数|Supported<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 驱动程序？|Supported<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 应用程序？|映射支持<br /><br /> 由 ODBC 3 中。*x*<br /><br /> 到的驱动程序管理器<br /><br /> ODBC 3。*x*驱动程序？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|否|没有 [1]|是|  
|**SQLAllocEnv**|否|没有 [1]|是|  
|**SQLAllocHandle**|是|用户帐户控制|否|  
|**SQLAllocStmt**|否|没有 [1]|是|  
|**SQLBindCol**|是|用户帐户控制|否|  
|**SQLBindParam**|否|是 [2]|是|  
|**SQLBindParameter**|是|用户帐户控制|否|  
|**SQLBrowseConnect**|是|用户帐户控制|否|  
|**SQLBulkOperations**|是|用户帐户控制|否|  
|**SQLCancel**|是|用户帐户控制|否|  
|**SQLCloseCursor**|是|用户帐户控制|否|  
|**SQLColAttribute**|是|用户帐户控制|否|  
|**SQLColAttributes**|没有 [3]|否|是|  
|**SQLColumnPrivileges**|是|用户帐户控制|否|  
|**SQLColumns**|是|用户帐户控制|否|  
|**SQLConnect**|是|用户帐户控制|否|  
|**SQLCopyDesc**|是|是|是 [4]|  
|**SQLDataSources**|否|用户帐户控制|是|  
|**SQLDescribeCol**|是|用户帐户控制|否|  
|**SQLDescribeParam**|是|用户帐户控制|否|  
|**SQLDisconnect**|是|用户帐户控制|否|  
|**SQLDriverConnect**|是|用户帐户控制|否|  
|**SQLDrivers**|否|用户帐户控制|是|  
|**SQLEndTran**|是|用户帐户控制|否|  
|**SQLError**|否|没有 [1]|是|  
|**SQLExecDirect**|是|用户帐户控制|否|  
|**SQLExecute**|是|用户帐户控制|否|  
|**SQLExtendedFetch**|是|是|否|  
|**SQLFetch**|是|用户帐户控制|否|  
|**SQLFetchScroll**|是|用户帐户控制|否|  
|**SQLForeignKeys**|是|用户帐户控制|否|  
|**SQLFreeConnect**|否|是 [1]|是|  
|**SQLFreeEnv**|否|是 [1]|是|  
|**SQLFreeHandle**|是|用户帐户控制|否|  
|**SQLFreeStmt**|是|用户帐户控制|否|  
|**SQLGetConnectAttr**|是|用户帐户控制|否|  
|**SQLGetConnectOption**|没有 [5]|没有 [1]|是|  
|**SQLGetCursorName**|是|用户帐户控制|否|  
|**SQLGetData**|是|用户帐户控制|否|  
|**SQLGetDescField**|是|用户帐户控制|否|  
|**SQLGetDescRec**|是|用户帐户控制|否|  
|**SQLGetDiagField**|是|用户帐户控制|否|  
|**SQLGetDiagRec**|是|用户帐户控制|否|  
|**SQLGetEnvAttr**|是|用户帐户控制|否|  
|**SQLGetFunctions**|没有 [6]|是|是|  
|**SQLGetInfo**|是|用户帐户控制|否|  
|**SQLGetStmtAttr**|是|用户帐户控制|否|  
|**SQLGetStmtOption**|没有 [5]|没有 [1]|是|  
|**SQLGetTypeInfo**|是|用户帐户控制|否|  
|**SQLMoreResults**|是|用户帐户控制|否|  
|**SQLNativeSql**|是|用户帐户控制|否|  
|**SQLNumParams**|是|用户帐户控制|否|  
|**SQLNumResultCols**|是|用户帐户控制|否|  
|**SQLParamData**|是|用户帐户控制|否|  
|**SQLParamOptions**|否|“否”|是|  
|**SQLPrepare**|是|用户帐户控制|否|  
|**SQLPrimaryKeys**|是|用户帐户控制|否|  
|**SQLProcedureColumns**|是|用户帐户控制|否|  
|**SQLProcedures**|是|用户帐户控制|否|  
|**SQLPutData**|是|用户帐户控制|否|  
|**SQLRowCount**|是|用户帐户控制|否|  
|**SQLSetConnectAttr**|是|用户帐户控制|否|  
|**SQLSetConnectOption**|没有 [5]|没有 [1]|是|  
|**SQLSetCursorName**|是|用户帐户控制|否|  
|**SQLSetDescField**|是|用户帐户控制|否|  
|**SQLSetDescRec**|是|用户帐户控制|否|  
|**SQLSetEnvAttr**|是|用户帐户控制|否|  
|**SQLSetPos**|是|用户帐户控制|否|  
|**SQLSetParam**|否|“否”|是|  
|**SQLSetScrollOption**|是|用户帐户控制|否|  
|**SQLSetStmtAttr**|是|用户帐户控制|否|  
|**SQLSetStmtOption**|没有 [5]|没有 [1]|是|  
|**SQLSpecialColumns**|是|用户帐户控制|否|  
|**SQLStatistics**|是|用户帐户控制|否|  
|**SQLTablePrivileges**|是|用户帐户控制|否|  
|**SQLTables**|是|用户帐户控制|否|  
|**SQLTransact**|否|没有 [1]|是|  
  
 [1] 此函数已弃用 ODBC 3 中。*x*。 ODBC 3。*x*应用程序不应使用此函数。 但是，开放组或符合 ISO CLI – 应用程序可以调用此函数。  
  
 [2] ODBC 3。*x*应用程序应使用**SQLBindParameter**而不是**SQLBindParam**。 但是，开放组或符合 ISO CLI – 应用程序可以调用此函数。  
  
 [3] 驱动程序编写器应该注意，ODBC 2。*x*列属性必须为 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH 支持， **SQLColAttribute**。  
  
 [4] **SQLCopyDesc**时描述符正在跨属于不同的驱动程序的连接进行复制的部分实现由驱动程序管理器。 支持所需的驱动程序**SQLCopyDesc**跨两个自己的连接。 函数如**SQLDrivers**，这实现仅由驱动程序管理器，不会显示在此列表。  
  
 [5] 在某些情况下，驱动程序可能需要支持此函数。 有关详细信息，请参阅此函数的引用页。  
  
 [6] 上，驱动程序可以选择支持**SQLGetFunctions**如果的一套驱动程序支持的函数会连接到连接发生变化。
