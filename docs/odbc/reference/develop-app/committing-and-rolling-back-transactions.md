---
title: 提交和回滚的事务 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 194a90482946814995ca1963f7c8fc4bce48d223
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126360"
---
# <a name="committing-and-rolling-back-transactions"></a>提交和回滚事务
若要提交或回滚事务，在手动提交模式下，应用程序调用**SQLEndTran**。 通常支持事务的 Dbms 的驱动程序实现此函数通过执行**提交**或**回滚**语句。 驱动程序管理器不会调用**SQLEndTran**时连接处于自动提交模式; 它只是会返回 SQL_SUCCESS，即使应用程序将尝试回滚事务。 因为不支持事务的 Dbms 的驱动程序始终处于自动提交模式下，它们可以实现**SQLEndTran**返回 SQL_SUCCESS，而不执行任何操作或未完全实现。  
  
> [!NOTE]  
>  应用程序不应提交或回滚事务通过执行**提交**或**回滚**语句与**SQLExecute**或**SQLExecDirect**. 执行此操作的影响是未定义的。 可能存在的问题包括不再知道当事务处于活动状态的驱动程序和针对不支持事务的数据源失败这些语句。 这些应用程序应调用**SQLEndTran**相反。  
  
 如果应用程序通过环境句柄**SQLEndTran**但不是会从概念上讲，未通过连接句柄，驱动程序管理器调用**SQLEndTran**与每个驱动程序的环境句柄的在环境中有一个或多个活动连接。 然后，驱动程序提交在环境中每个连接上的事务。 但是，务必要意识到驱动程序和驱动程序管理器都不在环境中; 中的连接执行两阶段提交这是仅是编程方便同时调用**SQLEndTran**适用于在环境中的所有连接。  
  
 (A*两阶段提交*通常用来提交可分布在多个数据源的事务。 在其第一个阶段中，有关它们是否能够提交其包含在事务轮询数据源。 在第二个阶段中，实际提交事务上的所有数据源。 如果任何数据源响应的第一阶段中它们不能提交事务，第二个阶段不会发生。）
