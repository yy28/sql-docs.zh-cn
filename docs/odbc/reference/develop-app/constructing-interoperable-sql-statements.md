---
title: 构造可互操作的 SQL 语句 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 647efb94415c056ea091791e3f789fdbc3ce05f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="constructing-interoperable-sql-statements"></a>构造可互操作的 SQL 语句
如前面的部分中所述，可互操作的应用程序应使用 ODBC SQL 语法。 除了使用此语法，但是，许多其他问题面临的可互操作的应用程序。 例如，应用程序作用是什么如果它想要使用包含的功能，如外部联接中，不支持的所有数据源？  
  
 此时，应用程序编写器必须进行有关哪些语言功能是必需的这是可选的一些决策事项。 在大多数情况下，如果特定的驱动程序不支持的功能所需的应用程序，应用程序只需拒绝使用该驱动程序运行。 但是，如果是一个可选功能，应用程序可以解决该功能。 例如，它可能会禁用允许要使用该功能的用户界面中的这些部分。  
  
 若要确定支持的功能，通过调用应用程序启动**SQLGetInfo** SQL_SQL_CONFORMANCE 选项。 SQL 一致性级别为应用程序提供了广泛视图 SQL 支持。 若要优化此视图中，应用程序调用**SQLGetInfo**与任意大量其他选项。 有关这些选项的完整列表，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。 最后， **SQLGetTypeInfo**返回有关所支持的数据源的数据类型的信息。 下列部分列出了大量的可能构造可互操作的 SQL 语句时应用程序应监视的因素。  
  
 本部分包含以下主题。  
  
-   [目录和架构使用情况](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目录位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [标识符大小写](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [转义序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [过程调用中的参数标记](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)
