---
title: Windows Server 故障转移群集 (WSFC) 与 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Windows Server Failover Clustering (WSFC), with SQL Server
- WSFC, with SQL Server
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 79d2ea5a-edd8-4b3b-9502-96202057b01a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f39911901b6ab729382c2e08b34c3452d4ec65cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63246038"
---
# <a name="windows-server-failover-clustering-wsfc-with-sql-server"></a>Windows Server 故障转移群集 (WSFC) 与 SQL Server
  “Windows Server 故障转移群集”  (WSFC) 群集是一组独立的服务器，它们共同协作以提高应用程序和服务的可用性。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 利用 WSFC 服务和功能支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例。  
  
 
  
##  <a name="TermsAndDefs"></a> 术语和定义  
 WSFC 群集 (WSFC cluster)  
 “Windows Server 故障转移群集”(WSFC) 群集是一组独立的服务器，它们共同协作以提高应用程序和服务的可用性。  
  
 故障转移群集实例 (Failover cluster instance)  
 一个 Windows 服务实例，用于管理 IP 地址资源、网络名称资源和运行一个或多个应用程序或服务所需的其他资源。 客户端可以使用网络名称访问组中的资源，类似于使用计算机名称访问物理服务器上的服务。 但是，因为故障转移群集实例是一个组，所以该实例可以故障转移到另一个节点，而不会影响基础名称或地址。  
  
 节点  
 作为服务器群集的活动或非活动成员的 Microsoft Windows Server 系统。  
  
 群集资源 (Cluster resource)  
 节点可以拥有的物理实体或逻辑实体，可联机和脱机、在节点间移动和作为群集对象进行管理。 在任何时间点，群集资源只能为单个节点所拥有。  
  
 资源组 (Resource group)  
 作为单个群集对象管理的群集资源集合。 通常，资源组包含运行特定应用程序或服务所需的所有群集资源。 故障转移和故障回复始终作用于资源组。  
  
 资源依赖项 (Resource dependency)  
 一个资源所依赖的另一个资源。 如果资源 A 依赖于资源 B，则 B 是 A 的依赖项。  
  
 网络名称资源 (Network name resource)  
 作为群集资源进行管理的逻辑服务器名称。 网络名称资源必须与一个 IP 地址资源结合使用。  
  
 首选所有者 (Preferred owner)  
 资源组优先运行的节点。 每个资源组都按优先顺序与首选的所有者列表关联。 在自动故障转移过程中，资源组将移动到首选所有者列表中的下一个首选节点。  
  
 可能的所有者 (Possible owner)  
 可在其上运行资源的辅助节点。 每个资源组都与一系列可能的所有者关联。 资源组仅可故障转移到作为可能的所有者列出的节点。  
  
 仲裁模式 (Quorum mode)  
 故障转移群集中的仲裁配置，用于确定群集可以承受的节点故障数。  
  
 强制仲裁 (Forced quorum)  
 即使仅有仲裁所需的少数元素进行通信，该过程也会启动群集。  
  
 有关详细信息，请参阅：[故障转移群集词汇表](/previous-versions/windows/desktop/MsCS/server-cluster-glossary)  
  
##  <a name="Overview"></a> Windows Server 故障转移群集概述  
 Windows Server 故障转移群集提供了各种基础结构功能来支持所承载的服务器应用程序（如 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 Microsoft Exchange）的高可用性和灾难恢复方案。  如果一个群集节点或服务失败，则该节点上承载的服务可在一个称为“故障转移”的过程中自动或手动转移到另一个可用节点。  
  
 WSFC 群集中的节点协同工作，共同提供这些类型的功能：  
  
-   **分布式元数据和通知。** 群集中的每个节点上维护着 WSFC 服务和承载的应用程序元数据。 除了承载的应用程序设置之外，此元数据还包括 WSFC 配置和状态。 对一个节点的元数据或状态进行的更改会自动传播到群集中的其他节点。  
  
-   **资源管理。** 群集中的各节点可能提供物理资源，如直接连接存储、网络接口和对共享磁盘存储的访问。 承载的应用程序将其本身注册为群集资源，并可配置启动和运行状况对于其他资源的依赖关系。  
  
-   **运行状况监视。** 节点间和主节点运行状况检测是通过结合使用信号样式的网络通信和资源监视来实现的。 群集的总体运行状况是由群集中节点仲裁的投票决定。  
  
-   **故障转移协调。** 每个资源都配置为由主节点承载，并且每个资源均可自动或手动转移到一个或多个辅助节点。 基于运行状况的故障转移策略控制节点之间资源所有权的自动转移。 在发生故障转移时通知节点和承载的应用程序，以便其做出适当的响应。  
  
 有关详细信息，请参阅：[Windows Server 2008 R2 中的故障转移群集](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
##  <a name="AlwaysOnWsfcTech"></a> SQL Server AlwaysOn 技术和 WSFC  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] *AlwaysOn*是新的高可用性和灾难恢复解决方案，充分利用 WSFC。 AlwaysOn 提供一个集成、灵活的解决方案，用于提高应用程序可用性，并提供更好的硬件投资回报，还简化高可用性部署和管理。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 和 AlwaysOn 故障转移群集实例将 WSFC 用作一种平台技术，将组件注册为 WSFC 群集资源。   相关的资源将合并为一个“资源组”，这些资源可能依赖于其他 WSFC 群集资源。 这样，WSFC 群集服务就可以感测并标明是否需要重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，或自动将其故障转移到 WSFC 群集中的不同服务器节点上。  
  
> [!IMPORTANT]  
>  若要充分利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]AlwaysOn 技术，您应该应用多个与 WSFC 相关的先决条件。  
>   
>  有关详细信息，请参阅：[先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
### <a name="instance-level-high-availability-with-alwayson-failover-cluster-instances"></a>实例级高可用性以及 AlwaysOn 故障转移群集实例  
 AlwaysOn“故障转移群集实例”  (FCI) 是安装在 WSFC 群集中的节点上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 这种类型的实例的资源依赖于共享磁盘存储（通过 Fibre 通道或 iSCSI SAN）和虚拟网络名称。 虚拟网络名称的资源依赖于一个或多个虚拟 IP 地址（每个地址位于不同子网中）。 SQL Server 服务和 SQL Server 代理服务均注册为资源，且都依赖于虚拟网络名称资源。  
  
 发生故障转移时，WSFC 服务将实例的资源所有权转移到指定的故障转移节点。 然后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例在故障转移节点上重新启动，数据库恢复如常。 在任何给定时刻，群集中只有一个节点可以承载 FCI 和基础资源。  
  
> [!NOTE]  
>  AlwaysOn 故障转移群集实例要求使用对称共享磁盘存储，如存储区域网络 (SAN) 或 SMB 文件共享。  共享磁盘存储卷必须可用于 WSFC 群集中所有可能的故障转移节点。  
  
 有关详细信息，请参阅：[AlwaysOn 故障转移群集实例](always-on-failover-cluster-instances-sql-server.md)  
  
### <a name="database-level-high-availability-with-includesshadrincludessshadr-mdmd"></a>数据库级高可用性与 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  
  “可用性组”是一组共同实现故障转移的用户数据库。 一个可用性组包含一个主“可用性副本”  和一至四个次要副本，这些副本通过基于 SQL Server 日志的数据移动来实现数据保护以进行维护，无需共享存储。 每个副本均由 WSFC 群集的不同节点上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例承载。 可用性组和相应的虚拟网络名称注册为 WSFC 群集中的资源。  
  
  主副本节点上的“可用性组侦听器” [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 响应要求连接到虚拟网络名称的传入客户端请求，侦听器基于连接字符串中的属性将每个请求重定向到相应的  实例。  
  
 当发生故障转移时，不是将共享物理资源的所有权转移到另一个节点，而是利用 WSFC 重新配置另一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上的辅助副本，使其成为可用性组的主副本。 然后，将可用性组的虚拟网络名称资源转移到该实例。  
  
 在任何给定时刻，只有单个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例可承载可用性组数据库的主副本，而所有关联的辅助副本都必须分别驻留在单独的实例上，并且每个实例必须驻留在单独的物理节点上。  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]不要求部署故障转移群集实例或使用异步共享存储（SAN 或 SMB）。  
>   
>  故障转移群集实例 (FCI) 可与可用性组结合使用，以提高可用性副本的可用性。 但是，为了防止 WSFC 群集中出现潜在的争用情况，不支持可用性组自动故障转移到驻留在 FCI 上的副本，也不支持从驻留在 FCI 上的副本自动故障转移到可用性组。  
  
 有关详细信息，请参阅：[AlwaysOn 可用性组概述&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
##  <a name="AlwaysOnWsfcHealth"></a> WSFC 运行状况监视和故障转移  
 AlwaysOn 解决方案的高可用性是通过积极主动地监视物理和逻辑 WSFC 群集资源的运行状况，以及自动故障转移到冗余硬件和重新配置冗余硬件来实现的。   系统管理员还可以对可用性组或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例启动从一个节点到另一个节点的“手动故障转移”。  
  
### <a name="failover-policies-for-nodes-failover-cluster-instances-and-availability-groups"></a>节点、故障转移群集实例和可用性组的故障转移策略  
 “故障转移策略”  是在 WSFC 群集节点、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障群集实例 (FCI) 以及可用性组级别配置的。   这些策略基于非正常运行的群集资源状态和节点响应的严重性、持续时间和频率，它们可以触发服务重新启动或将群集资源从一个节点“自动故障转移” [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 到另一个节点，或者可以触发将可用性组主副本从一个  实例移到另一个此类实例。  
  
 可用性组副本的故障转移不影响基础 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。  FCI 的故障转移将随实例一起移动所承载的可用性组副本。  
  
 有关详细信息，请参阅：[Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
### <a name="wsfc-resource-health-detection"></a>WSFC 资源运行状况检测  
 WSFC 群集节点中的每个资源都可以定期或按需报告其状态和运行状况。 很多情况可以指示资源故障；例如，电源故障、磁盘或内存错误、网络通信错误或服务不响应。  
  
 WSFC 群集资源（如网络、存储或服务）可能彼此依赖。 资源的累计运行状况由持续汇总其运行状况和其每个资源依赖项的运行状况来确定。  
  
### <a name="wsfc-inter-node-health-detection-and-quorum-voting"></a>WSFC 节点间运行状况检测和仲裁投票  
 WSFC 群集中的每个节点都参与周期性信号通信，以便与其他节点共享该节点的运行状况。 未响应的节点被认为是处于故障状态。  
  
  “仲裁”节点集是 WSFC 群集中的大多数投票节点和见证服务器。  WSFC 群集的总体运行状况和状态是由定期“仲裁投票”确定的。 仲裁的存在意味着群集运行状况正常，且能提供节点级别的容错能力。  
  
  “仲裁模式”在 WSFC 群集级别配置，用于指示用于仲裁投票的方法以及执行自动故障转移或使群集脱机的时间。  
  
> [!TIP]  
>  WSFC 群集中最好始终有奇数数目的仲裁投票。  为进行仲裁投票，不必在群集的所有节点上安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 其他服务器可以充当仲裁成员，或者可以将 WSFC 仲裁模式配置为将远程文件共享用作补救措施。  
>   
>  有关详细信息，请参阅：[WSFC 仲裁模式和投票配置 (SQL Server)](wsfc-quorum-modes-and-voting-configuration-sql-server.md)  
  
### <a name="disaster-recovery-through-forced-quorum"></a>通过强制仲裁进行灾难恢复  
 根据操作实践和 WSFC 群集配置，您可以引发自动故障转移和手动故障转移，同时仍保持可靠、容错的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 解决方案。 但是，如果 WSFC 群集中合格投票节点的仲裁彼此之间无法通信，或者 WSFC 群集无法执行运行状况验证，则 WSFC 群集可能会脱机。  
  
 如果 WSFC 群集由于计划外灾难或由于持续的硬件或通信故障而导致脱机，则需要管理员手动干预才能“强制仲裁”  ，并在非容错配置中将仍有效的群集节点变为联机状态。  
  
 之后，还必须执行一系列步骤来重新配置 WSFC 群集，恢复受影响的数据库副本，并重新建立一个新仲裁。  
  
 有关详细信息，请参阅：[通过强制仲裁进行 WSFC 灾难恢复 (SQL Server)](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="AlwaysOnWsfcRelationship"></a> SQL Server AlwaysOn 组件与 WSFC 的关系  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 和 WSFC 功能和组件之间存在多层关系。  
  
 AlwaysOn 可用性组承载于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上。  
 指定将连接到主数据库或辅助数据库的逻辑可用性组侦听器名称的客户端请求将重定向至基础 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例 (FCI) 的相应实例网络名称。  
  
 “SQL Server 实例”当前承载于单个节点上。  
 如果存在，则独立的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例始终驻留在具有静态实例网络名称的单个“节点”上。  如果存在，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 在两个或多个具有单个虚拟“实例网络名称”的可能的故障转移节点之一上处于活动状态。  
  
 “节点”为 WSFC 群集的成员。  
 每个节点上存储了所有节点的WSFC 配置元数据和状态。 每个服务器都为用户或系统数据库提供非对称存储或共享存储 (SAN) 卷。 在一个或多个 IP 子网上，每个服务器都至少具有一个物理网络接口。  
  
 WSFC 服务监视一组服务器的运行状况和管理它们的配置。  
 “Windows Server 故障转移群集 (WSFC)”服务将对“WSFC 配置”元数据和状态的更改传播到群集中的所有节点。 部分元数据和状态可能存储在 WSFC 仲裁见证服务器远程文件共享上。 两个或更多活动的节点或见证服务器构成一个仲裁，以便对 WSFC 群集的运行状况进行投票。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 注册表项是 WSFC 群集的子项。  
 如果您删除后重新创建了 WSFC 群集，则必须在原始 WSFC 群集上启用了 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的每个服务器实例上都禁用然后重新启用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能。 有关详细信息，请参阅[启用和禁用 AlwaysOn 可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
 ![SQL Server AlwaysOn 组件上下文关系图](../../../database-engine/media/alwaysoncomponentcontextdiagram.gif "SQL Server AlwaysOn 组件上下文关系图")  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [查看群集仲裁 NodeWeight 设置](view-cluster-quorum-nodeweight-settings.md)  
  
-   [配置群集仲裁 NodeWeight 设置](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [在无仲裁情况下强制启动 WSFC 群集](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [Windows Server 技术：故障转移群集](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Windows Server 2008 R2 中的故障转移群集](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
-   [查看故障转移群集的事件和日志](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 故障转移群集 Cmdlet](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 故障转移群集实例 (SQL Server)](always-on-failover-cluster-instances-sql-server.md)   
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [WSFC 仲裁模式和投票配置 (SQL Server)](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [故障转移群集实例的故障转移策略](failover-policy-for-failover-cluster-instances.md)   
 [通过强制仲裁进行 WSFC 灾难恢复 (SQL Server)](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
