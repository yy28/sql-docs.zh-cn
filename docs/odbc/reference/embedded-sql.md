---
title: 嵌入式 SQL |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306670"
---
# <a name="embedded-sql"></a>嵌入式 SQL
向 DBMS 发送 SQL 语句的第一种技术是嵌入式 SQL。 由于 SQL 不使用变量和流控制语句，因此它通常用作数据库子语言，可以添加到使用传统编程语言（如 C 或 COBOL）编写的程序中。 这是嵌入式 SQL 的核心思想：将 SQL 语句放在用主机编程语言编写的程序中。 简而言之，以下技术用于将 SQL 语句嵌入到宿主语言中：  
  
-   嵌入式 SQL 语句由特殊的 SQL 预编译器处理。 所有 SQL 语句都以介绍器开头，以终止符结尾，两者都标记预编译器的 SQL 语句。 介绍器和终止符随宿主语言而变化。 例如，介绍器在 C 中为"EXEC SQL"，在 MUMPS 中为"&SQL"，终止符为分号（;)在 C 和 MUMPS 中的右括号。  
  
-   应用程序中的变量称为主机变量，可以在允许常量的嵌入式 SQL 语句中使用。 这些可用于输入，以根据特定情况定制 SQL 语句，并在输出上用于接收查询结果。  
  
-   返回一行数据的查询使用单例 SELECT 语句处理;此语句指定要在其中返回数据的查询和主机变量。  
  
-   返回多行数据的查询使用游标处理。 游标跟踪结果集中的当前行。 DECLARE CURSOR 语句定义查询，OPEN 语句开始查询处理，FETCH 语句检索连续的数据行，CLOSE 语句结束查询处理。  
  
-   打开游标时，定位更新和定位删除语句可用于更新或删除游标当前选择的行。  
  
 本部分包含以下主题。  
  
-   [嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)  
  
-   [编译嵌入式 SQL 程序](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静态 SQL](../../odbc/reference/static-sql.md)  
  
-   [动态 SQL](../../odbc/reference/dynamic-sql.md)
