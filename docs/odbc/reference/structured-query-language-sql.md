---
title: 结构化查询语言 (SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86f9dd843171c02654302694c669f40b6b51ab78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232082"
---
# <a name="structured-query-language-sql"></a>结构化查询语言 (Structured Query Language) (SQL)
典型的 DBMS 允许用户存储、 访问和修改数据的方式组织，高效。 最初，Dbms 的用户是程序员。 访问存储的数据所需 COBOL 类编程语言中编写程序。 虽然这些程序通常被编写为非技术用户提供友好的界面，对数据本身的访问所需的知识渊博的专家程序员的服务。 对数据的临时访问实际上并不是。  
  
 用户未完全满意这种情况。 虽然他们无法访问数据，通常需要说服 DBMS 程序员能够编写特殊软件。 例如，如果销售部门需要看到在上个月的总销售额，按每个其销售人员，并且需要此服务在公司中的每个销售人员的长度按排名顺序的信息，它有两个选择：程序已经存在于允许完全这样一来，要访问的信息，或者在部门必须请求程序员来编写此类的程序。 在许多情况下，这是不是很值得，并且它始终是进行一次性，或即席，咨询昂贵的解决方案的更多工作。 随着越来越多的用户想要轻松访问，此问题的大小增长也越来越大。  
  
 允许用户访问临时上的数据所需为他们提供来表示它们的请求的语言。 对数据库的单个请求定义为查询的灵活性。这种语言称为一种查询语言。 许多查询语言开发用于此目的，但是其中一种变得最受欢迎：结构化的查询语言，在二十世纪七十年代发明，IBM。 它通过其首字母缩写，SQL，更常见的已知，并作为"ess 提示格"和"后续"发音。 SQL 转型成为标准 1986 年 ANSI 和 ISO 标准中 1987;它采用强大的多个数据库管理系统中。  
  
 尽管 SQL 来解决用户的特别需求，但需要的数据访问的计算机程序未不会消失。 实际上，大多数数据库访问权限仍 （现在） 以编程方式，在定期计划的报表和统计分析的窗体中，数据输入程序，如那些使用订单输入，以及数据处理程序，例如那些用于协调帐户和生成工作订单。  
  
 这些程序还使用 SQL，使用以下三种方法之一：  
  
-   **嵌入式 SQL**中的 SQL 语句中嵌入 C 或 COBOL 等主机语言。  
  
-   **SQL 模块**中的 SQL 语句都是在 DBMS 上编译，从主机语言调用。  
  
-   **调用级别接口**，或 CLI，其中包含要传递给 DBMS 的 SQL 语句，以及如何从 DBMS 检索结果所调用的函数。  
  
> [!NOTE]  
>  它是一词调用级别接口使用而不是应用程序编程接口 (API) 历史意外相同的操作的另一种说法。 在数据库领域中，API 用于描述 SQL 本身：SQL 是 DBMS 的 API。  
  
 这些选项的嵌入式的 SQL 是最常使用，虽然大多数主要 Dbms 支持专有 Cli。  
  
 本部分包含以下主题。  
  
-   [处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [嵌入式 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模块](../../odbc/reference/sql-modules.md)  
  
-   [调用级别接口](../../odbc/reference/call-level-interfaces.md)
