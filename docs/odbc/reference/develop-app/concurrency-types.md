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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12891d7ee674167157bcb02300d2e4181ef51734
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656447"
---
# <a name="concurrency-types"></a>并发类型
若要解决的游标中减少并发问题，ODBC 公开游标并发的四种不同的类型：  
  
-   **只读**游标可以读取数据但不能更新或删除数据。 这是默认并发类型。 尽管 DBMS 可能会锁定行，以强制执行可重复读和可序列化隔离级别，但它可以使用的读取的锁定，而不是写入锁。 这将导致更高的并发，因为其他事务可以至少读取数据。  
  
-   **锁定**游标使用的锁定确保它可以更新或删除行在结果集中所需的最低级别。 这通常导致非常低并发级别时，尤其是在 Repeatable Read 和 Serializable 事务隔离级别。  
  
-   **使用行版本的乐观并发访问和使用的值的开放式并发**游标使用乐观并发： 它会更新或删除行，仅当它们以来未更改在上一次读取。 若要检测的更改，它比较行版本或值。 则不能保证，光标将能够更新或删除行，但并发性比使用锁定时高得多。 有关详细信息，请参阅以下部分中，[乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。  
  
 应用程序指定哪种类型的并发它想要使用 sql_attr_concurrency 设置语句属性使用的光标。 若要确定支持哪些类型，它将调用**SQLGetInfo** SQL_SCROLL_CONCURRENCY 选项。
