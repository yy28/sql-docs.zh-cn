---
title: 诊断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0c7ddfeda7538027c56af17664e5962d09903b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686345"
---
# <a name="diagnostics"></a>诊断
在 ODBC 中的函数返回以下两种方式的诊断信息。 返回代码指示总体成功或失败的函数，而诊断记录提供有关该函数的详细的信息。 至少一个诊断记录，标头记录 — 即使如果函数成功，则返回。  
  
 在开发时使用的诊断信息来捕获中硬编码的 SQL 语句的编程错误，如无效句柄和语法错误。 它用于在运行时捕获用户输入的 SQL 语句中的运行时错误和警告，例如数据截断，访问冲突和语法错误。  
  
 本部分包含以下主题。  
  
-   [返回代码](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [诊断记录](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [诊断处理示例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
