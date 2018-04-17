---
title: 结构化查询语言 (SQL) |Microsoft 文档
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
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: babb38e88d471cedceaa94e3c6696f9b5b59dcce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="structured-query-language-sql"></a>结构化查询语言 (Structured Query Language) (SQL)
典型的 DBMS 允许用户存储、 访问和修改数据组织、 高效的方式。 最初，Dbms 的用户已程序员。 访问存储的数据所需如 COBOL 用编程语言编写的程序。 虽然这些程序通常被编写为向非技术的用户友好界面，访问数据本身所需的有经验的程序员的服务。 非正式访问数据实际上并不是。  
  
 用户未完全满意这种情况。 尽管它们无法访问数据，它通常需要诱使 DBMS 程序员能够写入的特殊软件。 例如，如果销售部门想要在上个月中看到的总销售额，由每个其销售人员，并且想要按顺序排名的公司中的服务的每位销售人员长度此信息，它有两个选择： 这两个程序已存在允许使用的信息完全这种方式，访问或部门不得不要求程序员来编写此类的程序。 在许多情况下，这是不是很值得，并且它始终是一个昂贵的解决方案，用于一次性，或即席，查询的更多工作。 随着越来越多的用户想要轻松访问，此问题是增长越来越大。  
  
 允许用户访问临时上的数据所需，从而表示其请求的语言。 对数据库的单个请求被指查询的灵活性。这种语言称为查询语言。 许多查询语言开发用于此目的，但是其中一种变得最常见： 结构化查询语言中，在 IBM 发明二十世纪七十年代。 它通过其首字母缩写，SQL 中，更常用识别并同时作为"ess 提示 ell"和"结果"中; 发音此手册使用以前的发音。 SQL 变为 ANSI 标准 1986 年和标准 1987; 中的 ISO它现在使用极佳的多个数据库管理系统中。  
  
 尽管 SQL 解决用户的即席需求，但需通过计算机程序的数据访问未不会消失。 事实上，大多数数据库访问仍 （现在） 进行编程，定期计划的报表和统计分析形式中，数据输入程序，如那些使用订单输入和数据处理程序，如用于对帐帐户和生成工作订单。  
  
 这些程序还使用 SQL 中，使用以下三个方法之一：  
  
-   **嵌入式 SQL**中的 SQL 语句都嵌入到主机语言，例如 C 或 COBOL。  
  
-   **SQL 模块**，而是在编译在 DBMS 上并从主机语言调用哪些 SQL 语句。  
  
-   **调用级接口**，或 CLI，其中包含要传递给 DBMS 的 SQL 语句并从 DBMS 中检索结果所调用的函数。  
  
> [!NOTE]  
>  它是的术语调用级接口使用而不是应用程序编程接口 (API) 历史意外的内容相同的另一个术语。 在数据库世界中，API 用于描述本身的 SQL: SQL 是到 DBMS 的 API。  
  
 这些选项的嵌入式的 SQL 是最常使用的虽然大多数主要 Dbms 支持专有 Cli。  
  
 本部分包含以下主题。  
  
-   [处理的 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [嵌入式 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模块](../../odbc/reference/sql-modules.md)  
  
-   [调用级别接口](../../odbc/reference/call-level-interfaces.md)
