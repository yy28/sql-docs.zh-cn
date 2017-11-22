---
title: "创建可用性组 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
caps.latest.revision: "196"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 35ccffcfbdce2c10b20c8459e59a1c2d41962088
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能启用了 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 的实例，将创建新的可用性组。  
  
> [!IMPORTANT]  
>  在要用作新可用性组的初始主副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上执行 CREATE AVAILABILITY GROUP。 此服务器实例必须驻留在 Windows Server 故障转移群集 (WSFC) 节点上。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```SQL  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL | EXTERNAL }  
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>参数  
 *组名*  
 指定新可用性组的名称。 *group_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][标识符](../../relational-databases/databases/database-identifiers.md)，并且它必须是唯一的 WSFC 群集中的所有可用性组。 可用性组名称的最大长度为 128 个字符。  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {主 |SECONDARY_ONLY |辅助 |无}  
 指定在选择执行备份的位置时有关备份作业应该如何评估主副本的首选项。 您可以编写给定备份作业的脚本，以便纳入自动备份首选项。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会强制执行首选项，因此它对即席备份没有影响，了解这一点很重要。  
  
 支持的值如下：  
  
 PRIMARY  
 指定备份应该始终在主副本上发生。 如果您需要在对辅助副本运行备份时不支持的备份功能，例如创建差异备份，此选项将很有用。  
  
> [!IMPORTANT]  
>  如果你计划使用日志传送为可用性组准备任何辅助数据库，请将自动备份首选项设置为“主要”，直到准备好所有辅助数据库并将其联接到可用性组。  
  
 SECONDARY_ONLY  
 指定备份应该永远不会在主副本上执行。 如果主副本是唯一的联机副本，则备份应不会发生。  
  
 SECONDARY  
 指定备份应在辅助副本上发生，但在主副本是唯一联机的副本时除外。 在该情况下，备份应在主副本上发生。 这是默认行为。  
  
 无  
 指定您希望在选择要执行备份的副本时备份作业将忽略可用性副本的角色。 请注意，备份作业可能评估其他因素，例如每个可用性副本的备份优先级及其操作状态和已连接状态。  
  
> [!IMPORTANT]  
>  不会强制实施 AUTOMATED_BACKUP_PREFERENCE 设置。 对此首选项的解释依赖于您为给定可用性组中的数据库撰写作业脚本的逻辑（如果有）。 自动备份首选项设置对即席备份没有影响。 有关详细信息，请参阅[可用性副本 &#40; 上配置备份SQL server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  若要查看现有可用性组的自动备份首选项，请选择**automated_backup_preference**或**automated_backup_preference_desc**列[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。 此外， [sys.fn_hadr_backup_is_preferred_replica &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)可以用于确定为首选备份副本。  此函数将返回 1 为至少一个副本，即使`AUTOMATED_BACKUP_PREFERENCE = NONE`。  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 |**3** | 4 | 5}  
 指定哪些故障条件触发此可用性组自动故障转移。 FAILURE_CONDITION_LEVEL 在组级别设置，但仅对配置为同步提交可用性模式的可用性副本 (AVAILIBILITY_MODE  **=**  synchronous_commit 的情况下)。 此外，故障条件可以触发自动故障转移，仅当主要和辅助副本配置为使用自动故障转移模式 (FAILOVER_MODE  **=** 自动) 并且辅助副本当前与主副本同步。  
  
 失败条件级别的范围 (1–5) 是从最少限制的级别 1 到最多限制的级别 5。 给定的条件级别包含所有限制较少的级别。 因此，最严格的条件级别 5 包含四个限制较少的级别 (1-4)，级别 4 包含级别 1-3，依此类推。 下表描述对应于每个级别的失败条件。  
  
|Level|失败条件|  
|-----------|-----------------------|  
|1|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务已关闭。<br /><br /> 的因为从服务器实例接收不到任何 ACK 连接到 WSFC 群集的可用性组租期到期。 有关详细信息，请参阅 [工作原理：SQL Server AlwaysOn 租约超时](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx)。|  
|2|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> -实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会连接到群集，并且超过了可用性组的用户指定 HEALTH_CHECK_TIMEOUT 阈值。<br /><br /> 可用性副本处于失败状态。|  
|3|指定在发生了严重的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时应启动自动故障转移。<br /><br /> 这是默认行为。|  
|4|指定在发生了中等程度的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部资源池中出现持久的内存不足情况）时应启动自动故障转移。|  
|5|指定在出现任何符合的失败条件时应启动自动故障转移，这些失败条件包括：<br /><br /> -SQL 引擎工作线程耗尽。<br /><br /> 无法解决的死锁的检测。|  
  
> [!NOTE]  
>  缺乏由的实例的响应[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为客户端请求不与可用性组。  
  
 FAILURE_CONDITION_LEVEL 和 HEALTH_CHECK_TIMEOUT 值中，定义*灵活的故障转移策略*为给定的组。 此灵活的故障转移策略向您提供对必须导致自动故障转移的条件的精确控制。 有关详细信息，请参阅[的自动故障转移的可用性组 &#40; 灵活的故障转移策略SQL server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *毫秒*  
 为指定的等待时间 （以毫秒为单位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程来返回服务器运行状况信息之前 WSFC 群集假定服务器实例很慢或会挂起。 HEALTH_CHECK_TIMEOUT 在组级别设置，但仅对配置为使用同步提交可用性模式以及自动故障转移的可用性副本 (AVAILIBILITY_MODE  **=** 同步_COMMIT)。  此外，运行状况检查超时可以触发自动故障转移，仅当主要和辅助副本配置为使用自动故障转移模式 (FAILOVER_MODE  **=** 自动) 数据库与辅助数据库副本当前与主副本同步。  
  
 默认的 HEALTH_CHECK_TIMEOUT 值为 30000 毫秒（30 秒）。 最小值为 15000 毫秒（15 秒），最大值为 4294967295 毫秒。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 在数据库级别不执行运行状况检查。  
  
 DB_FAILOVER  **=**  {ON |关闭}  
 指定当主副本上的数据库处于脱机状态时要执行的响应。 可用性组中数据库联机以外的任何状态设置为 ON 时，将触发自动故障转移。 当此选项设置为 OFF 时，仅实例的运行状况用于触发自动故障转移。  
  
  有关此设置的详细信息，请参阅[数据库级别运行状况检测选项](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT  **=**  {PER_DB |无}  
 指定是否通过分布式的事务处理协调器 (DTC) 支持跨数据库事务。 仅从支持跨数据库事务[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 PER_DB 创建可用性组具有对这些事务的支持。 有关详细信息，请参阅[用于 AlwaysOn 可用性组和数据库镜像的跨数据库事务和分布式事务 (SQL Server)](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)。  
  
 BASIC  
 用于创建基本可用性组。 基本可用性组仅限于一个数据库和两个副本： 主副本和一个辅助副本。 此选项是不推荐使用的数据库镜像 SQL Server 标准版上的功能的替代。 有关详细信息，请参阅[基本可用性组 &#40;Always On 可用性组 &#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). 从支持基本可用性组[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  

 DISTRIBUTED  
 用于创建分布式的可用性组。 此选项使用可用性组 ON 参数用于连接两个单独的 Windows Server 故障转移群集中的可用性组。  有关详细信息，请参阅[分布式可用性组&#40;Always On 可用性组&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。 从支持分布式的可用性组[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 自 2017 年 1 中引入。 用于设置最小同步提交主提交事务之前所需的辅助副本数。 保证 SQL Server 事务等待，直到事务日志更新辅助副本的最小数量。 默认值为 0，这将使 SQL Server 2016 相同的行为。 最小值为 0。 最大值为减 1 的副本数目。 此选项与在同步提交模式下的副本。 当副本在同步提交模式下时，写入主副本上的等待，直到同步辅助副本上的写入都将提交到副本数据库事务日志。 如果承载辅助同步副本的 SQL 服务器停止响应，则将该辅助副本承载主副本的 SQL 服务器标记为未同步，并且继续。 无响应的数据库重新联机它是处于"未同步"状态，直到主可以使其同步再次，副本将标记为不正常。 此设置可保证主副本等待的最小副本数已提交的每个事务。 如果不可用的最小副本数，则在主计算机上的提交失败。 对于群集类型`EXTERNAL`可用性组添加到群集资源时更改的设置。 请参阅[可用性组配置的高可用性和数据保护](../../linux/sql-server-linux-availability-group-ha.md)。

 CLUSTER_TYPE  
 SQL Server 自 2017 年 1 中引入。 用于标识可用性组是否在 Windows Server 故障转移群集 (WSFC)。  Windows Server 故障转移群集上的故障转移群集实例上可用性组时，将设置为 WSFC。 群集管理的群集管理器不是 Windows Server 故障转移群集，如 Linux Pacemaker 时设置为外部。 可用性组未使用 WSFC 群集协调时，则设置为无。 例如，当某一可用性组包括 Linux 服务器与任何群集管理器。 

 数据库*database_name*  
 指定本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例（也就是您正在其上创建可用性组的服务器实例）上的一个或多个用户数据库的列表。 您可以为一个可用性组指定多个数据库，但每个数据库只能属于一个可用性组。 有关类型的可用性组都可以支持的数据库的信息，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). 若要了解哪些本地数据库已属于某一可用性组，请参阅**replica_id**中的列[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。  
  
 DATABASE 子句是可选的。 如果省略此元素时，新的可用性组为空。  
  
 创建可用性组后，连接到承载辅助副本的每个服务器实例然后准备每个辅助数据库并将其联接到可用性组。 有关详细信息，请参阅本主题后面的 [启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
> [!NOTE]  
>  然后，您可以将承载当前主副本的服务器实例上的合格数据库添加到可用性组。 还可以从可用性组中删除数据库。 有关详细信息，请参阅 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell 将次要副本添加到现有的 AlwaysOn 可用性组。  
  
 REPLICA ON  
 指定一到五个 SQL Server 实例，以便承载新的可用性组中的可用性副本。  通过在每个副本的服务器实例地址后追加 WITH (…) 子句来指定每个副本。 至少，你必须指定你的本地服务器实例，这将成为初始主副本。 还可以选择指定最多四个辅助副本。  
  
 您需要将每个辅助副本联接到可用性组。 有关详细信息，请参阅 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell 将次要副本添加到现有的 AlwaysOn 可用性组。  
  
> [!NOTE]  
>  如果在创建可用性组，请指定不超过四个辅助副本，则可以附加的辅助副本在任何时候通过使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 你还可以使用此语句这从现有可用性组中删除任何辅助副本。  
  
 \<server_instance > 指定的实例的地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]副本的主机。 地址格式依赖于该实例是默认实例还是命名实例以及它是独立实例还是故障转移群集实例 (FCI)，如下所示：  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 此地址由以下部分组成：  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例所在的计算机系统的 NetBIOS 名称。 此计算机必须是一个 WSFC 节点。  
  
 *FCI_network_name*  
 用于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集的网络名称。 如果服务器实例作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移伙伴参与，则使用此名称。 执行 SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)在 FCI 上服务器实例将返回其整个*FCI_network_name*[\\*instance_name*] 字符串 (即完整副本名称）。  
  
 *instance_name*  
 是的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由承载*system_name*或*FCI_network_name* HADR 且服务已启用。 对于默认服务器实例， *instance_name* 是可选的。 此实例名不区分大小写。 在独立服务器实例中，此值名称是通过执行选择返回的值相同[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)。  
  
 \  
 是仅当指定时，才使用分隔符*instance_name*，以便使其从分离*system_name*或*FCI_network_name*。  
  
 有关 WSFC 节点和服务器实例的先决条件的信息，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **=**TCP**://***系统地址***:***端口*  
 指定的 URL 路径[数据库镜像端点](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]承载可用性副本，在你当前的 REPLICA ON 子句中定义。  
  
 ENDPOINT_URL 子句是必需的。 有关详细信息，请参阅 [在添加或修改可用性副本时指定终结点 URL (SQL Server)](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)配置服务器实例时遇到的典型问题。  
  
 TCP**://***系统地址***:***端口*  
 指定一个 URL，它用于指定端点 URL 或只读路由 URL。 URL 参数如下所示：  
  
 *system-address*  
 一个字符串，例如系统名称、完全限定的域名或 IP 地址，它们明确标识了目标计算机系统。  
  
 *port*  
 是与伙伴服务器实例的镜像端点关联的端口号（对于 ENDPOINT_URL 选项）或服务器实例的[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用的端口号（对于 READ_ONLY_ROUTING_URL 选项）。  
  
 AVAILABILITY_MODE  **=**  {{SYNCHRONOUS_COMMIT 的情况下 |ASYNCHRONOUS_COMMIT |CONFIGURATION_ONLY}  
 Synchronous_commit 的情况下或 ASYNCHRONOUS_COMMIT 指定是主副本等待辅助副本确认磁盘之前的主副本可以提交事务给定主计算机上的日志记录强化 （写入）数据库。 针对同一主副本上不同数据库的事务可以单独提交。 SQL Server 自 2017 年 CU 1 引入了 CONFIGURATION_ONLY。 CONFIGURATION_ONLY 副本仅适用于可用性组用于 CLUSTER_TYPE = 外部或 CLUSTER_TYPE = NONE。 
  
 SYNCHRONOUS_COMMIT  
 指定主副本等待提交事务，直到它们已进行强化此辅助副本 （同步提交模式）。 您可以为最多三个副本（包括主副本）指定 SYNCHRONOUS_COMMIT。  
  
 ASYNCHRONOUS_COMMIT  
 指定主副本无需等待此辅助副本对日志进行硬编码（同步提交可用性模式）即可提交事务。 您可以为最多五个可用性副本（包括主副本）指定 ASYNCHRONOUS_COMMIT。  

 CONFIGURATION_ONLY 指定主副本同步到此副本上的主数据库提交可用性组配置元数据。 副本将不包含用户数据。 此选项：

- 可以在任何版本的 SQL Server，包括 Express Edition 上承载。
- 需要镜像端点的 CONFIGURATION_ONLY 副本类型的数据`WITNESS`。
- 不能更改。
- 不是有效时`CLUSTER_TYPE = WSFC`。 

   有关详细信息，请参阅[配置唯一副本](../../linux/sql-server-linux-availability-group-ha.md)。
  
 AVAILABILITY_MODE 子句是必需的。 有关详细信息，请参阅 [可用性模式（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)或 PowerShell 来对 AlwaysOn 可用性组执行计划的手动故障转移或强制的手动故障转移（强制故障转移）。  
  
 FAILOVER_MODE  **=**  {自动 |手动}  
 指定您要定义的可用性副本的故障转移模式。  
  
 AUTOMATIC  
 启用自动故障转移。 仅在您还指定了 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 的情况下，才支持此选项。 您可以为最多两个可用性副本（包括主副本）指定 AUTOMATIC。  
  
> [!NOTE]  
>  SQL Server 故障转移群集实例 (FCI) 不支持通过可用性组来自动进行故障转移，因此，只能为手动故障转移配置任何由 FCI 承载的可用性副本。  
  
 MANUAL  
 启用计划的手动故障转移或强制手动故障转移 (通常称为*强制故障转移*) 由数据库管理员。  
  
 FAILOVER_MODE 子句是必需的。 在不同条件下支持两种手动故障转移：没有数据丢失的手动故障转移和强制故障转移（可能丢失数据）。 有关详细信息，请参阅 [故障转移和故障转移模式（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)概念。  
  
 SEEDING_MODE  **=**  {自动 |手动}  
 指定如何最初设定种子的辅助副本。  
  
 AUTOMATIC  
 启用直接的种子设定。 此方法通过网络设定种子的辅助副本。 此方法不需要你备份和还原主数据库副本上的副本。  
  
> [!NOTE]  
>  为直接种子设定，则必须允许数据库创建每个辅助副本上通过调用**ALTER AVAILABILITY GROUP**与**GRANT CREATE ANY DATABASE**选项。  
  
 MANUAL  
 指定手动种子设定的 （默认值）。 此方法要求你在主副本上创建数据库的备份并手动还原辅助副本上的该备份。  
  
 BACKUP_PRIORITY  **=** *n*  
 指定相对于同一可用性组中的其他副本，在此副本上执行备份的优先级。 该值是范围 0..100 中的整数。 这些值将具有以下含义：  
  
-   1..100 表示可被选择来执行备份的可用性副本。 1 表示最低优先级，100 表示最高优先级。 如果 BACKUP_PRIORITY = 1，则只有在没有更高的优先级可用性副本当前可用的情况下，才会选择可用性副本来执行备份。  
  
-   0 指示此可用性副本不针对执行备份操作。 例如，这对于您永远不希望备份故障转移到的远程可用性副本十分有用。  
  
 有关详细信息，请参阅 [活动辅助副本：辅助副本备份（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)概念。  
  
 SECONDARY_ROLE **(** ... **)**  
 指定如果此可用性副本当前拥有辅助角色会生效的特定于角色的设置 （即，只要它是一个辅助副本）。 在括号内指定一个或两个辅助角色选项。 如果指定两个选项，则使用以逗号分隔的列表。  
  
 辅助角色选项如下所示：  
  
 ALLOW_CONNECTIONS  **=**  {否 |READ_ONLY |所有}  
 指定给定的可用性副本（正在执行辅助角色，也就是充当辅助副本）的数据库是否可以接受来自客户端的连接，可以是以下之一：  
  
 是  
 不允许与此副本的辅助数据库的用户连接。 它们不可用于读访问。 这是默认行为。  
  
 READ_ONLY  
 仅允许连接到其中的应用程序意向属性设置为辅助副本中的数据库**ReadOnly**。 有关此属性的详细信息，请参阅 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 ALL  
 允许针对辅助副本中的数据库的所有连接进行只读访问。  
  
 有关详细信息，请参阅 [活动辅助副本：可读辅助副本（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)概念。  
  
 READ_ONLY_ROUTING_URL **=**TCP**://***系统地址***:***端口*  
 指定要用于此可用性副本的路由读意向连接请求的 URL。 这是 SQL Server 数据库引擎侦听的 URL。 通常，SQL Server 数据库引擎的默认实例侦听 TCP 端口 1433。  
  
 对于命名实例，你可以通过查询中获取的端口号**端口**和**type_desc**列[sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)动态管理视图。 服务器实例使用 Transact SQL 侦听器 (**type_desc = TSQL**)。  
  
 有关计算副本的只读路由 URL 的详细信息，请参阅[计算为 Alwayson 的 read_only_routing_url](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx)。  
  
> [!NOTE]  
>  对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的命名实例，应将 Transact-SQL 侦听器配置为使用特定端口。 有关详细信息，请参阅[将服务器配置为侦听特定 TCP 端口（SQL Sever 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
 PRIMARY_ROLE **(** ... **)**  
 指定如果此可用性副本当前拥有主角色生效的特定于角色的设置 （即，只要它是主副本）。 在括号内指定一个或两个主角色选项。 如果指定两个选项，则使用以逗号分隔的列表。  
  
 主角色选项如下所示：  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE |所有}  
 指定给定的可用性副本（正在执行主要角色，也就是充当主副本）的数据库可以接受的来自客户端的连接类型，可以是以下之一：  
  
 READ_WRITE  
 不允许 Application Intent 连接属性设置为 **ReadOnly** 的连接。  在 Application Intent 属性设置为 **ReadWrite** 或者未设置 Application Intent 连接属性时，将允许连接。 有关 Application Intent 连接属性的详细信息，请参阅 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 ALL  
 主副本中的数据库允许所有连接。 这是默认行为。  
  
 READ_ONLY_ROUTING_LIST  **=**  { **(**\<server_instance > [ **，**...*n* ] **)** |NONE} 指定承载此可用性组在辅助角色下运行时满足以下要求的可用性副本的服务器实例的以逗号分隔列表：  
  
-   被配置为允许所有连接或只读连接（参阅上文 SECONDARY_ROLE 选项的 ALLOW_CONNECTIONS 参数）。  
  
-   定义了只读路由 URL（参阅上文 SECONDARY_ROLE 选项的 READ_ONLY_ROUTING_URL 参数）。  
  
 READ_ONLY_ROUTING_LIST 的值如下：  
  
 \<server_instance > 指定的实例的地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它是在辅助角色下运行时是可读的辅助副本的副本的主机。  
  
 使用逗号分隔列表来指定可能承载可读的辅助副本的所有服务器实例。 只读路由将遵循在哪一台服务器实例列表中指定的顺序。 如果在副本的只读路由列表中包含副本的宿主服务器实例，通常将此服务器实例放在列表末尾比较好，这样在一个辅助副本可用时读意向连接将访问它。  
  
 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，你可以在可读辅助副本之间的读意向请求进行负载平衡。 这可以通过将副本放在嵌套的一组只读路由列表中的括号中指定。 有关详细信息和示例，请参阅[在只读副本间配置负载平衡](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。  
  
 无  
 指定此可用性副本时主副本，只读路由不支持。 这是默认行为。  
  
 SESSION_TIMEOUT  **=**  *整数*  
 以秒为单位指定会话超时期限。 如果不指定此选项，则在默认情况下，超时期限为 10 秒。 最小值为 5 秒。  
  
> [!IMPORTANT]  
>  我们建议您将超时期限保持为 10 秒或更长。  
  
 有关会话超时期限的详细信息，请参阅[概述的 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 上的可用性组  
 指定构成的两个可用性组*分布式的可用性组*。 每个可用性组是一部分自己 Windows Server 故障转移群集 (WSFC)。 当你创建分布式的可用性组时，当前的 SQL Server 实例上的可用性组将成为主要可用性组。 第二个可用性组将成为次要可用性组。  
  
 你需要次要可用性组加入分布式的可用性组。 有关详细信息，请参阅 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell 将次要副本添加到现有的 AlwaysOn 可用性组。  
  
 \<ag_name > 指定构成一个可用性组的名称的分布式的可用性组的一半。  
  
 侦听器**=**TCP**://***系统地址***:***端口*  
 指定与可用性组关联的侦听程序的 URL 路径。  
  
 侦听器子句是必需的。  
  
 TCP**://***系统地址***:***端口*  
 与可用性组侦听器指定的 URL。 URL 参数如下所示：  
  
 *system-address*  
 是一个字符串，例如系统名称、 完全限定的域名或 IP 地址，明确标识侦听器。  
  
 *port*  
 是与可用性组的镜像终结点相关联的端口号。 请注意，这不是侦听器的端口。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT 的情况下 |ASYNCHRONOUS_COMMIT |CONFIGURATION_ONLY}  
 指定是否要等待的时间要确认磁盘之前的主副本可以提交事务在给定的主数据库上的日志记录强化 （写入） 的次要可用性组主副本。  
  
 SYNCHRONOUS_COMMIT  
 指定主副本等待提交事务，直到它们已进行强化次要可用性组。 你可以为最多两个可用性组，包括主要可用性组指定 synchronous_commit 的情况。  
  
 ASYNCHRONOUS_COMMIT  
 指定主副本提交事务，而不等待此次要可用性组强制写入日志。 你可以为最多两个可用性组，包括主要可用性组指定 ASYNCHRONOUS_COMMIT。  
  
 AVAILABILITY_MODE 子句是必需的。  
  
 FAILOVER_MODE  **=**  {手动}  
 指定分布式的可用性组的故障转移的模式。  
  
 MANUAL  
 启用计划的手动故障转移或强制手动故障转移 (通常称为*强制故障转移*) 由数据库管理员。  
  
 FAILOVER_MODE 子句是必需的并为手动的唯一选项。 不支持自动故障转移到次要可用性组。  
  
 SEEDING_MODE  **=**  {自动 |手动}  
 指定如何最初设定种子次要可用性组。  
  
 AUTOMATIC  
 启用直接的种子设定。 此方法通过网络种子次要可用性组。 此方法不需要你备份和还原次要可用性组的副本上的主数据库的副本。  
  
 MANUAL  
 指定手动种子设定的 （默认值）。 此方法要求你在主副本上创建数据库的备份并手动还原该备份上的次要可用性组副本。  
  
 侦听器*dns_name***(** \<listener_option > **)**定义此新的可用性组侦听器可用性组。 LISTENER 是一个可选参数。  
  
> [!IMPORTANT]  
>  在创建第一个侦听器之前，我们强烈建议你阅读[创建或配置可用性组侦听器 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  为给定可用性组创建侦听器后，我们强烈建议您执行以下操作：  
>   
>  -   请求您的网络管理员将该侦听器的 IP 地址保留为专用。  
> -   将该侦听器的 DNS 主机名提供给应用程序开发人员，以便在请求与此可用性组的客户端连接时用于连接字符串中。  
  
 *dns_name*  
 指定可用性组侦听器的 DNS 主机名。 在域和 NetBIOS 中，侦听器的 DNS 名称必须唯一。  
  
 *dns_name*是一个字符串值。 该名称只能包含字母数字字符、破折号 (-) 和连字符 (_)，顺序不分先后。 DNS 主机名不区分大小写。 最大长度为 63 个字符。  
  
 我们建议您指定一个有意义的字符串。 例如，对于名为 `AG1`的可用性组，有意义的 DNS 主机名将是 `ag1-listener`。  
  
> [!IMPORTANT]  
>  NetBIOS 只识别 dns_name 中的前 15 个字符。 如果你有两个 WSFC 群集均由相同的 Active Directory 控制，并且你尝试在名称超过 15 个字符和相同的 15 字符前缀使用两个群集中创建可用性组侦听器，错误报告虚拟网络名称可能不能将资源联机。 有关 DNS 名称的前缀命名规则的信息，请参阅 [分配域名](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)。  
  
 \<listener_option > 侦听器采用下列任一\<listener_option > 选项： 
  
 与 DHCP [ON { **(***four_part_ipv4_address***'，'***four_part_ipv4_mask***)** }]  
 指定可用性组侦听器使用动态主机配置协议 (DHCP)。  （可选） 使用的 ON 子句标识在其创建此侦听器的网络。 DHCP 仅限于单个子网用于每个服务器实例承载可用性组中的副本。  
  
> [!IMPORTANT]  
>  不建议在生产环境中使用 DHCP。 如果停止工作且 DHCP IP 租期已到，则需要额外的时间来注册与侦听器 DNS 名称相关联且影响客户端连接的新 DHCP 网络 IP 地址。 但是，DHCP 适合用于设置开发和测试环境以验证可用性组的基本功能并适合与应用程序集成。  
  
 例如：  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 使用 IP **(** { **(***four_part_ipv4_address***'，'***four_part_ipv4_mask* **')** | **(***ipv6_address***)** } [ **，** ... *n*  ] **)** [ **，**端口 **=**  *listener_port*]  
 指定，而不是使用 DHCP，可用性组侦听器使用一个或多个静态 IP 地址。 若要跨多个子网创建一个可用性组，每个子网均需要一个侦听器配置中的静态 IP 地址。 对于某一给定子网，静态 IP 地址可以是 IPv4 地址或 IPv6 地址。 与网络管理员联系以获取每个承载的副本的新的可用性组的子网的静态 IP 地址。  
  
 例如：  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 指定可用性组侦听器的由四部分组成的 IPv4 地址。 例如， `10.120.19.155`。  
  
 *four_part_ipv4_mask*  
 指定可用性组侦听器的由四部分组成的 IPv4 掩码。 例如， `255.255.254.0`。  
  
 *ipv6_address*  
 指定可用性组侦听器的 IPv6 地址。 例如， `2001::4898:23:1002:20f:1fff:feff:b3a3`。  
  
 端口 **=**  *listener_port*  
 指定的端口号-*listener_port*-用于通过由 WITH IP 子句指定一个可用性组侦听器。 PORT 是可选的。  
  
 支持默认端口号 1433。 但出于安全考虑，我们建议使用其他端口号。  
  
 例如： `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>先决条件和限制  
 有关创建可用性组的先决条件的信息，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 有关限制上的可用性组 TRANSACT-SQL 语句的信息，请参阅[概述的 TRANSACT-SQL 语句的 Alwayson 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. 针对辅助副本、灵活的故障转移策略和连接访问配置备份  
 下面的示例为两个用户数据库 `MyAg` 和 `ThisDatabase` 创建了名为 `ThatDatabase` 的可用性组。 下表总结了为作为一个整体为可用性组设置的选项指定的值。  
  
|组选项|设置|Description|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|此自动备份首选项指示应在辅助副本上发生备份，但在主副本是唯一联机的副本时（这是默认行为）除外。 为使 AUTOMATED_BACKUP_PREFERENCE 设置生效，您需要编写可用性数据库上备份作业的脚本，以便考虑自动备份首选项。|  
|FAILURE_CONDITION_LEVEL|3|此失败条件级别设置指定在发生了严重的 SQL Server 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时应启动自动故障转移。|  
|HEALTH_CHECK_TIMEOUT|600000|此运行状况检查超时值，是 60 秒，指定，WSFC 群集会等到 60000 毫秒[sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程来返回有关服务器实例的服务器运行状况信息托管群集假设主机服务器实例为慢速或挂起之前自动同步提交副本。 （默认值为 30000 毫秒。）|  
  
 三个可用性副本将由名为 `COMPUTER01`、`COMPUTER02` 和 `COMPUTER03` 的计算机上的默认服务器实例承载。 下表总结了为每个副本的副本选项指定的值。  
  
|副本选项|`COMPUTER01` 上的设置|`COMPUTER02` 上的设置|`COMPUTER03` 上的设置|Description|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP: / /*COMPUTER01:5022*|TCP: / /*COMPUTER02:5022*|TCP: / /*COMPUTER03:5022*|在这个示例中，系统处于相同的域中，因此，端点 URL 可以使用计算机的名称作为系统地址。|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|两个副本使用同步提交模式。 同步时，它们支持故障转移而不会丢失数据。 第三个副本，将使用异步提交可用性模式。|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|同步提交副本支持自动故障转移和计划的手动故障转移。 同步提交可用性模式副本支持仅限强制的手动故障转移。|  
|BACKUP_PRIORITY|30|30|90|与同步提交副本相比，将更高的优先级 90 分配给异步提交副本。 备份往往在承载异步提交副本的服务器实例上发生。|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|只有异步提交副本作为可读的辅助副本。<br /><br /> 指定计算机名称和默认数据库引擎端口号 (1433)。<br /><br /> 此参数是可选的。|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|在主角色中，所有副本都拒绝读意向连接尝试。<br /><br /> 如果本地副本在辅助角色下运行时读意向连接请求路由到 COMPUTER03。 当该副本在主角色下运行时，禁用只读路由。<br /><br /> 此参数是可选的。|  
|SESSION_TIMEOUT|10|10|10|此示例指定默认会话超时值 (10)。 此参数是可选的。|  
  
 最后，该示例指定可选的 LISTENER 子句，以便为新的可用性组创建可用性组侦听器。 将为此侦听器指定唯一的 DNS 名称 `MyAgListenerIvP6`。 两个副本位于不同的子网，因此侦听器必须使用静态 IP 地址。 对于这两个可用性副本中的每一个，WITH IP 子句都指定一个将使用 IPv6 格式的静态 IP 地址 `2001:4898:f0:f00f::cf3c` 和 `2001:4898:e0:f213::4ce2`。 此示例还指定使用可选的 PORT 参数来将端口 `60173` 指定为侦听器端口。  
  
```SQL
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABIIITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建可用性组 (Transact-SQL)](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40;Transact SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [Alwayson 故障排除可用性组配置 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

