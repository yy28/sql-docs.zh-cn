---
title: 了解内存优化表上的事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4aaefdcd2739b2036703cdb7235fe56865ff1fed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064627"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>了解内存优化表的事务
  事务使用一种乐观多版本并发控制形式来访问内存优化表。 这意味着存在不同版本的数据。 每个事务都对自己的事务一致数据库版本进行操作（独立于其他并发运行的事务）。 此外，事务还在与其他并发事务不冲突的乐观假设下运行。 这样就无需使用锁，但需要系统检测冲突并终止冲突事务中的一个事务。 仅对于写/写事务和读/写事务会发生冲突。 如果存在写/写冲突，则终止一个写入事务。  
  
 内存优化表的并发控制与基于磁盘的表的并发控制在 READ_COMMITTED_SNAPSHOT 和 SNAPSHOT 事务隔离级别之间存在相似性。 (有关基于磁盘的表的详细信息，请参阅[数据库引擎中基于行版本控制的隔离级别](http://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx)。)  
  
## <a name="topics-in-this-section"></a>在本部分中的主题  
 本节说明了内存优化表中的事务，包含以下主题：  
  
-   [内存优化表事务隔离级别准则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [内存优化表事务重试逻辑准则](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [内存优化表中的事务](transactions-in-memory-optimized-tables.md)  
  
-   [事务隔离级别](transaction-isolation-levels.md)  
  
-   [跨容器事务](cross-container-transactions.md)  
  
 有关详细信息，请参阅[控制事务持续性](../relational-databases/logs/control-transaction-durability.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存优化表](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
