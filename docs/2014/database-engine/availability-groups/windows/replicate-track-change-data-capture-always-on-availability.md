---
title: 复制、 更改跟踪、 更改数据捕获和 AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], AlwaysOn Availability Groups
- change data capture [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: e17a9ca9-dd96-4f84-a85d-60f590da96ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c52283ce9d512da6dc2e5ad05a4c8356524bef01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814053"
---
# <a name="replication-change-tracking-change-data-capture-and-alwayson-availability-groups-sql-server"></a>复制、更改跟踪、更改数据捕获和 AlwaysOn 可用性组 (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]上支持复制、更改数据捕获 (CDC) 和更改跟踪 (CT)。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 有助于提供高可用性和附加数据库恢复功能。  
  
 
  
##  <a name="Overview"></a> 针对 AlwaysOn 可用性组的复制概述  
  
###  <a name="PublisherRedirect"></a> 发布服务器重定向  
 如果已发布的数据库可以识别 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，则使用 redirected_publishers 条目配置向发布数据库提供代理访问的分发服务器。 这些条目利用可用性组侦听器名称连接到发布服务器和发布数据库，重定向最初配置的发布服务器/数据库对。 通过可用性组侦听器名称建立的连接在故障转移时将会失败。 当复制代理在故障转移之后重新启动时，连接会自动重定向到新的主副本。  
  
 在 AlwaysOn 可用性组中，辅助数据库不能为发布服务器。 当复制与 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]组合在一起时，不支持重新发布。  
  
 如果已发布的数据库是可用性组的成员，并且已重定向发布服务器，则必须将该数据库重定向到与该可用性组关联的可用性组侦听器名称， 而不能重定向到显式节点。  
  
> [!NOTE]  
>  故障转移到辅助副本后，复制监视器无法调整 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的发布实例的名称，将继续在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的原始主实例名称下显示复制信息。 在故障转移之后，无法使用复制监视器输入跟踪令牌，但是可以在复制监视器中显示使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]在新发布服务器上输入的跟踪令牌。  
  
###  <a name="Changes"></a> 对复制代理以支持 AlwaysOn 可用性组的常规更改  
 修改了三个复制代理来支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 日志读取器代理、快照代理和合并代理经过了修改，现在可以查询重定向发布服务器的分发数据库，并且可以使用返回的可用性组侦听器名称来连接数据库发布服务器（如果已声明重定向的发布服务器）。  
  
 默认情况下，当代理查询分发服务器以确定是否已重定向原始发布服务器时，则在将重定向的主机返回到代理之前，将会验证当前目标或重定向的适用性。 建议执行此操作。 但是，如果代理启动过于频繁，则与验证存储过程相关的开销可能会过于昂贵。 已向日志读取器代理、快照代理和合并代理添加了新的命令行开关 *BypassPublisherValidation*。 使用此开关时，重定向的发布服务器将会立即返回到代理，并绕过验证存储过程的执行。  
  
 代理历史记录日志中会记录从验证存储过程中返回的故障。 严重性大于或等于 16 的错误将会导致代理终止。 这些代理中已经内置了一些重试功能，以便在其故障转移到新的主副本时处理预计会出现的与已发布的数据库断开连接的情况。  
  
#### <a name="log-reader-agent-modifications"></a>日志读取器代理修改  
 日志读取器代理包含以下更改。  
  
-   **已复制数据库的一致性**  
  
     如果已发布的数据库是 AlwaysOn 可用性组的成员，默认情况下，日志读取器不会处理尚未在所有可用性组辅助副本上强制写入的日志记录。 这确保了在故障转移时，复制到订阅服务器的所有行在新的主副本上也同时存在。  
  
     当发布服务器只有两个 AlwaysOn 可用性副本（一个主副本和一个辅助副本）且发生故障转移时，原始主副本仍保持关闭，因为日志读取器在所有辅助数据库都恢复联机状态之前或在从可用性组中删除发生故障的辅助副本之前不会前移。 日志读取器（现在对辅助数据库运行）将不会前移，因为 AlwaysOn 无法对任何辅助数据库强制执行任何更改。 若要允许日志读取器进一步进行处理并且仍具有灾难恢复能力，请使用 ALTER AVAILABITY GROUP <group_name> REMOVE REPLICA 从可用性组中删除原始主副本。 然后将新的辅助副本添加到可用性组。  
  
-   **跟踪标志 1448**  
  
     跟踪标志 1448 支持复制日志读取器前移，即便在异步辅助副本未确认接受更改的情况下，也是如此。 甚至在此跟踪标志启用的情况下，日志读取器也始终等待同步辅助副本。 日志读取器将不会超过同步辅助副本的最小确认。 此跟踪标志应用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例，而不仅仅应用于可用性组、可用性数据库或日志读取器实例。 此跟踪标志会立即生效，无需重新启动。 它可提前激活或在异步辅助副本失败时激活。  
  
###  <a name="StoredProcs"></a> 支持 AlwaysOn 的存储的过程  
  
-   **sp_redirect_publisher**  
  
     存储过程 **sp_redirect_publisher** 用于为现有的发布服务器/数据库对指定重定向的发布服务器。 如果发布服务器数据库属于某个可用性组，那么重定向的发布服务器将为可用性组侦听器名称。  
  
-   **sp_get_redirected_publisher**  
  
     复制代理使用存储过程 **sp_get_redirected_publisher** 来查询分发服务器，以便确定发布服务器/数据库对是否包含定义的重定向发布服务器。 此存储过程有两个用途。 首先，它允许该代理确定原始发布服务器是否已经重定向。 其次，它还可以启动在分发服务器上运行的验证存储过程 (**sp_validate_redirected_publisher**)，用来验证重定向的目标节点是否适合充当指定数据库的发布服务器。  
  
     若要执行此存储过程，调用方必须是 **sysadmin** 服务器角色的成员、分发数据库的 **db_owner** 数据库角色的成员，或者是与此发布服务器数据库相关联的已定义发布的 **发布访问列表** 的成员。  
  
-   **sp_validate_redirected_publisher**  
  
     此存储过程尝试验证当前发布服务器是否有能力承载已发布的数据库。 可以随时调用它，以验证已发布数据库的当前主机是否有能力支持复制。  
  
-   **sp_validate_replicate_hosts_as_publishers**  
  
     尽管由代理确保当前主副本能够充当发布服务器数据库的复制发布服务器非常有用，但需要更综合的验证能力来建立整个复制拓扑在 AlwaysOn 可用性数据库上的有效性。 存储过程 **sp_validate_replica_hosts_as_publishers** 正是为满足这一需要而设计的。  
  
     此存储过程总是手动运行。 调用方必须是分发服务器的 **sysadmin** 、分发数据库的 **dbowner** ，或者是发布服务器数据库的某一发布的 **发布访问列表** 的成员。 此外，调用方的登录名必须是对所有可用性副本主机有效的登录名，并且对与发布服务器数据库关联的可用性数据库具有 select 权限。  
  
###  <a name="CDC"></a> 变更数据捕获  
 启用了变更数据捕获 (CDC) 的数据库能够利用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 来确保数据库在出现故障时保持可用，而且确保持续监视针对数据库表的更改并将更改存入 CDC 更改表。 配置 CDC 和 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的顺序并不重要。 可以将启用 CDC 的数据库添加到 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，而且属于 AlwaysOn 可用性组成员的数据库也可以启用 CDC。 但是，在这两种情况下，CDC 配置都是始终在当前或目标主副本上执行。 CDC 使用日志读取器代理，它具有本主题前面的“日志读取器代理修改”  部分所述的相同限制。  
  
-   **对未启用复制的变更数据捕获的捕获更改**  
  
     如果为数据库启用了 CDC，但未启用复制，用来捕获日志中的更改并将其存入 CDC 更改表的捕获进程在 CDC 主机上作为主机自己的 SQL 代理作业运行。  
  
     为了在故障转移后继续搜集更改，存储过程 **sp_cdc_add_job** 必须在新的主副本上运行，以创建本地捕获作业。  
  
     下例创建一个捕获作业。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'capture';  
    ```  
  
-   **对启用复制的变更数据捕获的捕获更改**  
  
     如果为数据库同时启用了 CDC 和复制，日志读取器负责处理 CDC 更改表的填充。 在这种情况下，为利用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 所采用的复制技术将能够确保在故障转移后继续从日志中捕获更改，并将更改存入 CDC 更改表。 对于此配置中的 CDC，无需执行其他任何操作，以确保填充更改表。  
  
-   **变更数据捕获清理**  
  
     若要确保在新的主数据库上执行适当的清除，应始终创建一个本地清除作业。 下例创建一个清除作业。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'cleanup';  
    ```  
  
    > [!NOTE]  
    >  在故障转移之前，您应在所有可能的故障转移目标上创建作业，并将其标记为禁用，直到主机上的可用性副本成为新的主副本。 当本地数据库变为辅助数据库时，还应禁用旧的主数据库上运行的 CDC 作业。 若要禁用和启用作业，请使用 [sp_update_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) 的 @enabled 选项。 有关创建 CDC 作业的详细信息，请参阅 [sys.sp_cdc_add_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)上支持复制、更改数据捕获 (CDC) 和更改跟踪 (CT)。  
  
-   **向 AlwaysOn 主数据库副本中添加 CDC 角色**  
  
     在为 CDC 启用表之后，可以将数据库角色与捕获实例相关联。 如果指定某个角色，则希望使用 CDC 表值函数来访问表更改的用户不仅必须具有对所跟踪的表列的选择访问权限，而且还必须是该指定角色的成员。 如果指定的角色尚未存在，则将创建该角色。 在将数据库角色自动添加到 AlwaysOn 主数据库时，还会将这些角色传播到可用性组的辅助数据库。  
  
-   **客户端应用程序访问 CDC 更改数据，且始终启用**  
  
     使用表值函数 (TVF) 或链接服务器来访问更改表数据的客户端应用程序还需要能够在故障转移后定位到相应的 CDC 主机。 可用性组侦听器名称是 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 提供的机制，用于以透明的方式允许将连接重定向到其他主机。 一旦将某个可用性组侦听器名称与某个可用性组关联，即可在 TCP 连接字符串中使用它。 通过可用性组侦听器名称，可支持两个不同的连接方案。  
  
    -   其中一个方案确保始终将连接请求定向到当前主副本。  
  
    -   另一个方案则确保将连接请求定向到只读的辅助副本。  
  
     如果要用来查找只读的辅助副本，则还必须为可用性组定义一个只读的路由列表。 有关详细信息，请参阅 [为只读路由配置可用性副本](../../listeners-client-connectivity-application-failover.md#ConfigureARsForROR)。  
  
    > [!NOTE]  
    >  在创建可用性组侦听器名称时以及在客户端应用程序使用该名称来访问可用性组数据库副本时，会出现一些传播延迟。  
  
     可使用以下查询来确定是否已为承载 CDC 数据库的可用性组定义了可用性组侦听器名称。 如果已创建，则查询将返回相应的可用性组侦听器名称。  
  
    ```  
    SELECT dns_name   
    FROM sys.availability_group_listeners AS l  
    INNER JOIN sys.availability_databases_cluster AS d  
        ON l.group_id = d.group_id  
    WHERE d.database_name = N'MyCDCDB';  
    ```  
  
-   **将查询负载重定向到可读辅助副本**  
  
     在许多情况下，客户端应用程序将始终希望能够连接到当前主副本（这并非利用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的唯一方法）。 如果将可用性组配置为支持可读的辅助副本，则还可从辅助节点中收集更改数据。  
  
     在配置可用性组之后，可使用与 SECONDARY_ROLE 关联的 ALLOW_CONNECTIONS 属性来指定受支持的辅助访问的类型。 如果配置为 ALL，则将允许所有指向辅助副本的连接，但是，只有那些要求只读访问的连接才会成功。 如果配置为 READ_ONLY，则在连接到辅助数据库时必须指定只读意向才能使连接成功。 有关详细信息，请参阅[配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
     以下查询可用来确定是否需要只读意向才能连接到可读辅助副本。  
  
    ```  
    SELECT g.name AS AG, replica_server_name, secondary_role_allow_connections_desc  
    FROM sys.availability_replicas AS r  
    JOIN sys.availability_groups AS g  
        ON r.group_id = g.group_id  
    WHERE g.name = N'MY_AG_NAME;  
    ```  
  
     可用性组侦听器名称或显式节点名称都可用来查找辅助副本。 如果使用可用性组侦听器名称，则会将访问定向到任何合适的辅助副本。  
  
     当`sp_addlinkedserver`用于创建链接的服务器以访问辅助副本时， *@datasrc*参数用于可用性组侦听器名称或显式服务器名称，并 *@provstr*参数用于指定只读意向。  
  
    ```  
    EXEC sp_addlinkedserver   
    @server = N'linked_svr',   
    @srvproduct=N'SqlServer',  
    @provider=N'SQLNCLI11',   
    @datasrc=N'AG_Listener_Name',   
    @provstr=N'ApplicationIntent=ReadOnly',   
    @catalog=N'MY_DB_NAME';  
    ```  
  
-   **对 CDC 变更数据和域登录名的客户端访问**  
  
     一般情况下，您应使用域登录名来对驻留在作为 AlwaysOn 可用性组的成员的数据库中的更改数据进行客户端访问。 若要确保在故障转移后能够继续对变更数据进行访问，域用户将需要具有对支持可用性组副本的所有主机的访问权限。 如果将一个数据库用户添加到主副本中的数据库，则会将该用户与一个域登录名关联，然后将该数据库用户传播到辅助数据库，并且继续与指定的域登录名关联。 如果将新数据库用户与一个 SQL Server 身份验证登录名关联，则将传播辅助数据库上的用户而不关联登录名。 尽管可以使用关联的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证登录名来访问最初定义数据库用户的主副本上的更改数据，但该节点是能够进行访问的唯一节点。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证登录名将无法访问任何辅助数据库中的数据，也无法访问除定义了数据库用户的原始数据库之外的任何新的主数据库中的数据。  
  
###  <a name="CT"></a> 更改跟踪  
 启用了更改跟踪 (CT) 的数据库可以成为 AlwaysOn 可用性组的一部分。 无需任何其他配置。 使用 CDC 表值函数 (TVF) 来访问更改数据的更改跟踪客户端应用程序将需要具备在故障转移后定位主副本的能力。 如果客户端应用程序通过可用性组侦听器名称进行连接，则连接请求将始终会适当地定向到当前主副本。  
  
> [!NOTE]  
>  必须始终从主副本中获取更改跟踪数据。 尝试访问辅助副本中的更改数据将会导致以下错误：  
>   
>  消息 22117，级别 16，状态 1，第 1 行  
>   
>  对于作为辅助副本成员的数据库（即，辅助数据库）而言，不支持更改跟踪。 对主副本中的数据库运行更改跟踪查询。  
  
##  <a name="Prereqs"></a> 有关使用复制的先决条件、限制和注意事项  
 本节介绍使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]部署复制时的注意事项，包括先决条件、限制和建议。  
  
### <a name="prerequisites"></a>先决条件  
  
-   在使用事务复制并且发布数据库位于可用性组中时，发布服务器和分发服务器都必须至少运行 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。 订阅服务器可以使用较低级别的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   在使用合并复制并且发布数据库位于某一可用性组中时：  
  
    -   推送订阅：发布服务器和分发服务器必须至少运行[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
    -   请求订阅：发布服务器、 分发服务器和订阅服务器数据库必须至少位于[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。 这是因为订阅服务器上的合并代理必须知道可用性组如何将故障转移到其辅助代理。  
  
-   不支持将分发数据库放置在可用性组上。  
  
-   发布服务器实例满足加入 AlwaysOn 可用性组所需的所有先决条件。 有关详细信息，请参阅[针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
### <a name="restrictions"></a>限制  
 针对 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的复制所支持的组合：  
  
|||||  
|-|-|-|-|  
||**发布服务器**|**分发服务器** <sup>3</sup>|**订阅服务器**|  
|**事务性**|是<sup>1</sup>|否|是<sup>2</sup>|  
|**P2P**|否|否|否|  
|**合并**|是|否|是<sup>2</sup>|  
|**快照**|是|否|是<sup>2</sup>|  
  
 <sup>1</sup>不包括对双向和相互事务复制的支持。  
  
 <sup>2</sup>故障转移到副本数据库是一个手动过程。 不提供自动故障转移。  
  
 <sup>3</sup>将分发服务器数据库不支持用于[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]或数据库镜像。  
  
### <a name="considerations"></a>注意事项  
  
-   不支持将分发数据库用于 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 或数据库镜像。 复制配置与配置了分发服务器的 SQL Server 实例相关联，因此无法镜像或复制分发数据库。 为了让分发服务器提供高可用性，请使用 SQL Server 故障转移群集。 有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   尽管支持订阅服务器故障转移到辅助数据库，但这是一个相对复杂的手动过程。 该过程与故障转移镜像的订阅服务器数据库所用的方法基本相同。 订阅服务器必须运行 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 或更高版本才能加入可用性组。  
  
-   存在于数据库外部的元数据和对象不会传播到辅助副本，包括登录名、作业和链接服务器。 如果您在故障转移后需要新的主数据库中有元数据和对象，则必须手动复制它们。 有关详细信息，请参阅 [管理可用性组中数据库的登录名和作业 (SQL Server)](../../logins-and-jobs-for-availability-group-databases.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **复制**  
  
-   [为 AlwaysOn 可用性组 (SQL Server) 配置复制](always-on-availability-groups-sql-server.md)  
  
-   [维护 AlwaysOn 发布数据库&#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [复制管理常见问题解答](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
 **Change data capture**  
  
-   [启用和禁用变更数据捕获 (SQL Server)](../../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)  
  
-   [管理和监视变更数据捕获 (SQL Server)](../../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
-   [处理变更数据 (SQL Server)](../../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
 **Change tracking**  
  
-   [启用和禁用更改跟踪 (SQL Server)](../../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)  
  
-   [管理更改跟踪 (SQL Server)](../../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
-   [处理更改跟踪 (SQL Server)](../../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [复制订阅服务器和 AlwaysOn 可用性组&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组：互操作性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md) [AlwaysOn 故障转移群集实例 (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)   
 [关于变更数据捕获 (SQL Server)](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [关于更改跟踪 (SQL Server)](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [SQL Server 复制](../../../relational-databases/replication/sql-server-replication.md)   
 [跟踪数据更改 (SQL Server)](../../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [sys.sp_cdc_add_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)  
  
  
