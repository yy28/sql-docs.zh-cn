---
title: 交易对游标和准备语句的影响 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300467"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>对游标和已准备语句的事务影响
提交或回滚事务对游标和访问计划具有以下影响：  
  
-   所有游标都将关闭，并且将删除该连接上已准备好的语句的访问计划。  
  
-   所有游标都已关闭，并且该连接上已准备好的语句的访问计划保持不变。  
  
-   所有游标保持打开状态，并且在该连接上准备好的语句的访问计划保持不变。  
  
 例如，假设数据源显示此列表中的第一个行为，即这些行为中限制最严格的行为。 现在假设应用程序执行以下操作：  
  
1.  将提交模式设置为手动提交。  
  
2.  在报表 1 上创建销售订单的结果集。  
  
3.  当用户突出显示该订单时，在报表 2 上的销售订单中创建行的结果集。  
  
4.  调用**SQLExecute**以执行在用户更新行时在语句 3 上编写的定位更新语句。  
  
5.  调用**SQLEndTran**提交定位的更新语句。  
  
 由于数据源的行为，步骤 5 中对**SQLEndTran**的调用会导致它关闭语句 1 和 2 上的游标，并删除所有语句的访问计划。 应用程序必须重新执行语句 1 和 2 才能重新创建结果集，并在语句 3 上重新准备语句。  
  
 在自动提交模式下 **，SQLEndTran**提交事务以外的函数：  
  
-   **SQLExecute**或**SQLExecDirect**在前面的示例中，步骤 4 中对**SQLExecute**的调用提交事务。 这将导致数据源关闭语句 1 和 2 上的游标，并删除该连接上所有语句的访问计划。  
  
-   **SQLBulk操作**或**SQLSetPos**在前面的示例中，假设在步骤 4 中，应用程序使用语句 2 上的SQL_UPDATE选项调用**SQLSetPos，** 而不是在语句 3 上执行定位的更新语句。 这将提交事务，并导致数据源关闭语句 1 和 2 上的游标，并丢弃该连接上的所有访问计划。  
  
-   **SQLCloseCursor**在前面的示例中，假设当用户突出显示不同的销售订单时，应用程序在报表 2 上调用**SQLCloseCursor，** 然后再为新销售订单的行创建结果。 对**SQLCloseCursor 的**调用提交**SELECT**语句，该语句创建了结果行集，并导致数据源关闭语句 1 上的游标，然后丢弃该连接上的所有访问计划。  
  
 应用程序（尤其是基于屏幕的应用程序，用户滚动的结果集并更新或删除行）必须小心编写围绕此行为的代码。  
  
 要确定数据源在提交或回滚事务时的行为方式，应用程序使用SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR选项调用**SQLGetInfo。**
