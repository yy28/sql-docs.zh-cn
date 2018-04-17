---
title: 过程调用 |Microsoft 文档
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
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b12586b2da965ef159766e670ecc9456260c75d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="procedure-calls"></a>过程调用
A*过程*是数据源上存储的可执行对象。 通常，它是一个或更多的已经预编译的 SQL 语句。 调用过程的转义序列是  
  
 **{**[**？ =**]**调用***过程名称*[**(**[*参数*] [**，**[*参数*]]...**)**]**}**  
  
 其中*过程名称*指定过程的名称和*参数*指定过程参数。  
  
 有关过程调用转义序列的详细信息，请参阅[过程调用转义序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)附录 c: SQL 语法中。  
  
 一个过程可以有零个或多个参数。 它还可以返回一个值，由可选的参数标记**？ =**开头的语法。 如果*参数*是输入 / 输出参数，它可以是一个文本值或参数标记。 但是，可互操作的应用程序应始终使用参数标记，因为某些数据源不接受文本的参数值。 如果*参数*是一个输出参数，它必须是参数标记。 必须通过绑定参数标记**SQLBindParameter**之前过程调用执行语句。  
  
 过程调用的输入和输入/输出参数可以省略。 如果调用了过程用括号但不带任何参数，如 {调用*过程名称*（)}，驱动程序指示要使用的第一个参数的默认值的数据源。 如果该过程不具有任何参数，这可能会导致失败的过程。 如果调用过程时不带括号，如 {调用*过程名称*}，驱动程序不发送任何参数值。  
  
 可以为过程调用中的输入和输入/输出参数指定文字。 例如，假设过程**InsertOrder**有五个输入参数。 以下调用到**InsertOrder**省略第一个参数，第二个参数，提供文本，参数标记用于第三、 第四个和第五个参数：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 请注意，是否省略一个参数，仍必须显示的逗号分隔该参数与其他参数。 如果省略输入参数或输入/输出参数，过程会使用该参数的默认值。 另一种方法指定的输入或输入/输出参数的默认值是设置的长度/指示器缓冲区值绑定到 SQL_DEFAULT_PARAM 的参数。  
  
 如果省略一个输入/输出参数，或为参数提供文本，驱动程序将丢弃的输出值。 同样，如果省略过程返回值的参数标记，驱动程序将放弃返回值。 最后一点，如果应用程序为不返回值的过程指定返回值参数，驱动程序将绑定到该参数的长度/指示器缓冲区的值设置为 SQL_NULL_DATA。  
  
 假设过程 PARTS_IN_ORDERS 创建包含的包含的特定部件号的订单列表的结果集。 下面的代码为部件号 544 调用此过程：  
  
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
  
 若要确定数据源是否支持过程，应用程序调用**SQLGetInfo** SQL_PROCEDURES 选项。  
  
 有关过程的详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。
