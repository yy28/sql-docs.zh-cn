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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282227"
---
# <a name="procedure-calls"></a>过程调用
*过程*是存储在数据源中的可执行对象。 通常，它是一个或更多的已经预编译的 SQL 语句。 用于调用过程的转义序列是  
  
 **{**[**？ =**]**调用***过程-name*[**（**[*parameter*] [**，**[*parameter*]] .。。**)**]**}**  
  
 其中，*过程名称*指定过程的名称，*参数*指定过程参数。  
  
 有关过程调用转义序列的详细信息，请参阅附录 C： SQL 语法中的[过程调用转义序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)。  
  
 一个过程可以有零个或多个参数。 它还可以返回值，如语法开头的可选参数标记 **？ =** 所示。 如果*参数*是一个输入参数或输入/输出参数，则它可以是文字或参数标记。 但是，可交互应用程序应始终使用参数标记，因为某些数据源不接受文本参数值。 如果*参数*是输出参数，则它必须是参数标记。 执行过程调用语句之前，必须与**SQLBindParameter**绑定参数标记。  
  
 过程调用的输入和输入/输出参数可以省略。 如果使用括号（如 {call *procedure-name*（）}）调用过程，则驱动程序会指示数据源使用第一个参数的默认值。 如果该过程不具有任何参数，则这可能会导致过程失败。 如果在不使用括号的情况下调用过程（如 {call *procedure-name*}），驱动程序不会发送任何参数值。  
  
 可以为过程调用中的输入和输入/输出参数指定文字。 例如，假设过程**InsertOrder**有五个输入参数。 以下对**InsertOrder**的调用省略第一个参数，为第二个参数提供文本，并为第三个、第四个和第五个参数使用参数标记：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 请注意，如果省略了某个参数，则该参数必须与其他参数分隔开。 如果省略输入参数或输入/输出参数，过程会使用该参数的默认值。 指定输入参数或输入/输出参数的默认值的另一种方法是将绑定到参数的长度/指示器缓冲区的值设置为 SQL_DEFAULT_PARAM。  
  
 如果省略了输入/输出参数或为参数提供了文字，驱动程序将丢弃输出值。 同样，如果省略过程返回值的参数标记，驱动程序将放弃返回值。 最后一点，如果应用程序为不返回值的过程指定返回值参数，驱动程序将绑定到该参数的长度/指示器缓冲区的值设置为 SQL_NULL_DATA。  
  
 假设此过程 PARTS_IN_ORDERS 创建一个结果集，该结果集包含包含特定部件号的订单列表。 以下代码对第544部分调用此过程：  
  
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
  
 若要确定数据源是否支持过程，应用程序需要使用 SQL_PROCEDURES 选项调用**SQLGetInfo** 。  
  
 有关过程的详细信息，请参阅[过程](../../../odbc/reference/develop-app/procedures-odbc.md)。
