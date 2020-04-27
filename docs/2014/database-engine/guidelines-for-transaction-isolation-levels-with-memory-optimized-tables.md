---
title: 具有内存优化表的事务隔离级别的准则 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26f0193d40a01858bc3fe651a23b389a4ffcb6ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779152"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>内存优化表事务隔离级别准则
  在许多情况下，必须指定事务隔离级别。 内存优化表的事务隔离不同于基于磁盘的表。  
  
 对于指定事务隔离级别的要求：  
  
-   对于包含本机编译存储过程内容的原子块，TRANSACTION ISOLATION LEVEL 为必需选项。  
  
-   由于在跨容器事务中使用隔离级别存在限制，因此在解释型 [!INCLUDE[tsql](../includes/tsql-md.md)] 中使用内存优化表时通常必须随附一个表提示，以指定用于访问该表的隔离级别。 有关隔离级别提示和跨容器事务的详细信息，请参阅[事务隔离级别](../../2014/database-engine/transaction-isolation-levels.md)。  
  
-   必须显式声明所需的事务隔离级别。 无法使用锁提示（如 XLOCK）来保证事务中特定行或表的隔离。  
  
-   访问数据库的应用程序应实现重试逻辑，以处理由于注定事务终止冲突、验证失败和提交依赖关系失败所导致的错误。 请注意，即使对于只读事务，也可能会发生提交依赖关系失败。  
  
-   对于内存优化表，应避免长时间运行的事务。 这类事务会增加冲突的可能性，使后续事务终止。 长时间运行的事务还会延迟垃圾回收。 一个事务的运行时间越长，内存中 OLTP 保留最近删除的行版本的时间就越长，这可能会降低新事务的查找性能。  
  
 基于磁盘的表通常依赖于锁定和阻塞来实现事务隔离。 而内存优化表依赖于多版本控制和冲突检测来确保隔离。 有关详细信息，请参阅[内存优化表的事务](../relational-databases/in-memory-oltp/memory-optimized-tables.md)中的冲突检测、验证和提交依赖项检查部分。  
  
 基于磁盘的表允许隔离级别 SNAPSHOT 和 READ_COMMITTED_SNAPSHOT 进行多版本控制。 对于内存优化表，所有隔离级别都是基于多版本的，包括 REPEATABLE READ 和 SERIALIZABLE。  
  
## <a name="types-of-transactions"></a>事务的类型  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的每个查询都运行在事务的上下文中。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中有三种事务类型：  
  
-   自动提交事务。 如果没有活动的事务上下文，且在会话中未将隐式事务设置为 ON，则每个查询都有自己的事务上下文。 事务在语句开始执行时启动，在语句结束时完成。  
  
-   显式事务。 用户通过显式的 BEGIN TRAN 或 BEGIN ATOMIC 启动事务。 事务跟随在相应的 COMMIT 和 ROLLBACK 或 END（如果是原子块）后完成。  
  
-   隐式事务。 选项 IMPLICIT_TRANSACTIONS 设为 ON 时，每当用户执行一条语句且没有活动的事务上下文时，就会隐式启动事务。 该事务通过显式的 COMMIT 和 ROLLBACK 完成。  
  
## <a name="baseline-read-committed-isolation"></a>基准 READ COMMITTED 隔离  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的默认隔离级别为 READ COMMITTED。  
  
 隔离级别 READ COMMITTED 确保事务不会看到来自当前事务外的更改的任何未提交数据。 换言之，事务只读取已提交到数据库或已由当前事务更改的数据。  
  
 内存优化表支持的所有隔离级别都可提供已提交读保障。 因此，如果事务不需要更严格的保障，则可使用内存优化表支持的任一隔离级别。 与其他隔离级别相比，SNAPSHOT 使用的系统资源最少。  
  
 SNAPSHOT 隔离级别提供的保障（内存优化表支持的最低隔离级别）包括 READ COMMITTED 保障。 事务中的每条语句都读取相同、一致的数据库版本。 不仅该事务读取的所有行都提交到数据库，而且所有读取操作都会看到由同一组事务所作更改的集合。  
  
 **准则**：如果只需要已提交读隔离，请将快照隔离用于本机编译的存储过程，并通过解释[!INCLUDE[tsql](../includes/tsql-md.md)]的访问内存优化表。  
  
 对于自动提交事务，隔离级别 READ COMMITTED 会隐式映射到内存优化表的 SNAPSHOT。 因此，如果 TRANSACTION ISOLATION LEVEL 会话设置设为 READ COMMITTED，则在访问内存优化表时无需通过表提示指定隔离级别。  
  
 下面的自动提交事务示例介绍内存优化表 Customers 与常规表 [Order History] 之间的联接（作为即席批处理的一部分）：  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 下面的显式或隐式事务示例介绍同一联接，但这次是在显式用户事务中。 内存优化表 Customers 在快照隔离下访问（如表提示 WITH (SNAPSHOT) 所示），而常规表 [Order History] 在已提交读隔离下访问：  
  
```sql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
...  
COMMIT  
```  
  
### <a name="operational-differences"></a>操作差异  
 除已提交读保障外，使用基于磁盘的表的应用程序可能还依赖另外两个关键实现细节。 在将使用 READ COMMITTED 隔离访问的基于磁盘的表转换为使用 SNAPSHOT 隔离访问的内存优化表时，需注意以下事项：  
  
-   基于磁盘的表的 READ COMMITTED 隔离级别的实现（假定 READ_COMMITTED_SNAPSHOT 为 OFF）使用锁来防止读取器与编写器之间的冲突。 编写器开始更新行时，会获取一个锁，且直到事务提交后才释放锁。 所有读取操作被阻塞并等待写入事务提交。  
  
     某些应用程序可能会假定读取器总是等待编写器提交，特别是当应用程序层中的两个事务之间没有任何同步时。  
  
     **指导原则：** 应用程序不能依赖阻止行为。 如果应用程序需要并发事务之间的同步，则可以通过[sp_getapplock &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql)，在应用层或数据库层中实现此类逻辑。  
  
-   在使用 READ COMMITTED 隔离的事务中，每条语句都会看到数据库中各行的最新版本。 因此，后续语句看到的是数据库状态的更改。  
  
     采用这一假设的应用程序模式的一个示例：使用 WHILE 循环轮询表，直至发现新行为止。 该循环每次迭代时，查询将看到数据库中的最新更新。  
  
     **指导原则：** 如果应用程序需要轮询内存优化表以获取写入到表中的最新行，请将轮询循环移出事务的作用域之外。  
  
     下面的示例介绍采用这一假设的应用程序模式。 使用 WHILE 循环轮询表，直至发现新行。 在每次循环迭代中，查询将访问数据库中的最新更新。  
  
 下面的示例脚本轮询表 t1，直至该表中出现行为止。 之后，其从该表中移除一行，以作进一步处理。  
  
 注意，需要将轮询逻辑放在事务范围之外，因为其使用快照隔离访问表 t1。 在事务范围内使用轮询逻辑会产生一个需要长时间运行的事务，这是个糟糕的做法。  
  
```sql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>锁定表提示  
 对于基于磁盘的表，可以使用锁定提示（[表提示 &#40;transact-sql&#41;](/sql/t-sql/queries/hints-transact-sql-table)）（例如，HOLDLOCK 和 XLOCK），以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]获得超过指定隔离级别所需的锁。  
  
 内存优化表不使用锁。 可以使用更高的隔离级别（如 REPEATABLE READ 和 SERIALIZABLE）声明所需的保障。  
  
 不支持锁定提示。 改为通过事务隔离级别声明所需的保障。 （支持 NOLOCK 是因为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不对内存优化表使用锁。 请注意，与基于磁盘的表不同，NOLOCK 对于内存优化表并不暗示 READ UNCOMMITTED 行为。）  
  
## <a name="see-also"></a>另请参阅  
 [了解内存优化表上的事务](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [内存优化表上的事务重试逻辑指南](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [事务隔离级别](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
