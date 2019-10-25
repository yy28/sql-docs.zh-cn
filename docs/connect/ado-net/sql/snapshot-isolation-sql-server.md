---
title: SQL Server 中的快照隔离
description: 描述对快照隔离的支持，这是一种旨在减少事务应用程序中的阻塞的行版本控制机制。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8ef462246d35694ba9bf38954ca8c58635e44e7f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452087"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server 中的快照隔离

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

快照隔离增强了 OLTP 应用程序的并发性。  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>了解快照隔离和行版本控制  
启用快照隔离之后，系统将在 tempdb 中维护每个事务的已更新行版本  。 唯一的事务序列号标识每个事务，并为每个行版本记录这些唯一的编号。 该事务适用于其序列号在事务序列号之前的最新行版本。 事务将忽略在事务开始后创建的更新的行版本。  
  
术语 "快照" 反映的事实是，事务中的所有查询都能看到数据库的相同版本（或快照），这取决于事务开始时数据库的状态。 不会对快照事务中的基础数据行或数据页获取锁定，这允许其他事务执行，而不会被之前的 incompleted 事务阻止。 修改数据的事务不会阻止读取数据的事务，并且读取数据的事务不会阻止写入数据的事务，因为在 SQL Server 中，通常会在默认的已提交读隔离级别下执行这些操作。 这种不会产生阻止的行为也大大降低了复杂事务出现死锁的可能性。  
  
快照隔离使用开放式并发模型。 如果快照事务尝试提交对事务开始后已更改的数据所做的修改，则将回滚该事务，并引发错误。 您可以通过对访问要修改的数据的 SELECT 语句使用 UPDLOCK 提示来避免这种情况。 有关详细信息，请参阅 SQL Server 联机丛书中的 "锁定提示"。  
  
在事务中使用快照隔离之前，必须通过设置 ALLOW_SNAPSHOT_ISOLATION ON database 选项来启用快照隔离。 这样将激活在临时数据库 (tempdb) 中存储行版本的机制  。 必须在将快照隔离与 Transact-sql ALTER DATABASE 语句一起使用的每个数据库中启用快照隔离。 在这一点上，快照隔离不同于传统的已提交读、可重复读取、可序列化和不需要配置的隔离级别。 以下语句激活快照隔离，并将默认的已提交的读取行为替换为快照：  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
设置 READ_COMMITTED_SNAPSHOT ON 选项可在默认的已提交读隔离级别下访问版本控制的行。 如果将 READ_COMMITTED_SNAPSHOT 选项设置为 OFF，则必须为每个会话显式设置快照隔离级别，以便访问版本控制的行。  
  
## <a name="managing-concurrency-with-isolation-levels"></a>管理隔离级别的并发  
Transact-sql 语句所执行的隔离级别决定了其锁定和行版本控制行为。 隔离级别具有连接范围的作用域，并在为连接设置了设置事务隔离级别语句后保持有效，直到关闭连接或设置另一个隔离级别。 当连接关闭并返回到池时，将保留上一次设置事务隔离级别语句的隔离级别。 后续连接重新使用已入池的连接时，将使用在连接到池中时生效的隔离级别。  
  
连接中发出的单个查询可以包含修改单个语句或事务的隔离但不会影响连接隔离级别的锁提示。 在存储过程或函数中设置的隔离级别或锁定提示不会更改调用它们的连接的隔离级别，并且仅在存储过程或函数调用的持续时间内有效。  
  
在早期版本的 SQL Server 中支持在 SQL-92 标准中定义的四个隔离级别：  
  
- 未提交读是限制最少的隔离级别，因为它会忽略其他事务放置的锁。 在未提交读的下执行的事务可以读取其他事务尚未提交的已修改数据值;这称为 "脏" 读取。  
  
- SQL Server 的默认隔离级别为 READ COMMITTED。 它通过指定语句不能读取其他事务已修改但尚未提交的数据值，从而防止脏读。 其他事务仍可以在当前事务中的各个语句执行之间修改、插入或删除数据，从而导致不可重复的读取或 "虚拟" 数据。  
  
- 可重复读取是比已提交读更严格的隔离级别。 它包含已提交读，另外还指定在当前事务提交之前，任何其他事务都不能修改或删除已由当前事务读取的数据。 并发性低于读取已提交的数据，因为在事务的持续时间内保留了读取数据上的共享锁，而不是在每个语句结束时释放。  
  
- SERIALIZABLE 是限制最多的隔离级别，因为它锁定了键的整个范围，并在事务完成之前一直保持锁定状态。 它包含可重复读取并添加了限制，其他事务不能将新行插入到事务已读取的范围中，直到事务完成。  
  
有关详细信息，请参阅[事务锁定和行版本控制指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)。  
  
### <a name="snapshot-isolation-level-extensions"></a>快照隔离级别扩展  
SQL Server 通过引入 SNAPSHOT 隔离级别并另外实现了 READ COMMITTED，引入对 SQL-92 隔离级别的扩展。 新的 READ_COMMITTED_SNAPSHOT 隔离级别可以透明的方式替换所有事务的 READ COMMITTED。  
  
- 快照隔离指定事务内读取的数据永远不会反映其他同时事务所做的更改。 事务使用事务开始时存在的数据行版本。 读取数据时不会对数据进行锁定，因此快照事务不会阻止其他事务写入数据。 写入数据的事务也不会阻止快照事务读取数据。 若要使用快照隔离，需要通过设置 ALLOW_SNAPSHOT_ISOLATION 数据库选项来启用快照隔离。  
  
- 当在数据库中启用快照隔离时，READ_COMMITTED_SNAPSHOT 数据库选项将确定默认的已提交读隔离级别的行为。 如果未显式指定 READ_COMMITTED_SNAPSHOT，则 "已提交读" 将应用于所有隐式事务。 这将产生与将 READ_COMMITTED_SNAPSHOT 设置为 OFF （默认值）相同的行为。 当 READ_COMMITTED_SNAPSHOT OFF 有效时，数据库引擎使用共享锁来强制实施默认隔离级别。 如果将 READ_COMMITTED_SNAPSHOT 数据库选项设置为 ON，则数据库引擎将使用行版本控制和快照隔离作为默认值，而不是使用锁来保护数据。  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>快照隔离和行版本控制的工作原理  
启用 SNAPSHOT 隔离级别后，每次更新行时，SQL Server 数据库引擎在 tempdb 中存储原始行的副本，并为该行添加事务序列号  。 下面是发生的事件的顺序：  
  
1. 将启动新事务，并为其分配事务序列号。  
  
2. 数据库引擎在事务中读取某行，并从 tempdb 中检索其序列号与事务序列号最接近并且小于事务序列号的行版本  。  
  
3. 数据库引擎将检查事务序列号是否不在快照事务启动时处于活动状态的未提交事务的事务序列号的列表中。  
  
4. 事务从 tempdb 中读取自事务开始以来最新的行版本  。 由于这些序列号值将高于事务序列号的值，因此它将不会看到在启动事务后插入的新行。  
  
5. 当前事务将看到事务开始后删除的行，因为 tempdb 中的行版本具有更低的序列号值  。  
  
快照隔离的最终效果是，事务在事务开始时查看所有数据，而不考虑或对基础表施加任何锁定。 这可能会导致存在争用的情况下提高性能。  
  
快照事务始终使用乐观并发控制，这会阻止其他事务更新行的任何锁。 如果快照事务尝试提交对事务开始后已更改的行的更新，则将回滚该事务，并引发错误。  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>在 ADO.NET 中使用快照隔离  
@No__t_0 类支持 ADO.NET 中的快照隔离。 如果数据库已启用了快照隔离，但是未配置 READ_COMMITTED_SNAPSHOT ON，必须在调用 <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> 方法时，使用 IsolationLevel.Snapshot 枚举值启动 <xref:Microsoft.Data.SqlClient.SqlTransaction>  。 此代码段假定连接是打开的 <xref:Microsoft.Data.SqlClient.SqlConnection> 对象。  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>示例  
下面的示例演示了如何通过尝试访问锁定的数据来表现不同的隔离级别，并且不应在生产代码中使用。  
  
该代码连接到 SQL Server 中的 AdventureWorks 示例数据库上，并创建一个名为 TestSnapshot 的表，然后插入一行数据   。 该代码使用 ALTER DATABASE Transact-sql 语句来为数据库启用快照隔离，但它不会设置 READ_COMMITTED_SNAPSHOT 选项，而是使默认的已提交读隔离隔离级别的行为生效。 然后，该代码执行以下操作：  
  
1. 它开始但未完成，sqlTransaction1，它使用可序列化隔离级别来启动更新事务。 这具有锁定表的效果。  
  
2. 打开第二个连接，并使用 SNAPSHOT 隔离级别开始第二个事务，读取 TestSnapshot 表中的数据  。 由于启用了快照隔离，因此此事务可以读取 sqlTransaction1 开始之前已存在的数据。  
  
3. 它将打开第三个连接，并使用 "已提交读" 隔离级别启动一个事务来尝试读取表中的数据。 在这种情况下，代码无法读取数据，因为代码在第一个事务中无法通过在表上放置的锁进行读取，因而超时。如果使用 REPEATABLE READ 和 SERIALIZABLE 隔离级别，因为这些隔离级别也无法通过第一个事务中放置的锁，因而会出现同样的结果。  
  
4. 它将打开第四个连接，并使用 "未提交读" 隔离级别启动一个事务，该隔离级别对 sqlTransaction1 中未提交的值执行脏读。 如果第一个事务未提交，则此值在数据库中实际上不存在。  
  
5. 回滚第一个事务，并通过删除 TestSnapshot 表以及禁用 AdventureWorks 数据库的快照隔离来进行清理   。  
  
> [!NOTE]
>  下面的示例使用与关闭连接池相同的连接字符串。 如果连接已建立池连接，则重置其隔离级别不会在服务器上重置隔离级别。 因此，使用同一个共用内部连接的后续连接将会启动，并将其隔离级别设置为池连接的隔离级别。 关闭连接池的另一种方法是为每个连接显式设置隔离级别。  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>示例  
下面的示例演示了在修改数据时快照隔离的行为。 此代码执行以下操作：  
  
1. 连接到 AdventureWorks 示例数据库并启用 SNAPSHOT 隔离  。  
  
2. 创建一个名为 TestSnapshotUpdate 的表并插入三行示例数据  。  
  
3. 使用快照隔离开始但不能完成，sqlTransaction1。 在事务中选择三行数据。  
  
4. 创建第二个通向 AdventureWorks 的 SqlConnection，并使用 READ COMMITTED 隔离级别创建第二个事务，更新在 sqlTransaction1 中选择的其中一行的值   。  
  
5. 提交 sqlTransaction2。  
  
6. 返回到 sqlTransaction1 并尝试更新 sqlTransaction1 已提交的同一行。 引发错误3960，并且 sqlTransaction1 自动回滚。 控制台窗口中将显示 SqlException.Number 和 SqlException.Message   。  
  
7. 执行清理代码以关闭 AdventureWorks 中的快照隔离并删除 TestSnapshotUpdate 表   。  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>使用锁提示和快照隔离  
在上面的示例中，第一个事务选择数据，第二个事务更新第一个事务完成之前的数据，并在第一个事务尝试更新同一行时导致更新冲突。 通过在事务开始时提供锁提示，可以减少长时间运行的快照事务中的更新冲突的可能性。 以下 SELECT 语句使用 UPDLOCK 提示锁定所选行：  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
在第一个事务完成之前，使用 UPDLOCK 锁提示会阻止尝试更新行的任何行。 这可确保所选行在稍后在事务中更新时不会发生冲突。 请参阅 SQL Server 联机丛书中的 "锁定提示"。  
  
如果你的应用程序有很多冲突，则快照隔离可能不是最佳选择。 只应在真正需要时使用提示。 您的应用程序不应设计为能持续依赖于锁定提示进行操作。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
- [事务锁定和行版本控制指南](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
