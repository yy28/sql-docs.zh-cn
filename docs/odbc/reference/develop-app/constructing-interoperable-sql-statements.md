---
title: 构造交互 SQL 语句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87ad7b8b36c80d86e0c3ac0335dd6f348a30c7bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002239"
---
# <a name="constructing-interoperable-sql-statements"></a>构造交互 SQL 语句
如前面各节中所述，可互操作应用程序应使用 ODBC SQL 语法。 除了使用此语法，但是，许多其他问题所面临的可互操作应用程序。 例如，有什么作用应用程序？ 想要使用的所有数据源不都支持的功能，如外部联接  
  
 此时，应用程序编写器必须进行一些有关哪些语言功能是必需，哪些是可选的决策。 在大多数情况下，如果特定的驱动程序不支持一项功能所需的应用程序，该应用程序只需拒绝使用该驱动程序运行。 但是，如果该功能是可选的该应用程序可以解决该功能。 例如，它可能会禁用允许要使用该功能的用户界面中的这些部分。  
  
 若要确定支持哪些功能，通过调用应用程序启动**SQLGetInfo** SQL_SQL_CONFORMANCE 选项。 SQL 一致性级别为应用程序提供了广泛的支持 SQL 视图。 若要优化此视图中，应用程序调用**SQLGetInfo**与任何数目的其他选项。 有关这些选项的完整列表，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。 最后， **SQLGetTypeInfo**返回有关所支持的数据源的数据类型的信息。 以下各节列出的应用程序构建可互操作的 SQL 语句时应监视可能因素的数量。  
  
 本部分包含以下主题。  
  
-   [目录和架构使用情况](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目录位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [标识符大小写](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [转义序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [文本前缀和后缀](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [过程调用中的参数标记](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 语句](../../../odbc/reference/develop-app/ddl-statements.md)
