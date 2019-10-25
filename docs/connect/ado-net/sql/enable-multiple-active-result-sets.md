---
title: 启用多个活动结果集
description: 讨论如何在 SQL Server 中使用 MARS。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452228"
---
# <a name="enabling-multiple-active-result-sets"></a>启用多个活动结果集

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

多重活动结果集 (MARS) 是一项用于 SQL Server 的功能，可用来对单个连接执行多个批处理。 如果对 SQL Server 启用了 MARS，使用的每个命令对象都将向该连接添加一个会话。  
  
> [!NOTE]
>  单个 MARS 会话打开一个用于 MARS 的逻辑连接，并为每个活动的命令打开一个逻辑连接。  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>在连接字符串中启用和禁用 MARS  
  
> [!NOTE]
>  下列连接字符串使用随 SQL Server 提供的 AdventureWorks 示例数据库。 提供的连接字符串假定数据库安装在名为 MSSQL1 的服务器上。 根据环境的需要修改连接字符串。  
  
默认情况下，MARS 功能处于禁用状态。 可以通过在连接字符串中添加 "MultipleActiveResultSets = True" 关键字对来启用它。 “True”是启用 MARS 的唯一有效值。 下面的示例演示如何连接到 SQL Server 的实例，以及如何指定是否应启用 MARS。 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
可以通过在连接字符串中添加 "MultipleActiveResultSets = False" 关键字对来禁用 MARS。 “False”是禁用 MARS 的唯一有效值。 以下连接字符串演示了如何禁用 MARS。  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>使用 MARS 时的特殊注意事项  
通常，现有应用程序不应进行修改即可使用启用 MARS 的连接。 但是，如果想要在应用程序中使用 MARS 功能，则应了解以下特别注意事项。  
  
### <a name="statement-interleaving"></a>语句交错  
MARS 操作在服务器上同步执行。 允许使用 SELECT 语句和 BULK INSERT 语句的语句交错。 但数据操作语言（DML）和数据定义语言（DDL）语句以原子方式执行。 在执行原子批处理时尝试执行的任何语句都将被阻止。 服务器上的并行执行不是 MARS 功能。  
  
如果在 MARS 连接下提交了两个批处理，其中一个批处理包含 SELECT 语句，另一个包含 DML 语句，则 DML 可以在 SELECT 语句的执行中开始执行。 但是，必须先运行 DML 语句才能完成，然后 SELECT 语句才能进行进度。 如果这两个语句在同一事务下运行，则在执行 SELECT 语句后，DML 语句所做的任何更改都不会对读取操作显示。  
  
SELECT 语句中的 WAITFOR 语句在等待时不会生成事务，即直到生成第一行。 这意味着在某个 WAITFOR 语句等待时，不能在同一连接内执行其他批处理。  
  
### <a name="mars-session-cache"></a>MARS 会话缓存  
在启用 MARS 的情况下打开连接时，将创建一个逻辑会话，这会增加额外的开销。 为了将系统开销降至最低并提高性能，SqlClient 将 MARS 会话缓存在连接内。 缓存最多包含10个 MARS 会话。 此值不可调整用户。 如果达到会话限制，则会创建一个新的会话，而不会生成一个错误。 其中包含的缓存和会话是按连接进行的;它们不会在连接间共享。 当会话发布时，除非已达到池的上限，否则会将其返回到池中。 如果缓存池已满，则会话将关闭。 MARS 会话不会过期。 仅当连接对象被释放时，它们才会被清除。 MARS 会话缓存未预加载。 它在应用程序需要更多会话时加载。  
  
### <a name="thread-safety"></a>线程安全性  
MARS 操作不是线程安全的。  
  
### <a name="connection-pooling"></a>连接池  
启用 MARS 的连接与任何其他连接共用。 如果某个应用程序打开两个连接，一个启用了 MARS，另一个禁用了 MARS，则这两个连接在不同的池中。
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server 批处理执行环境  
打开连接时，将定义默认环境。 然后，将此环境复制到逻辑 MARS 会话中。  
  
批处理执行环境包括以下组件：  
  
- Set 选项（例如，ANSI_NULLS、DATE_FORMAT、LANGUAGE、TEXTSIZE）  
  
- 安全上下文（用户/应用程序角色）  
  
- 数据库上下文（当前数据库）  
  
- 执行状态变量（例如，@ @ERROR，@ @ROWCOUNT，@ @FETCH_STATUS @ @IDENTITY）  
  
- 顶级临时表  
  
使用 MARS 时，默认执行环境与连接相关联。 在特定连接下开始执行的每个新批处理都将接收默认环境的一个副本。 每当在给定批处理中执行代码时，对环境所做的所有更改都将作用于特定批。 执行完成后，执行设置将复制到默认环境中。 如果单个批处理发出几个要按顺序在同一事务中执行的命令，则语义与涉及前面的客户端或服务器的连接公开的语义相同。  
  
### <a name="parallel-execution"></a>并行执行  
MARS 并未设计为删除应用程序中多个连接的所有要求。 如果应用程序需要对服务器执行真正的命令并行执行，则应使用多个连接。  
  
例如，请考虑以下情况。 将创建两个命令对象，一个用于处理结果集，另一个用于更新数据;它们通过 MARS 共享公用连接。 在此方案中，`Transaction`.`Commit` 在更新时失败，直到在第一个命令对象上读取了所有结果，并生成以下异常：  
  
消息：其他会话正在使用事务的上下文。  
  
源： Microsoft SqlClient 数据提供程序  
  
应为：（null）  
  
收到： SqlClient. SqlException  
  
有三个选项可用于处理此方案：  
  
- 创建读取器后启动事务，使其不是事务的一部分。 然后，每个更新都成为其自己的事务。  
  
- 读取器关闭后提交所有工作。 这可能会产生大量的更新。  
  
- 不要使用 MARS;相反，对每个命令对象使用单独的连接，就像在 MARS 之前一样。  
  
### <a name="detecting-mars-support"></a>检测 MARS 支持  
应用程序可以通过读取 `SqlConnection.ServerVersion` 值来检查 MARS 支持。 对于 SQL Server 2008 SQL Server 2005 和10，主编号应为9。  
  
## <a name="next-steps"></a>后续步骤
- [多重活动结果集 (MARS)](multiple-active-result-sets-mars.md)
