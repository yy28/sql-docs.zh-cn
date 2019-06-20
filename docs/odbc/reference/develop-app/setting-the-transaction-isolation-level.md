---
title: 将事务隔离级别设置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b575f9e208b5a1b7fa03b170b74633da149c67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237878"
---
# <a name="setting-the-transaction-isolation-level"></a>设置事务隔离级别
若要设置事务隔离级别，应用程序，请使用 SQL_ATTR_TXN_ISOLATION 连接属性。 如果数据源不支持所请求的隔离级别，则驱动程序或数据源可以设置更高的级别。 若要确定哪些事务隔离级别的数据源支持和默认隔离级别是，应用程序调用**SQLGetInfo** SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 选项分别。  
  
 更高版本的事务隔离级别提供数据库数据的大多数完整性的保护。 可序列化事务都保证是不受其他事务的影响，因此保证维护数据库的完整性。  
  
 但是，更高版本的事务隔离级别可能导致性能下降，因为它增加了应用程序必须等待锁释放的数据的可能性。 应用程序可以指定较低级别的隔离，以提高性能，在以下情况下：  
  
-   当它可以保证其他任何事务存在，可能会影响应用程序的事务。 这种情况仅在有限的情况下，如小型公司中的某个人时维护 dBASE 文件包含一台计算机上的人员数据中发生，不会共享这些文件。  
  
-   当速度比准确性和任何错误很可能是小型更为重要。 例如，假设一家公司，使得许多小型销售和大单销售很少。 估计总销售额值中所有打开的事务可以安全地使用 Read Uncommitted 隔离级别。 尽管该事务将包含订单是得到打开或关闭，随后可以回滚，这些将通常相互抵消，事务会快得多，因为它不会阻止每次它遇到这种订单。  
  
 有关详细信息，请参阅[乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
