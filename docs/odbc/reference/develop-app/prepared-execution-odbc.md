---
title: "准备好执行 ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6b2437d1958e2583dabb75c0a4c26a2ed472975
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="prepared-execution-odbc"></a>准备好的执行 ODBC
准备好的执行是一种高效的方式来多次执行语句。 首次编译该语句，或*已准备好，*到访问计划。 然后执行一个或更多次在更高版本时，访问计划。 有关访问计划的详细信息，请参阅[处理 SQL 语句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 准备好的执行通常由垂直和自定义应用程序用于重复执行同一、 参数化 SQL 语句。 例如，下面的代码准备的语句，若要更新的不同部分的价格。 然后，它将执行每次对不同的参数值多次的语句。  
  
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
  
 准备好的执行速度快于直接执行一次执行的语句，主要是因为该语句编译一次;直接执行语句进行编译，它们将执行每个时间。 准备好的执行也可以提供网络流量减少由于驱动程序可以访问计划标识符到数据源每次发送该语句执行，而不是整个 SQL 语句，如果数据源支持访问计划标识符。  
  
 应用程序可以检索的结果集准备该语句后，在执行之前的元数据。 但是，返回的元数据已准备好，快进的语句很高的某些驱动程序，应尽可能避免由可互操作的应用程序。 有关详细信息，请参阅[结果设置元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 不应对执行一次的语句使用准备好的执行。 对于此类语句中，这是比直接执行稍慢，因为它需要额外 ODBC 函数调用。  
  
> [!IMPORTANT]  
>  提交或回滚事务，通过显式调用**SQLEndTran**或通过在自动提交模式下工作，会导致某些数据源，若要删除的所有语句，在连接上的访问计划。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。  
  
 若要准备数据库并执行语句，应用程序：  
  
1.  调用**SQLPrepare**并将其传递包含 SQL 语句的字符串。  
  
2.  设置任何参数的值。 之前或之后准备语句，则实际上可以设置参数。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
3.  调用**SQLExecute** ，并执行任何额外的处理所必需的如提取数据。  
  
4.  根据需要重复步骤 2 和 3。  
  
5.  当**SQLPrepare**调用时，该驱动程序：  
  
    -   修改 SQL 语句以使用数据源的 SQL 语法，而无需分析该语句。 这包括替换中所述的转义序列[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 应用程序可以通过调用中检索的 SQL 语句修改窗体**SQLNativeSql**。 如果 SQL_ATTR_NOSCAN 语句特性设置，不会替换转义序列。  
  
    -   将该语句发送到准备的数据源。  
  
    -   将返回的访问计划标识符供以后执行存储 （如果所做的准备成功） 或 （如果所做的准备失败），则返回任何错误。 错误包括语法错误如 SQLSTATE 42000 （语法错误或访问冲突） 和语义错误如 SQLSTATE 42S02 （基础表或视图未找到）。  
  
        > [!NOTE]  
        >  某些驱动程序执行不返回错误，此时，但改为执行语句时或当调用目录函数时返回它们。 因此， **SQLPrepare**可能看起来已成功时实际上它已失败。  
  
6.  当**SQLExecute**调用时，该驱动程序：  
  
    -   检索当前参数值，并根据需要转换这些。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
    -   将访问计划标识符和已转换的参数值发送到数据源。  
  
    -   返回任何错误。 这些是通常的运行时错误如 SQLSTATE 24000 （无效的游标状态）。 但是，某些驱动程序将在此时返回语法和语义错误。  
  
 如果数据源不支持语句准备，该驱动程序必须模拟它的限度内。 例如，该驱动程序可能不执行任何操作时**SQLPrepare**调用，然后执行直接执行语句时**SQLExecute**调用。  
  
 如果数据源支持语法检查且没有执行，该驱动程序可能会提交检查时的语句**SQLPrepare**调用并将其提交执行的语句时**SQLExecute**是调用。  
  
 如果该驱动程序不能模拟语句准备，它会将存储该语句时**SQLPrepare**称为并提交以供执行时**SQLExecute**调用。  
  
 模拟的语句准备不是理想选择，因为**SQLExecute**可以返回通常返回的任何错误**SQLPrepare**。
