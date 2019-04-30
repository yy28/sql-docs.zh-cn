---
title: 并发控制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e54298e9c25777f10b92f322f1b1e6a3d94c243
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191758"
---
# <a name="concurrency-control"></a>并发控制
*并发*是两个事务能够一次使用相同的数据和与增加的交易隔离通常并发减少。 这是因为由锁定行，通常实现事务隔离，因为锁定了更多的行，可以不会被锁定的行至少暂时阻止的情况下完成较少的事务。 并发减少通常被认为有必要维护数据库的完整性更高事务隔离级别的权衡，尽管它可以与使用游标的高读/写活动成为交互式应用程序中的问题。  
  
 例如，假设应用程序执行 SQL 语句**选择\*从订单**。 它将调用**SQLFetchScroll**滚动结果集和允许用户更新，请删除或插入订单。 用户更新、 删除或插入订单后，应用程序提交事务。  
  
 如果隔离级别为 Repeatable Read，-具体取决于实现方式的事务可能会锁定返回的每一行**SQLFetchScroll**。 如果隔离级别为 Serializable，事务可能会锁定整个 Orders 表。 在任一情况下，事务仅当提交或回滚时，才释放其锁定。 因此如果花了很多时间读取订单和很短的时间更新、 删除或将它们插入，事务可以轻松地锁定大量行，使其不可用于其他用户。  
  
 即使游标是只读的并在应用程序允许用户读取唯一现有订单，这是一个问题。 在这种情况下，应用程序提交事务，并释放锁，当它调用**SQLCloseCursor** （在自动提交模式下） 或**SQLEndTran** （在手动提交模式下）。  
  
 本部分包含以下主题。  
  
-   [并发类型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)
