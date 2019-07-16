---
title: 映射已弃用的函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 307f0f54434fdcb4ebb19c38256a7a04f4a5c46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990708"
---
# <a name="mapping-deprecated-functions"></a>映射已弃用的函数
本部分介绍如何已弃用的函数映射由 ODBC *3.x*驱动程序管理器，以保证向后兼容性的 ODBC *3.x*用于 ODBC 的驱动程序*2.x*应用程序。 驱动程序管理器执行此映射不考虑应用程序的版本。 因为每个 ODBC *2.x*以下列表中的函数映射到相应 ODBC *3.x*函数在 ODBC 中调用时*3.x*驱动程序，ODBC *3.x*驱动程序不需要实现 ODBC *2.x*函数。  
  
 ODBC 驱动程序时，会触发在列表中的映射*3.x*驱动程序和驱动程序不支持要映射的函数。  
  
 下表列出了所有重复在 ODBC 中引入的功能*3.x*。  
  
|ODBC *2.x*函数|ODBC *3.x*函数|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt**与*选项*的 SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 即使在 ODBC 中不存在此函数*2.x*，它是 Open Group 和 ISO 标准中。  
  
 [2] 这是 ODBC 1.0 函数。  
  
 本部分包含以下主题。  
  
-   [SQLAllocConnect 映射](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv 映射](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [SQLAllocStmt 映射](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam 映射](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes 映射](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError 映射](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect 映射](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv 映射](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt 映射](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption 映射](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption 映射](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator 映射](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions 映射](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam 映射](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions 映射](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption 映射](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact 映射](../../../odbc/reference/appendixes/sqltransact-mapping.md)
