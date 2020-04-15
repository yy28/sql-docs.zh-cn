---
title: 程序调用 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282227"
---
# <a name="procedure-calls"></a>过程调用
*过程*是存储在数据源上的可执行对象。 通常，它是一个或更多的已经预编译的 SQL 语句。 调用过程的转义序列是  
  
 **[****]** 调用**call***过程名称*[**[***参数*]**,**，*[* 参数 ] ， 参数 * ...**)**]**}**  
  
 其中*过程名称*指定过程的名称，*参数*指定过程参数。  
  
 有关过程调用转义序列的详细信息，请参阅附录 C 中[的过程呼叫转义序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)：SQL 语法。  
  
 一个过程可以有零个或多个参数。 它还可以返回一个值，如语法开头的可选参数标记 **？*** 所示。 如果*参数*是输入参数或输入/输出参数，则可以是文本或参数标记。 但是，可互操作的应用程序应始终使用参数标记，因为某些数据源不接受文本参数值。 如果*参数*是输出参数，则它必须是参数标记。 在执行过程调用语句之前，必须使用**SQLBind 参数**绑定参数标记。  
  
 过程调用的输入和输入/输出参数可以省略。 如果使用括号调用过程，但没有任何参数（如 [调用*过程名称*（）]），则驱动程序指示数据源对第一个参数使用默认值。 如果过程没有任何参数，则可能导致该过程失败。 如果调用过程时没有括号（如 [调用*过程名称*]），则驱动程序不会发送任何参数值。  
  
 可以为过程调用中的输入和输入/输出参数指定文字。 例如，假设过程**InsertOrder**有五个输入参数。 以下对**InsertOrder**的调用省略了第一个参数，为第二个参数提供了文本，并使用参数标记进行第三个、第四个和第五个参数：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 请注意，如果省略了参数，则仍必须显示从其他参数分隔它的逗号。 如果省略输入参数或输入/输出参数，过程会使用该参数的默认值。 指定输入或输入/输出参数的默认值的另一种方法是将绑定到参数的长度/指示器缓冲区的值设置为SQL_DEFAULT_PARAM。  
  
 如果省略输入/输出参数，或者为该参数提供了文本，则驱动程序将丢弃输出值。 同样，如果省略过程返回值的参数标记，驱动程序将放弃返回值。 最后一点，如果应用程序为不返回值的过程指定返回值参数，驱动程序将绑定到该参数的长度/指示器缓冲区的值设置为 SQL_NULL_DATA。  
  
 假设过程PARTS_IN_ORDERS创建一个包含特定零件号的订单列表的结果集。 以下代码调用零件号 544 的过程：  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 要确定数据源是否支持过程，应用程序使用SQL_PROCEDURES选项调用**SQLGetInfo。**  
  
 有关过程的详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。
