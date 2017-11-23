---
title: "标量函数调用 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e45b0f8bf4944b1f683245033123b15d76c1befa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="scalar-function-calls"></a>标量函数调用
标量函数返回每一行的值。 例如，该绝对值标量函数将作为自变量的数值列，并返回列中的每个值的绝对值的数值。 调用标量函数的转义序列是  
  
 **{fn***标量函数* **}**   
  
 其中*标量函数*是中列出的函数之一[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 有关标量函数转义序列的详细信息，请参阅[标量函数转义序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)附录 c: SQL 语法中。  
  
 例如，以下 SQL 语句创建相同的结果集中的大写客户名称。 第一个语句中使用转义序列语法。 第二个语句用于 OS/2 Ingres 本机语法，并不是可互操作。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 应用程序可以混合使用对使用本机语法的标量函数的调用和对使用 ODBC 语法的标量函数的调用。 例如，假定员工表中的名称，存储为姓氏、 逗号、 和第一个名称。 以下 SQL 语句创建员工表中的员工的姓氏结果集。 该语句使用 ODBC 标量函数**子字符串**和 SQL Server 标量函数**CHARINDEX**并且将仅在 SQL 服务器上正确执行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 应用程序应使用的最大互操作性，**转换**标量函数，以确保一个标量函数的输出所需的类型。 **转换**函数将数据从一种 SQL 数据类型转换为指定的 SQL 数据类型。 语法**转换**技术支持部门  
  
 **转换 (** *value_exp* **，** *data_type***)**  
  
 其中*value_exp*列名称，另一个标量函数，或文本值，而结果和*data_type*是匹配的关键字**#define**使用的名称SQL 数据类型标识符中定义[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。 例如，以下 SQL 语句使用**转换**若要确保的函数的输出**CURDATE**函数是一个日期，而不是时间戳或字符数据：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 若要确定数据源支持的标量函数，应用程序调用**SQLGetInfo**与 SQL_CONVERT_FUNCTIONS、 SQL_NUMERIC_FUNCTIONS、 SQL_STRING_FUNCTIONS、 SQL_SYSTEM_FUNCTIONS 和 SQL_TIMEDATE_函数选项。 若要确定支持的转换操作**转换**函数，应用程序调用**SQLGetInfo**与任意开头 SQL_CONVERT 的选项。
