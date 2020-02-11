---
title: 桌面数据库驱动程序的诊断 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031219"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>桌面数据库驱动程序的诊断
驱动程序管理器未检查或部分检查的所有错误和警告都由驱动程序处理。 驱动程序还将本机错误或数据源返回的错误映射到 SQLSTATEs。 *ODBC 程序员参考*中列出的每个函数都包含一个用于指定条件和消息的 "诊断" 部分。  
  
 应用程序调用**SQLGetDiagRec**来检索 SQLSTATE、本机错误代码和诊断消息。 调用**SQLGetDiagField**并指定字段将检索各个诊断字段。 下表列出了诊断标识符的支持级别。  
  
|DiagIdentifiers|支持级别|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|不支持|  
|SQL_DIAG_CLASS_ORIGIN|。 对于此驱动程序的版本3.0 和更高版本，始终为 "ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|支持|  
|SQL_DIAG_CURSOR_ROW_COUNT|不支持|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|不支持|  
|SQL_DIAG_MESSAGE_TEXT|支持|  
|SQL_DIAG_NATIVE|支持|  
|SQL_DIAG_NUMBER|支持|  
|SQL_DIAG_RETURNCODE|支持，但由驱动程序管理器实现|  
|SQL_DIAG_ROW_COUNT|支持|  
|SQL_DIAG_ROW_NUMBER|支持|  
|SQL_DIAG_SERVER_NAME|不支持|  
|SQL_DIAG_SQLSTATE|支持|  
|SQL_DIAG_SUBCLASS_ORIGIN|支持|
