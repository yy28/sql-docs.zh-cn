---
title: 乐观同一性 |微软文档
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
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282479"
---
# <a name="optimistic-concurrency"></a>开放式并发
*乐观并发*源于一种乐观的假设，即事务之间的冲突很少发生;当另一个事务更新或删除当前事务读取的时间与更新或删除数据的时间之间的一行数据时，即发生冲突。 它与*悲观并发*性或锁定相反，其中应用程序开发人员认为此类冲突司空见惯。  
  
 在乐观并发中，行保持解锁，直到更新或删除它的时间。 此时，将重新读取并检查该行，以查看自上次读取以来是否更改了该行。 如果行已更改，更新或删除将失败，必须重试。  
  
 要确定行是否已更改，则会对照该行的缓存版本检查其新版本。 此检查可以基于行版本，例如 SQL Server 中的时间戳列或行中每列的值。 许多 DBMS 不支持行版本。  
  
 乐观并发可以由数据源或应用程序实现。 在这两种情况下，应用程序都应使用低事务隔离级别，如"读取已提交";在任种情况下，应用程序都应使用"已提交"这样的低事务隔离级别。使用较高的水平否定了使用乐观并发获得的增加并发。  
  
 如果乐观并发由数据源实现，则应用程序将SQL_ATTR_CONCURRENCY语句属性设置为SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 要更新或删除行，它执行定位的更新或删除语句或调用**SQLSetPos，** 就像使用悲观并发一样;如果更新或删除由于冲突而失败，驱动程序或数据源将返回 SQLSTATE 01001（Cursor 操作冲突）。  
  
 如果应用程序本身实现乐观并发，它将SQL_ATTR_CONCURRENCY语句属性设置到SQL_CONCUR_READ_ONLY读取行。 如果它将比较行版本，但不知道行版本列，它将使用SQL_ROWVER选项调用**SQLSpecialColumn**以确定此列的名称。  
  
 应用程序通过增加与SQL_CONCUR_LOCK并发（获取对行的写入访问权限）以及使用**WHERE**子句执行**更新**或**DELETE**语句来更新或删除该行，该语句指定该行读取该行时的版本或值。 如果此后该行已更改，则语句将失败。 如果**WHERE**子句不唯一标识该行，则 语句也可能更新或删除其他行;否则，该语句也可能更新或删除其他行。行版本始终唯一标识行，但行值仅在包含主键时才唯一标识行。
