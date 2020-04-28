---
title: 设置事务隔离级别 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299807"
---
# <a name="setting-the-transaction-isolation-level"></a>设置事务隔离级别
若要设置事务隔离级别，应用程序需要使用 SQL_ATTR_TXN_ISOLATION 连接属性。 如果数据源不支持所请求的隔离级别，则驱动程序或数据源可以设置更高的级别。 若要确定数据源所支持的事务隔离级别以及默认隔离级别，应用程序需要分别使用 SQL_TXN_ISOLATION_OPTION 和 SQL_DEFAULT_TXN_ISOLATION 选项来调用**SQLGetInfo** 。  
  
 较高的事务隔离级别为数据库数据的完整性提供了最大程度的保护。 可序列化事务不受其他事务影响，因此保证保持数据库的完整性。  
  
 但是，较高的事务隔离级别可能会导致性能降低，因为这会增加应用程序需要等待数据锁定的几率。 在以下情况下，应用程序可以指定较低的隔离级别来提高性能：  
  
-   可以确保不存在可能干扰应用程序事务的其他事务。 仅在有限的情况下才会发生这种情况，例如，小型公司中的一个人在一台计算机上维护包含人事数据的 dBASE 文件，而不共享这些文件。  
  
-   当速度比准确性更重要时，任何错误都可能会很小。 例如，假设某家公司的销售规模很小，但这种情况很少发生。 估算所有开放式销售的总值的事务可能会安全地使用未提交读隔离级别。 尽管该事务包括正在打开或关闭的订单，并随后将其回滚，但这些订单通常会彼此取消，并且事务的速度将更快，因为每次遇到此类订单时，该事务不会被阻止。  
  
 有关详细信息，请参阅[乐观并发](../../../odbc/reference/develop-app/optimistic-concurrency.md)。
