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
ms.openlocfilehash: 77a94c7505b5ab221fee4896e91f9b26850669df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795646"
---
# <a name="writing-odbc-3x-drivers"></a>编写 ODBC 3.x 驱动程序
下表显示了在 ODBC 3 函数支持。*x*驱动程序和 ODBC 应用程序，以及针对 ODBC 3 调用函数时执行由驱动程序管理器中的映射。*x*驱动程序。  
  
|函数|是否支持<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 驱动程序？|是否支持<br /><br /> 通过<br /><br /> ODBC 3。*x*<br /><br /> 应用程序？|映射的/受支持<br /><br /> 通过 ODBC 3 中。*x*<br /><br /> 为驱动程序管理器<br /><br /> ODBC 3。*x*驱动程序？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|否|没有 [1]|用户帐户控制|  
|**SQLAllocEnv**|否|没有 [1]|用户帐户控制|  
|**SQLAllocHandle**|用户帐户控制|是|否|  
|**SQLAllocStmt**|否|没有 [1]|用户帐户控制|  
|**SQLBindCol**|用户帐户控制|是|否|  
|**SQLBindParam**|否|是 [2]|用户帐户控制|  
|**SQLBindParameter**|用户帐户控制|是|否|  
|**SQLBrowseConnect**|用户帐户控制|是|否|  
|**SQLBulkOperations**|用户帐户控制|是|否|  
|**SQLCancel**|用户帐户控制|是|否|  
|**SQLCloseCursor**|用户帐户控制|是|否|  
|**SQLColAttribute**|用户帐户控制|是|否|  
|**SQLColAttributes**|没有 [3]|否|用户帐户控制|  
|**SQLColumnPrivileges**|用户帐户控制|是|否|  
|**SQLColumns**|用户帐户控制|是|否|  
|**SQLConnect**|用户帐户控制|是|否|  
|**SQLCopyDesc**|用户帐户控制|用户帐户控制|是 [4]|  
|**SQLDataSources**|否|是|用户帐户控制|  
|**SQLDescribeCol**|用户帐户控制|是|否|  
|**SQLDescribeParam**|用户帐户控制|是|否|  
|**SQLDisconnect**|用户帐户控制|是|否|  
|**SQLDriverConnect**|用户帐户控制|是|否|  
|**SQLDrivers**|否|是|用户帐户控制|  
|**SQLEndTran**|用户帐户控制|是|否|  
|**SQLError**|否|没有 [1]|用户帐户控制|  
|**SQLExecDirect**|用户帐户控制|是|否|  
|**SQLExecute**|用户帐户控制|是|否|  
|**SQLExtendedFetch**|用户帐户控制|否|否|  
|**SQLFetch**|用户帐户控制|是|否|  
|**SQLFetchScroll**|用户帐户控制|是|否|  
|**SQLForeignKeys**|用户帐户控制|是|否|  
|**SQLFreeConnect**|否|是 [1]|用户帐户控制|  
|**SQLFreeEnv**|否|是 [1]|用户帐户控制|  
|**SQLFreeHandle**|用户帐户控制|是|否|  
|**SQLFreeStmt**|用户帐户控制|是|否|  
|**SQLGetConnectAttr**|用户帐户控制|是|否|  
|**SQLGetConnectOption**|没有 [5]|没有 [1]|用户帐户控制|  
|**SQLGetCursorName**|用户帐户控制|是|否|  
|**SQLGetData**|用户帐户控制|是|否|  
|**SQLGetDescField**|用户帐户控制|是|否|  
|**SQLGetDescRec**|用户帐户控制|是|否|  
|**SQLGetDiagField**|用户帐户控制|是|否|  
|**SQLGetDiagRec**|用户帐户控制|是|否|  
|**SQLGetEnvAttr**|用户帐户控制|是|否|  
|**SQLGetFunctions**|没有 [6]|用户帐户控制|用户帐户控制|  
|**SQLGetInfo**|用户帐户控制|是|否|  
|**SQLGetStmtAttr**|用户帐户控制|是|否|  
|**SQLGetStmtOption**|没有 [5]|没有 [1]|用户帐户控制|  
|**SQLGetTypeInfo**|用户帐户控制|是|否|  
|**SQLMoreResults**|用户帐户控制|是|否|  
|**SQLNativeSql**|用户帐户控制|是|否|  
|**SQLNumParams**|用户帐户控制|是|否|  
|**SQLNumResultCols**|用户帐户控制|是|否|  
|**SQLParamData**|用户帐户控制|是|否|  
|**SQLParamOptions**|否|否|用户帐户控制|  
|**SQLPrepare**|用户帐户控制|是|否|  
|**SQLPrimaryKeys**|用户帐户控制|是|否|  
|**SQLProcedureColumns**|用户帐户控制|是|否|  
|**SQLProcedures**|用户帐户控制|是|否|  
|**SQLPutData**|用户帐户控制|是|否|  
|**SQLRowCount**|用户帐户控制|是|否|  
|**SQLSetConnectAttr**|用户帐户控制|是|否|  
|**SQLSetConnectOption**|没有 [5]|没有 [1]|用户帐户控制|  
|**SQLSetCursorName**|用户帐户控制|是|否|  
|**SQLSetDescField**|用户帐户控制|是|否|  
|**SQLSetDescRec**|用户帐户控制|是|否|  
|**SQLSetEnvAttr**|用户帐户控制|是|否|  
|**SQLSetPos**|用户帐户控制|是|否|  
|**SQLSetParam**|否|否|用户帐户控制|  
|**SQLSetScrollOption**|用户帐户控制|是|否|  
|**SQLSetStmtAttr**|用户帐户控制|是|否|  
|**SQLSetStmtOption**|没有 [5]|没有 [1]|用户帐户控制|  
|**SQLSpecialColumns**|用户帐户控制|是|否|  
|**SQLStatistics**|用户帐户控制|是|否|  
|**SQLTablePrivileges**|用户帐户控制|是|否|  
|**SQLTables**|用户帐户控制|是|否|  
|**SQLTransact**|否|没有 [1]|用户帐户控制|  
  
 [1] 此函数已弃用在 ODBC 3。*x*。 ODBC 3。*x*应用程序不应使用此函数。 但是，Open Group 或 ISO CLI 兼容的应用程序可以调用此函数。  
  
 [2] ODBC 3。*x*应用程序应使用**SQLBindParameter**而不是**SQLBindParam**。 但是，Open Group 或 ISO CLI 兼容的应用程序可以调用此函数。  
  
 [3] 驱动程序编写人员应该注意，ODBC 2。*x*列属性必须与支持 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH **SQLColAttribute**。  
  
 [4] **SQLCopyDesc**部分实现由驱动程序管理器复制描述符时跨属于不同的驱动程序的连接。 支持所需的驱动程序**SQLCopyDesc**跨两个其自己的连接。 之类的函数**SQLDrivers**，这实现仅由驱动程序管理器，不会显示在此列表上。  
  
 [5] 在某些情况下，驱动程序可能需要支持此函数。 有关详细信息，请参阅此函数的参考页。  
  
 [6]，驱动程序可以选择以支持**SQLGetFunctions**如果的驱动程序支持的函数集各不相同连接连接。
