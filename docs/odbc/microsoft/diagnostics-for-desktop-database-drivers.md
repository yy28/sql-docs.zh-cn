---
title: 诊断对于桌面数据库驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031219"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面数据库驱动程序的诊断
由驱动程序处理所有错误和警告不检查或部分选中由驱动程序管理器。 该驱动程序还映射本机错误或错误返回给 SQLSTATEs 的数据源。 中列出的每个函数*ODBC 程序员参考*包含指定状态和消息的"诊断"部分。  
  
 应用程序调用**SQLGetDiagRec**检索 SQLSTATE、 本机错误代码和诊断消息。 调用**SQLGetDiagField**并指定字段中检索单个诊断字段。 下表中列出的诊断标识符的支持级别。  
  
|DiagIdentifiers|支持级别|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支持|  
|SQL_DIAG_CLASS_ORIGIN|支持。 始终"ODBC 3.0"此驱动程序版本 3.0 及更高版本。|  
|SQL_DIAG_COLUMN_NUMBER|支持|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支持|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支持|  
|SQL_DIAG_MESSAGE_TEXT|支持|  
|SQL_DIAG_NATIVE|支持|  
|SQL_DIAG_NUMBER|支持|  
|SQL_DIAG_RETURNCODE|支持，但实现由驱动程序管理器|  
|SQL_DIAG_ROW_COUNT|支持|  
|SQL_DIAG_ROW_NUMBER|支持|  
|SQL_DIAG_SERVER_NAME|不支持|  
|SQL_DIAG_SQLSTATE|支持|  
|SQL_DIAG_SUBCLASS_ORIGIN|支持|
