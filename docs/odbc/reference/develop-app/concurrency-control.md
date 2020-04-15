---
title: 并发控制 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294847"
---
# <a name="concurrency-control"></a>并发控制
*并发*性是两个事务同时使用相同的数据的能力，随着事务隔离的增加，并发性通常会减少。 这是因为事务隔离通常是通过锁定行实现的，并且随着锁定的行数增加，可以完成较少的事务，而不会至少被锁定的行临时阻止。 虽然减少并发性通常被认为是对维护数据库完整性所需的更高事务隔离级别的权衡，但在具有使用游标的高读/写活动的交互式应用程序中，它可能成为一个问题。  
  
 例如，假设应用程序执行 SQL 语句 **"从订单\*中选择**"。 它调用**SQLFetchScroll**滚动结果集，并允许用户更新、删除或插入订单。 用户更新、删除或插入订单后，应用程序将提交事务。  
  
 如果隔离级别是可重复读取，则事务可能会（取决于实现方式）锁定**SQLFetchScroll**返回的每一行。 如果隔离级别是可序列化的，则事务可能会锁定整个订单表。 在这两种情况下，事务仅在提交或回滚时释放其锁。 因此，如果用户花费大量时间阅读订单，而更新、删除或插入订单的时间很少，则事务可以轻松地锁定大量行，从而使其他用户无法访问这些行。  
  
 这是一个问题，即使游标是只读的，并且应用程序允许用户只读取现有订单。 在这种情况下，应用程序在调用**SQLCloseCursor（** 在自动提交模式下）或**SQLEndTran（** 在手动提交模式下）时提交事务并释放锁。  
  
 本部分包含以下主题。  
  
-   [并发类型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [开放式并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)
