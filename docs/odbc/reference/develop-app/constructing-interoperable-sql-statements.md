---
title: 构造可互操作的 SQL 语句 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282508"
---
# <a name="constructing-interoperable-sql-statements"></a>构造交互 SQL 语句
如前面几节中所述，可互操作应用程序应使用 ODBC SQL 语法。 但除了使用此语法以外，许多其他问题都是由互操作应用程序所导致的。 例如，如果应用程序想要使用并非所有数据源都支持的功能（例如外部联接），该应用程序会执行什么操作？  
  
 此时，应用程序编写者必须对所需的语言功能和可选的功能做出一些决策。 在大多数情况下，如果特定驱动程序不支持应用程序所需的功能，则该应用程序只是拒绝使用该驱动程序运行。 但是，如果此功能是可选的，则应用程序可以绕过该功能。 例如，它可能会禁用允许用户使用该功能的接口部分。  
  
 若要确定支持的功能，应用程序首先使用 SQL_SQL_CONFORMANCE 选项调用**SQLGetInfo** 。 SQL 一致性级别为应用程序提供了受支持的 SQL 的广泛视图。 为了优化此视图，应用程序将使用多个其他选项中的任意一个来调用**SQLGetInfo** 。 有关这些选项的完整列表，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。 最后， **SQLGetTypeInfo**返回有关数据源支持的数据类型的信息。 以下部分列出了应用程序在构造可互操作的 SQL 语句时应注意的一些因素。  
  
 本部分包含以下主题。  
  
-   [目录和架构使用情况](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目录位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [标识符大小写](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [转义序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [过程调用中的参数标记](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)
