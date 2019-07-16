---
title: 动态 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 131abdd4a401e336ccd78ca79fdf6666b1911fee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915448"
---
# <a name="dynamic-sql"></a>动态 SQL
尽管静态 SQL 适用于很多情况下，没有应用程序的数据访问无法预先确定的类。 例如，假设一个电子表格，用户可以输入查询，该电子表格然后将发送到 DBMS 中检索数据。 此查询的内容很明显不能是已知的程序员写入电子表格程序时。  
  
 若要解决此问题，电子表格，请使用名为动态 SQL 的嵌入式 SQL 的一种形式。 与不同的静态 SQL 语句，这是硬编码在程序中，可以在运行时生成动态 SQL 语句，并放入字符串主机变量中。 它们随后会发送到 DBMS 进行处理。 DBMS 必须生成为动态 SQL 语句的运行时访问计划，因为动态 SQL 时静态 SQL 比通常慢。 编译包含动态 SQL 语句的程序时，动态 SQL 语句都不会去除从该程序，如静态 SQL 中所示。 相反，它们替换为将该语句传递给 DBMS; 一个函数调用通常情况下将被视为同一程序中的静态 SQL 语句。  
  
 执行动态 SQL 语句的最简单方法是使用直接执行语句。 此语句将 SQL 语句传递给 DBMS 进行编译和执行。  
  
 直接执行语句的一个缺点是 DBMS 必须经历的每个处理 SQL 语句每次执行该语句的五个步骤。 如果动态地执行多个语句，并且如果这些语句相似，它是一种浪费，此过程中涉及的开销可能很大。 若要解决这种情况下，动态 SQL，提供了名为准备好的执行，使用以下步骤执行的优化的形式：  
  
1.  该程序构造 SQL 语句在缓冲区中，就像直接执行语句的操作一样。 而不是主机变量，可以将问号 （？） 替换为任意位置中的语句文本以指示将更高版本提供常量值的常量。 问号调用作为参数标记。  
  
2.  该程序将 SQL 语句传递给使用准备语句，哪些请求，DBMS 分析、 验证和优化该语句并生成一个执行计划为其 DBMS。 程序然后使用 EXECUTE 语句 （不直接执行语句） 执行在更高版本时在准备语句。 它将传递通过名为 SQL 数据区域或 SQLDA 的特殊数据结构的语句的参数值。  
  
3.  该程序可以使用 EXECUTE 语句重复，提供每次执行动态语句的不同参数值。  
  
 准备好的执行仍不是静态 SQL 相同。 静态 SQL 中的前四个步骤的处理 SQL 语句发生在编译时。 准备好的执行，在执行这些步骤仍在运行时，但它们只执行一次;仅当调用 EXECUTE 时进行计划的执行。 这有助于消除一些固有的动态 SQL 的体系结构中的性能劣势。 下图显示了静态 SQL、 动态 SQL 与立即执行和动态 SQL，以及准备好的执行之间的差异。
