---
title: 准备好执行 ODBC |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7bd6bc8281dd6bdc3bcfbd437380b2d5269ee43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199100"
---
# <a name="prepared-execution-odbc"></a>已准备的执行 ODBC
准备好的执行是多次执行语句的有效方法。 首次编译该语句，或*准备好，* 到访问计划。 然后执行一个或更多时间在更高版本时，访问计划。 有关访问计划的详细信息，请参阅[处理 SQL 语句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 垂直和自定义应用程序通常使用准备好的执行来重复执行相同的参数化 SQL 语句。 例如，下面的代码准备某个语句，若要更新的不同部分的价格。 然后执行每次使用不同的参数值多次的语句。  
  
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
  
 主要是因为一次; 编译语句的准备好的执行速度快于直接执行的语句执行一次以上，直接执行的语句是在执行每次编译。 准备好的执行还可以提供网络流量减少由于驱动程序可以访问计划标识符到数据源，每次发送该语句执行，而不是整个 SQL 语句，如果数据源支持访问计划的标识符。  
  
 应用程序中检索结果集准备的语句之后之前执行它, 的元数据。 但是，返回的元数据准备，未执行的语句很高的某些驱动程序，应尽可能避免通过可互操作应用程序。 有关详细信息，请参阅[结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 不应对执行一次的语句使用准备好的执行。 对于此类语句，它是比直接执行稍慢，因为它需要的其他 ODBC 函数调用。  
  
> [!IMPORTANT]  
>  提交或回滚事务，通过显式调用**SQLEndTran**或通过在自动提交模式下工作，导致某些数据源，以删除在连接上的所有语句访问计划。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。  
  
 若要准备和执行语句，该应用程序：  
  
1.  调用**SQLPrepare**并将其传递包含 SQL 语句的字符串。  
  
2.  设置任何参数的值。 之前或之后准备语句，则实际上可以设置参数。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
3.  调用**SQLExecute**并执行所必需的例如提取数据的任何其他处理。  
  
4.  根据需要重复步骤 2 和 3。  
  
5.  当**SQLPrepare**调用时，该驱动程序：  
  
    -   修改 SQL 语句，以使用数据源的 SQL 语法，而不分析该语句。 这包括替换中所述的转义序列[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 应用程序可以通过调用检索 SQL 语句的已修改的窗体**SQLNativeSql**。 如果设置 SQL_ATTR_NOSCAN 语句属性不替换转义序列。  
  
    -   将语句发送到准备的数据源。  
  
    -   返回的访问计划将标识符存储于更高版本执行 （如果准备成功） 或返回任何错误 （如果所做的准备失败）。 错误包括语法错误，如 SQLSTATE 42000 （语法错误或访问冲突） 和语义错误，如 SQLSTATE 42S02 （基数为表或视图找不到）。  
  
        > [!NOTE]  
        >  某些驱动程序执行操作现在返回错误，但改为执行该语句时或调用目录函数时返回它们。 因此， **SQLPrepare**可能看起来已成功时实际上它已失败。  
  
6.  当**SQLExecute**调用时，该驱动程序：  
  
    -   检索当前的参数值，并根据需要将其转换。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
    -   将访问计划标识符和已转换的参数值发送到数据源。  
  
    -   返回的任何错误。 这些是如 SQLSTATE 24000 通常运行时错误 （无效的游标状态）。 但是，某些驱动程序将在这里返回语法和语义错误。  
  
 如果数据源不支持语句准备，该驱动程序必须模拟它的范围内。 例如，驱动程序可能不执行任何操作时**SQLPrepare**调用，然后执行直接执行语句时**SQLExecute**调用。  
  
 如果数据源支持语法而无需执行检查，该驱动程序可能会提交的语句的检查时**SQLPrepare**调用并将其提交有关执行语句时**SQLExecute**是调用。  
  
 如果该驱动程序不能模拟语句准备，它会将存储该语句时**SQLPrepare**调用，并将其提交执行时**SQLExecute**调用。  
  
 模拟的语句准备并不完美，因为**SQLExecute**可以返回正常返回的任何错误**SQLPrepare**。
