---
title: 已准备好的执行 ODBC |微软文档
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
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282307"
---
# <a name="prepared-execution-odbc"></a>已准备的执行 ODBC
准备执行是多次执行语句的有效方法。 该语句首先编译或*准备*到访问计划中。 然后，稍后将执行一次或多次访问计划。 有关访问计划的详细信息，请参阅处理[SQL 语句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 垂直和自定义应用程序通常使用准备执行来重复执行相同的参数化 SQL 语句。 例如，以下代码准备一个语句来更新不同部件的价格。 然后，它每次使用不同的参数值多次执行语句。  
  
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
  
 准备执行比多次执行语句的直接执行快，这主要是因为语句只编译一次;每次执行语句时，都会编译直接执行的语句。 准备好的执行还可以减少网络流量，因为如果数据源支持访问计划标识符，则驱动程序可以在每次执行语句时向数据源发送访问计划标识符，而不是整个 SQL 语句。  
  
 应用程序可以在准备语句后和执行语句之前检索结果集的元数据。 但是，返回已准备好的未执行语句的元数据对于某些驱动程序来说非常昂贵，如果可能，应避免互操作应用程序。 有关详细信息，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 不应对执行一次的语句使用准备好的执行。 对于此类语句，它比直接执行稍慢，因为它需要额外的 ODBC 函数调用。  
  
> [!IMPORTANT]  
>  通过显式调用**SQLEndTran**或以自动提交模式工作来提交或回滚事务，会导致某些数据源删除连接上所有语句的访问计划。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明中SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR选项。  
  
 要准备和执行语句，应用程序：  
  
1.  调用**SQLPrepare**并传递包含 SQL 语句的字符串。  
  
2.  设置任何参数的值。 参数实际上可以在准备语句之前或之后设置。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
3.  调用**SQLExecute**并执行任何必要的其他处理，例如提取数据。  
  
4.  根据需要重复步骤 2 和 3。  
  
5.  调用**SQLPrepare**时，驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法，而无需分析该语句。 这包括替换[ODBC 中的转义序列中](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)讨论的转义序列。 应用程序可以通过调用**SQLNativeSql**来检索 SQL 语句的修改形式。 如果设置了SQL_ATTR_NOSCAN语句属性，则不会替换转义序列。  
  
    -   将语句发送到数据源进行准备。  
  
    -   存储返回的访问计划标识符以备以后执行（如果准备成功）或返回任何错误（如果准备失败）。 错误包括语法错误，如 SQLSTATE 42000（语法错误或访问冲突）和语义错误，如 SQLSTATE 42S02（找不到基本表或视图）。  
  
        > [!NOTE]  
        >  某些驱动程序此时不返回错误，而是在执行语句或调用目录函数时返回错误。 因此 **，SQLPrepare**在实际上出现故障时可能似乎已经成功。  
  
6.  调用**SQLExecute**时，驱动程序：  
  
    -   检索当前参数值并根据需要转换它们。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   将访问计划标识符和转换的参数值发送到数据源。  
  
    -   返回任何错误。 这些通常是运行时错误，如 SQLSTATE 24000（无效游标状态）。 但是，此时某些驱动程序返回语法和语义错误。  
  
 如果数据源不支持语句准备，驱动程序必须尽可能模拟它。 例如，在调用**SQLPrepare**时，驱动程序可能不执行任何操作，然后在调用**SQLExecute**时直接执行语句。  
  
 如果数据源支持不执行的语法检查，驱动程序可能会提交语句以在调用**SQLPrepare**时进行检查，并在调用**SQLExecute**时提交语句以执行。  
  
 如果驱动程序无法模拟语句准备，它将在调用**SQLPrepare**时存储语句，并在调用**SQLExecute**时提交该语句以执行。  
  
 由于模拟语句准备不完美 **，SQLExecute**可以返回**SQLPrepare**通常返回的任何错误。
