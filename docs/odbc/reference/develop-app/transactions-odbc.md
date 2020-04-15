---
title: 交易 ODBC |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297952"
---
# <a name="transactions-odbc"></a>事务 ODBC
*事务*是作为单个原子操作完成的工作单元;也就是说，操作作为一个整体成功或失败。 例如，考虑将资金从一个银行帐户转移到另一个银行帐户。 这涉及两个步骤：从第一个账户提取资金，然后存入第二个账户。 这两个步骤都很重要;一步成功是不能接受的，另一个步骤是失败的。 支持事务的数据库能够保证这一点。  
  
 事务可以通过*提交*或*回滚*来完成。 提交事务时，该事务中所做的更改将永久化。 回滚事务时，受影响的行将返回到启动事务之前的状态。 要扩展帐户转移示例，应用程序将执行一个 SQL 语句来借记第一个帐户，另一个 SQL 语句贷记第二个帐户。 如果两个语句都成功，则应用程序随后将提交事务。 但是，如果任一语句由于任何原因失败，应用程序将回滚事务。 在这两种情况下，应用程序都保证事务结束时的状态一致。  
  
 单个事务可以包含在不同时间发生的多个数据库操作。 如果其他事务完全有权访问中间结果，则事务可能会相互干扰。 例如，假设一个事务插入一行，第二个事务读取该行，第一个事务回滚。 第二个事务现在具有不存在的行的数据。  
  
 为了解决这个问题，有各种方案可以隔离事务彼此。 *事务隔离*通常通过锁定行实现，这排除了多个事务同时使用同一行。 在某些数据库中，锁定行也可能锁定其他行。  
  
 随着事务隔离的增加，*并发性降低，* 或者两个事务同时使用相同的数据的能力。 有关详细信息，请参阅[设置事务隔离级别](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 本部分包含以下主题。  
  
-   [ODBC 中的事务](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [并发控制](../../../odbc/reference/develop-app/concurrency-control.md)
