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
ms.openlocfilehash: bd6640c0dc06d9e957176717ef26aa3e444ffa9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022517"
---
# <a name="diagnostics"></a>诊断
ODBC 中的函数以两种方式返回诊断信息。 返回代码指示函数的总体成功或失败，而诊断记录则提供有关函数的详细信息。 至少要返回一条诊断记录-标头记录-即使函数成功也是如此。  
  
 在开发时使用诊断信息来捕获编程错误，如硬编码的 SQL 语句中的无效句柄和语法错误。 它用于在运行时捕获用户输入的 SQL 语句中的运行时错误和警告，如数据截断、访问冲突和语法错误。  
  
 本部分包含下列主题。  
  
-   [返回代码](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [诊断记录](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [诊断处理示例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
