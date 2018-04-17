---
title: 映射函数弃用 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfa4d8cd2a21363e1b3aa0588ae4def8ed011005
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mapping-deprecated-functions"></a>映射函数弃用
本部分介绍如何已弃用的函数映射由 ODBC 3*.x*驱动程序管理器，以保证向后兼容性的 ODBC 3*.x*与 ODBC 2 一起使用的驱动程序。*x*应用程序。 驱动程序管理器执行此映射而不考虑应用程序的版本。 因为每个 ODBC 2。*x*以下列表中的函数映射到相应的 ODBC 3*.x*函数 ODBC 3 中调用时*.x*驱动程序，ODBC 3*.x*驱动程序不需要实现 ODBC 2。*x*函数。  
  
 在列表中的映射触发该驱动程序时 ODBC 3*.x*驱动程序和驱动程序不支持正在映射的函数。  
  
 下表列出了所有重复的 ODBC 3 中引入的功能*.x*。  
  
|ODBC 2。*x*函数|ODBC 3*.x*函数|  
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
  
 [1] 即使此函数不存在于 ODBC 2*.x*，它是 Open Group 和 ISO 标准中。  
  
 [2] 这是一个 ODBC 1.0 函数。  
  
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
