---
title: "ALTER AVAILABILITY GROUP (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/02/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d9f18ee709fde7c9f239b08f553eaf43fad6e9d2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  更改现有 Always On 可用性组中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 只有当前主副本支持大多数 ALTER AVAILABILITY GROUP 参数。 但是，只有辅助副本支持 JOIN、FAILOVER 和 FORCE_FAILOVER_ALLOW_DATA_LOSS 参数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```SQL  
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   | ADD LISTENER ‘dns_name’ ( <add_listener_option> )  
   | MODIFY LISTENER ‘dns_name’ ( <modify_listener_option> )  
   | RESTART LISTENER ‘dns_name’  
   | REMOVE LISTENER ‘dns_name’  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
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
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>参数  
 *group_name*  
 指定新可用性组的名称。 *group_name*必须为有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符，和它必须是唯一的 WSFC 群集中的所有可用性组。  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {主 |SECONDARY_ONLY |辅助 |无}  
 指定在选择执行备份的位置时有关备份作业应该如何评估主副本的首选项。 您可以编写给定备份作业的脚本，以便纳入自动备份首选项。 务必了解首选项不会强制执行由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因此它对即席备份没有任何影响。  
  
 仅在主副本上受支持。  
  
 这些值如下所示：  
  
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
>  不会强制实施 AUTOMATED_BACKUP_PREFERENCE 设置。 对此首选项的解释依赖于您为给定可用性组中的数据库撰写作业脚本的逻辑（如果有）。 自动备份首选项设置对即席备份没有任何影响。 有关详细信息，请参阅[可用性副本 &#40; 上配置备份SQL server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  若要查看现有可用性组的自动备份首选项，请选择**automated_backup_preference**或**automated_backup_preference_desc**列[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目录视图。 此外， [sys.fn_hadr_backup_is_preferred_replica &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)可以用于确定为首选备份副本。  此函数始终对至少一个副本返回 1（即使 `AUTOMATED_BACKUP_PREFERENCE = NONE`）。  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 指定将为此可用性组触发自动故障转移的失败条件。 FAILURE_CONDITION_LEVEL 在组级别设置，但仅对配置为同步提交可用性模式的可用性副本 (AVAILIBILITY_MODE  **=**  synchronous_commit 的情况下)。 此外，故障条件可以触发自动故障转移，仅当主要和辅助副本配置为使用自动故障转移模式 (FAILOVER_MODE  **=** 自动) 并且辅助副本当前与主副本同步。  
  
 仅在主副本上受支持。  
  
 失败条件级别的范围 (1–5) 是从最少限制的级别 1 到最多限制的级别 5。 给定的条件级别包含限制较少的级别的所有。 因此，最严格的条件级别 5 包含四个限制较少的级别 (1-4)，级别 4 包含级别 1-3，依此类推。 下表描述对应于每个级别的失败条件。  
  
|Level|失败条件|  
|-----------|-----------------------|  
|1|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务停止。<br /><br /> 因为没有从服务器实例接收到 ACK，连接到 WSFC 群集的可用性组的租期到期。 有关详细信息，请参阅 [工作原理：SQL Server AlwaysOn 租约超时](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)。|  
|2|指定在发生以下任何情况时应启动自动故障转移：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例未连接到群集，并且超出了可用性组的用户指定的 HEALTH_CHECK_TIMEOUT 阈值。<br /><br /> 可用性副本处于失败状态。|  
|3|指定在发生了严重的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时应启动自动故障转移。<br /><br /> 这是默认行为。|  
|4|指定在发生了中等程度的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部错误（例如在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部资源池中出现持久的内存不足情况）时应启动自动故障转移。|  
|5|指定在出现任何符合的失败条件时应启动自动故障转移，这些失败条件包括：<br /><br /> SQL 引擎的工作线程耗尽。<br /><br /> 检测到无法解决的死锁。|  
  
> [!NOTE]  
>  缺乏由的实例的响应[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为客户端请求不与可用性组。  
  
 FAILURE_CONDITION_LEVEL 和 HEALTH_CHECK_TIMEOUT 值中，定义*灵活的故障转移策略*为给定的组。 此灵活的故障转移策略向您提供对必须导致自动故障转移的条件的精确控制。 有关详细信息，请参阅[的自动故障转移的可用性组 &#40; 灵活的故障转移策略SQL server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *毫秒*  
 为指定的等待时间 （以毫秒为单位） [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系统存储过程来返回服务器运行状况信息之前 WSFC 群集假定服务器实例很慢或会挂起。 HEALTH_CHECK_TIMEOUT 在组级别设置，但仅对配置为使用同步提交可用性模式以及自动故障转移的可用性副本 (AVAILIBILITY_MODE  **=** 同步_COMMIT)。  此外，运行状况检查超时可以触发自动故障转移，仅当主要和辅助副本配置为使用自动故障转移模式 (FAILOVER_MODE  **=** 自动) 数据库与辅助数据库副本当前与主副本同步。  
  
 默认的 HEALTH_CHECK_TIMEOUT 值为 30000 毫秒（30 秒）。 最小值为 15000 毫秒（15 秒），最大值为 4294967295 毫秒。  
  
 仅在主副本上受支持。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 在数据库级别不执行运行状况检查。  
  
 DB_FAILOVER  **=**  {ON |关闭}  
 指定当主副本上的数据库处于脱机状态时要执行的响应。 可用性组中数据库联机以外的任何状态设置为 ON 时，将触发自动故障转移。 当此选项设置为 OFF 时，仅实例的运行状况用于触发自动故障转移。  
 
 有关此设置的详细信息，请参阅[数据库级别运行状况检测选项](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 

 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 自 2017 年 1 中引入。 用于设置最小同步提交主提交事务之前所需的辅助副本数。 保证 SQL Server 事务将等待，直到事务日志更新辅助副本的最小数量。 默认值为 0，这将使 SQL Server 2016 相同的行为。 最小值为 0。 最大值为减 1 的副本数目。 此选项与在同步提交模式下的副本。 当副本在同步提交模式下时，写入主副本上的等待，直到同步辅助副本上的写入都将提交到副本数据库事务日志。 如果承载辅助同步副本的 SQL 服务器停止响应，SQL Server 承载主副本将标记该辅助副本未同步，并且继续。 当无响应的数据库重新联机时它将处于"未同步"状态和副本将被标记为不正常，直到主可以使其同步试。 此设置可保证之前的最小副本数已提交的每个事务,，主副本将不会继续。 如果不可用的最小副本数则在主计算机上的提交将失败。 对于群集类型`EXTERNAL`可用性组添加到群集资源时更改的设置。 请参阅[可用性组配置的高可用性和数据保护](../../linux/sql-server-linux-availability-group-ha.md)。
  
 将数据库添加*database_name*  
 指定要添加到可用性组的一个或多个用户数据库的列表。 这些数据库必须位于承载当前主副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上。 您可以为一个可用性组指定多个数据库，但每个数据库只能属于一个可用性组。 有关类型的可用性组都可以支持的数据库的信息，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). 若要了解哪些本地数据库已属于某一可用性组，请参阅**replica_id**中的列[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。  
  
 仅在主副本上受支持。  
  
> [!NOTE]  
>  在创建可用性组后，将需要连接到承载辅助副本的每个服务器实例，然后准备每个辅助数据库并将它们加入可用性组。 有关详细信息，请参阅本主题后面的 [启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
 删除数据库*database_name*  
 从可用性组中删除指定的主数据库和相应的辅助数据库。 仅在主副本上受支持。  
  
 建议跟进后从可用性组中删除可用性数据库有关的信息，请参阅[从可用性组 &#40; 中删除主数据库SQL server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 ADD REPLICA ON  
 指定一到八个 SQL Server 实例以便在可用性组中承载辅助副本。  通过在每个副本的服务器实例地址后追加 WITH (…) 子句来指定每个副本。  
  
 仅在主副本上受支持。  
  
 您需要将每个新的辅助副本联接到可用性组。 有关详细信息，请参阅本节后面对 JOIN 选项的说明。  
  
 \<server_instance>  
 指定的实例的地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]副本的主机。 地址格式依赖于该实例是默认实例还是命名实例以及它是独立实例还是故障转移群集实例 (FCI)。 语法如下：  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 此地址由以下部分组成：  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例所在的计算机系统的 NetBIOS 名称。 此计算机必须是一个 WSFC 节点。  
  
 *FCI_network_name*  
 用于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集的网络名称。 如果服务器实例作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移伙伴参与，则使用此名称。 执行 SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)在 FCI 上服务器实例将返回其整个*FCI_network_name*[\\*instance_name*] 字符串 (即完整副本名称）。  
  
 *instance_name*  
 是的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由承载*system_name*或*FCI_network_name*并具有始终在启用的。 对于默认服务器实例，*instance_name* 是可选的。 此实例名不区分大小写。 在独立服务器实例中，此值名称是通过执行选择返回的值相同[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)。  
  
 \  
 是仅当指定时，才使用分隔符*instance_name*，以便使其从分离*system_name*或*FCI_network_name*。  
  
 有关 WSFC 节点和服务器实例的先决条件的信息，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL = TCP: / /*系统地址*:*端口*  
 指定的 URL 路径[数据库镜像端点](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将承载要添加或修改的可用性副本。  
  
 ENDPOINT_URL 在 ADD REPLICA ON 子句中是必需的，在 MODIFY REPLICA ON 子句中是可选的。  有关详细信息，请参阅[在添加或修改可用性副本时指定终结点 URL (SQL Server)](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)。  
  
 **'**TCP**://***system-address***:***port***'**  
 指定一个 URL，它用于指定端点 URL 或只读路由 URL。 URL 参数如下所示：  
  
 *system-address*  
 一个字符串，例如系统名称、完全限定的域名或 IP 地址，它们明确标识了目标计算机系统。  
  
 *port*  
 是与服务器实例的镜像端点关联的端口号（对于 ENDPOINT_URL 选项）或服务器实例的[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用的端口号（对于 READ_ONLY_ROUTING_URL 选项）。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT 的情况下 |ASYNCHRONOUS_COMMIT |CONFIGURATION_ONLY}  
 指定在主副本可以在给定主数据库上提交事务前，是否必须等待辅助副本确认日志记录硬编码（写入）到磁盘。 针对同一主副本上不同数据库的事务可以单独提交。  
  
 SYNCHRONOUS_COMMIT  
 指定主副本已在此辅助副本上进行硬编码（同步提交模式）前，将等待提交事务。 您可以为最多三个副本（包括主副本）指定 SYNCHRONOUS_COMMIT。  
  
 ASYNCHRONOUS_COMMIT  
 指定主副本无需等待此辅助副本对日志进行硬编码（同步提交可用性模式）即可提交事务。 您可以为最多五个可用性副本（包括主副本）指定 ASYNCHRONOUS_COMMIT。  

 CONFIGURATION_ONLY 指定主副本同步到此副本上的主数据库提交可用性组配置元数据。 副本将不包含用户数据。 此选项：

- 可以在任何版本的 SQL Server，包括 Express Edition 上承载。
- 需要镜像端点的 CONFIGURATION_ONLY 副本类型的数据`WITNESS`。
- 不能更改。
- 不是有效时`CLUSTER_TYPE = WSFC`。 

   有关详细信息，请参阅[配置唯一副本](../../linux/sql-server-linux-availability-group-ha.md)。
    
 AVAILABILITY_MODE 在 ADD REPLICA ON 子句中是必需的，在 MODIFY REPLICA ON 子句中是可选的。 有关详细信息，请参阅 [可用性模式（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)。  
  
 FAILOVER_MODE  **=**  {自动 |手动}  
 指定您要定义的可用性副本的故障转移模式。  
  
 AUTOMATIC  
 启用自动故障转移。 仅在指定 VAILABILITY_MODE = SYNCHRONOUS_COMMIT 的情况下才支持 AUTOMATIC。 您可以为最多两个可用性副本（包括主副本）指定 AUTOMATIC。  
  
> [!NOTE]  
>  SQL Server 故障转移群集实例 (FCI) 不支持通过可用性组来自动进行故障转移，因此，只能为手动故障转移配置任何由 FCI 承载的可用性副本。  
  
 MANUAL  
 允许手动故障转移或强制手动故障转移 (*强制故障转移*) 由数据库管理员。  
  
 FAILOVER_MODE 在 ADD REPLICA ON 子句中是必需的，在 MODIFY REPLICA ON 子句中是可选的。 存在在不同条件下支持的两种手动故障转移，没有数据丢失的手动故障转移和强制故障转移（可能存在数据丢失）。  有关详细信息，请参阅 [故障转移和故障转移模式（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)概念。  
  
 SEEDING_MODE  **=**  {自动 |手动}  
 指定如何辅助副本会进行初始种子设定。  
  
 AUTOMATIC  
 启用直接的种子设定。 此方法将通过网络为种子的辅助副本。 此方法不需要你备份和还原主数据库副本上的副本。  
  
> [!NOTE]  
>  为直接种子设定，则必须允许数据库创建每个辅助副本上通过调用**ALTER AVAILABILITY GROUP**与**GRANT CREATE ANY DATABASE**选项。  
  
 MANUAL  
 指定手动种子设定的 （默认值）。 此方法要求你在主副本上创建数据库的备份并手动还原辅助副本上的该备份。  
  
 BACKUP_PRIORITY **=***n*  
 指定相对于同一可用性组中的其他副本，在此副本上执行备份的优先级。 该值是范围 0..100 中的整数。 这些值将具有以下含义：  
  
-   1..100 表示可被选择来执行备份的可用性副本。 1 表示最低优先级，100 表示最高优先级。 如果 BACKUP_PRIORITY = 1，则只有在没有更高的优先级可用性副本当前可用的情况下，才会选择可用性副本来执行备份。  
  
-   0 表示此可用性副本将永远不会被选择执行备份。 例如，这对于您永远不希望备份故障转移到的远程可用性副本十分有用。  
  
 有关详细信息，请参阅 [活动辅助副本：辅助副本备份（AlwaysOn 可用性组）](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)概念。  
  
 SECONDARY_ROLE **(** ... **)**  
 指定在此可用性副本当前拥有辅助角色（即它是辅助副本）时将要生效的角色特有设置。 在括号内指定一个或两个辅助角色选项。 如果指定两个选项，则使用以逗号分隔的列表。  
  
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
  
 READ_ONLY_ROUTING_URL **=**TCP**://***系统地址***:***端口*****  
 指定要用于此可用性副本的路由读意向连接请求的 URL。 这是 SQL Server 数据库引擎侦听的 URL。 通常，SQL Server 数据库引擎的默认实例侦听 TCP 端口 1433。  
  
 对于命名实例，你可以通过查询中获取的端口号**端口**和**type_desc**列[sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)动态管理视图。 服务器实例使用 Transact SQL 侦听器 (**type_desc = TSQL**)。  
  
 有关计算可用性副本的只读路由 URL 的详细信息，请参阅[计算为 Alwayson 的 read_only_routing_url](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)。  
  
> [!NOTE]  
>  对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的命名实例，应将 Transact-SQL 侦听器配置为使用特定端口。 有关详细信息，请参阅[将服务器配置为侦听特定 TCP 端口（SQL Sever 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
 PRIMARY_ROLE **(** ... **)**  
 指定在此可用性副本当前拥有主角色（即它是主副本）时将要生效的角色特有设置。 在括号内指定一个或两个主角色选项。 如果指定两个选项，则使用以逗号分隔的列表。  
  
 主角色选项如下所示：  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE |所有}  
 指定给定的可用性副本（正在执行主要角色，也就是充当主副本）的数据库可以接受的来自客户端的连接类型，可以是以下之一：  
  
 READ_WRITE  
 不允许 Application Intent 连接属性设置为 **ReadOnly** 的连接。  在 Application Intent 属性设置为 **ReadWrite** 或者未设置 Application Intent 连接属性时，将允许连接。 有关 Application Intent 连接属性的详细信息，请参阅 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 ALL  
 主副本中的数据库允许所有连接。 这是默认行为。  
  
 READ_ONLY_ROUTING_LIST  **=**  { **(**\<server_instance > [ **，**...*n* ] **)** |无}  
 指定一个以逗号分隔的服务器实例列表，这些实例承载在以辅助角色运行时满足以下要求的此可用性组的可用性副本：  
  
-   被配置为允许所有连接或只读连接（参阅上文 SECONDARY_ROLE 选项的 ALLOW_CONNECTIONS 参数）。  
  
-   定义了只读路由 URL（参阅上文 SECONDARY_ROLE 选项的 READ_ONLY_ROUTING_URL 参数）。  
  
 READ_ONLY_ROUTING_LIST 的值如下：  
  
 \<server_instance>  
 指定承载可用性副本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的地址，该副本在以辅助角色运行时是可读辅助副本。  
  
 使用以逗号分隔的列表指定可能承载可读辅助副本的所有服务器实例。 只读路由将遵循在列表中指定服务器实例的顺序。 如果在副本的只读路由列表中包含副本的宿主服务器实例，通常将此服务器实例放在列表末尾比较好，这样在一个辅助副本可用时读意向连接将访问它。  
  
 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，你可以在可读辅助副本之间的读意向请求进行负载平衡。 这可以通过将副本放在嵌套的一组只读路由列表中的括号中指定。 有关详细信息和示例，请参阅[在只读副本间配置负载平衡](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。  
  
 无  
 指定此可用性副本为主副本时将不支持只读路由。 这是默认行为。 与 MODIFY REPLICA ON 一起使用时，此值将禁用现有列表（如果有）。  
  
 SESSION_TIMEOUT **= * * * （秒)*  
 以秒为单位指定会话超时期限。 如果不指定此选项，则在默认情况下，超时期限为 10 秒。 最小值为 5 秒。  
  
> [!IMPORTANT]  
>  我们建议您将超时期限保持为 10 秒或更长。  
  
 有关会话超时期限的详细信息，请参阅[概述的 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 MODIFY REPLICA ON  
 修改可用性组的任何副本。 要修改的副本列表包含每个副本的服务器实例地址和 WITH (…) 子句。  
  
 仅在主副本上受支持。  
  
 REMOVE REPLICA ON  
 从可用性组中删除指定的辅助副本。 不能从可用性组删除当前的主副本。 在删除时，副本停止接收数据。 其辅助数据库从可用性组中删除，并且进入 RESTORING 状态。  
  
 仅在主副本上受支持。  
  
> [!NOTE]  
>  如果您在某一副本处于不可用或失败状态时删除该副本，则在其恢复联机状态时，将会发现不再属于该可用性组。  
  
 JOIN  
 导致本地服务器实例承载指定可用性组中的辅助副本。  
  
 仅在尚未加入可用性组的辅助副本上支持。  
  
 有关详细信息，请参阅[将辅助副本联接到可用性组 (SQL Server)](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
 FAILOVER  
 启动可用性组的手动故障转移，并且没有对您连接到的辅助副本的数据丢失。 您对其输入故障转移目标故障转移命令副本称为。  故障转移目标将接管主要角色，恢复各数据库的副本并且使它们作为新的主数据库处于联机状态。 以前的主副本同时转换为辅助角色，并且其数据库将成为辅助数据库且立即挂起。 在发生一系列故障后，这些角色可能来回切换。  
  
 仅在当前与主副本同步的同步提交辅助副本上支持。 请注意，对于要同步的辅助副本，主副本也必须在同步提交模式下运行。  
  
> [!NOTE]  
>  故障转移命令将在故障转移目标接受它之后立即返回。 但是，在可用性组完成故障转移之后，数据库恢复操作将以异步方式执行。  
  
 先决条件和建议执行计划的手动故障转移，有关的限制的信息，请参阅[执行的计划手动故障转移可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  强制故障转移（这可能会涉及一些数据丢失）严格来说是一种灾难恢复方法。 因此，我们强烈建议您仅在以下情况下才强制故障转移：主副本不再运行、您愿意承担丢失数据的风险并且您必须立即将服务还原到可用性组。  
  
 仅在其角色处于 SECONDARY 或 RESOLVING 状态的副本上支持。 您对其输入故障转移命令--副本称为*故障转移目标*。  
  
 强制将可用性组故障转移到故障转移目标（可能会丢失数据）。 故障转移目标将接管主要角色，恢复各数据库的副本并且使它们作为新的主数据库处于联机状态。 在剩余的任何辅助副本上，在手动恢复前每个辅助数据库都处于挂起状态。 在以前的主副本可用前，它将切换到辅助角色，并且其数据库将成为挂起的辅助数据库。  
  
> [!NOTE]  
>  故障转移命令将在故障转移目标接受它之后立即返回。 但是，在可用性组完成故障转移之后，数据库恢复操作将以异步方式执行。  
  
 先决条件和建议在可用性组中，以前的主数据库上强制故障转移和强制故障转移的效果有关的限制的信息，请参阅[执行强制手动故障转移的可用性Group &#40;SQL server&#41;](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
 ADD LISTENER **‘***dns_name***’(** \<add_listener_option> **)**  
 为此可用性组定义新的可用性组侦听器。 仅在主副本上受支持。  
  
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
>  NetBIOS 只识别 dns_name 中的前 15 个字符。 如果您的两个 WSFC 群集均由同一 Active Directory 控制，而您试图使用超过 15 个字符的名称（具有相同的 15 字符前缀）在这两个群集中创建可用性组侦听器，此时您将收到错误，报告无法使虚拟网络名称资源联机。 有关 DNS 名称的前缀命名规则的信息，请参阅 [分配域名](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)。  
  
 在加入可用性组  
 将联接到*分布式的可用性组*。 当你创建分布式的可用性组时，其中创建的群集上的可用性组是主要可用性组。 联接分布式的可用性组的可用性组是次要可用性组。  
  
 \<ag_name>  
 指定构成一个可用性组的名称的分布式的可用性组的一半。  
  
 LISTENER **='**TCP**://***system-address***:***port***'**  
 指定与可用性组关联的侦听程序的 URL 路径。  
  
 侦听器子句是必需的。  
  
 **'**TCP**://***system-address***:***port***'**  
 与可用性组侦听器指定的 URL。 URL 参数如下所示：  
  
 *system-address*  
 是一个字符串，例如系统名称、 完全限定的域名或 IP 地址，明确标识侦听器。  
  
 *port*  
 是与可用性组的镜像终结点相关联的端口号。 请注意，这不是侦听器的端口。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT 的情况下 |ASYNCHRONOUS_COMMIT}  
 指定是否要等待的时间要确认磁盘之前的主副本可以提交事务在给定的主数据库上的日志记录强化 （写入） 的次要可用性组主副本。  
  
 SYNCHRONOUS_COMMIT  
 指定主副本将等待提交事务，直到它们已进行强化次要可用性组。 你可以为最多两个可用性组，包括主要可用性组指定 synchronous_commit 的情况。  
  
 ASYNCHRONOUS_COMMIT  
 指定主副本提交事务，而不等待此次要可用性组强制写入日志。 你可以为最多两个可用性组，包括主要可用性组指定 ASYNCHRONOUS_COMMIT。  
  
 AVAILABILITY_MODE 子句是必需的。  
  
 FAILOVER_MODE  **=**  {手动}  
 指定分布式的可用性组的故障转移的模式。  
  
 MANUAL  
 启用计划的手动故障转移或强制手动故障转移 (通常称为*强制故障转移*) 由数据库管理员。  
  
 不支持自动故障转移到次要可用性组。  
  
 SEEDING_MODE **=**  {自动 |手动}  
 指定如何将最初种子次要可用性组。  
  
 AUTOMATIC  
 启用自动种子设定。 此方法将通过网络种子次要可用性组。 此方法不需要你备份和还原次要可用性组的副本上的主数据库的副本。  
  
 MANUAL  
 指定手动种子设定。 此方法要求你在主副本上创建数据库的备份并手动还原该备份上的次要可用性组副本。  
  
 在修改可用性组  
 修改任何分布式的可用性组的可用性组设置。 要修改的可用性组的列表包含可用性组名称和 WITH 每个可用性组 （...） 子句。  
  
> [!IMPORTANT]  
>  必须在主要可用性组和次要可用性组实例上重复此命令。  
  
 授予创建任意数据库  
 允许要创建代表主副本，支持直接的种子设定的数据库的可用性组 (SEEDING_MODE = AUTOMATIC)。 此参数应在每个支持直接的种子设定后该辅助数据库加入可用性组的辅助副本上运行。  需要 CREATE ANY DATABASE 权限。  
  
 拒绝创建任意数据库  
 删除可用性组能够创建代表主副本的数据库。  
  
 \<add_listener_option>  
 ADD LISTENER 采用以下选项之一：  
  
 WITH DHCP [ ON { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** } ]  
 指定可用性组侦听器将使用动态主机配置协议 (DHCP)。  或者，使用 ON 子句标识将在其上创建此侦听器的网络。 DHCP 限制为单个子网，该子网用于在可用性组中承载可用性副本的每个服务器实例。  
  
> [!IMPORTANT]  
>  不建议在生产环境中使用 DHCP。 如果停止工作且 DHCP IP 租期已到，则需要额外的时间来注册与侦听器 DNS 名称相关联且影响客户端连接的新 DHCP 网络 IP 地址。 但是，DHCP 适合用于设置开发和测试环境以验证可用性组的基本功能并适合与应用程序集成。  
  
 例如：  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** | **(‘***ipv6_address***’)** } [ **,** ...*n* ] **)** [ **,** PORT **=***listener_port* ]  
 指定可用性组侦听器将使用一个或多个静态 IP 地址，而不使用 DHCP。 若要跨多个子网创建一个可用性组，每个子网均需要一个侦听器配置中的静态 IP 地址。 对于某一给定子网，静态 IP 地址可以是 IPv4 地址或 IPv6 地址。 请与您的网络管理员联系以获取将承载新可用性组的可用性副本的每个子网的静态 IP 地址。  
  
 例如：  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 指定可用性组侦听器的由四部分组成的 IPv4 地址。 例如， `10.120.19.155`。  
  
 *four_part_ipv4_mask*  
 指定可用性组侦听器的由四部分组成的 IPv4 掩码。 例如， `255.255.254.0`。  
  
 *ipv6_address*  
 指定可用性组侦听器的 IPv6 地址。 例如， `2001::4898:23:1002:20f:1fff:feff:b3a3`。  
  
 PORT **=** *listener_port*  
 指定的端口号-*listener_port*-用于通过由 WITH IP 子句指定一个可用性组侦听器。 PORT 是可选的。  
  
 支持默认端口号 1433。 但出于安全考虑，我们建议使用其他端口号。  
  
 例如： `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
 MODIFY LISTENER **‘***dns_name***’(** \<modify_listener_option> **)**  
 修改此可用性组的现有可用性组侦听器。 仅在主副本上受支持。  
  
 \<modify_listener_option>  
 MODIFY LISTENER 采用以下选项之一：  
  
 添加 IP { **(***four_part_ipv4_address***'，'***four_part_ipv4_mask***)** | **(**dns_name*ipv6_address***')**}  
 将指定的 IP 地址添加到可用性组侦听器指定*dns_name*。  
  
 PORT **=** *listener_port*  
 请参阅本节前面对此参数的说明。  
  
 重新启动侦听器*****dns_name*****  
 重新启动与指定的 DNS 名称关联的侦听器。 仅在主副本上受支持。  
  
 删除侦听器*****dns_name*****  
 删除与指定的 DNS 名称关联的侦听器。 仅在主副本上受支持。  
  
 OFFLINE  
 使联机的可用性组脱机。 同步提交数据库没有数据丢失。  
  
 在某一可用性组脱机后，其数据库将不可用于客户端，并且您无法使该可用性组重新联机。 因此，在将可用性组资源迁移到新 WSFC 群集时，仅在 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 的跨群集迁移过程中使用 OFFLINE 选项。  
  
 有关详细信息，请参阅[执行可用性组脱机 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md).  
  
## <a name="prerequisites-and-restrictions"></a>先决条件和限制  
 有关先决条件和限制的可用性副本和在主机服务器实例和计算机上，请参阅[先决条件、 限制和建议 Always On 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 有关限制上的可用性组 TRANSACT-SQL 语句的信息，请参阅[概述的 TRANSACT-SQL 语句的 Alwayson 可用性组 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  此外需要 ALTER ANY DATABASE 权限。   
  
## <a name="examples"></a>示例  
  
###  <a name="Join_Secondary_Replica"></a> A. 将辅助副本联接到可用性组  
 下面的示例将你连接到的辅助副本联接`AccountsAG`可用性组。  
  
```SQL  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="Force_Failover"></a> B. 强制可用性组的故障转移  
 下面的示例强制 `AccountsAG` 可用性组故障转移到您所连接的辅助副本。  
  
```SQL
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建可用性组 &#40;Transact SQL &#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40;Transact SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Alwayson 故障排除可用性组配置 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听器、 客户端连接和应用程序故障转移 &#40;SQL server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
