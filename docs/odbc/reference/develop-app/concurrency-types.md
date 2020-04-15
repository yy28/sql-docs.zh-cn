---
title: 并发类型 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299097"
---
# <a name="concurrency-types"></a>并发类型
为了解决游标中并发性降低的问题，ODBC 公开了四种不同类型的游标并发：  
  
-   **只读**游标可以读取数据，但不能更新或删除数据。 这是默认并发类型。 尽管 DBMS 可能会锁定行以强制实施可重复读取和可序列化隔离级别，但它可以使用读取锁而不是写入锁。 这将导致更高的并发性，因为其他事务至少可以读取数据。  
  
-   **锁定**游标使用所需的最低锁定级别，以确保它可以更新或删除结果集中的行。 这通常会导致非常低的并发级别，尤其是在可重复读取和可序列化事务隔离级别。  
  
-   **使用行版本进行乐观并发，并使用值进行乐观并发**游标使用乐观并发：它仅在行自上次读取以来未更改时更新或删除行。 为了检测更改，它会比较行版本或值。 不能保证游标能够更新或删除行，但并发性远远高于使用锁定时。 有关详细信息，请参阅以下部分"[乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)"。  
  
 应用程序指定希望游标与SQL_ATTR_CONCURRENCY语句属性一起使用的并发类型。 要确定支持哪些类型，它使用SQL_SCROLL_CONCURRENCY选项调用**SQLGetInfo。**
