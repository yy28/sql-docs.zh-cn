---
title: "用于数据库管理员的诊断连接 | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
caps.latest.revision: "65"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 27e43fe72eefa18e7e42dea1a18b63a7005074fe
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="diagnostic-connection-for-database-administrators"></a>用于数据库管理员的诊断连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为管理员提供了一种特殊的诊断连接，以供在无法与服务器建立标准连接时使用。 即使在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不响应标准连接请求时，管理员也可以使用此诊断连接访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以便执行诊断查询并解决问题。  
  
 此专用管理员连接 (DAC) 支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的加密功能和其他安全功能。 DAC 只允许将用户上下文切换到其他管理用户。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尽力使 DAC 连接成功，但在非常特殊的情况下也可能会出现连接失败。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。|  
  
## <a name="connecting-with-dac"></a>使用 DAC 连接  
 默认情况下，只能从服务器上运行的客户端建立连接。 不允许进行网络连接，除非它们是使用带 [remote admin connections 选项](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)的 sp_configure 存储过程配置的。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 角色的成员可以使用 DAC 进行连接。  
  
 通过使用专用的管理员开关 ( **-A** ) 的**sqlcmd**命令提示实用工具，可以支持和使用 DAC。 有关使用 **sqlcmd** 的详细信息，请参阅[将 sqlcmd 与脚本变量结合使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。 还可以将前缀 **admin:** 连接到格式为 **sqlcmd -Sadmin:***<instance_name>* 的实例名。 你还可以通过连接到 **admin:**\<*instance_name*>，从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器启动 DAC。  
  
## <a name="restrictions"></a>限制  
 由于 DAC 仅用于在极少数情况下诊断服务器问题，因此对连接有一些限制：  
  
-   为了保证有可用的连接资源，每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例只允许使用一个 DAC。 如果 DAC 连接已经激活，则通过 DAC 进行连接的任何新请求都将被拒绝，并出现错误 17810。  
  
-   为了保留资源， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 不侦听 DAC 端口，除非使用跟踪标志 7806 进行启动。  
  
-   DAC 最初尝试连接到与登录帐户关联的默认数据库。 连接成功后，可以连接到 master 数据库。 如果默认数据库脱机或不可用，则连接返回错误 4060。 但是，如果使用以下命令覆盖默认数据库，改为连接到 master 数据库，则连接会成功：  
  
     **sqlcmd –A –d master**  
  
     由于只要启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，就能保证 master 数据库处于可用状态，因此建议使用 DAC 连接到 master 数据库。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 禁止使用 DAC 运行并行查询或命令。 例如，如果使用 DAC 执行下列任何语句，都会生成错误 3637。  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   DAC 只能使用有限的资源。 请勿使用 DAC 运行需要消耗大量资源的查询（例如， 对大型表执行复杂的联接）或可能造成阻塞的查询。 这有助于防止将 DAC 与任何现有的服务器问题混淆。 为了避免发生潜在的阻塞情况，如果必须执行可能会发生阻塞的查询，则尽可能在基于快照的隔离级别下运行查询；或者，将事务隔离级别设置为 READ UNCOMMITTED，将 LOCK_TIMEOUT 值设置为较短的值（如 2000 毫秒），或者同时执行这两种操作。 这可以防止 DAC 会话被阻塞。 但是，根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所处的状态，DAC 会话可能会在闩锁上被阻塞。 可以使用 CNTRL-C 终止 DAC 会话，但不能保证一定成功。 如果失败，唯一的选择是重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   为保证连接成功并排除 DAC 故障， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留了一定的资源用于处理 DAC 上运行的命令。 通常这些资源只够执行简单的诊断和故障排除功能，如下所示。  
  
 虽然理论上可以运行任何不必在 DAC 上并行执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，但极力建议您限制使用下列诊断和故障排除命令：  
  
-   查询动态管理视图以进行基本的诊断，例如查询 sys.dm_tran_locks 以了解锁定状态，查询 sys.dm_os_memory_cache_counters 以检查缓存质量，查询 sys.dm_exec_requests 和 sys.dm_exec_sessions 以了解活动的会话和请求。 避免使用需要消耗大量资源的动态管理视图（例如，sys.dm_tran_version_store 扫描整个版本存储区，并且会导致大量的 I/O）或使用了复杂联接的动态管理视图。 有关性能影响的信息，请参阅特定 [动态管理视图](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)的文档。  
  
-   查询目录视图。  
  
-   基本 DBCC 命令，例如 DBCC FREEPROCCACHE、DBCC FREESYSTEMCACHE、DBCC DROPCLEANBUFFERS**,** 和 DBCC SQLPERF。 请勿运行需要消耗大量资源的命令，如 **DBCC** CHECKDB、DBCC DBREINDEX 或 DBCC SHRINKDATABASE。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] KILL\<spid> 命令。 根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的状态，KILL 命令并非一定会成功；如果失败，则唯一的选择是重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 下面是一般的指导原则：  
  
    -   请通过查询 `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`来验证 SPID 是否已被实际终止。 如果没有返回任何行，则表明会话已被终止。  
  
    -   如果会话仍在运行，则通过运行查询 `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`来验证是否为此会话分配了任务。 如果发现还有任务，则很可能当前正在终止会话。 注意，此操作可能会持续很长时间，也可能根本不会成功。  
  
    -   如果在与此会话关联的 sys.dm_os_tasks 中没有任何任务，但是在执行 KILL 命令后该会话仍然出现在 sys.dm_exec_sessions 中，则表明没有可用的工作线程。 选择某个当前正在运行的任务（在 sys.dm_os_tasks 视图中列出的 `sessions_id <> NULL`的任务），并终止与其关联的会话以释放工作线程。 请注意，终止单个会话可能不够，可能需要终止多个会话。  
  
## <a name="dac-port"></a>DAC 端口  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 TCP 端口 1434（如果可用）上侦听 DAC，或者在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 启动时动态分配的 TCP 端口上侦听 DAC。 错误日志包含所侦听的 DAC 所在的端口号。 默认情况下，DAC 侦听器只接受本地端口上的连接。 有关激活远程管理连接的代码示例的详细信息，请参阅 [remote admin connections 服务器配置选项](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)。  
  
 配置远程管理连接之后，会立即启用 DAC 侦听器而不必重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并且客户端可以立即远程连接到 DAC。 通过先在本地使用 DAC 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后再执行 sp_configure 存储过程接受远程连接，则即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止响应，DAC 侦听器仍然可以接受远程连接。  
  
 对于群集配置，DAC 在默认情况下是禁用的。 用户可以执行 sp_configure 的 remote admin connection 选项，使 DAC 侦听器能够访问远程连接。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止响应并且未启用 DAC 侦听器，则可能必须重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来连接 DAC。 因此，建议在群集系统上启用 remote admin connections 配置选项。  
  
 DAC 端口由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在启动时动态分配。 当连接到默认实例时，DAC 会避免在连接时对 SQL Server Browser 服务使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 解决协议 (SSRP) 请求。 它先通过 TCP 端口 1434 进行连接。 如果失败，则通过 SSRP 调用来获取端口。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器没有侦听 SSRP 请求，则连接请求将返回错误。 若要了解 DAC 所侦听的端口号，请参阅错误日志。 如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为接受远程管理连接，则必须使用显式端口号启动 DAC：  
  
 sqlcmd–Stcp: \<server>,\<port>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志列出了 DAC 的端口号，默认情况下为 1434。 如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为只接受本地 DAC 连接，请使用以下命令和环回适配器进行连接：  
  
 **sqlcmd–S127.0.0.1**,**1434**  
  
> [!TIP]  
>  连接到具有 DAC 的 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 时，还必须通过使用 -d 选项在连接字符串中指定数据库名称。  
  
## <a name="example"></a>示例  
 在此示例中，管理员发现服务器 `URAN123` 不响应，因此要诊断该问题。 为此，用户激活 `sqlcmd` 命令提示实用工具，并使用 `URAN123` 指明 DAC 连接到服务器 `-A` 。  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> –A`  
  
 现在，管理员可以执行查询来诊断问题，并且可以终止停止响应的会话。  
  
 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的类似示例将使用包括 -d 参数的以下命令指定数据库：  
  
 `sqlcmd -S serverName.database.windows.net,1434 -U sa -P <xxx> -d AdventureWorks`  
  
## <a name="related-tasks"></a>相关任务  
  
## <a name="related-content"></a>相关内容  
 [将 sqlcmd 与脚本变量结合使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)  
  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
  
 [sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
 [sp_lock (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)  
  
 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)  
  
 [DBCC CHECKALLOC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
  
 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
 [DBCC OPENTRAN (Transact-SQL)](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)  
  
 [DBCC INPUTBUFFER (Transact-SQL)](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
 [与事务相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
 [跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  

