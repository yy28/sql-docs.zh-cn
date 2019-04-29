---
title: 考虑使用数据库功能 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92eeb64b95d666b15c03c70d656d2309a63eabf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042183"
---
# <a name="considering-database-features-to-use"></a>考虑使用数据库功能
基本级别的互操作性已知后，必须考虑应用程序使用的数据库功能。 例如，哪些 SQL 语句将该应用程序执行？ 将应用程序使用可滚动游标？ 事务？ 过程？ 长整型数据？ 有关所有 Dbms 可能不都支持哪些功能的看法，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，并[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数描述，以及[附录 c:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 应用程序所需的功能可能会消除某些 Dbms 从目标 Dbms 的列表。 它们还可能会显示该应用程序可以轻松地面向许多 Dbms。  
  
 例如，如果所需的功能很简单，它们可以通常实现具有高度的互操作性。 执行一个简单的应用程序**选择**与只进游标的语句并检索结果很可能是由于其简单性高度可互操作：几乎所有驱动程序和 Dbms 支持其所需的功能。  
  
 但是，如果所需的功能是更复杂，例如可滚动游标，定位的 update 和 delete 语句和过程，必须经常进行的权衡。 有几种可能性：  
  
-   **较低的互操作性，更多的功能。** 应用程序包括但仅适用于支持它们的 Dbms 的功能。  
  
-   **更高版本的互操作性较少的功能。** 应用程序删除功能，但适用于多个 Dbms。  
  
-   **更高版本的互操作性的可选功能。** 应用程序包括功能，但使其可仅与这些 Dbms 支持它们。  
  
-   **更高版本的互操作性，更多的功能。** 应用程序使用支持它们的 Dbms 的功能，并模拟它们的 Dbms 不这样做。  
  
 前两个用例是相对较容易实施，因为与所有受支持的 Dbms 或任何使用这些功能。 另一方面后, 两种情况下，是更复杂。 有必要在这两种情况下，若要检查 DBMS 是否支持的功能，并在最后一种情况下，只需编写代码来模拟这些功能可能很大少量。 因此，这些方案可能需要更多的开发时间，并在运行时可能会降低。  
  
 请考虑可以连接到单个数据源的通用查询应用程序。 应用程序接受来自用户查询，并在窗口中显示结果。 现在假设此应用程序有一项功能，允许用户显示结果的多个将同时查询。 也就是说，它们可以执行查询和看一下结果、 执行不同的查询和看一下其结果，然后返回到第一个查询。 这提供了互操作性问题，因为某些驱动程序支持单个活动语句。  
  
 应用程序具有多种选择，基于该驱动程序返回中的 SQL_MAX_CONCURRENT_ACTIVITIES 选项**SQLGetInfo**:  
  
-   **始终支持多个查询。** 连接到驱动程序后，应用程序将检查活动语句数。 如果该驱动程序支持只有一个活动语句，该应用程序关闭连接，并通知用户该驱动程序不支持所需的功能。 应用程序很容易实现和具有完整功能，但具有较低的互操作性。  
  
-   **永远不会支持多个查询。** 应用程序中完全删除该功能。 它很容易实现和高互操作性，但有更少的功能。  
  
-   **仅当驱动程序执行，则支持多个查询。** 连接到驱动程序后，应用程序将检查活动语句数。 应用程序允许用户在一个已处于活动状态，仅当该驱动程序支持多个活动语句时启动新的语句。 应用程序具有更高版本的功能和互操作性，但很难实现。  
  
-   **应始终支持多个查询，并模拟它们在必要时。** 连接到驱动程序后，应用程序将检查活动语句数。 应用程序始终允许用户启动新的语句时已处于活动状态。 如果该驱动程序支持只有一个活动语句，应用程序将打开该驱动程序的其他连接，并且该连接上执行新语句。 应用程序具有完整的功能和高互操作性，但很难实现。
