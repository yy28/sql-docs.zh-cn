---
title: SQL-92 CAST 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6682ae98f2da64f6936049bee96fe2fff2a84db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057066"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 函数
**CAST** SQL-92 中定义的函数等效于**转换**在 ODBC 中定义的函数。 等效的函数的语法如下所示：  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92**强制转换**函数要求的数据类型可以转换为哪些其他数据类型。 （有关详细信息，请参阅 SQL-92 规范）。**强制转换**FIPS 过渡级别支持函数。  
  
 应用程序可以确定对支持**强制转换**函数，如下所示：  
  
1.  调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 信息类型的返回值是 SQL_SC_FIPS127_2_TRANSITIONAL、 SQL_SC_SQL92_INTERMEDIATE，还是 SQL_SC_SQL92_FULL，如果**强制转换**支持函数。  
  
2.  如果 SQL_SQL_CONFORMANCE 信息类型的返回值为 SQL_SC_ENTRY_LEVEL 或 0，则调用**SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 信息类型。 如果设置 SQL_SVE_CAST 位，则**强制转换**支持函数。
