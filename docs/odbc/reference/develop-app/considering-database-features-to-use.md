---
title: "考虑到使用的数据库功能 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d17758711dd0e4e1590a3b4176829d9709a5dfd0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="considering-database-features-to-use"></a>考虑到使用的数据库功能
基本级别的互操作性知道后，必须考虑应用程序使用的数据库功能。 例如，哪些 SQL 语句将应用程序执行？ 将应用程序使用可滚动游标？ 事务？ 过程？ Long 数据？ 有关哪些功能的建议可能不支持所有的 Dbms，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数描述，以及[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 应用程序所需的功能可以消除一些 Dbms 从目标 Dbms 的列表。 它们还可能会显示应用程序可以轻松地针对许多 Dbms。  
  
 例如，如果所需的功能很简单，它们可以通常实现具有高度的互操作性。 应用程序执行一个简单**选择**语句并检索结果与只进游标很可能是因为其简易性高度可互操作： 几乎所有驱动程序和 Dbms 支持的功能它需求。  
  
 但是，如果所需的功能更复杂，例如可滚动游标、 定位的更新和 delete 语句和过程，必须经常进行权衡。 有几种可能性：  
  
-   **较低的互操作性，更多的功能。** 应用程序包括功能，但仅适用于支持它们的 Dbms。  
  
-   **更高版本的互操作性较少的功能。** 应用程序会删除功能，但适用于详细 Dbms。  
  
-   **更高版本互操作性，可选功能。** 应用程序包括功能，但将使它们可只能与支持这些这些 Dbms。  
  
-   **更高版本互操作性，更多的功能。** 应用程序使用支持它们的 Dbms 的功能，并为不希望这样做的 Dbms 模仿它们。  
  
 前两种情况就相对简单，若要实现的因为与所有受支持的 Dbms 或任何使用这些功能。 另一方面，后者的两种情况下，是更复杂。 它是在这两个用例以检查是否 DBMS 支持的功能和最后一种情况中，只需编写代码以模拟这些功能可能会极少量必需的。 因此，这些方案可能需要更多的开发时间，并且在运行时可能会降低。  
  
 请考虑的一般查询应用程序可以连接到单个数据源。 应用程序接受来自用户的查询，并在窗口中显示结果。 现在假设此应用程序具有一项功能，允许用户显示结果的多个将同时查询。 也就是说，它们可以执行查询和了解在某些操作的结果、 执行不同的查询和了解在其结果的某些，然后返回到第一个查询。 这会带来互操作性问题，因为某些驱动程序支持单个活动语句。  
  
 应用程序具有大量基于该驱动程序中的 SQL_MAX_CONCURRENT_ACTIVITIES 选项返回的内容的选项**SQLGetInfo**:  
  
-   **始终支持多个查询。** 连接到驱动程序后，应用程序检查活动语句的次数。 如果该驱动程序支持只有一个活动语句，应用程序将关闭连接，并向用户通知驱动程序不支持所需的功能。 应用程序很容易实现并具有完整功能，但具有较低的互操作性。  
  
-   **永远不会支持多个查询。** 应用程序会完全删除该功能。 它很容易实现和具有高互操作性，但其功能较少。  
  
-   **仅当驱动程序并支持多个查询。** 连接到驱动程序后，应用程序检查活动语句的次数。 应用程序允许用户启动新语句，当其中一个已处于活动状态，仅当该驱动程序支持多个活动语句。 应用程序具有更高版本的功能和互操作性，但将更难以实现。  
  
-   **始终支持多个查询和模拟它们在必要时。** 连接到驱动程序后，应用程序检查活动语句的次数。 应用程序始终允许用户在已处于活动状态时启动新语句。 如果该驱动程序支持只有一个活动语句，应用程序打开该驱动程序的其他连接，并在该连接上执行新的语句。 应用程序具有完整功能和高互操作性，但将更难以实现。
