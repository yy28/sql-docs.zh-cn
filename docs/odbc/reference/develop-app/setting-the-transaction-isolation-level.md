---
title: "将事务隔离级别设置 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d91c7789fbcd0c4dc197f2da13b23c1da34666bb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-transaction-isolation-level"></a>将事务隔离级别设置
若要设置的事务隔离级别，应用程序，请使用 SQL_ATTR_TXN_ISOLATION 连接属性。 如果数据源不支持所请求的隔离级别，该驱动程序或数据源可以设置更高的级别。 若要确定哪些事务隔离级别的数据源支持和默认隔离级别是，应用程序调用**SQLGetInfo**使用 SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 选项，分别。  
  
 更高的事务隔离级别提供完整性的数据库数据的大多数保护。 可序列化事务都保证不会影响由其他事务，因此保证维护数据库的完整性。  
  
 但是，因为它会增加应用程序将需要等待数据要释放的锁的可能性更高的事务隔离级别可以会导致性能降低。 应用程序可以指定较低级别的隔离，以提高性能，在以下情况：  
  
-   当它可以保证其他任何事务存在，可能会妨碍应用程序的事务。 这种情况仅在有限的情况下，例如当小公司中的某个人维护 dBASE 文件包含一台计算机上的人员数据中发生，并且不共享这些文件。  
  
-   当速度比准确性和任何错误更重要的可能性很小。 例如，假设，公司可以使许多小型销售和大型销售很少。 估计总销售额值中所有打开的事务可能会安全地使用 Read Uncommitted 隔离级别。 尽管事务将包含订单是正在打开或关闭，随后可以回滚，这些将通常相互抵消和事务会快得多，因为它不会阻止每次它遇到此类订单。  
  
 有关详细信息，请参阅[开放式并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。

