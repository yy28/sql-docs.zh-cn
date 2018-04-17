---
title: 指示执行 ODBC |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09ea0f6d6046a6deb24431dd29d0f91f78226120
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="direct-execution-odbc"></a>直接执行 ODBC
直接执行是执行语句的最简单方法。 当针对执行提交该语句时，数据源将它编译成一个访问计划，然后执行该访问计划。  
  
 常用的泛型应用程序生成并在运行时中执行语句中直接执行。 例如，下面的代码生成 SQL 语句，并执行它一次：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接执行适合于语句将执行一次。 其主要缺点是每次执行时解析的 SQL 语句。 此外，应用程序无法检索结果集的语句 （如果有） 之后创建语句将; 相关信息如果准备并在两个单独步骤中执行语句，这是可行的。  
  
 若要执行语句直接，应用程序执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
2.  调用**SQLExecDirect**并将其传递包含 SQL 语句的字符串。  
  
3.  当**SQLExecDirect**调用时，该驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法，而无需分析语句;这包括替换中所述的转义序列[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 应用程序可以通过调用中检索的 SQL 语句修改窗体**SQLNativeSql**。 如果 SQL_ATTR_NOSCAN 语句特性设置，不会替换转义序列。  
  
    -   检索当前参数值，并根据需要转换这些。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
    -   发送到数据源执行的语句和已转换的参数值。  
  
    -   返回任何错误。 其中包括序列化或状态的诊断，例如 SQLSTATE 24000 （无效的游标状态）、 SQLSTATE 42000 （语法错误或访问冲突），如语法错误和语义错误如 SQLSTATE 42S02 （基础表或视图未找到）。
