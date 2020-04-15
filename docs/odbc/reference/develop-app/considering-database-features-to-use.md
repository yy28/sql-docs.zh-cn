---
title: 考虑要使用的数据库功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9d966781def1c3eab6a9568eab07ab591326171
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299007"
---
# <a name="considering-database-features-to-use"></a>考虑使用数据库功能
已知基本互操作性级别后，必须考虑应用程序使用的数据库功能。 例如，应用程序将执行哪些 SQL 语句？ 应用程序是否会使用可滚动的游标？ 交易？ 程序？ 长数据？ 有关哪些功能可能不受所有 DBMS 支持的想法，请参阅[SQLGetInfo、SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数描述以及[附录 C：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 应用程序所需的功能可能会从目标 DBMS 列表中消除某些 DBMS。 它们还可以表明，应用程序可以轻松定位许多 DBMS。  
  
 例如，如果所需的功能很简单，它们通常可以通过高度的互操作性实现。 执行简单**SELECT**语句并使用仅转发游标检索结果的应用程序由于其简单性，很可能高度互操作：几乎所有驱动程序和 DBMS 都支持所需的功能。  
  
 但是，如果所需的功能更为复杂，例如可滚动游标、定位更新和删除语句以及过程，则通常必须进行权衡。 有几种可能性：  
  
-   **降低互操作性，提供更多功能。** 该应用程序包括这些功能，但仅适用于支持它们的 DBMS。  
  
-   **更高的互操作性，更少的功能。** 应用程序删除功能，但适用于更多的 DBMS。  
  
-   **更高的互操作性，可选功能。** 该应用程序包括这些功能，但仅提供支持这些功能的 DBMS。  
  
-   **更高的互操作性，更多的功能。** 应用程序使用具有支持它们的 DBMS 的功能，并为不支持它们的 DBMS 模拟这些功能。  
  
 前两种情况的实现相对简单，因为这些功能要么与所有支持的 DBMS 一起使用，要么与无。 另一方面，后两种情况更为复杂。 在这两种情况下，都需要检查 DBMS 是否支持这些功能，最后情况下，需要编写大量代码来模拟这些功能。 因此，这些方案可能需要更多的开发时间，并且在运行时可能较慢。  
  
 请考虑可以连接到单个数据源的通用查询应用程序。 应用程序接受用户的查询，并在窗口中显示结果。 现在假设此应用程序具有一个功能，允许用户同时显示多个查询的结果。 也就是说，他们可以执行查询并查看某些结果，执行不同的查询并查看其某些结果，然后返回到第一个查询。 这会带来互操作性问题，因为某些驱动程序仅支持单个活动语句。  
  
 应用程序有许多选择，具体取决于驱动程序返回的**SQLGetInfo**中SQL_MAX_CONCURRENT_ACTIVITIES选项 ：  
  
-   **始终支持多个查询。** 连接到驱动程序后，应用程序将检查活动语句的数量。 如果驱动程序仅支持一个活动语句，则应用程序将关闭连接并通知用户驱动程序不支持所需的功能。 该应用程序易于实现，具有完整的功能，但互操作性较低。  
  
-   **从不支持多个查询。** 应用程序完全放弃该功能。 它易于实现，具有高互操作性，但功能较少。  
  
-   **仅当驱动程序支持多个查询时，才支持多个查询。** 连接到驱动程序后，应用程序将检查活动语句的数量。 仅当驱动程序支持多个活动语句时，应用程序才允许用户启动新语句。 该应用程序具有更高的功能和互操作性，但更难实现。  
  
-   **始终支持多个查询，并在必要时对其进行模拟。** 连接到驱动程序后，应用程序将检查活动语句的数量。 应用程序始终允许用户在已处于活动状态时启动新语句。 如果驱动程序仅支持一个活动语句，则应用程序将打开到该驱动程序的附加连接，并在该连接上执行新语句。 该应用程序具有完整的功能和高互操作性，但更难实现。
