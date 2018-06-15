---
title: 并发类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b5970995d3b8f881b62556b0f12eac96d302760
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911852"
---
# <a name="concurrency-types"></a>并发类型
若要解决的游标中减少并发问题，ODBC 公开四种不同类型的游标并发：  
  
-   **只读**光标可以读取数据，但不能更新或删除数据。 这是默认的并发类型。 尽管 DBMS 可能会锁定行强制 Repeatable Read 和 Serializable 隔离级别，它可以使用读的锁定，而不是写入锁。 这将导致更高的并发，因为其他事务至少可以读取的数据。  
  
-   **锁定**光标使用锁定确保它能够更新或删除在结果集中的行所需的最低级别。 这通常导致非常低的并发级别，尤其是在使用 Repeatable Read 和 Serializable 的事务隔离级别中。  
  
-   **使用行版本的乐观并发访问和使用值的开放式并发**光标使用开放式并发： 它更新或删除行，仅当它们以来未更改了最后一个对其进行读取。 若要检测的更改，它将比较行版本或值。 就不能保证，光标将能够更新或删除行，但并发性比使用锁定时要高得多。 有关详细信息，请参阅以下部分：[开放式并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。  
  
 应用程序指定哪种类型的并发它想要将与 SQL_ATTR_CONCURRENCY 语句属性一起使用的光标。 若要确定支持哪些类型，它调用**SQLGetInfo** SQL_SCROLL_CONCURRENCY 选项。
