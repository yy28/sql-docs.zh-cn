---
title: 编写 ODBC 3.x 驱动程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300357"
---
# <a name="writing-odbc-3x-drivers"></a>编写 ODBC 3.x 驱动程序
下表显示了 ODBC 3 中的功能支持。*x*驱动程序和 ODBC 应用程序，以及驱动程序管理器在针对 ODBC 3 调用函数时执行的映射。*x*驱动程序。  
  
|函数|支持<br /><br /> 由<br /><br /> ODBC 3.*x*<br /><br /> 司机？|支持<br /><br /> 由<br /><br /> ODBC 3.*x*<br /><br /> 应用？|映射/支持<br /><br /> 由 ODBC 3。*x*<br /><br /> 驱动程序管理器到<br /><br /> ODBC 3.*x*驱动程序？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAlloc连接**|否|否[1]|是|  
|**SQLAllocEnv**|否|否[1]|是|  
|**SQLAllocHandle**|是|是|否|  
|**SQLAllocStmt**|否|否[1]|是|  
|**SQLBindCol**|是|是|否|  
|**SQLBindParam**|否|是[2]|是|  
|**SQLBindParameter**|是|是|否|  
|**SQLBrowseConnect**|是|是|否|  
|**SQLBulk 操作**|是|是|否|  
|**SQLCancel**|是|是|否|  
|**SQLCloseCursor**|是|是|否|  
|**SQLColAttribute**|是|是|否|  
|**SQLColattributes**|否[3]|否|是|  
|**SQLColumnPrivileges**|是|是|否|  
|**SQLColumns**|是|是|否|  
|**SQLConnect**|是|是|否|  
|**SQLCopyDesc**|是|是|是[4]|  
|**SQLData源**|否|是|是|  
|**SQLDescribeCol**|是|是|否|  
|**SQLDescribeParam**|是|是|否|  
|**SQL 断开**|是|是|否|  
|**SQLDriverConnect**|是|是|否|  
|**SQLDrivers**|否|是|是|  
|**SQLEndTran**|是|是|否|  
|**SQLError**|否|否[1]|是|  
|**SQLExecDirect**|是|是|否|  
|**SQLExecute**|是|是|否|  
|**SQL 扩展获取**|是|否|否|  
|**SQLFetch**|是|是|否|  
|**SQLFetchScroll**|是|是|否|  
|**SQLForeignKeys**|是|是|否|  
|**SQLFreeConnect**|否|是[1]|是|  
|**SQLFreeEnv**|否|是[1]|是|  
|**SQLFreeHandle**|是|是|否|  
|**SQLFreeStmt**|是|是|否|  
|**SQLGetConnectAttr**|是|是|否|  
|**SQLGetConnectOption**|否[5]|否[1]|是|  
|**SQLGetCursorName**|是|是|否|  
|**SQLGetData**|是|是|否|  
|**SQLGetDescField**|是|是|否|  
|**SQLGetDescRec**|是|是|否|  
|**SQLGetDiagField**|是|是|否|  
|**SQLGetDiagRec**|是|是|否|  
|**SQLGetEnvAttr**|是|是|否|  
|**SQLGetFunctions**|否[6]|是|是|  
|**SQLGetInfo**|是|是|否|  
|**SQLGetStmtAttr**|是|是|否|  
|**SQLGetStmtOption**|否[5]|否[1]|是|  
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
|**SQLSet 连接选项**|否[5]|否[1]|是|  
|**SQLSetCursor 名称**|是|是|否|  
|**SQLSetDescField**|是|是|否|  
|**SQLSetDescRec**|是|是|否|  
|**SQLSetEnvAttr**|是|是|否|  
|**SQLSetPos**|是|是|否|  
|**SQLSetParam**|否|否|是|  
|**SQLSetScrollOption**|是|是|否|  
|**SQLSetStmtAttr**|是|是|否|  
|**SQLSetStmtOption**|否[5]|否[1]|是|  
|**SQLSpecialColumns**|是|是|否|  
|**SQLStatistics**|是|是|否|  
|**SQLTablePrivileges**|是|是|否|  
|**SQLTables**|是|是|否|  
|**SQLTransact**|否|否[1]|是|  
  
 [1] 此函数在 ODBC 3 中被弃用。*x*. . ODBC 3.*x*应用程序不应使用此函数。 但是，开放组或符合 ISO CLI 的应用程序可以调用此功能。  
  
 [2] ODBC 3。*x*应用程序应使用**SQLBind 参数**而不是**SQLBindParam**。 但是，开放组或符合 ISO CLI 的应用程序可以调用此功能。  
  
 [3] 驱动程序编写器应注意 ODBC 2。*x* **sqlColattribute**必须支持 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 和SQL_COLUMN_LENGTH的 x 列属性。  
  
 [4] **SQLCopyDesc**部分由驱动程序管理器实现，当跨属于不同驱动程序的连接复制描述符时。 驱动程序需要跨两个连接支持**SQLCopyDesc。** 仅由驱动程序管理器实现的**SQLDriver**等函数不会显示在此列表中。  
  
 [5] 在某些情况下，驱动程序可能需要支持此功能。 有关详细信息，请参阅此函数的参考页。  
  
 [6] 如果驱动程序支持的函数集因连接而异，驱动程序可以选择支持**SQLGet 功能**。
