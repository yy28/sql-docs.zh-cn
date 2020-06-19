---
title: 执行可用性组的计划手动故障转移 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c62942eaa8f4ab4472bca5c7123e5999eb069216
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936668"
---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>执行可用性组的计划手动故障转移 (SQL Server)
  本主题介绍如何通过在中使用、或 PowerShell，对 AlwaysOn 可用性组执行手动故障转移（*计划的手动故障转移*） [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。 可用性组在可用性副本级别进行故障转移。 计划的手动故障转移（类似于任何 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 故障转移）将辅助副本转换为主角色，同时将以前的主副本转换为辅助角色。  
  
 仅当主副本和目标辅助副本在同步提交模式下运行且当前同步时，才支持计划的手动故障转移，这种故障转移保留加入到目标辅助副本上的可用性组的辅助数据库中的所有数据。 一旦以前的主副本转换为辅助角色，其数据库将变成辅助数据库，并开始与新的主数据库进行同步。 在将其全部转换为 SYNCHRONIZED 状态之后，新的辅助副本将变成适于充当将来计划的手动故障转移的目标。  
  
> [!NOTE]  
>  如果辅助副本和主副本都配置为自动故障转移模式，则一旦辅助副本同步，该副本还可以充当自动故障转移的目标。 有关详细信息，请参阅[可用性模式（AlwaysOn 可用性组）](availability-modes-always-on-availability-groups.md)。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   故障转移命令将在目标辅助副本接受它之后立即返回。 但是，在可用性组完成故障转移之后，数据库恢复操作将以异步方式执行。  
  
-   故障转移时，不维护可用性组中数据库间的跨数据库一致性。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 不支持跨数据库事务和分布式事务。 有关详细信息，请参阅[数据库镜像或 AlwaysOn 可用性组不支持跨数据库事务 (SQL Server)](transactions-always-on-availability-and-database-mirroring.md)。  
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a>先决条件和限制  
  
-   目标辅助副本和主副本必须同时在同步提交可用性模式下运行。  
  
-   目标辅助副本当前必须与主副本同步。 这要求此辅助副本上的所有辅助数据库必须已加入到可用性组，并与其对应的主数据库同步（即本地辅助数据库必须为 SYNCHRONIZED）。  
  
    > [!TIP]  
    >  若要确定次要副本的故障转移就绪状态，请查询 [sys.dm_hadr_database_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql) 动态管理视图中的 **is_failover_ready** 列，或查看 [AlwaysOn 组面板](use-the-always-on-dashboard-sql-server-management-studio.md)的“故障转移就绪”**** 列。  
  
-   只有目标辅助副本支持该任务。 您必须连接到承载目标辅助副本的服务器实例。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **对可用性组执行手动故障转移**  
  
1.  在对象资源管理器中，连接到承载着需要进行故障转移的可用性组的一个辅助副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  右键单击要进行故障转移的可用性组，然后选择“故障转移”  命令。  
  
4.  这将启动“故障转移可用性组向导”。 有关详细信息，请参阅本主题后面的 [使用故障转移可用性组向导 (SQL Server Management Studio)](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)或 PowerShell 对 AlwaysOn 可用性组执行强制故障转移（可能会丢失数据）。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **对可用性组执行手动故障转移**  
  
1.  连接到承载目标辅助副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     其中， *group_name* 是可用性组的名称。  
  
     下面的示例将*MyAg*可用性组手动故障转移到连接的辅助副本。  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
 **对可用性组执行手动故障转移**  
  
1.  将目录 (`cd`) 更改为承载目标辅助副本的服务器实例。  
  
2.  使用 `Switch-SqlAvailabilityGroup` cmdlet。  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
     下面的示例将*MyAg*可用性组手动故障转移到具有指定路径的辅助副本。  
  
    ```powershell
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="follow-up-after-manually-failing-over-an-availability-group"></a><a name="FollowUp"></a>跟进：在对可用性组进行手动故障转移后  
 如果您故障转移到可用性组的 [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] 之外，则调整 WSFC 节点的仲裁投票以反映新的可用性组配置。 有关详细信息，请参阅 [Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [故障转移和故障转移模式 &#40;AlwaysOn 可用性组&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [执行可用性组的强制手动故障转移 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
