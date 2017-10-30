---
title: "升级 AlwaysOn 可用性组副本实例 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1783e700e516978e4eded68fa675addd8d31a234
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>升级 AlwaysOn 可用性组副本实例
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  在将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn 可用性组升级到新的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本、新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务包或积累更新，或在安装到新的 Windows 服务包或积累更新时，可以通过执行滚动升级将主要副本的故障时间降低到仅需一次手动故障转移（或者如果无法故障转移回原始的主要副本，则需两次手动故障转移）。 在升级过程中，次要副本将不可用于故障转移或只读操作，并且在升级之后，次要副本可能需要花费一些时间来与主要副本节点保持同步，具体时间取决于主要副本节点上的活动量（因此需要较高的网络流量）。  
  
> [!NOTE]  
>  此主题仅讨论 SQL Server 本身的升级。 它不涵盖升级包含 Windows Server 故障转移群集 (WSFC) 的操作系统。 Windows Server 2012 R2 之前的操作系统不支持升级承载故障转移群集的 Windows 操作系统。 若要升级在 Windows Server 2012 R2 上运行的群集节点，请参阅 [Cluster Operating System Rolling Upgrade](https://technet.microsoft.com/library/dn850430.aspx)（群集操作系统滚动升级）  
  
## <a name="prerequisites"></a>先决条件  
 开始之前，请仔细阅读以下重要信息：  
  
-   [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)：验证是否可以从你的 Windows 操作系统版本和 SQL Server 版本升级到 SQL Server 2016。 例如，不能直接从 SQL Server 2005 实例升级到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)︰检查支持的版本和版本升级以及环境中安装的其他组件，并据此选择适当的升级方法和步骤，按正确顺序升级组件。  
  
-   [计划并测试数据库引擎升级计划](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)：查看发行说明和已知升级问题、预升级清单，并制定和测试升级计划。  
  
-   [安装 SQL Server 2016 的硬件和软件要求](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)：查看安装 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的软件要求。 如果需要其他软件，则应在升级过程开始之前在每个节点上安装该软件，从而最大程度减少故障时间。  
  
## <a name="rolling-upgrade-best-practices-for-always-on-availability-groups"></a>AlwaysOn 可用性组的滚动升级最佳做法  
 在执行服务器升级或更新时应按照以下最佳做法操作，以最大程度减少可用性组的故障时间和数据丢失量：  
  
-   在开始滚动升级前，  
  
    -   至少对一个同步提交副本实例执行实际手动故障转移  
  
    -   通过对每个可用性数据库执行完整数据库备份来保护您的数据  
  
    -   在每个可用性数据库上运行 DBCC CHECKDB  
  
-   始终首先升级远程次要副本实例，然后升级本地次要副本实例，最后升级主要副本实例。  
  
-   无法在正在升级的数据库中执行备份。  在升级辅助副本之前，请将自动备份首选项配置为仅在主副本上运行备份。  在版本升级期间，任何副本都不可读取并且不能用于备份。 在非版本升级期间，可以先配置要在次要副本上运行的自动备份，再升级主要副本。  
  
-   在版本升级期间，在升级可读次要副本之后，以及在主要副本故障转移到已更新的次要副本或者升级主要副本之前，无法读取可读的次要副本。  
  
-   若要防止可用性组在升级过程中执行意外的故障转移，请在开始前从所有同步提交副本中删除可用性故障转移。  
  
-   在将可用性组故障转移到具有次要副本的已升级实例之前，不要升级主要副本实例。 否则，在主要副本实例上进行升级期间，客户端应用程序的故障时间可能更长。  
  
-   始终将可用性组故障转移到同步提交的次要副本实例。 如果故障转移到异步提交的次要副本实例，数据库将发生数据丢失，且数据移动会自动暂停，直到手动恢复数据移动为止。  
  
-   在升级或更新任何其他的次要副本实例之前，不要升级主要副本实例。 已升级的主要副本不再将日志传送到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 实例尚未升级到同一版本的任何次要副本。 在挂起到辅助副本的数据移动时，对于该副本无法进行自动故障转移，且您的可用性数据库很可能发生数据丢失。  
  
-   在故障转移可用性组前，请验证故障转移目标的同步状态为 SYNCHRONIZED。  
  
## <a name="rolling-upgrade-process"></a>滚动升级过程  
 实际上，确切的过程取决于一些因素，如可用性组的部署拓扑和每个副本的提交模式。 但在最简单的方案中，滚动升级是涉及以下步骤的多阶段过程：  
  
 ![HADR 方案中的可用性组升级](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "HADR 方案中的可用性组升级")  
  
1.  在所有同步提交的副本上删除自动故障转移  
  
2.  升级运行异步提交次要副本的所有远程次要副本实例  
  
3.  升级当前未运行主要副本的所有本地副本的次要实例  
  
4.  将可用性组手动故障转移到本地同步提交的次要副本  
  
5.  升级或更新以前承载主要副本的本地副本实例  
  
6.  根据需要配置自动故障转移伙伴  
  
 如果需要，您可以执行额外的手动故障转移以将可用性组恢复到原始配置。  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>具有一个远程辅助副本的可用性组  
 如果您仅为灾难恢复部署了一个可用性组，可能需要将该可用性组故障转移到异步提交的辅助副本。 这样的配置如下图所示：  
  
 ![DR 方案中的可用性组升级](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "DR 方案中的可用性组升级")  
  
 在此情况下，在滚动升级期间必须将可用性组故障转移到异步提交的次要副本。 要防止数据丢失，请在故障转移可用性组前将提交模式更改为同步提交并等待辅助副本同步。 因此，滚动升级过程可能如下所示：  
  
1.  在远程站点上升级次要副本实例  
  
2.  将提交模式更改为同步提交  
  
3.  等待直到同步状态为 SYNCHRONIZED  
  
4.  在远程站点上将可用性组故障转移到次要副本  
  
5.  升级或更新本地（主站点）副本实例  
  
6.  将可用性组故障转移回主站点  
  
7.  将提交模式更改为异步提交  
  
 因为同步提交模式不是用于数据同步到远程站点的建议设置，客户端应用程序可能发现在设置更改后，数据库延迟时间立即增加。 此外，执行故障转移将导致丢弃所有未确认的日志消息。 由于两个站点之间的高网络延迟，丢弃的日志消息量可能很大，这导致客户端经历大量事务失败。 您可以通过执行以下操作之一来尽量降低对客户端应用程序的影响：  
  
-   在低客户端流量期间认真选择一个维护窗口  
  
-   在主站点上升级/更新 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 时，将可用性模式改回异步提交，在准备好再次故障转移到主站点时再将其恢复为同步提交  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>具有故障转移群集实例节点的可用性组  
 如果可用性组包含故障转移群集实例 (FCI) 节点，应先升级不活动的节点，再升级活动的节点。 下图显示一个常见的可用性组方案（它包含 FCI 用于本地高可用性且用于远程灾难恢复的 FCI 之间采用异步提交模式）和升级顺序。  
  
 ![FCI 的可用性组升级](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "FCI 的可用性组升级")  
  
1.  升级或更新 REMOTE2  
  
2.  将 FCI2 故障转移到 REMOTE2  
  
3.  升级或更新 REMOTE1  
  
4.  升级或更新 PRIMARY2  
  
5.  将 FCI1 故障转移到 PRIMARY2  
  
6.  升级或更新 PRIMARY1  
  
## <a name="upgrade-update-sql-server-instances-with-multiple-availability-groups"></a>升级或更新包含多个可用性组的 SQL Server 实例  
 如果正在单独的服务器节点（活动/活动配置）上运行包含主要副本的多个可用性组，则升级路径涉及更多故障转移步骤以在过程中保持高可用性。 假定您正在三个服务器节点上运行三个可用性组（如下表所示），所有辅助副本正在同步提交模式下运行。  
  
|可用性组|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1|主|||  
|AG2||主||  
|AG3|||主|  
  
 按以下顺序执行负载平衡的滚动升级可能适合你的情况：  
  
1.  将 AG2 故障转移到 Node3（以空出 Node2）  
  
2.  升级或更新 Node2  
  
3.  将 AG1 故障转移到 Node2（以空出 Node1）  
  
4.  升级或更新 Node1  
  
5.  将 AG2 和 AG3 故障转移到 Node1（以空出 Node3）  
  
6.  升级或更新 Node3  
  
7.  将 AG3 故障转移到 Node3  
  
 此升级顺序具有每个可用性组小于两个故障转移的平均故障时间。 最终配置如下表所示。  
  
|可用性组|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||主||  
|AG2|主|||  
|AG3|||主|  
  
 基于你的特定实现，你的升级路径可能不同，客户端应用程序经历的故障时间也可能不同。  
  
> [!NOTE]  
>  在许多情况下，滚动升级完成后，将会故障转移回原始的主要副本。  
  
## <a name="see-also"></a>另请参阅  
 [使用安装向导（安装程序）升级到 SQL Server 2016](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [从命令提示符安装 SQL Server 2016](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  

