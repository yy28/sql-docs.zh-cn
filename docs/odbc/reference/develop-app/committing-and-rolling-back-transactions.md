---
title: 提交和回滚事务 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299107"
---
# <a name="committing-and-rolling-back-transactions"></a>提交和回滚事务
若要在手动提交模式下提交或回滚事务，应用程序将调用**SQLEndTran**。 支持事务的 Dbms 驱动程序通常通过执行**COMMIT**或**ROLLBACK**语句来实现此功能。 当连接处于自动提交模式时，驱动程序管理器不会调用**SQLEndTran** ;它只会返回 SQL_SUCCESS，即使应用程序尝试回滚事务。 由于不支持事务的 Dbms 的驱动程序始终处于自动提交模式，因此它们可以实现**SQLEndTran**来返回 SQL_SUCCESS，而无需执行任何操作。  
  
> [!NOTE]  
>  应用程序不应通过使用**SQLExecute**或**SQLExecDirect**执行**commit**或**ROLLBACK**语句来提交或回滚事务。 执行此操作的效果是不确定的。 可能的问题包括：驱动程序不再知道事务处于活动状态，并且这些语句对于不支持事务的数据源失败。 这些应用程序应改为调用**SQLEndTran** 。  
  
 如果某个应用程序将环境句柄传递到**SQLEndTran** ，但未通过连接句柄，则驱动程序管理器将在概念上为在环境中具有一个或多个活动连接的每个驱动程序调用**SQLEndTran**和环境句柄。 然后，该驱动程序在环境中的每个连接上提交事务。 不过，请注意，驱动程序和驱动程序管理器都不会对环境中的连接执行两阶段提交;这只是为环境中的所有连接同时调用**SQLEndTran**的编程便捷。  
  
 （*两阶段提交*通常用于提交分布于多个数据源的事务。 在其第一阶段中，数据源将被轮询，以确定它们是否可以提交事务的一部分。 在第二阶段中，事务实际上是在所有数据源上提交的。 如果在第一个阶段中，任何数据源都在无法提交事务的情况下进行回复，则不会发生第二阶段。）
