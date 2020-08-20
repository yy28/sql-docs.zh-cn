---
description: 考虑使用数据库功能
title: 正在考虑使用数据库功能 |Microsoft Docs
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
ms.openlocfilehash: 2abaed3806514a161c5c506d8bad89b4d3b75153
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465889"
---
# <a name="considering-database-features-to-use"></a>考虑使用数据库功能
了解基本的互操作性级别后，必须考虑应用程序使用的数据库功能。 例如，应用程序将执行哪些 SQL 语句？ 应用程序是否将使用可滚动游标？ 记录? 操作? 长数据？ 有关所有 Dbms 可能不支持哪些功能的建议，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 函数说明和 [附录 C： SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 应用程序所需的功能可能会从目标 Dbms 列表中消除某些 Dbms。 它们也可能会显示应用程序可以轻松地以很多 Dbms 为目标。  
  
 例如，如果所需的功能很简单，通常可以通过高度的互操作来实现。 执行简单的 **SELECT** 语句并使用只进游标检索结果的应用程序可能会因为其简易性而高度可互操作：几乎所有驱动程序和 dbms 都支持所需的功能。  
  
 但是，如果所需的功能更复杂，例如可滚动游标、定位更新和删除语句以及过程，则通常必须进行权衡。 有几种可能性：  
  
-   **互操作性更低，功能更多。** 该应用程序包括功能，但仅适用于支持这些功能的 Dbms。  
  
-   **更高的互操作性，更少的功能。** 应用程序会丢弃功能，但会使用更多 Dbms。  
  
-   **更高的互操作性和可选功能。** 该应用程序包括功能，但仅使它们可用于支持这些功能的 Dbms。  
  
-   **互操作性更高，功能更多。** 应用程序使用支持这些功能的 Dbms，并对不支持这些功能的 Dbms 进行模拟。  
  
 前两种情况相对简单，可实现，因为这些功能适用于所有受支持的 Dbms 或无。 另一方面，这两种情况更复杂。 在这两种情况下都需要检查 DBMS 是否支持这些功能，在最后一种情况下，可以编写可能大量的代码来模拟这些功能。 因此，这些方案可能需要更多的开发时间，并且在运行时可能会更慢。  
  
 假设可以连接到单个数据源的一般查询应用程序。 应用程序接受来自用户的查询，并在窗口中显示结果。 现在假设此应用程序具有一项功能，使用户能够同时显示多个查询的结果。 也就是说，他们可以执行查询并查看一些结果，执行其他查询并查看其中一些结果，然后返回到第一个查询。 这会带来互操作性问题，因为某些驱动程序只支持单个活动语句。  
  
 应用程序具有许多选择，具体取决于驱动程序为 **SQLGetInfo**中的 SQL_MAX_CONCURRENT_ACTIVITIES 选项返回的内容：  
  
-   **始终支持多个查询。** 连接到驱动程序后，应用程序会检查活动语句的数量。 如果驱动程序仅支持一个活动语句，则应用程序会关闭连接，并通知用户驱动程序不支持所需的功能。 此应用程序易于实现并具有完整的功能，但互操作性较低。  
  
-   **从不支持多个查询。** 应用程序将完全删除该功能。 它易于实现并具有高互操作性，但功能更少。  
  
-   **仅当驱动程序支持多个查询时才支持。** 连接到驱动程序后，应用程序会检查活动语句的数量。 如果驱动程序支持多个活动语句，则应用程序允许用户在一个已处于活动状态的新语句时启动该语句。 应用程序具有更高的功能和互操作性，但难以实现。  
  
-   **始终支持多个查询并在必要时对其进行模拟。** 连接到驱动程序后，应用程序会检查活动语句的数量。 当应用程序已处于活动状态时，应用程序始终允许用户启动新语句。 如果驱动程序仅支持一个活动语句，则应用程序将打开与该驱动程序的其他连接，并对该连接执行新的语句。 应用程序具有完整的功能和高互操作性，但难以实现。
