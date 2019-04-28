---
title: 内存优化表中的事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2cd07d26-a1f1-4034-8d6f-f196eed1b763
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc72eeeb154749b0e889b495fab79bb8bf86db10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843092"
---
# <a name="transactions-in-memory-optimized-tables"></a>内存优化表中的事务
  基于磁盘的表的行版本控制（使用 SNAPSHOT 隔离或 READ_COMMITTED_SNAPSHOT）提供了一种乐观并发控制形式。 读取器和编写器不会相互阻止。 对于内存优化表，编写器不会阻止编写器。 使用基于磁盘的表的行版本控制时，一个事务会锁定行，而尝试更新行的并发事务会被阻塞。 对于内存优化表则没有锁定。 如果两个事务尝试更新同一行，则会发生写/写冲突（错误 41302）。  
  
 与基于磁盘的表不同内存优化表允许使用更高隔离级别，REPEATABLE READ 和 SERIALIZABLE 乐观并发控制。 不会使用锁来强制实现隔离级别。 而是在事务验证结束时使用锁，以确保可重复读或可序列化假定。 如果违反了假定，则事务将会终止。 有关详细信息，请参阅 [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md)。  
  
 内存优化表的重要事务语义包括：  
  
-   多版本控制  
  
-   基于快照的事务隔离  
  
-   乐观  
  
-   冲突检测  
  
 以下各部分说明了每个语义。  
  
## <a name="multi-versioning-in-memory-optimized-tables"></a>内存优化表中的多版本控制  
 内存优化表中的行可具有不同版本。 并发事务可以访问同一行的不同版本。  
  
 内存优化表数据基于版本。 对于任何行，可能具有在不同时间点有效的不同行版本。 当 READ_COMMITTED_SNAPSHOT 或 ALLOW_SNAPSHOT_ISOLATION 设置为 ON 时，基于磁盘的表会保留不同的行版本。 内存优化表会保留不同的行版本，即使 READ_COMMITTED_SNAPSHOT 和 ALLOW_SNAPSHOT_ISOLATION 设置为 OFF 时也是如此。 内存优化表的行版本不保持在 tempdb 中。 而行版本以内联方式作为在内存中存储行的内存优化数据结构的一部分来保留。  
  
## <a name="snapshot-based-transaction-isolation-for-memory-optimized-tables"></a>内存优化表的基于快照的事务隔离  
 单个事务中的所有操作都使用内存优化表的相同事务一致快照。 内存优化表的所有事务隔离都基于快照的事务隔离。 例如，使用可序列化隔离级别来访问内存优化表的事务将对同一个事务一致快照执行所有操作。  
  
 访问内存优化表的事务使用此行版本控制来获取表中行的事务一致快照。 事务中由任何语句读取的数据是在该事务启动时就存在的事务一致版本数据。 因此，并发运行的事务所进行的任何修改都对当前事务中的语句不可见。  
  
## <a name="optimistic-concurrency-control-for-memory-optimized-tables"></a>内存优化表的乐观并发控制  
 冲突和失败很少出现，并且有关内存优化表的事务会假定与同时发生的事务间不存在冲突且操作成功。 事务不会对内存优化表使用锁和闩锁，以保证事务隔离。 编写器不会阻止读取器。 编写器不会阻止编写器。 相反，事务将在与其他事务不存在冲突的（乐观）假定下继续。 不使用锁和闩锁，也无需等待其他事务完成对相同行的处理，因此能提高性能。  
  
 此外，如果某一事务 (TxA) 读取处于提交过程中的其他事务 (TxB) 已插入或修改的行，则该事务会乐观地假设其他事务将提交而不等待提交发生。 在此情况下，事务 TxA 将对事务 TxB 具有提交依赖关系。  
  
## <a name="conflict-detection-validation-and-commit-dependency-checks"></a>冲突检测、验证和提交依赖关系检查  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 检测并发事务之间的冲突以及隔离级别冲突，并终止冲突事务中的一个事务。 此事务将需要重试。 (有关详细信息，请参阅[内存优化表上的事务的重试逻辑准则](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。)  
  
 系统乐观地假定不存在冲突并且未违反事务隔离。 如果发生可能在数据库中导致不一致或可能违反事务隔离的任何冲突，则会检测到这些冲突，并且事务终止。  
  
 如果检测到冲突，则会终止事务，并且客户端需要重试。  
  
 下表总结了与访问内存优化表的事务相关的错误情况。  
  
### <a name="error-conditions-for-transactions-accessing-memory-optimized-tables"></a>访问内存优化表的事务的错误情况。  
  
|错误|应用场景|  
|-----------|--------------|  
|写冲突。 尝试更新自该事务启动以来已更新的记录。|对由并发事务更新或删除的行执行 UPDATE 或 DELETE 操作。|  
|可重复读验证失败。|由事务读取的行自该事务启动以来已更改（更新或删除）。 可重复读验证通常在使用 REPEATABLE READ 和 SERIALIZABLE 事务隔离级别时进行。|  
|可序列化验证失败。|新的（虚拟）行自事务启动以来已插入到该事务中的一个扫描范围内。 如果行在事务启动之前已提交给数据库，则该行应该对该事务可见。 SERIALIZABLE 验证通常在使用 SERIALIZABLE 隔离并验证 PRIMARY KEY 约束时进行。|  
|提交依赖关系失败。|该事务依赖于其他事务，而后者由于此表中的一个失败、内存不足的情况或由于未能提交到事务日志而未能提交。 读/写事务和只读事务可能会发生此失败。|  
  
### <a name="transaction-lifetime"></a>事务生存期  
 上表中提及的失败可能会在事务的不同时间点发生。 下图说明了访问内存优化表的事务的各个阶段。  
  
 ![事务的生存期。](../../2014/database-engine/media/hekaton-transactions.gif "的事务的生存期。")  
访问内存优化表的事务的生存期。  
  
#### <a name="regular-processing"></a>常规处理  
 在此阶段中，将会执行用户发出的 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。 从表读取行，然后将新行版本写入数据库。 该事务与所有其他并发事务隔离。 该事务使用自该事务启动以来存在的内存优化表的快照。  
  
 在事务的此阶段对表进行的写入对其他事务尚不可见，不过有一个例外：行更新和删除对其他事务中的更新和删除操作可见，以便检测写冲突。  
  
 如果删除或更新操作发现自该事务逻辑启动以来已更新或删除一行，则操作会失败，并显示错误为 41302。 错误 41302 的消息为“当前事务尝试更新的 X 表中的记录自此事务启动后已更新。 该事务已中止。”  
  
 此错误会终止事务（即使 XACT_ABORT 为 OFF 也是如此），这意味着事务将在用户会话结束时回滚。 失败的事务无法提交，仅支持不写入日志和不访问内存优化表的读取操作。  
  
#####  <a name="cd"></a> 提交依赖关系  
 在常规处理过程中，事务可以读取由其他事务写入并处于验证或提交阶段、但尚未提交的行。 这些行是可见的，因为在验证阶段开始时已分配事务的逻辑结束时间。  
  
 如果事务读取这类未提交的行，则会对该事务形成提交依赖关系。 这具有两种主要含义：  
  
-   事务在所依赖的事务提交之前无法提交。 换言之，在所有依赖关系都已清除之前，该事务无法进入提交阶段。  
  
-   此外，在所有依赖关系都已清除之前，结果集不会返回给客户端。 这会防止客户端观察未提交的数据。  
  
 如果任何依赖的事务无法提交，则会发生提交依赖关系失败。 这意味着该事务无法提交，并显示错误 41301（“当前事务与其存在依赖关系的以前的事务已中止，并且当前事务不再提交。”）。  
  
#### <a name="validation-phase"></a>验证阶段  
 在验证阶段，系统会验证请求的事务隔离级别所需的假定在该事务的逻辑开始和逻辑结束时间之间是否为 true。  
  
 在验证阶段开始时，将向事务分配逻辑结束时间。 写入数据库的行版本会在此逻辑结束时对其他事务可见。 有关详细信息，请参阅[提交依赖关系](#cd)。  
  
##### <a name="repeatable-read-validation"></a>可重复读验证  
 如果该事务的隔离级别为 REPEATABLE READ 或 SERIALIZABLE，或者在 REPEATABLE READ 或 SERIALIZABLE 隔离下访问表 (详细信息，请参阅部分中的单个操作的隔离中[事务隔离级别](../../2014/database-engine/transaction-isolation-levels.md))，则系统会验证读取是否可重复。 这意味着它会验证由事务读取的行的版本在事务逻辑结束时是否仍是有效行版本。  
  
 如果任何行已更新或更改，则事务无法提交，并显示错误 41305（“由于可重复读验证失败，当前事务无法提交。”）。  
  
 如果表在插入、更新或删除之后以及事务提交之前被删除，则也可能会发生此错误。 这仅适用于本机编译存储过程中的插入、更新或删除操作。 通过解释的 [!INCLUDE[tsql](../includes/tsql-md.md)] 执行的这类写操作会导致 DROP TABLE 语句阻塞并等待事务提交。  
  
##### <a name="serializable-validation"></a>可序列化验证  
 将在两种情况下执行可序列化验证：  
  
-   如果事务的隔离级别为 SERIALIZABLE，或者在 SERIALIZABLE 隔离下对表进行访问。  
  
-   如果使用唯一索引（例如，为 PRIMARY KEY 约束创建的索引）来插入行。 系统会验证没有并发插入具有相同键的行。  
  
 系统会验证没有将虚拟行写入数据库。 将对由事务执行的读操作进行评估，以确定没有在这些读操作的扫描范围内插入新行。  
  
 使用唯一索引插入键包括一个隐式读操作，用于确定没有与该键重复的键。 唯一索引的可序列化验证可确保这些索引不能重复，以免两个事务并发插入相同的键。  
  
 如果检测到虚拟行，则事务无法提交，并显示错误 41325（“由于可序列化验证失败，当前事务无法提交。”）。  
  
#### <a name="commit-processing"></a>提交处理  
 如果验证成功且所有事务依赖关系都已清除，则该事务会进入提交处理阶段。 在此阶段中，对持久表的更改会写入日志，随后日志会写入磁盘以确保持续性。 事务的日志记录写入磁盘，控件后返回到客户端。  
  
 将清除此事务的所有提交依赖关系，并且等待此事务提交的所有事务都可以继续。  
  
## <a name="limitations"></a>限制  
  
-   内存优化表不支持跨数据库事务。 访问内存优化表的每个事务都无法访问多个数据库（对 tempdb 进行的读/写访问以及对系统主数据库进行的只读访问除外）。  
  
-   内存优化表不支持分布式事务。 以 BEGIN DISTRIBUTED TRANSACTION 开头的分布式事务无法访问内存优化表。  
  
-   内存优化表不支持锁定。 内存优化表不支持通过锁提示（如 TABLOCK、XLOCK、ROWLOCK）实现的显式锁。  
  
## <a name="see-also"></a>请参阅  
 [了解内存优化表的事务](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
  
