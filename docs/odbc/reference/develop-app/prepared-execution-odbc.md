---
description: 已准备的执行 ODBC
title: 已准备好执行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6141af2cde7106419ab1eb68f86d5817f055aab2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465739"
---
# <a name="prepared-execution-odbc"></a>已准备的执行 ODBC
准备好的执行是多次执行语句的有效方法。 首先将语句编译或 *准备好* 到访问计划。 然后，访问计划稍后会执行一次或多次。 有关访问计划的详细信息，请参阅 [处理 SQL 语句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 已准备好的执行通常由垂直和自定义应用程序用于重复执行相同的参数化 SQL 语句。 例如，下面的代码准备一个语句来更新不同部件的价格。 然后，它每次用不同的参数值多次执行语句。  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 由于语句仅编译一次，因此已准备好的执行速度比直接执行语句多：直接执行的语句将在每次执行时进行编译。 准备好的执行还可以减少网络流量，因为如果数据源支持访问计划标识符，则每次执行语句时，驱动程序都可以将访问计划标识符发送到数据源，而不是整个 SQL 语句。  
  
 应用程序可以在准备好语句之后、执行语句之前检索结果集的元数据。 但是，对于某些驱动程序，为已准备好的未执行语句返回元数据非常昂贵，并且如果可能，应尽量避免使用可互操作的应用程序。 有关详细信息，请参阅 [结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 不应对执行一次的语句使用准备好的执行。 对于此类语句，它比直接执行略慢，因为它需要额外的 ODBC 函数调用。  
  
> [!IMPORTANT]  
>  通过显式调用 **SQLEndTran** 或在自动提交模式下工作，提交或回滚事务会导致某些数据源删除连接上所有语句的访问计划。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项。  
  
 若要准备和执行语句，应用程序需要：  
  
1.  调用 **SQLPrepare** 并向其传递包含 SQL 语句的字符串。  
  
2.  设置任何参数的值。 参数实际上可以在准备语句之前或之后设置。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
3.  调用 **SQLExecute** ，并执行所需的任何其他处理，如提取数据。  
  
4.  根据需要重复步骤2和3。  
  
5.  调用 **SQLPrepare** 时，驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法，而不分析语句。 这包括替换 [ODBC 中转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中讨论的转义序列。 应用程序可以通过调用 **SQLNativeSql**来检索 SQL 语句的修改形式。 如果设置了 SQL_ATTR_NOSCAN 语句特性，则不会替换转义序列。  
  
    -   将语句发送到数据源以准备。  
  
    -   存储返回的访问计划标识符以供以后执行 (如果准备) 成功，则为; 如果准备失败) ，则返回 (错误。 错误包括语法错误，如 SQLSTATE 42000 (语法错误或访问冲突) 和语义错误，如 SQLSTATE 42S02 (基表或找不到) 。  
  
        > [!NOTE]  
        >  某些驱动程序在此时不会返回错误，而是在执行语句或调用目录函数时返回错误。 因此， **SQLPrepare** 可能看起来是成功的，但实际上它已失败。  
  
6.  调用 **SQLExecute** 时，驱动程序：  
  
    -   检索当前参数值，并根据需要对其进行转换。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   向数据源发送访问计划标识符和已转换的参数值。  
  
    -   返回任何错误。 这些错误通常是运行时错误，例如 SQLSTATE 24000 (无效的游标状态) 。 但是，某些驱动程序此时返回语法和语义错误。  
  
 如果数据源不支持语句准备，驱动程序必须将其模拟到可能的范围。 例如，在调用 **SQLPrepare** 时，驱动程序可能不执行任何操作，然后在调用 **SQLExecute** 时直接执行语句。  
  
 如果数据源不执行语法检查，则在调用 **SQLPrepare** 时，驱动程序可能会提交用于检查的语句，并在调用 **SQLExecute** 时提交要执行的语句。  
  
 如果驱动程序无法模拟语句准备，则在调用 **SQLPrepare** 时将存储该语句，并在调用 **SQLExecute** 时提交该语句以执行。  
  
 由于模拟语句准备并不完美， **SQLExecute** 可能会返回 **SQLPrepare**正常返回的任何错误。
