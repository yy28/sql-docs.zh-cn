---
title: Scalar 函数调用 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304258"
---
# <a name="scalar-function-calls"></a>标量函数调用
Scalar 函数返回每行的值。 例如，绝对值标量函数将数字列作为参数，并返回列中每个值的绝对值。 调用标量函数的转义序列是  
  
 **[fn**_标量函数_**]**    
  
 *其中标量函数*是附录 E 中列出的函数之一[：Scalar 函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 有关标量函数转义序列的详细信息，请参阅附录 C 中的[Scalar 函数转义序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)：SQL 语法。  
  
 例如，以下 SQL 语句创建大写客户名称的相同结果集。 第一个语句使用转义序列语法。 第二个语句使用 OS/2 的 Ingres 的本机语法，并且不可互操作。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 应用程序可以混合对使用本机语法的标量函数的调用，以及对使用 ODBC 语法的标量函数的调用。 例如，假设"员工"表中的名称存储为姓氏、逗号和名字。 以下 SQL 语句在"员工"表中创建一组员工姓氏的结果。 该语句使用 ODBC 标量函数**SUBSTRING**和 SQL Server 标量函数**CHARINDEX，** 并且仅在 SQL Server 上正确执行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 为了达到最大的互操作性，应用程序应使用**CONVERT**标量函数来确保标量函数的输出是所需的类型。 **CONVERT**函数将数据从一种 SQL 数据类型转换为指定的 SQL 数据类型。 **CONVERT**函数的语法是  
  
 **转换（value_exp** _value_exp_ **，** _data_type_**）**  
  
 其中*value_exp*是列名、另一个标量函数的结果或文本值，并且*data_type*是一个关键字，与[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)定义中的 SQL 数据类型标识符使用的 **#define**名称匹配。 例如，以下 SQL 语句使用**CONVERT**函数来确保**CURDATE**函数的输出是日期，而不是时间戳或字符数据：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 要确定数据源支持哪些标量函数，应用程序使用SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS和SQL_TIMEDATE_FUNCTIONS选项调用**SQLGetInfo。** 要确定哪些转换操作受**CONVERT**函数支持，应用程序将**SQLGetInfo**调用，并带有以SQL_CONVERT开头的任何选项。
