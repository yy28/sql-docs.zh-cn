---
title: 设置事务隔离级别 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299807"
---
# <a name="setting-the-transaction-isolation-level"></a>设置事务隔离级别
要设置事务隔离级别，应用程序使用SQL_ATTR_TXN_ISOLATION连接属性。 如果数据源不支持请求的隔离级别，驱动程序或数据源可以设置更高的级别。 要确定数据源支持哪些事务隔离级别以及默认隔离级别是什么，应用程序分别使用SQL_TXN_ISOLATION_OPTION和SQL_DEFAULT_TXN_ISOLATION选项调用**SQLGetInfo。**  
  
 较高的事务隔离级别为数据库数据的完整性提供了最大的保护。 可序列化事务保证不受其他事务的影响，因此保证保持数据库完整性。  
  
 但是，较高的事务隔离级别可能会导致性能降低，因为它会增加应用程序必须等待数据释放锁的可能性。 在以下情况下，应用程序可以指定较低的隔离级别以提高性能：  
  
-   当可以保证不存在可能干扰应用程序事务的其他事务时。 这种情况仅在有限的情况下发生，例如，当一个小公司中的一个人维护 dBASE 文件，这些文件在一台计算机上包含人员数据，并且不共享这些文件时。  
  
-   当速度比精度更重要，并且任何错误都可能很小时。 例如，假设一家公司销售很少，而且销售量大是罕见的。 估计所有未结销售总价值的事务可能安全地使用未提交的读取隔离级别。 尽管事务将包括正在打开或关闭并随后回滚的订单，但通常这些订单会相互取消，并且事务会更快，因为它不会每次遇到此类订单时被阻止。  
  
 有关详细信息，请参阅[乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
