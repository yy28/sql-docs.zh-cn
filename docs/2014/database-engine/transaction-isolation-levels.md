---
title: 事务隔离级别内存优化表 |Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea34b8ad278447d9e9085d99acb8500d14d5e7a
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637786"
---
# <a name="transaction-isolation-levels-in-memory-optimized-tables"></a>内存优化表中的事务隔离级别

  访问内存优化表的事务支持以下隔离级别。  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 可以在本机编译存储过程的原子块中指定事务隔离级别。 有关详细信息，请参阅 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)。 在从解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 访问内存优化表时，可以使用表级提示指定隔离级别。  
  
 定义本机编译存储过程时必须指定事务隔离级别。 在从解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 中的用户事务访问内存优化表时，必须使用表级提示指定隔离级别。 有关详细信息，请参阅[包含内存优化表的事务隔离级别的准则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 自动提交事务对于内存优化表支持隔离级别 READ COMMITTED。 READ COMMITTED 在用户事务或原子块中无效。 显式或隐式用户事务不支持 READ COMMITTED。 具有自动提交事务的内存优化表支持隔离级别 READ_COMMITTED_SNAPSHOT，并且仅在查询未访问任何基于磁盘的表时才支持。 此外，在 SNAPSHOT 隔离级别下通过解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 启动的事务不能访问内存优化表。 在 REPEATABLE READ 或 SERIALIZABLE 隔离级别下使用解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 的事务必须使用 SNAPSHOT 隔离级别访问内存优化表。 有关此方案的详细信息，请参阅[跨容器事务](cross-container-transactions.md)。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的默认隔离级别为 READ COMMITTED。 在会话的隔离级别为 READ COMMITED（或更低级别）时，可以执行以下操作之一：  
  
-   显式使用更高的隔离级别来访问内存优化表（例如，WITH (SNAPSHOT)）。  
  
-   指定 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT` 设置选项，它将内存优化表的隔离级别设置为 SNAPSHOT（如同向每个内存优化表加入 WITH(SNAPSHOT) 提示）。 有关 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`的详细信息，请参阅[ALTER DATABASE SET &#40;选项 transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 或者，如果会话的隔离级别为 READ COMMITTED，则可以使用自动提交事务。  
  
 以解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 开头的 SNAPSHOT 事务无法访问内存优化表。  
  
 内存优化表所支持的事务隔离级别提供与基于磁盘的表相同的逻辑保证。 但用于提供隔离级别保证的机制有所不同。  
  
 对于基于磁盘的表，将使用锁定实现大多数隔离级别保证，从而防止因阻塞发生冲突。 对于内存优化表，将使用一种冲突检测机制来提供保证，从而无需使用锁。 基于磁盘的表的 SNAPSHOT 隔离属于例外情况。 该隔离与内存优化表的 SNAPSHOT 隔离类似，也通过冲突检测机制实现。  
  
 SNAPSHOT  
 此隔离级别指定：事务中任何语句所读取的数据都将是在该事务开始时便存在的数据的事务性一致版本。 事务只能识别在其开始之前提交的数据修改。 在当前事务中执行的语句将看不到在当前事务开始以后由其他事务所做的数据修改。 事务中的语句所获取的已提交数据快照对应于该数据在事务开始时的状态。  
  
 写操作（更新、插入和删除）始终与其他事务完全隔离。 因此，SNAPSHOT 事务中的写操作可能与其他事务的写操作发生冲突。 如果当前事务尝试更新或删除的行已由当前事务启动后提交的其他事务更新或删除，则当前事务会终止并显示以下错误消息。  
  
 错误 41302。 当前事务尝试更新的 X 表中的记录自此事务启动后已更新。 该事务已中止。  
  
 如果当前事务尝试插入的行所包含的主键值与在当前事务之前提交的其他事务所插入行的主键值相同，将会发生提交失败并显示以下错误消息。  
  
 错误41325。 因某个序列化读取验证失败，当前事务无法提交。  
  
 如果一个事务向该事务提交之前已删除的表写入数据，则该事务会终止并显示以下错误消息：  
  
 错误41305。 因某个可重复读取验证失败，当前事务无法提交。  
  
 REPEATABLE READ  
 此隔离级别包含由 SNAPSHOT 隔离级别提供的保证。 此外，REPEATABLE READ 还保证，对于由该事务读取的任何行，在该事务提交时，该行都不会由任何其他事务更改。 在事务结束之前，该事务中的每个读取操作都是可重复的。  
  
 如果当前事务读取的任何行已由在当前事务之前提交的其他事务更新，则提交会失败并显示以下错误消息。  
  
 错误41305。 因某个可重复读取验证失败，当前事务无法提交。  
  
 SERIALIZABLE  
 此隔离级别包含由 REPEATABLE READ 提供的保证。 在获取快照与事务结束之间不会出现任何虚拟行。 虚拟行与选择、更新或删除的筛选条件匹配。  
  
 事务执行时就好像不存在并发事务。 所有操作实际上发生在单个序列点（提交时间）。  
  
 如果违反了其中任何一个保证，则该事务无法提交并显示以下错误消息：  
  
 错误41325。 因某个序列化读取验证失败，当前事务无法提交。  
  
## <a name="see-also"></a>另请参阅  
 [了解内存优化表上的事务](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [具有内存优化表的事务隔离级别的准则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [内存优化表事务重试逻辑准则](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
