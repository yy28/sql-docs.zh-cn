---
title: 乐观并发 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa80ff3359e3bbbed9e28044cce7514006c40f10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446209"
---
# <a name="optimistic-concurrency"></a>乐观并发
*乐观并发*的乐观假设从派生其名称，将很少发生事务之间的冲突; 冲突说明已发生时其他事务更新或删除读取它的时间之间的数据行由当前事务和时间它更新或删除。 它正好相反*保守式并发*或锁定，在该应用程序开发人员认为此类冲突是司空见惯。  
  
 在乐观并发，行左解锁之前要更新或删除它。 此时，该行中重新读取并检查以查看它以来是否发生了更改上次读取。 如果行已更改，则更新或删除将失败，并且必须再次尝试。  
  
 若要确定是否已更改行，行的缓存版本检查其新版本。 此检查可基于行版本，如 SQL Server 或行中的每个列的值中的时间戳列。 许多 Dbms 不支持行版本。  
  
 可以由数据源或应用程序实现乐观并发。 在任一情况下，应用程序应使用较低的事务隔离级别 Read Committed; 例如使用更高的级别对使用乐观并发的可以获得提高的并行性求反。  
  
 如果数据源实现乐观并发，应用程序将设置为 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES sql_attr_concurrency 设置语句属性。 若要更新或删除的行，它执行定位的更新或删除语句或调用**SQLSetPos**如果驱动程序或数据源就像使用保守式并发; 返回 SQLSTATE 01001 （游标操作冲突）update 或 delete 由于冲突而失败。  
  
 如果应用程序本身实现乐观并发，它将 sql_attr_concurrency 设置语句属性设置为 SQL_CONCUR_READ_ONLY 来读取行。 如果它将比较行版本，但不知道在行版本列，则会调用**SQLSpecialColumns** SQL_ROWVER 选项以确定此列的名称。  
  
 应用程序更新或删除的行通过增加 SQL_CONCUR_LOCK （若要获取对行的写访问权限） 和执行并发**更新**或**删除**语句**其中**子句指定的版本或行的值必须在应用程序中读取它时。 如果行已更改自那时起，该语句将失败。 如果**其中**子句不唯一标识行，该语句还可能会更新或删除其他行; 行版本始终唯一地标识行，但行值唯一地标识行，仅当它们包含的主键。
