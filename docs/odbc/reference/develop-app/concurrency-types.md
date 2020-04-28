---
title: 并发类型 |Microsoft Docs
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
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299097"
---
# <a name="concurrency-types"></a>并发类型
为了解决在游标中降低并发性的问题，ODBC 公开了四种不同类型的游标并发：  
  
-   **只读**游标可以读取数据，但不能更新或删除数据。 这是默认的并发类型。 尽管 DBMS 可能会锁定行以强制执行可重复读取和可序列化隔离级别，但它可以使用读取锁而不是写入锁。 这会导致更高的并发性，因为其他事务至少可以读取数据。  
  
-   **锁定**游标使用所需的最低锁定级别，确保它可以更新或删除结果集中的行。 这通常会导致并发级别非常低，尤其是在可重复读取和可序列化事务隔离级别。  
  
-   **使用行版本的开放式并发和使用值的开放式并发**游标使用乐观并发：仅当行自上次读取后未发生更改时才更新或删除行。 为了检测更改，它会比较行版本或值。 不保证游标能够更新或删除行，但在使用锁定时，并发性要高得多。 有关详细信息，请参阅以下 "[开放式并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)" 一节。  
  
 应用程序指定它希望游标与 SQL_ATTR_CONCURRENCY 语句特性一起使用的并发类型。 若要确定受支持的类型，它将调用带有 SQL_SCROLL_CONCURRENCY 选项的**SQLGetInfo** 。
