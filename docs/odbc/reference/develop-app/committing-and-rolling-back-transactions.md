---
title: 提交和回滚的事务 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b828c7080737989c4bcefa99f18d715fe04eddc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="committing-and-rolling-back-transactions"></a>提交和回滚的事务
若要提交或回滚的事务在手动提交模式下，应用程序调用**SQLEndTran**。 通常支持事务的 Dbms 的驱动程序实现此函数通过执行**提交**或**回滚**语句。 驱动程序管理器不会调用**SQLEndTran**连接时在自动提交模式下; 它只需返回 SQL_SUCCESS，即使应用程序将尝试回滚事务。 因为不支持事务的 Dbms 的驱动程序始终处于自动提交模式下，它们可以实现**SQLEndTran**不执行任何操作就返回 SQL_SUCCESS 或根本未实现。  
  
> [!NOTE]  
>  应用程序不应提交或回滚的事务通过执行**提交**或**回滚**具有语句**SQLExecute**或**SQLExecDirect**. 执行此操作的效果是不确定的。 可能的问题包括不再知道事务处于活动状态时的驱动程序和针对不支持事务的数据源失败这些语句。 这些应用程序应调用**SQLEndTran**相反。  
  
 如果应用程序传递的环境句柄**SQLEndTran**但不是会无法通过连接句柄，驱动程序管理器从概念上讲调用**SQLEndTran**与每个驱动程序的环境句柄，在环境中具有一个或多个活动连接。 该驱动程序然后提交事务对在环境中的每个连接。 但是，务必要意识到该驱动程序和驱动程序管理器都不在环境中; 的连接执行两阶段提交这是只是为了同时调用的编程的方便**SQLEndTran**环境中的所有连接。  
  
 (A*两阶段提交*通常用来提交事务分布在多个数据源。 在其第一个阶段中，数据源会轮询有关它们是否能够提交其包含在事务中。 在第二个阶段中，实际提交事务对所有数据源。 如果任何数据源答复在第一阶段，它们无法提交事务，第二个阶段不会发生。）
