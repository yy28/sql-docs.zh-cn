---
title: 嵌入式 SQL |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915426"
---
# <a name="embedded-sql"></a>嵌入式 SQL
嵌入的第一个方法用于将 SQL 语句发送到 DBMS SQL。 因为 SQL 不使用变量和控制流语句，它是通常用作可以添加到以传统的编程语言，例如 C 或 COBOL 编写的程序数据库子语言。 这是一个中央嵌入式 SQL 的概念： SQL 语句置于主机编程语言中编写的程序。 简单地说，以下方法用于在宿主语言中嵌入的 SQL 语句：  
  
-   由特殊 SQL 使用预编译器处理嵌入的 SQL 语句。 所有 SQL 语句与引导开头和结尾终结器，这两个标记的 SQL 语句预编译器。 引导和终结器因主机语言。 例如，引导是在 C 中的"执行 SQL"和"& SQL ("中腮腺炎，终止符是以分号 （;） 在 C 和腮腺炎中的右括号中。  
  
-   只要允许使用常量，可以在嵌入的 SQL 语句中使用从应用程序，称为主机变量的变量。 这些可用于在输入定制到特定的情况并输出接收查询的结果上的 SQL 语句。  
  
-   返回单个数据行的查询处理与单独的 SELECT 语句;此语句指定查询和返回数据中的主机变量。  
  
-   返回多行数据的查询处理与游标的游标。 跟踪结果集内的当前行的游标。 DECLARE CURSOR 语句定义查询、 OPEN 语句启动的查询处理、 FETCH 语句检索的数据，连续的行和 CLOSE 语句结束查询处理。  
  
-   打开游标时，可以使用定位的更新和定位的 delete 语句，若要更新或删除当前选择光标的行。  
  
 本部分包含以下主题。  
  
-   [嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)  
  
-   [编译嵌入式 SQL 程序](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [静态 SQL](../../odbc/reference/static-sql.md)  
  
-   [动态 SQL](../../odbc/reference/dynamic-sql.md)
