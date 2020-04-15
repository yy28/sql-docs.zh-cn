---
title: 结构化查询语言 （SQL） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293387"
---
# <a name="structured-query-language-sql"></a>结构化查询语言 (Structured Query Language) (SQL)
典型的 DBMS 允许用户以有组织的高效方式存储、访问和修改数据。 最初，DBMS 的用户是程序员。 访问存储的数据需要用编程语言（如 COBOL）编写程序。 虽然这些程序通常是为向非技术用户提供友好的接口而编写的，但访问数据本身需要知识渊博的程序员的服务。 随意访问数据是不现实的。  
  
 用户并不完全满意这种情况。 虽然他们可以访问数据，但通常需要说服 DBMS 程序员编写特殊软件。 例如，如果销售部门希望查看每个销售人员上个月的总销售额，并希望此信息按公司中每个销售人员的服务年限顺序排列，则它有两种选择：要么已经存在允许以这种方式访问信息的程序，要么部门必须要求程序员编写此类程序。 在许多情况下，这是比它的价值更多的工作，它总是一个昂贵的解决方案，一次性或临时，查询。 随着越来越多的用户希望轻松访问，此问题变得越来越大。  
  
 允许用户临时访问数据，需要为他们提供表达请求的语言。 对数据库的单个请求定义为查询;对数据库的单个请求将定义为查询。这种语言称为查询语言。 许多查询语言都是为此目的开发的，但其中一种成为最流行的：结构化查询语言，在 20 世纪 70 年代在 IBM 中发明。 它更常见的缩写为 SQL，并且发音为"es-cue-ell"和"sequel"。 SQL 于 1986 年成为 ANSI 标准，1987 年成为 ISO 标准;它今天在许多数据库管理系统中使用。  
  
 尽管 SQL 解决了用户的临时需求，但计算机程序对数据访问的需求并没有消失。 事实上，大多数数据库访问仍然是（并且）以定期计划的报告和统计分析的形式编程，数据输入程序（如用于订单输入的程序）和数据操作程序（如用于对帐和生成工作订单的程序）。  
  
 这些程序还使用 SQL，使用以下三种技术之一：  
  
-   **嵌入式 SQL**，其中 SQL 语句嵌入在宿主语言（如 C 或 COBOL）中。  
  
-   **SQL 模块**，其中 SQL 语句在 DBMS 上编译，并从宿主语言调用。  
  
-   **调用级接口**或 CLI，它由调用的函数组成，这些函数用于将 SQL 语句传递给 DBMS 并从 DBMS 检索结果。  
  
> [!NOTE]  
>  使用术语调用级接口而不是应用程序编程接口 （API） 是一个历史事故，这是另一个相同术语的术语。 在数据库世界中，API 用于描述 SQL 本身：SQL 是 DBMS 的 API。  
  
 在这些选择中，嵌入式 SQL 是最常用的，尽管大多数主要 DBMS 都支持专有的 CLIs。  
  
 本部分包含以下主题。  
  
-   [处理 SQL 语句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [嵌入式 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模块](../../odbc/reference/sql-modules.md)  
  
-   [调用级别接口](../../odbc/reference/call-level-interfaces.md)
