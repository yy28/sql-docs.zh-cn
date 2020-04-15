---
title: 提交和回滚事务 |微软文档
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
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299107"
---
# <a name="committing-and-rolling-back-transactions"></a>提交和回滚事务
要在手动提交模式下提交或回滚事务，应用程序将调用**SQLEndTran**。 支持事务的 DBMS 的驱动程序通常通过执行**COMMIT**或**ROLLBACK**语句来实现此函数。 当连接处于自动提交模式时，驱动程序管理器不调用 SQLEndTran;但是，驱动程序管理器不会调用**SQLEndTran。** 它只是返回SQL_SUCCESS，即使应用程序尝试回滚事务。 由于不支持事务的 DBMS 的驱动程序始终处于自动提交模式，因此它们可以实现**SQLEndTran**返回SQL_SUCCESS而不执行任何操作或根本不实现它。  
  
> [!NOTE]  
>  应用程序不应通过使用 SQLExecute 或**SQLExecDirect**执行**COMMIT**或**SQLExecDirect****ROLLBACK**语句来提交或回滚事务。 执行此操作的效果未定义。 可能的问题包括驱动程序不再知道事务何时处于活动状态，以及这些语句对不支持事务的数据源失败。 这些应用程序应调用**SQLEndTran。**  
  
 如果应用程序将环境句柄传递给**SQLEndTran，** 但不传递连接句柄，则驱动程序管理器在概念上调用**SQLEndTran，** 并针对环境中具有一个或多个活动连接的每个驱动程序调用环境句柄。 然后，驱动程序在环境中的每个连接上提交事务。 但是，请务必认识到，驱动程序和驱动程序管理器都不会对环境中的连接执行两阶段提交;因此，驾驶员经理对环境中的连接执行两阶段提交。这只是同时调用**SQLEndTran**环境中所有连接的编程便利。  
  
 （*两阶段提交*通常用于提交分布在多个数据源的事务。 在第一阶段，将轮询数据源，以决定是否可以提交其部分事务。 在第二阶段，事务实际上是在所有数据源上提交的。 如果第一阶段的任何数据源答复它们无法提交事务，则第二阶段不会发生。
