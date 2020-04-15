---
title: 桌面数据库驱动程序的诊断 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303478"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面数据库驱动程序的诊断
驱动程序管理器未检查或部分检查的所有错误和警告都由驱动程序处理。 该驱动程序还将本机错误或数据源返回的错误映射到 SQLSTAT。 *ODBC 程序员参考*中列出的每个函数都包含一个"诊断"部分，用于指定条件和消息。  
  
 应用程序调用**SQLGetDiagRec**来检索 SQLSTATE、本机错误代码和诊断消息。 调用**SQLGetDiagField**并指定该字段将检索各个诊断字段。 下表列出了诊断标识符的支持级别。  
  
|诊断标识符|支持级别|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支持|  
|SQL_DIAG_CLASS_ORIGIN|支持。 对于此驱动程序的版本 3.0 和更高版本，始终为"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|支持|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支持|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支持|  
|SQL_DIAG_MESSAGE_TEXT|支持|  
|SQL_DIAG_NATIVE|支持|  
|SQL_DIAG_NUMBER|支持|  
|SQL_DIAG_RETURNCODE|驱动程序管理器支持但实施|  
|SQL_DIAG_ROW_COUNT|支持|  
|SQL_DIAG_ROW_NUMBER|支持|  
|SQL_DIAG_SERVER_NAME|不支持|  
|SQL_DIAG_SQLSTATE|支持|  
|SQL_DIAG_SUBCLASS_ORIGIN|支持|
