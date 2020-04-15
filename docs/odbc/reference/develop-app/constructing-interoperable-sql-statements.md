---
title: 构造可互操作的 SQL 语句 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282508"
---
# <a name="constructing-interoperable-sql-statements"></a>构造交互 SQL 语句
如前一节所述，可互操作的应用程序应使用 ODBC SQL 语法。 但是，除了使用此语法之外，可互操作的应用程序还面临着许多其他问题。 例如，如果应用程序想要使用并非所有数据源都支持的功能（如外部联接），它该怎么办？  
  
 此时，应用程序编写器必须做出一些决定，确定哪些语言功能是必需的，哪些是可选的。 在大多数情况下，如果特定驱动程序不支持应用程序所需的功能，则应用程序只是拒绝使用该驱动程序运行。 但是，如果该功能是可选的，则应用程序可以围绕该功能进行处理。 例如，它可能会禁用允许用户使用该功能的界面部分。  
  
 要确定支持哪些功能，应用程序首先使用SQL_SQL_CONFORMANCE选项调用**SQLGetInfo。** SQL 一致性级别为应用程序提供了支持 SQL 的广泛视图。 要优化此视图，应用程序使用许多其他选项中的任何一个调用**SQLGetInfo。** 有关这些选项的完整列表，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。 最后 **，SQLGetTypeInfo**返回有关数据源支持的数据类型的信息。 以下各节列出了应用程序在构造可互操作 SQL 语句时应注意的一些可能因素。  
  
 本部分包含以下主题。  
  
-   [目录和架构使用情况](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目录位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [标识符大小写](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [转义序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [过程调用中的参数标记](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)
