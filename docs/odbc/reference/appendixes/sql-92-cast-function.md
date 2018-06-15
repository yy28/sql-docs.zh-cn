---
title: SQL 92 CAST 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d7d3d00128d4ddbb79c43f53c0d439e6974ddb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910932"
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
