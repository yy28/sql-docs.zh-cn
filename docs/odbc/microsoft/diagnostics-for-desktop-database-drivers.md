---
title: "桌面的诊断数据库驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5440d7cb38dfeef678a9b665397b789bf506be72
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostics-for-desktop-database-drivers"></a>对于桌面数据库驱动程序的诊断
由驱动程序处理所有错误和警告不检查或部分选中的驱动程序管理器。 该驱动程序还会将映射本机错误或由数据源中，向 SQLSTATEs 返回的错误。 中列出每个函数*ODBC 程序员参考*包含指定条件和消息的"诊断"部分。  
  
 应用程序调用**SQLGetDiagRec**来检索 SQLSTATE、 本机错误代码和诊断消息。 调用**SQLGetDiagField**并指定该字段中检索各个诊断字段。 下表中列出的诊断标识符将支持级别。  
  
|DiagIdentifiers|支持级别|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支持|  
|SQL_DIAG_CLASS_ORIGIN|支持。 始终"ODBC 3.0"此驱动程序版本 3.0 及更高版本。|  
|SQL_DIAG_COLUMN_NUMBER|是否支持|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支持|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支持|  
|SQL_DIAG_MESSAGE_TEXT|是否支持|  
|SQL_DIAG_NATIVE|是否支持|  
|SQL_DIAG_NUMBER|是否支持|  
|SQL_DIAG_RETURNCODE|支持，但实现由驱动程序管理器|  
|SQL_DIAG_ROW_COUNT|是否支持|  
|SQL_DIAG_ROW_NUMBER|是否支持|  
|SQL_DIAG_SERVER_NAME|不支持|  
|SQL_DIAG_SQLSTATE|是否支持|  
|SQL_DIAG_SUBCLASS_ORIGIN|是否支持|
