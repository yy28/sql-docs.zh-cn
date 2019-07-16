---
title: 对游标和预定义的语句的事务影响 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83b693922d08f7298d0c5282fe2c7d1c20149d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046879"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>对游标和已准备语句的事务影响
提交或回滚事务会有以下影响游标和访问计划：  
  
-   所有游标都将都关闭，并删除该连接上的预定义语句访问计划。  
  
-   所有游标都将都关闭，并访问该连接上预定义语句的计划将保持不变。  
  
-   所有游标都保持打开状态，并访问该连接上预定义语句的计划将都保持不变。  
  
 例如，假设数据源将展示在此列表中，这些行为最具限制性的第一行为。 现在假设应用程序执行以下操作：  
  
1.  将提交模式设置为手动提交。  
  
2.  对 1 的语句创建销售订单的结果集。  
  
3.  当用户将突出显示该顺序语句 2，销售订单中创建结果集的行。  
  
4.  调用**SQLExecute**时要执行已准备好的定位的更新语句语句 3，用户更新行。  
  
5.  调用**SQLEndTran**提交定位的 update 语句。  
  
 由于数据源的行为，调用**SQLEndTran**在步骤 5 会导致它以关闭游标语句 1 和 2 并删除所有语句上的访问计划。 应用程序必须重新执行语句 1 和 2 来重新创建结果集和 reprepare 语句 3 中的语句。  
  
 在自动提交模式下，函数以外**SQLEndTran**提交事务：  
  
-   **SQLExecute**或**SQLExecDirect**在前面的示例中，调用**SQLExecute**在步骤 4 提交事务。 这会导致要关闭的游标语句 1 和 2，并删除该连接上的所有语句上的访问计划的数据源。  
  
-   **SQLBulkOperations**或**SQLSetPos**在前面的示例，假设，在步骤 4 中在应用程序调用**SQLSetPos**带有 SQL_UPDATE 选项语句 2，而不是执行语句 3 上定位的 update 语句。 此提交事务和数据源将关闭游标语句 1 和 2，并放弃在该连接上的所有访问计划。  
  
-   **SQLCloseCursor**在前面的示例，假设用户突出显示了不同的销售订单时，调用应用程序**SQLCloseCursor**上语句 2，然后才能创建新的销售的行的结果顺序。 在调用**SQLCloseCursor**提交**选择**创建行的结果集和数据源将关闭游标语句 1，然后放弃上的所有访问计划的语句连接。  
  
 应用程序，尤其是基于屏幕的应用程序在其中在用户滚动的结果集和更新或删除行，必须小心针对此行为进行编码。  
  
 若要确定数据源时提交或回滚事务的行为，应用程序调用**SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 选项。
