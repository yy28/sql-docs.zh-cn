---
title: 交叉容器事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290aff0bfcb01e098ae87b48cf582cdf999314c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807421"
---
# <a name="cross-container-transactions"></a>交叉容器事务
  交叉容器事务是隐式或显式用户事务，这些事务包含对本机编译存储过程的调用或对内存优化表的操作。  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，对存储过程的调用不会启动事务。 在自动提交模式下执行本机编译过程（不在用户事务的上下文中）不被视为交叉容器事务。  
  
 引用内存优化表的任何解释型查询都被视为交叉容器事务的一部分，而无论是从显式或隐式事务中执行，还是在自动提交模式下执行。  
  
##  <a name="isolation"></a> 单个操作的隔离  
 每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 事务都有一个隔离级别。 默认隔离级别为 Read Committed。 若要使用不同的隔离级别，可以设置隔离级别使用[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。  
  
 内存优化表和基于磁盘的表上的操作常常需要采用不同的隔离级别执行。 在事务中，可为一组语句或单个读取操作设置不同的隔离级别。  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>指定单个操作的隔离级别  
 若要为事务中的一组语句设置不同的隔离级别，可以使用 `SET TRANSACTION ISOLATION LEVEL`。 下面的事务示例使用可序列化隔离级别作为默认级别。 对 t3、t2 和 t1 的插入和选择操作在“可重复读”隔离级别下执行。  
  
```sql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 若要为各个读取操作分别设置不同于事务默认级别的隔离级别，可以使用表提示（例如，可序列化）。 每个选择操作对应于一个读取操作，每个更新操作和每个删除操作对应于一个读取操作，因为始终需要先读取行才能进行更新或删除。 插入操作没有隔离级别，因为在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中始终要隔离写操作。 在下面的示例中，事务的默认隔离级别是“已提交读”，但在可序列化隔离级别下访问表 t1，在快照隔离级别下访问表 t2。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>单个操作的隔离语义  
 可序列化事务 T 在完全隔离下执行。 此事务执行时，就好像其他每个事务要么都在 T 启动之前提交，要么都在 T 提交之后启动。 当一个事务中的不同操作具有不同隔离级别时，情况会变得更加复杂。  
  
 中的事务隔离级别的常规语义[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以及锁定的含义，详见[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。  
  
 对于不同操作可能具有不同隔离级别的交叉容器事务，您需要理解各个读取操作的隔离语义。 将始终对写操作进行隔离。 不同事务中的写操作不能相互影响。  
  
 数据读取操作返回很多符合筛选条件的行。  
  
 读取来执行读取操作的事务 t。 隔离级别的一部分可以理解的  
  
 提交状态  
 提交状态指数据读取是否能够提交。  
  
 （事务）一致性  
 一组读取操作的事务一致性是指行版本读取是否都能保证包括来自完全相同的一组事务的更新。  
  
 系统提供给事务 T 的有关数据读取的稳定性保证。  
 稳定性是指事务的读取是否可重复。 也就是，重复读取操作是否始终返回相同的行和行版本？  
  
 特定保证是指事务的逻辑结束时间。 一般情况下，逻辑结束时间是将事务提交到数据库的时间。 如果事务访问内存优化表，则从技术上看，逻辑结束时间就是验证阶段的开始时间。 (有关详细信息，请参阅中的事务生存期讨论[内存优化表中的事务](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 无论隔离级别如何，事务 (T) 始终能看到自身的更新：  
  
 READ UNCOMMITTED  
 数据读取可能未提交、不一致或不稳定。 不过，它将包含由 T 执行的更早的写操作。  
  
 READ COMMITTED  
 将提交数据读取。  
  
 SNAPSHOT  
 由 T 在快照隔离下执行的所有读取操作都具有相同的逻辑读取时间，即事务开始的时间。 从该逻辑读取时间起，可以保证数据读取得到提交并保持一致。 从原始读取时间起，重复执行的读取操作可以保证返回相同的结果。  
  
 REPEATABLE READ  
 到事务的逻辑结束时间，可以保证数据读取得到提交并保持稳定。  
  
 SERIALIZABLE  
 可重复读加上避免虚拟及事务一致性保证所有可序列化的读取操作由 t。 虚拟避免意味着扫描操作只能返回由 T，写入的其他行执行的所有保证，但没有已由其他事务写入的行。  
  
 请考虑以下事务：  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 此事务在“已提交读”隔离级别下删除 t3 的所有行，在可序列化隔离级别下将所有行从 t1 复制到 t3，然后将 t1 和 t3 进行比较。 t3 表在清空后可能添加了一些行 [不在 t1 中]。 由于 t1 副本是可序列化的，因此该表中没有添加任何行。  
  
 虽然在事务结束时从 t1 读取在语法上属于“已提交读”隔离级别，但在效果上是可序列化隔离级别，原因是事务中之前在可序列化隔离下执行过相同的读操作：可序列化性保证随后在事务中任何较晚时刻执行读操作都会返回相同的行。  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>交叉容器事务和隔离级别  
 可将交叉容器事务视为具有两个方面：基于磁盘的方面（对于基于磁盘的表的操作）和内存优化的方面（对于内存优化的表的操作）。 这两方面可以有不同的隔离级别。 实际上，每个方面的各个读取操作可以分别有不同的隔离级别。  
  
 给定事务 T 的基于磁盘的方面在满足以下条件之一的情况下达到特定隔离级别 X：  
  
-   它在 X 中启动。也就是说，会话的默认级别为 X，或者因为您执行`SET TRANSACTION ISOLATION LEVEL`，或者它是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]默认值。  
  
-   在该事务执行期间，默认隔离级别通过 `SET TRANSACTION ISOLATION LEVEL` 更改为 X。  
  
-   对基于磁盘的表的读取操作通过语法 `WITH (X)` 在隔离级别 X 下执行。  
  
 如果在 T 执行期间，在隔离级别 Y 下对内存优化的表或任何本机编译的存储过程执行任何读取操作，则 T 的内存优化的方面达到隔离级别 Y。  
  
 请以下面的事务为例。 在此，t1 和 t2 是基于磁盘的表，而 t3 和 t4 是内存优化表。  
  
 该事务基于磁盘的方面由于在“已提交读”隔离级别启动，因此达到该隔离级别。 基于磁盘的方面还达到“可重复读”级别，因为第一个读取操作是在该隔离级别下执行的。 事务结束处的删除操作在“已提交读”隔离级别执行，因此不会引入新的隔离级别。  
  
 该事务的内存优化的方面可达到以下两个级别之一：如果 condition1 为 true，则达到可序列化级别；如果 condition1 为 false，则内存优化的方面只达到快照隔离级别。  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>交叉容器事务所支持的隔离级别  
 对于交叉容器事务中为内存优化表上的操作所应用的隔离级别，存在一定的限制。  
  
 内存优化表支持隔离级别 SNAPSHOT、REPEATABLE READ 和 SERIALIZABLE。 对于自动提交事务，内存优化表支持隔离级别 READ COMMITTED。  
  
 支持以下方案：  
  
-   READ UNCOMMITTED、READ COMMITTED 和 READ_COMMITTED_SNAPSHOT 交叉容器事务可以在 SNAPSHOT、REPEATABLE READ 和 SERIALIZABLE 隔离级别下访问内存优化表。 READ COMMITTED 保证对该事务的保留；由该事务读取的所有行都已提交到数据库。  
  
-   REPEATABLE READ 和 SERIALIZABLE 事务可以在 SNAPSHOT 隔离级别下访问内存优化表。  
  
## <a name="read-only-cross-container-transactions"></a>只读交叉容器事务  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中大多数只读事务将在提交时回滚。 由于没有要提交到数据库的更改，系统直接释放该事务所使用的资源。 对于基于磁盘的只读事务，此时会释放由该事务持有的所有锁。 对于只占用一个本机编译过程执行的只读内存优化事务，不会执行验证。  
  
 该事务结束时，自动提交模式下的交叉容器只读事务直接回滚。 不执行任何验证。  
  
 如果显式或隐式交叉容器只读事务在 REPEATABLE READ 或 SERIALIZABLE 隔离级别下访问内存优化表，则该事务在提交时执行验证。 有关验证的详细信息请参阅部分冲突检测、 验证和提交依赖关系检查[内存优化表中的事务](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
## <a name="see-also"></a>请参阅  
 [了解内存优化表上的事务](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [具有内存优化表的事务隔离级别的准则](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [内存优化表事务重试逻辑准则](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
