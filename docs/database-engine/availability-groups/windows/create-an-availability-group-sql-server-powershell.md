---
title: 使用 PowerShell 创建可用性组
description: 使用 PowerShell 创建 AlwaysOn 可用性组的步骤。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 58b0010f2440a95b698bb37d99e8e3bc11cce218
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209976"
---
# <a name="create-an-always-on-availability-group-using-powershell"></a>使用 PowerShell 创建 AlwaysOn 可用性组
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何使用 PowerShell cmdlet 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中通过 PowerShell 创建和配置 AlwaysOn 可用性组。 “可用性组”  定义一组用户数据库，这些用户数据库将以支持故障转移的单个单元和一组故障转移伙伴（称作“可用性副本” ）的形式进行故障转移。  
  
> [!NOTE]  
>  有关可用性组的简介，请参阅 [AlwaysOn 可用性组概述 (SQL Server)](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)中通过 PowerShell 创建和配置 AlwaysOn 可用性组。  
  
-   **开始之前：**  
  
     [先决条件、限制和建议](#PrerequisitesRestrictions)  
  
     [安全性](#Security)  
  
     [任务和相应 PowerShell Cmdlet 的摘要](#SummaryPSStatements)  
  
     [设置和使用 SQL Server PowerShell 提供程序](#PsProviderLinks)  
  
-   **若要创建和配置可用性组，请使用：**[使用 PowerShell 创建和配置可用性组](#PowerShellProcedure)  
  
-   **示例：**[使用 PowerShell 创建可用性组](#ExampleConfigureGroup)  
  
-   [相关任务](#RelatedTasks)  
  
-   [相关内容](#RelatedContent)  
  
> [!NOTE]  
>  除了使用 PowerShell cmdlet 之外，您还可以使用“创建可用性组”向导或 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。 有关详细信息，请参阅 [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 或 [创建可用性组 (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)中通过 PowerShell 创建和配置 AlwaysOn 可用性组。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 我们强烈建议您首先阅读此部分，再尝试创建您的第一个可用性组。  
  
###  <a name="PrerequisitesRestrictions"></a> 先决条件、限制和建议  
  
-   创建可用性组之前，请先验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机实例分别位于单个 WSFC 故障转移群集的不同 Windows Server 故障转移群集 (WSFC) 节点上。 此外，还要验证您的服务器实例满足其他服务器实例先决条件，并且其他所有 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]要求都得到满足且您知道有关建议。 有关详细信息，我们强烈建议你参阅[针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
###  <a name="SummaryPSStatements"></a> 任务和相应 PowerShell Cmdlet 的摘要  
 下表列出了涉及配置可用性组的基本任务，并且指出了 PowerShell cmdlet 支持的任务。 必须按照任务在表中出现的顺序执行 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 任务。  
  
|任务|PowerShell Cmdlet（如果可用）或 Transact-SQL 语句|执行任务的位置**\***|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|创建数据库镜像端点（每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例一次）|**New-SqlHadrEndPoint**|在缺少数据库镜像端点的每个服务器实例上执行。<br /><br /> 注意：若要更改现有数据库镜像端点，请使用 Set-SqlHadrEndpoint。|  
|创建可用性组|首先，将 **New-SqlAvailabilityReplica** cmdlet 与 **-AsTemplate** 参数一起使用，以便为你计划包括在可用性组中的两个可用性副本中的每一个都创建内存中可用性副本对象。<br /><br /> 然后，通过使用 **New-SqlAvailabilityGroup** cmdlet 并引用你的可用性副本对象，创建可用性组。|在要承载初始主副本的服务器实例上执行。|  
|将辅助副本联接到可用性组|**Join-SqlAvailabilityGroup**|在承载辅助副本的各服务器实例上执行。|  
|准备辅助数据库|**Backup-SqlDatabase** 和 **Restore-SqlDatabase**|在承载主副本的服务器实例上创建备份。<br /><br /> 使用 **NoRecovery** 还原参数在承载辅助副本的各服务器实例上还原备份。 如果文件路径在承载主副本和目标辅助副本的计算机之间存在差异，还要使用 **RelocateFile** 还原参数。|  
|通过将各辅助数据库联接到可用性组，开始数据同步|**Add-SqlAvailabilityDatabase**|在承载辅助副本的各服务器实例上执行。|  
  
 \*若要执行某个给定任务，请将目录 (**cd**) 更改为指示的一个或多个服务器实例。  
  
###  <a name="PsProviderLinks"></a> 设置和使用 SQL Server PowerShell 提供程序  
  
-   [SQL Server PowerShell 提供程序](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [获取 SQL Server PowerShell 帮助](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell 创建和配置可用性组  
  
> [!NOTE]  
>  若要查看给定 cmdlet 的语法和示例，请使用 **PowerShell 环境中的** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
1.  将目录 (**cd**) 更改为承载主要副本的服务器实例。  
  
2.  为主副本创建内存中可用性副本对象。  
  
3.  为每个辅助副本创建内存中可用性副本对象。  
  
4.  创建可用性组。  
  
    > [!NOTE]  
    >  可用性组名称的最大长度为 128 个字符。  
  
5.  将新的辅助副本联接到可用性组。 有关详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)或 PowerShell 将辅助数据库联接到 Always On 可用性组。  
  
6.  对于可用性组中的每个数据库，通过使用 RESTORE WITH NORECOVERY 还原主数据库的最近的备份，创建辅助数据库。  
  
7.  将每个新的辅助数据库联接到可用性组。 有关详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)中通过 PowerShell 创建和配置 AlwaysOn 可用性组。  
  
8.  或者，使用 Windows **dir** 命令可以验证新的可用性组的内容。  
  
> [!NOTE]  
>  如果服务器实例的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户基于不同的域用户帐户运行，则在各服务器实例上，为其他服务器实例创建一个登录名，并且授予此登录名对本地数据库镜像端点的 CONNECT 权限。  
  
##  <a name="ExampleConfigureGroup"></a> 示例：使用 PowerShell 创建可用性组  
 下面的 PowerShell 示例创建并配置一个名为 `MyAG` 的简单可用性组，该可用性组具有两个可用性副本和一个可用性数据库。 示例：  
  
1.  备份 `MyDatabase` 及其事务日志。  
  
2.  使用 `MyDatabase` -NoRecovery **选项还原** 及其事务日志。  
  
3.  创建主副本的内存中表示形式，它将由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例（名为 `PrimaryComputer\Instance`）承载。  
  
4.  创建辅助副本的内存中表示形式，它将由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例（名为 `SecondaryComputer\Instance`）承载。  
  
5.  创建名为 `MyAG`的可用性组。  
  
6.  将辅助副本联接到该可用性组。  
  
7.  将辅助数据库联接到该可用性组。  
  
```  
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "MyAG" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "MyDatabase"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "MyAG"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\MyAG" -Database "MyDatabase"  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **为 AlwaysOn 可用性组配置服务器实例**  
  
-   [启用和禁用 AlwaysOn 可用性组 (SQL Server)](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [为 AlwaysOn 可用性组创建数据库镜像终结点 (SQL Server PowerShell)](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **配置可用性组和副本属性**  
  
-   [更改可用性副本的可用性模式 (SQL Server)](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [更改可用性副本的故障转移模式 (SQL Server)](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [配置灵活的故障转移策略以控制自动故障转移的条件（AlwaysOn 可用性组）](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL (SQL Server)](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [配置可用性副本备份 (SQL Server)](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [更改可用性副本的会话超时期限 (SQL Server)](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **完成可用性组配置**  
  
-   [将辅助副本联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [为可用性组手动准备辅助数据库 (SQL Server)](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **用于创建可用性组的其他方法**  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [创建可用性组 (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **解决 AlwaysOn 可用性组配置问题**  
  
-   [AlwaysOn 可用性组配置故障排除 (SQL Server)](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [添加文件操作失败的故障排除（AlwaysOn 可用性组）](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [Always On - HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [使用 SQL Server PowerShell 配置 AlwaysOn](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [SQL Server Always On 团队博客：SQL Server Always On 团队官方博客](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **视频：**  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series,Part 1:Introducing the Next Generation High Availability Solution](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)（Microsoft SQL Server Code-Named "Denali" Always On 系列，第 1 部分：介绍下一代高可用性解决方案）  
  
     [Microsoft SQL Server Code-Named "Denali" Always On Series,Part 2:Building a Mission-Critical High Availability Solution Using Always On](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)（Microsoft SQL Server Code-Named "Denali" Always On 系列，第 2 部分：使用 Always On 生成关键任务高可用性解决方案）  
  
-   **白皮书：**  
  
     [用于高可用性和灾难恢复的 Microsoft SQL Server AlwaysOn 解决方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](https://sqlcat.com/)  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像终结点 (SQL Server)](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  







