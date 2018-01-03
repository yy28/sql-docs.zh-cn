---
title: "对游标和已准备的语句的事务的影响 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 836cef9465c2ee935628e92168b9ace7650b8e66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>对游标和已准备的语句的事务的影响
提交或回滚事务将产生以下影响游标和访问计划：  
  
-   所有游标都将都关闭，并且会删除该连接上的已准备的语句的访问计划。  
  
-   所有游标都将都关闭，并在该连接上的已准备的语句的访问计划保持不变。  
  
-   所有游标都保持打开状态，并在该连接上的已准备的语句的访问计划都保持不变。  
  
 例如，假设数据源出现在此列表中，最严格的这些行为的第一个行为。 现在应用程序执行以下假设：  
  
1.  将提交模式设置为手动提交。  
  
2.  在语句 1 上创建一个销售订单的结果集。  
  
3.  用户突出显示该订单时，2，对帐单上销售订单中创建结果集的行。  
  
4.  调用**SQLExecute**时要执行已准备好的定位的更新语句上语句 3，用户更新行。  
  
5.  调用**SQLEndTran**提交定位的 update 语句。  
  
 由于数据源的行为，调用**SQLEndTran**在步骤 5 会导致它时关闭游标语句 1 和 2 以及删除所有的语句上的访问计划。 应用程序必须重新执行语句 1 和 2 以重新创建的结果集和 reprepare 语句 3 中的语句。  
  
 在自动提交模式下，函数以外**SQLEndTran**提交的事务：  
  
-   **SQLExecute**或**SQLExecDirect**在前面的示例中，调用**SQLExecute**在步骤 4 提交事务。 这会导致数据源，以关闭在 1 和 2 的语句游标并删除该连接上的所有语句上的访问计划。  
  
-   **SQLBulkOperations**或**SQLSetPos**在前面的示例中，假设，在步骤 4 中在应用程序调用**SQLSetPos** SQL_UPDATE 上使用选项语句 2，而不是执行定位在语句 3 上的 update 语句。 此提交事务和会导致数据源时关闭游标语句 1 和 2，并放弃该连接上的所有访问计划。  
  
-   **SQLCloseCursor**在前面的示例中，假设用户突出显示不同的销售订单时，调用应用程序**SQLCloseCursor**上 2 的语句才能创建新的销售的行的结果顺序。 调用**SQLCloseCursor**提交**选择**语句创建的行结果集和会导致数据源时关闭游标语句 1，然后放弃上的所有访问计划连接。  
  
 应用程序，特别是基于屏幕的应用程序在其中在用户滚动的结果集和更新或删除行，必须小心地选择对解决此问题的代码。  
  
 若要确定数据源在提交或回滚事务时的行为，应用程序调用**SQLGetInfo**使用 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项。
