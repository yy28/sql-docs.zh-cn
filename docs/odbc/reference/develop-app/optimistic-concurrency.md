---
title: 开放式并发 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01076f3f9167af8b67153abf9f3458a63bed1bf3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="optimistic-concurrency"></a>开放式并发
*开放式并发*从开放式假设派生其名称，将很少发生事务之间的冲突; 冲突称为已发生另一个事务更新或删除读取它的时间之间的数据行时按当前事务和时间更新或删除。 它截然相反*保守式并发，*或锁定，在该应用程序开发人员认为此类冲突是司空见惯。  
  
 在乐观并发，行左解锁，直到时间来更新或删除它。 此时，行是重新读取和检查，以查看是否已更改其已上次读取后。 如果行已更改，则更新或删除将失败，并且必须重试。  
  
 若要确定是否已更改行，该行的缓存版本检查其新版本。 这种检查可以基于行版本，如 SQL Server 或行中的每个列的值中的时间戳列。 许多 Dbms 不支持行版本。  
  
 通过对数据源或应用程序，可以实现开放式并发。 在任一情况下，应用程序应使用较低的事务的隔离级别 Read Committed; 例如使用更高级别对使用乐观并发中获得的增加的并发求反。  
  
 如果数据源实现乐观并发，应用程序将设置到 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 语句属性。 若要更新或删除的行，它执行的定位的更新或删除语句或调用**SQLSetPos**就像使用保守式并发; 将驱动程序或数据源返回 SQLSTATE 01001 （游标操作冲突），如果更新或删除由于冲突而失败。  
  
 如果应用程序本身实现开放式并发，它将 SQL_ATTR_CONCURRENCY 语句属性设置为 SQL_CONCUR_READ_ONLY 要读取一行。 如果它将对行版本进行比较，并不知道在行版本列，则会调用**SQLSpecialColumns** SQL_ROWVER 选项，来确定此列的名称。  
  
 应用程序更新或删除的行通过增加到 SQL_CONCUR_LOCK （若要获取对行的写入访问权限） 和执行的并发**更新**或**删除**语句**其中**时该应用程序读取它具有指定的版本或值的行的子句。 如果行已更改自那时起，该语句将失败。 如果**其中**子句不唯一标识行，该语句可能还更新或删除其他行; 行版本始终唯一标识行，但行值唯一标识行，仅当它们包括为主键。
