---
title: 动态 SQL |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306685"
---
# <a name="dynamic-sql"></a>动态 SQL
尽管静态 SQL 在许多情况下工作良好，但有一类应用程序无法提前确定数据访问。 例如，假设电子表格允许用户输入查询，然后电子表格将查询发送到 DBMS 以检索数据。 编写电子表格程序时，程序员显然无法知道此查询的内容。  
  
 为了解决此问题，电子表格使用一种称为动态 SQL 的嵌入式 SQL 形式。 与静态 SQL 语句（在程序中硬编码）不同，动态 SQL 语句可以在运行时生成并放置在字符串主机变量中。 然后，它们将发送到 DBMS 进行处理。 由于 DBMS 必须在运行时为动态 SQL 语句生成访问计划，因此动态 SQL 通常比静态 SQL 慢。 编译包含动态 SQL 语句的程序时，动态 SQL 语句不会从程序中剥离，如静态 SQL 中那样。 相反，它们被将语句传递给 DBMS 的函数调用替换;同一程序中的静态 SQL 语句得到正常处理。  
  
 执行动态 SQL 语句的最简单方法是使用 EXECUTE 立即语句。 此语句将 SQL 语句传递给 DBMS 进行编译和执行。  
  
 EXECUTE 立即语句的一个缺点是，每次执行语句时，DBMS 都必须执行处理 SQL 语句的五个步骤中的每个步骤。 如果动态执行许多语句，则此过程所涉及的开销可能很大，如果这些语句相似，则浪费。 为了解决此问题，动态 SQL 提供了一种优化的执行形式，称为准备执行，它使用以下步骤：  
  
1.  程序在缓冲区中构造 SQL 语句，就像执行立即语句一样。 可以代替宿主变量，将问号 （？） 替换为语句文本中任意位置的常量，以指示稍后将提供常量的值。 问号称为参数标记。  
  
2.  程序使用 PREPARE 语句将 SQL 语句传递给 DBMS，该语句请求 DBMS 解析、验证和优化该语句并为其生成执行计划。 然后，程序使用 EXECUTE 语句（而不是 EXECUTE 立即语句）在以后执行 PREPARE 语句。 它通过称为 SQL 数据区域或 SQLDA 的特殊数据结构传递语句的参数值。  
  
3.  程序可以重复使用 EXECUTE 语句，每次执行动态语句时提供不同的参数值。  
  
 准备执行仍与静态 SQL 不同。 在静态 SQL 中，处理 SQL 语句的前四个步骤发生在编译时。 在准备执行时，这些步骤仍发生在运行时，但它们只执行一次;计划执行仅在调用 EXECUTE 时执行。 这有助于消除动态 SQL 体系结构中固有的一些性能劣势。 下图显示了静态 SQL、具有即时执行的动态 SQL 和具有准备执行的动态 SQL 之间的区别。
