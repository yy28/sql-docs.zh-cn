---
title: 过程调用 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926ee91fae207d50248df4c82d1b82bb6424e239
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023251"
---
# <a name="procedure-calls"></a>过程调用
一个*过程*是数据源上存储的可执行对象。 通常，它是一个或更多的已经预编译的 SQL 语句。 调用过程的转义序列是  
  
 **{** [ **？ =** ]**调用** *过程名称*[ **(** [*参数*] [ **，** [*参数*]]... **)** ] **}**  
  
 其中*过程名称*指定过程的名称和*参数*指定过程参数。  
  
 有关过程调用转义序列的详细信息，请参阅[过程调用转义序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)附录 c： 驱动器中SQL 语法。  
  
 一个过程可以有零个或多个参数。 它还可以返回一个值，可选参数标记所示 **？ =** 语法开头。 如果*参数*是输入 / 输出参数，它可以是文字或参数标记。 但是，可互操作应用程序应始终使用参数标记，因为某些数据源不接受文本的参数值。 如果*参数*是输出参数，它必须是参数标记。 必须通过绑定参数标记**SQLBindParameter**语句执行之前在过程调用。  
  
 过程调用的输入和输入/输出参数可以省略。 如果调用过程时使用括号但不带任何参数，如 {调用*过程名称*（)}，驱动程序将指示要使用的第一个参数的默认值的数据源。 如果该过程不具有任何参数，这可能会导致失败的过程。 如果调用过程时不带括号，如 {调用*过程名称*}，该驱动程序不会发送任何参数值。  
  
 可以为过程调用中的输入和输入/输出参数指定文字。 例如，假设过程**InsertOrder**具有五个输入参数。 以下调用到**InsertOrder**省略了第一个参数，提供的第二个参数的文本并使用参数标记为第三、 第四个和第五个参数：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 请注意，是否省略一个参数，则仍必须显示的逗号分隔该参数与其他参数。 如果省略输入参数或输入/输出参数，过程会使用该参数的默认值。 另一种方法来指定输入参数或输入/输出参数的默认值是设置的长度/指示器缓冲区的值绑定到为 SQL_DEFAULT_PARAM 参数。  
  
 如果省略输入/输出参数或参数提供文字，驱动程序将放弃输出值。 同样，如果省略过程返回值的参数标记，驱动程序将放弃返回值。 最后一点，如果应用程序为不返回值的过程指定返回值参数，驱动程序将绑定到该参数的长度/指示器缓冲区的值设置为 SQL_NULL_DATA。  
  
 假设过程 PARTS_IN_ORDERS 创建结果集，其中包含的包含的特定部件号的订单列表。 下面的代码将为部件号 544 调用此过程：  
  
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
