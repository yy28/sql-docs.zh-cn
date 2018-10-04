---
title: 事务 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840655"
---
# <a name="transactions-odbc"></a>事务 ODBC
一个*事务*是工作单元，都将作为一个原子操作; 也就是说，操作是成功还是失败作为一个整体。 例如，考虑将资金从一个银行帐户转移到另一个。 这涉及到两个步骤： 从第一个帐户存款资金并存储在第二个。 非常重要，这两个步骤都成功;不可以接受的一个步骤成功，另一个失败。 支持事务的数据库可为确保这一点。  
  
 可以通过在完成事务*提交*或正在*回滚*。 已提交事务时，所做的在事务进行永久更改。 当事务回滚后时，受影响的行返回到事务开始前的状态。 若要将帐户传输示例扩展，应用程序执行一个 SQL 语句的第一个帐户中借记和信用额度的第二个帐户的不同 SQL 语句。 如果这两个语句都成功，然后，应用程序提交事务。 但如果出于任何原因失败任一语句，该应用程序回滚该事务。 在任一情况下，应用程序可保证在事务结束时处于一致状态。  
  
 在单个事务可以包含多个数据库操作发生在不同的时间。 如果其他事务具有完全访问的中间结果，事务可能会影响需要与另一个。 例如，假设一个事务插入一行，第二个事务读取的行和第一个事务将回滚。 第二个事务现在已不存在的行的数据。  
  
 若要解决此问题，有各种方案来隔离从另一个事务。 *事务隔离*通常由实现锁定行，它可以阻止从在同一时间使用同一行的多个事务。 在某些数据库中，锁定行可能还锁定的其他行。  
  
 增加的事务隔离，提供了降低*并发程度，* 或两个事务能够同时使用相同的数据。 有关详细信息，请参阅[设置事务隔离级别](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 中的事务](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [并发控制](../../../odbc/reference/develop-app/concurrency-control.md)
