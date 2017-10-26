---
title: "事务 ODBC |Microsoft 文档"
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
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11b681fa324c2c0b514bfb43aa67d51ce19a1ba
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="transactions-odbc"></a>ODBC 事务
A*事务*是工作的单元，都将作为一个原子操作; 也就是说，此操作成功，要么作为一个整体失败。 例如，考虑将资金从一个银行帐户转移到另一个。 这涉及到两个步骤： 从第一个帐户中取出 money 和存储在第二个。 很重要，这两个步骤都成功;不是可接受的一个步骤，若要成功执行，另一个失败。 支持事务的数据库就能够保证这一点。  
  
 可以通过在完成事务*提交*或*回滚*。 提交事务时，事务将变成永久性的因为所做的更改。 当事务回滚后时，受影响的行返回到之前事务开始所处的状态。 若要扩展帐户传输示例，应用程序执行了一条 SQL 语句，借记的第一个帐户和信用额度第二个帐户的不同 SQL 语句。 如果这两个语句都成功，然后，应用程序提交事务。 但如果出于任何原因失败任一语句，应用程序回滚事务。 在任一情况下，应用程序可保证末尾的事务一致的状态。  
  
 单个事务可以包含多个数据库操作发生在不同时间。 如果其他事务具有完全访问权限的中间结果，事务可能会妨碍与另一个。 例如，假设一个事务中插入一行，第二个事务读取的行和第一个事务将回滚。 第二个事务现在已为不存在的行的数据。  
  
 若要解决此问题，有各种方案，以隔离来自另一个事务。 *事务隔离*通常由实现锁定的行，它可以阻止从在同一时间使用同一行的多个事务。 有些数据库中锁定行可能还锁定其他行。  
  
 增加的事务隔离伴随降低*的并发程度，*或两个事务能够在同一时间使用相同的数据。 有关详细信息，请参阅[设置事务的隔离级别](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 中的事务](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [并发控制](../../../odbc/reference/develop-app/concurrency-control.md)

