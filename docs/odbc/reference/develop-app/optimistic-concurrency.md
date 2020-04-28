---
title: 开放式并发 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282479"
---
# <a name="optimistic-concurrency"></a>开放式并发
*乐观并发*从乐观假设中派生出其名称，这种情况很少发生事务之间的冲突;当另一个事务更新或删除了当前事务读取的数据行与更新或删除数据的时间之间存在冲突。 这与*悲观并发*或锁定相反，应用程序开发人员认为这种冲突是很常见的。  
  
 在乐观并发中，行被解除锁定，直到更新或删除行。 此时，将重新读取行并对其进行检查，以查看它自上次读取后是否已更改。 如果行已更改，则更新或删除将失败，并且必须重试。  
  
 若要确定某行是否已更改，则会对照缓存的行版本检查其新版本。 此检查可以基于行版本（如 SQL Server 中的 timestamp 列）或行中每列的值。 许多 Dbms 不支持行版本。  
  
 开放式并发可以通过数据源或应用程序实现。 在这两种情况下，应用程序应使用低事务隔离级别，如 "已提交读";使用较高的级别会使使用开放式并发获得的并发并发性更高。  
  
 如果数据源实现了开放式并发，则应用程序会将 SQL_ATTR_CONCURRENCY 语句特性设置为 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES。 若要更新或删除行，它将执行定位的 update 或 delete 语句，或调用**SQLSetPos** ，就像使用悲观并发一样;如果更新或删除由于冲突而失败，则驱动程序或数据源将返回 SQLSTATE 01001 （游标操作冲突）。  
  
 如果应用程序本身实现了开放式并发，则它会将 SQL_ATTR_CONCURRENCY 语句特性设置为 SQL_CONCUR_READ_ONLY 读取行。 如果它将比较行版本且不知道 "行版本" 列，则它会调用 SQL_ROWVER **SQLSpecialColumns**选项，以确定此列的名称。  
  
 应用程序通过将并发性提高到 SQL_CONCUR_LOCK （以获取对行的写入访问权限），并使用**WHERE**子句执行**UPDATE**或**DELETE**语句，该语句可指定该行在应用程序读取时所具有的版本或值。 如果行之后已更改，则该语句将失败。 如果**WHERE**子句不唯一地标识行，则该语句可能还会更新或删除其他行;行版本始终唯一标识行，但行值仅在包含主键的情况下唯一标识行。
