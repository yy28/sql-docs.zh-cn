---
title: 动态 SQL |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 465f9785436880fce74136dd293abab33d1d2b4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-sql"></a>动态 SQL
尽管静态 SQL 适用于许多情况下，但是没有该数据访问无法预先确定的应用程序的类。 例如，假设电子表格，用户可以输入一个查询，后者电子表格随后发送到 DBMS 中检索数据。 此查询的内容显然无法知道向程序员写入电子表格程序时。  
  
 若要解决此问题，该电子表格，请使用一种形式的调用动态 SQL 的嵌入式 SQL。 不同于静态 SQL 语句，采用硬编码在程序中，可以在运行时生成动态 SQL 语句，并置于字符串主机变量中。 它们随后会发送到 DBMS 以进行处理。 由于 DBMS 必须生成一个访问计划在运行时针对动态 SQL 语句，则动态 SQL 是通常比静态 SQL 速度慢。 编译后的程序包含动态 SQL 语句，都不会在程序中，如下所示静态 SQL 去除动态 SQL 语句。 相反，它们会被函数调用中将该语句传递到 DBMS; 代替将通常被视为同一程序中的静态 SQL 语句。  
  
 执行动态 SQL 语句的最简单方法是与立即执行的语句一起使用。 此语句将传递给进行编译和执行 DBMS 的 SQL 语句。  
  
 立即执行的一个缺点是语句的 DBMS 必须通过每个处理每次执行该语句的 SQL 语句的五个步骤。 如果很多语句执行动态，并且如果这些语句相似，它是一种浪费，此过程中涉及的开销非常显著。 若要解决这种情况下，动态 SQL，请提供优化的形式的执行调用准备好的执行，使用以下步骤：  
  
1.  立即执行的语句一样，程序将构造在缓冲区中的 SQL 语句。 而不是主机变量，可以为任何位置中的语句文本以指示将更高版本提供常量的值的常量替换问号 （？）。 问号称为参数标记。  
  
2.  程序将传递给使用准备语句，哪些请求，DBMS 分析、 验证和优化的语句和生成执行计划为其 DBMS 的 SQL 语句。 然后，程序使用 EXECUTE 语句 （不立即执行的语句） 来执行稍后在准备语句。 它将传递通过 SQL 数据区域或 SQLDA 调用一种特殊的数据结构的语句的参数值。  
  
3.  程序可以使用 EXECUTE 语句重复，提供每次执行动态语句的不同的参数值。  
  
 准备好的执行仍不是静态 SQL 相同。 在静态 SQL 中，处理的 SQL 语句的前四个步骤发生在编译时。 在准备好的执行这些步骤仍发生在运行时，但它们只执行一次;执行计划仅在调用 EXECUTE 时才发生。 这有助于消除一些动态 SQL 的体系结构中的固有的性能缺点。 下图显示静态 SQL、 与立即执行的动态 SQL 和与已准备好执行动态 SQL 之间的差异。
