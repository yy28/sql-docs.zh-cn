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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297952"
---
# <a name="transactions-odbc"></a>事务 ODBC
*事务*是作为单个原子操作完成的工作单元;也就是说，该操作将作为一个整体成功或失败。 例如，考虑将资金从一个银行帐户转移到另一个银行帐户。 这涉及两个步骤：从第一个帐户取出钱，并将其放在第二个帐户中。 这两个步骤都成功，这一点很重要。一个步骤成功，另一个步骤失败是不可接受的。 支持事务的数据库能够保证这一点。  
  
 可以通过*提交*或*回滚*事务来完成事务。 提交事务后，在该事务中所做的更改将成为永久更改。 回滚事务后，受影响的行将返回到事务开始之前所处的状态。 若要扩展帐户传输示例，应用程序需要执行一条 SQL 语句来借此使用第一个帐户和不同的 SQL 语句来贷记第二个帐户。 如果这两个语句都成功，应用程序会提交事务。 但是，如果任一语句由于任何原因而失败，则应用程序会回滚事务。 在任一情况下，应用程序在事务结束时保证一致的状态。  
  
 单个事务可包含在不同时间发生的多个数据库操作。 如果其他事务对中间结果具有完全访问权限，这些事务可能会相互干扰。 例如，假设一个事务插入一行，另一个事务读取该行，第一个事务被回滚。 第二个事务现在包含了不存在的行的数据。  
  
 若要解决此问题，可以使用多种不同的方案将事务相互隔离。 *事务隔离*通常是通过锁定行来实现的，这会阻止多个事务同时使用同一个行。 在某些数据库中，锁定行还可能会锁定其他行。  
  
 增加事务隔离会降低*并发性，* 或者两个事务同时使用相同数据的能力。 有关详细信息，请参阅[设置事务隔离级别](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 中的事务](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [并发控制](../../../odbc/reference/develop-app/concurrency-control.md)
