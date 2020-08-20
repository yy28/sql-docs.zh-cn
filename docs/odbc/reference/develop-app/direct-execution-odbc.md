---
description: 直接执行 ODBC
title: 直接执行 ODBC |Microsoft Docs
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
ms.openlocfilehash: 9be03c4f20a82e134481f8fd9bb849ffd830567a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476699"
---
# <a name="direct-execution-odbc"></a>直接执行 ODBC
直接执行是执行语句的最简单方法。 提交语句执行时，数据源会将其编译为访问计划，然后执行该访问计划。  
  
 直接执行通常由在运行时生成和执行语句的泛型应用程序使用。 例如，下面的代码生成一个 SQL 语句，并一次执行它：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接执行最适用于将执行一次的语句。 它的主要缺点是每次执行 SQL 语句时都将对其进行分析。 此外，应用程序无法检索有关语句创建的结果集的信息， (如果任何) 到执行语句之后，如果语句以两个单独的步骤准备并执行，则可以执行此操作。  
  
 若要直接执行语句，应用程序需要执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  调用 **SQLExecDirect** 并向其传递包含 SQL 语句的字符串。  
  
3.  调用 **SQLExecDirect** 时，驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法而不分析语句;这包括替换 [ODBC 中转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中讨论的转义序列。 应用程序可以通过调用 **SQLNativeSql**来检索 SQL 语句的修改形式。 如果设置了 SQL_ATTR_NOSCAN 语句特性，则不会替换转义序列。  
  
    -   检索当前参数值，并根据需要对其进行转换。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   将语句和转换的参数值发送到数据源以便执行。  
  
    -   返回任何错误。 其中包括序列化或状态诊断，例如 SQLSTATE 24000 (无效的游标状态) 、语法错误（如 SQLSTATE 42000） (语法错误或访问冲突) ）以及语义错误，如 SQLSTATE 42S02 (基表或找不到视图) 。
