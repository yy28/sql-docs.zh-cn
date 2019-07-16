---
title: 标量函数调用 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897750"
---
# <a name="scalar-function-calls"></a>标量函数调用
标量函数返回每一行的值。 例如，该绝对值标量函数将数值列作为参数并返回列中的每个值的绝对值。 用于调用标量函数转义序列  
  
 **{fn** _标量函数_ **}**  
  
 其中*标量函数*是中列出的函数之一[附录 e:标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 有关标量函数转义序列的详细信息，请参阅[标量函数转义序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)附录 c： 驱动器中SQL 语法。  
  
 例如，以下 SQL 语句创建大写客户相同的结果的集名称。 第一个语句使用转义序列语法。 第二个语句使用的 OS/2 Ingres 本机语法并不是可互操作。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 应用程序可以混合使用本机语法的标量函数的调用和对使用 ODBC 语法的标量函数的调用。 例如，假设 Employee 表中的名称存储为最后一个名称、 逗号和名字。 以下 SQL 语句在 Employee 表中创建结果集的最后一个雇员的姓名。 该语句使用 ODBC 标量函数**SUBSTRING**和 SQL Server 标量函数**CHARINDEX**并且将仅在 SQL 服务器上正确执行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 应用程序应使用的最大互操作性**转换**标量函数，以确保标量函数的输出所需的类型。 **转换**函数将数据从一个 SQL 数据类型转换为指定的 SQL 数据类型。 语法**转换**函数  
  
 **CONVERT(** _value_exp_ **,** _data_type_ **)**  
  
 其中*value_exp*是一个列名称，另一个标量函数或文本值的结果并*data_type*是匹配的关键字 **#define**用的名称SQL 数据类型标识符，如中所定义[附录 d:数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。 例如，使用以下 SQL 语句**转换**请确保函数的输出**CURDATE**函数是日期，而不是时间戳列或字符数据：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 若要确定数据源支持的标量函数，应用程序调用**SQLGetInfo**与 SQL_CONVERT_FUNCTIONS、 SQL_NUMERIC_FUNCTIONS、 SQL_STRING_FUNCTIONS、 SQL_SYSTEM_FUNCTIONS 和 SQL_TIMEDATE_函数选项。 若要确定支持的转换操作**转换**函数，应用程序调用**SQLGetInfo**与任何使用 SQL_CONVERT 启动的选项。
