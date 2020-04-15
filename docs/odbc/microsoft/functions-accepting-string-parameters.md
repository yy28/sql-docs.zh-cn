---
title: 接受字符串参数的功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d0f143c72f57e946f7fe2bf52a50910d4e56aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286297"
---
# <a name="functions-accepting-string-parameters"></a>接受字符串参数的函数
所有采用字符串参数的函数都将转换为 Unicode。 （将导出函数的"W"形式。字节计数将转换为适用于 ODBC API 的字符计数。 这适用于以下功能：  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLColattributes**  
  
-   **SQLDescribeCol**  
  
-   **SQLError（** 替换为**SQLGetDiagField）**  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursor 名称**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** （成为**SQLGetStmtAttr**）  
  
-   **SQLSetStmtOption** （成为**SQLSetStmtAttr**）  
  
-   **SQLGetConnectOption**  
  
-   **SQLSet 连接选项**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQLNativeSQL**  
  
-   **SQLSpecialColumns**  
  
-   **配置DSNEx**  
  
-   **配置DSN**
