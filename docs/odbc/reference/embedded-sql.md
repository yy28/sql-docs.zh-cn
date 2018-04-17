---
title: 嵌入式 SQL |Microsoft 文档
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
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e7d51d8ae632f30528510448e52fc6c363d066d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="embedded-sql"></a>嵌入式的 SQL
将 SQL 语句发送到 DBMS 的第一个技术嵌入 SQL。 因为 SQL 不使用变量和控制的流语句，它通常用于为数据库子语言，可以添加到在传统的编程语言中，例如 C 或 COBOL 编写的程序。 这是一个中央的嵌入式 SQL 了解： 置于主机编程语言中编写的程序的 SQL 语句。 简言之，以下方法用于在主机语言中嵌入的 SQL 语句：  
  
-   由特殊 SQL 预编译器处理嵌入的 SQL 语句。 所有 SQL 语句开头引导，结尾的终止符，这两种预编译器标志的 SQL 语句。 引导和终结器因主机语言。 例如，引导是在 C 中的"执行 SQL"和"（& a) SQL ("腮腺炎，在终结器是一个分号 （;） 和 C 和腮腺炎中的右括号中。  
  
-   只要允许使用常量，从应用程序，称为主机变量的变量可以在嵌入的 SQL 语句中使用。 这些可用输入来定制特定的情况，然后在接收查询结果的输出的 SQL 语句。  
  
-   返回数据的单个行的查询处理与单独的 SELECT 语句;此语句指定查询和主机变量中返回数据。  
  
-   返回多行数据的查询的处理游标。 将跟踪游标的结果集内的当前行。 DECLARE CURSOR 语句定义查询、 OPEN 语句开始查询处理、 FETCH 语句检索的数据，连续行和关闭语句结束查询处理。  
  
-   打开游标时，可以使用定位的更新和定位的 delete 语句，来更新或删除当前选择光标的行。  
  
 本部分包含以下主题。  
  
-   [嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)  
  
-   [编译嵌入式 SQL 程序](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静态 SQL](../../odbc/reference/static-sql.md)  
  
-   [动态 SQL](../../odbc/reference/dynamic-sql.md)
