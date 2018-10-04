---
title: Alwayson 策略针对运行问题的 Always On 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1e4c878004f3cdcc492637d338e8ff6c8d92937
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104167"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>针对 AlwaysOn 可用性组运行问题的 AlwaysOn 策略 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]运行状况模型评估一组基于预定义策略的管理 (PBM) 策略。 可以使用这些策略查看 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中可用性组及其可用性副本和数据库的运行状况。  
  
 
  
##  <a name="TermsAndDefinitions"></a> 术语和定义  
 AlwaysOn 预定义策略  
 利用一组内置策略，数据库管理员可以检查可用性组及其可用性副本和数据库是否与由 AlwaysOn 策略定义的状态兼容。  
  
 [AlwaysOn 可用性组](always-on-availability-groups-sql-server.md)提供替代数据库镜像的企业级方案的高可用性和灾难恢复解决方案。  
  
 可用性组 (availability group)  
 一个容器，用于一组共同实现故障转移的离散用户数据库（被称为可用性数据库）。  
  
 可用性副本  
 可用性组的实例化，该可用性组由特定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例承载，该实例维护属于该可用性组的每个可用性数据库的本地副本。  存在两种类型的可用性副本：一个“主副本” 和一至四个“辅助副本”。 承载给定可用性组的可用性副本的服务器实例必须位于单个 Windows Server 故障转移群集 (WSFC) 群集的不同节点上。  
  
 可用性数据库 (availability database)  
 属于可用性组的数据库。 对于每个可用性数据库，可用性组将保留一个读写副本（主数据库）和一个到四个只读副本（辅助数据库）。  
  
 AlwaysOn 面板  
 一个 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 面板，该面板针对可用性组的运行状况提供了一目了然的视图。 有关详细信息，请参阅本主题后面的 [AlwaysOn 面板](#Dashboard)。  
  
##  <a name="AlwaysOnPBM"></a> 预定义策略和问题  
 下表概述了预定义策略。  
  
|策略名称|问题|类别**<sup>*</sup>**|方面|  
|-----------------|-----------|------------------------------|-----------|  
|WSFC 群集状态|[WSFC 群集服务处于脱机状态](wsfc-cluster-service-is-offline.md)。|严重|SQL Server 实例|  
|可用性组联机状态|[可用性组处于脱机状态](availability-group-is-offline.md)。|严重|可用性组 (availability group)|  
|可用性组自动故障转移就绪|[Availability group is not ready for automatic failover](availability-group-is-not-ready-for-automatic-failover.md)。|严重|可用性组 (availability group)|  
|可用性副本数据同步状态|[一些可用性副本未同步数据](some-availability-replicas-are-not-synchronizing-data.md)。|警告|可用性组 (availability group)|  
|同步副本数据同步状态|[一些同步副本不同步](some-synchronous-replicas-are-not-synchronized.md)。|警告|可用性组 (availability group)|  
|可用性副本角色状态|[一些可用性副本不具有正常运行的角色](some-availability-replicas-do-not-have-a-healthy-role.md)。|警告|可用性组 (availability group)|  
|可用性副本连接状态|[断开一些可用性副本的连接](some-availability-replicas-are-disconnected.md)。|警告|可用性组 (availability group)|  
|可用性副本角色状态|[可用性副本不具有运行状况良好的角色](availability-replica-does-not-have-a-healthy-role.md)。|严重|可用性副本|  
|可用性副本连接状态|[断开可用性副本的连接](availability-replica-is-disconnected.md)。|严重|可用性副本|  
|可用性副本联接状态|[可用性副本未联接](availability-replica-is-not-joined.md)。|警告|可用性副本|  
|可用性副本数据同步状态|[一些可用性数据库的数据同步状态不正常](data-synchronization-state-of-some-availability-database-is-not-healthy.md)。|警告|可用性副本|  
|可用性数据库挂起状态|[Availability database is suspended](availability-database-is-suspended.md)。|警告|可用性数据库|  
|可用性数据库联接状态|[未联接辅助数据库](secondary-database-is-not-joined.md)。|警告|可用性数据库|  
|可用性数据库数据同步状态|[可用性数据库的数据同步状态不正常](data-synchronization-state-of-availability-database-is-not-healthy.md)。|警告|可用性数据库|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>**  对于 AlwaysOn 策略，类别名称用作 Id。 更改 AlwaysOn 类别的名称将会破坏其运行状况评价功能。 因此，请不要修改 AlwaysOn 类别的名称。  
  
##  <a name="Dashboard"></a> AlwaysOn 仪表板  
 AlwaysOn 面板为您提供了针对可用性组的运行状况的一目了然的视图。 AlwaysOn 面板包括以下功能：  
  
-   使您能够轻松显示有关给定的可用性组、其可用性副本以及其数据库的详细信息。  
  
-   显示关键状态的可视化表示以帮助数据库管理员快速决定执行哪些操作。  
  
-   提供故障排除方案的启动点。  
  
-   对于给定的操作问题，在 **“策略评估结果”** 对话框中填入有关特定的 AlwaysOn 运行状况策略违反情况的信息和指向更新帮助的链接。  
  
-   提供一个运行状况扩展事件查看器，用于显示以前的特定于 AlwaysOn 的问题的事件。  
  
-   如果可用性组的故障转移可以纠正问题，则提供[故障转移可用性组向导](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)链接的启动点。 此向导将指导数据库管理员完成手动故障转移过程。  
  
##  <a name="ExtendHealthModel"></a> 扩展 AlwaysOn 运行状况模型  
 扩展 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 运行状况模型只是创建您自己的用户定义策略，并基于您正在监视的对象类型将其放入特定类别。  在更改了一些设置后，AlwaysOn 面板将自动评估您自己的用户定义策略以及 AlwaysOn 预定义策略。  
  
 用户定义策略可以使用任何可用的 PBM 方面，包括那些由 AlwaysOn 预定义策略使用的方面（请参阅本主题前面的[预定义策略和问题](#AlwaysOnPBM)）。 服务器方面提供以下属性用于监视[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]运行状况: (`IsHadrEnabled`和`HadrManagerStatus`)。 服务器方面还提供了下列用于监视 WSFC 群集配置的策略：`ClusterQuorumType` 和 `ClusterQuorumState`。  
  
 有关详细信息，请参阅 [AlwaysOn 运行状况模型第二部分 -- 扩展运行状况模型](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)（SQL Server AlwaysOn 团队博客）。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用 AlwaysOn 策略查看可用性组的运行状况&#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [通过强制仲裁进行 WSFC 灾难恢复 (SQL Server)](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [在无仲裁情况下强制启动 WSFC 群集](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [执行可用性组的强制手动故障转移 (SQL Server)](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [解决失败的添加文件操作问题&#40;AlwaysOn 可用性组&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [AlwaysOn 运行状况模型第 1 部分-运行状况模型体系结构](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [AlwaysOn 运行状况模型第 2 部分-扩展运行状况模型](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [Microsoft SQL Server AlwaysOn 解决方案指南有关高可用性和灾难恢复](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组 (SQL Server)](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [管理可用性组 (SQL Server)](administration-of-an-availability-group-sql-server.md)   
 [监视可用性组 (SQL Server)](monitoring-of-availability-groups-sql-server.md)  
  
  
