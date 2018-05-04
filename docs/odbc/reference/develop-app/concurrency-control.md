---
title: 并发控制 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d0a9065248139fe3d2e369062301b76b4839955
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="concurrency-control"></a>并发控制
*并发*是两个事务能够在同一时间，使用相同的数据和增加的事务隔离通常伴随并发减少。 这是因为事务隔离通常实现锁定的行，并且因为锁定更多的行，可以不会被锁定的行至少暂时阻止的情况下完成更少的事务。 尽管并发减少通常作为用来维护数据库完整性更高事务隔离级别权衡可接受，它可以获得交互式应用程序中的问题就成为与使用游标的高读/写活动。  
  
 例如，假设应用程序执行的 SQL 语句**选择\*从订单**。 它调用**SQLFetchScroll**滚动解决结果设置，并允许用户更新，删除或插入订单。 用户更新、 删除或插入订单后，应用程序提交事务。  
  
 事务的隔离级别是否 Repeatable Read，可能-具体取决于实现方式-锁定返回每个行**SQLFetchScroll**。 如果隔离级别，可序列化事务可能会锁定整个 Orders 表。 在任一情况下，事务释放其锁定，仅当提交或回滚。 因此，如果用户耗费大量时间读取订单和更新、 删除很少的时间或将它们插入，事务无法轻松地锁定大量行，使其不可用于其他用户。  
  
 这是问题，即使光标是只读的和应用程序允许用户读取唯一现有订单。 在这种情况下，应用程序提交事务，并在它调用时释放锁， **SQLCloseCursor** （在自动提交模式下） 或**SQLEndTran** （在手动提交模式下）。  
  
 本部分包含以下主题。  
  
-   [并发类型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)
