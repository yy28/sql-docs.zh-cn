---
title: "SQL 92 CAST 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8389ff0812c91ca5a35007a21d70a2a1ca0baee8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-92-cast-function"></a>SQL 92 CAST 函数
**强制转换**SQL 92 中定义的函数等效于**转换**ODBC 中定义的函数。 等效的函数的语法如下所示：  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL 92**强制转换**函数规定哪些数据类型可以转换为的其他数据类型。 （有关详细信息，请参阅 sql-92 规范）。**强制转换**函数支持在 FIPS 过渡的级别。  
  
 应用程序可以确定对支持**强制转换**函数，如下所示：  
  
1.  调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 如果信息类型的返回值是 SQL_SC_FIPS127_2_TRANSITIONAL、 SQL_SC_SQL92_INTERMEDIATE 或 SQL_SC_SQL92_FULL，**强制转换**支持函数。  
  
2.  如果 SQL_SQL_CONFORMANCE 信息类型的返回值是 SQL_SC_ENTRY_LEVEL 或 0，调用**SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 信息类型。 如果设置 SQL_SVE_CAST 位，**强制转换**支持函数。

