---
title: 直接执行 ODBC |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305158"
---
# <a name="direct-execution-odbc"></a>直接执行 ODBC
直接执行是执行语句的最简单方法。 提交语句执行时，数据源将其编译为访问计划，然后执行该访问计划。  
  
 直接执行通常用于在运行时生成和执行语句的通用应用程序。 例如，以下代码生成 SQL 语句并执行一次：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接执行最适合将执行一次的语句。 它的主要缺点是每次执行 SQL 语句时都会对其进行分析。 此外，在执行语句之前，应用程序无法检索有关语句创建的结果集（如果有）的信息;如果语句以两个单独的步骤准备和执行，则这是可能的。  
  
 要直接执行语句，应用程序将执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  调用**SQLExecDirect**并传递包含 SQL 语句的字符串。  
  
3.  调用**SQLExecDirect**时，驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法，而不分析 语句;这包括替换[ODBC 中的转义序列中](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)讨论的转义序列。 应用程序可以通过调用**SQLNativeSql**来检索 SQL 语句的修改形式。 如果设置了SQL_ATTR_NOSCAN语句属性，则不会替换转义序列。  
  
    -   检索当前参数值并根据需要转换它们。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   将语句和转换后的参数值发送到数据源以执行。  
  
    -   返回任何错误。 这些包括排序或状态诊断，如 SQLSTATE 24000（无效游标状态）、语法错误（如 SQLSTATE 42000（语法错误或访问冲突）以及语义错误，如 SQLSTATE 42S02（找不到基表或视图）。
