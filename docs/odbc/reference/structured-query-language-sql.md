---
title: 结构化查询语言（SQL） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293387"
---
# <a name="structured-query-language-sql"></a>结构化查询语言 (Structured Query Language) (SQL)
典型的 DBMS 允许用户以有序且高效的方式存储、访问和修改数据。 最初，Dbms 的用户是程序员。 访问所存储的数据需要用编程语言（例如 COBOL）编写程序。 尽管这些程序经常编写为向非技术用户提供友好界面，但对数据本身的访问需要具有丰富程序员的服务。 偶尔访问数据是不切实际的。  
  
 对于这种情况，用户并不完全满意。 虽然它们可以访问数据，但通常需要说服 DBMS 程序员编写特殊软件。 例如，如果某一销售部门想要查看上个月中每个销售人员的总销售额，并希望此信息按公司每位销售人员的服务长度排名来确定，则有两个选择：已存在允许以这种方式访问该信息的程序，或部门必须要求程序员编写这样的程序。 在许多情况下，这种方法比实际情况要多，而且它始终是一种长期或即席查询的昂贵解决方案。 随着越来越多的用户想要轻松访问，此问题增长得更大，更大。  
  
 允许用户以即席方式访问数据需要提供一种语言来表达其请求。 对数据库的单个请求定义为查询;这种语言称为查询语言。 出于此目的，开发了许多查询语言，但其中一个是最受欢迎的语言：结构化查询语言，这是在一年的 IBM。 它更常见的情况是，其缩写词为 SQL，并同时作为 "ess-单元格" 和 "脚步"。 SQL 变为1986的 ANSI 标准，以及1987中的 ISO 标准。它目前在很多数据库管理系统中使用。  
  
 尽管 SQL 已经解决了用户的即席需求，但计算机程序访问数据的需要不会消失。 事实上，对于定期计划的报表和统计分析、数据输入程序（例如用于订单输入的项目）和数据操作程序（例如用于对帐户进行协调和生成工作订单的程序），大多数数据库访问仍以编程方式进行。  
  
 这些程序也使用以下三种方法中的一种：  
  
-   **嵌入式 sql**，其中的 sql 语句嵌入在 C 或 COBOL 等主机语言中。  
  
-   **Sql 模块**，在该模块中，sql 语句在 DBMS 上编译并从主机语言调用。  
  
-   **调用级别接口**（或 CLI），它由调用的函数（用于向 DBMS 传递 SQL 语句和从 dbms 检索结果）组成。  
  
> [!NOTE]  
>  这是一种意外情况，就是使用术语调用级接口而不是应用程序编程接口（API），另一种术语用于相同的目的。 在数据库领域，API 用于描述 SQL 本身： SQL 是 DBMS 的 API。  
  
 在这些选择中，嵌入的 SQL 是最常用的，尽管大多数主要 Dbms 支持专用 Cli。  
  
 本部分包含以下主题。  
  
-   [处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [嵌入式 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模块](../../odbc/reference/sql-modules.md)  
  
-   [调用级别接口](../../odbc/reference/call-level-interfaces.md)
