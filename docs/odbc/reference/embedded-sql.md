---
title: Embedded SQL |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915426"
---
# <a name="embedded-sql"></a>嵌入式 SQL
向 DBMS 发送 SQL 语句的第一种方法是嵌入式 SQL。 由于 SQL 不使用变量和控制流语句，因此它通常用作可以添加到用传统编程语言（例如 C 或 COBOL）编写的程序的数据库子语言。 这是嵌入式 SQL 的中心理念：将 SQL 语句置于用主机编程语言编写的程序中。 简单地说，以下方法用于以主机语言嵌入 SQL 语句：  
  
-   嵌入式 SQL 语句由特殊的 SQL 预编译器处理。 所有 SQL 语句都以引导开头，以结束符结尾，这两个语句均标记预编译器的 SQL 语句。 引导和终止符因主机语言而异。 例如，引导是 C 中的 "EXEC SQL" 和 "&SQL （" 在 MUMPS 中，终止符为分号（;)在 C 中为 MUMPS 中的右括号。  
  
-   应用程序中的变量称为主机变量，可在允许使用常量的嵌入式 SQL 语句中使用。 它们可用于输入，以便在特定情况下将 SQL 语句定制为特定情况，并用于接收查询结果。  
  
-   返回单个数据行的查询使用单独的 SELECT 语句进行处理;此语句指定要返回数据的查询和主机变量。  
  
-   返回多个数据行的查询将通过游标进行处理。 游标跟踪结果集中的当前行。 DECLARE CURSOR 语句定义查询，OPEN 语句开始进行查询处理，FETCH 语句检索连续的数据行，CLOSE 语句结束查询处理。  
  
-   当游标处于打开状态时，定位更新和定位 delete 语句可用于更新或删除游标当前选定的行。  
  
 本部分包含下列主题。  
  
-   [嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)  
  
-   [编译嵌入式 SQL 程序](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静态 SQL](../../odbc/reference/static-sql.md)  
  
-   [动态 SQL](../../odbc/reference/dynamic-sql.md)
