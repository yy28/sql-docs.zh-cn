---
title: AlwaysOn 可用性组（SQL Server）的先决条件、限制和建议 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b12b9030d27e371e0299e06917464b1467b9b10e
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782961"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)
  本主题介绍在部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]时的注意事项，包括针对主机、Windows Server 故障转移群集 (WSFC) 群集、服务器实例和可用性组的先决条件、限制和建议。 对于上述各组件，还指出了安全注意事项和所需权限（如果有）。  
  
> [!IMPORTANT]  
>  在部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]之前，强烈建议您阅读本主题的每个章节。  
  
 
  
##  <a name="DotNetHotfixes"></a>支持 AlwaysOn 可用性组的 .net 修补程序  
 根据您将用于 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]组件和功能，您可能需要安装在下表中标识的其他 .Net 修补程序。 可以按任意顺序安装这些修补程序。  
  
||依赖功能|修补程序|链接|  
|------|-----------------------|------------|----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|.Net 3.5 SP1 修补程序添加对读意向、只读和多子网故障转移的 SQL Client for AlwaysOn 功能的支持。 此修补程序需要安装在每个 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表服务器上。|KB 2654347：[.Net 3.5 SP1 修补程序添加对 AlwaysOn 功能的支持](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a> Windows 系统要求和建议  
  
  
###  <a name="SystemRequirements"></a>清单：要求（Windows 系统）  
 为了支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能，请确保要参与一个或多个可用性组的每台计算机都满足以下基本要求：  
  
||要求|链接|  
|------|-----------------|----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|确保此系统不是域控制器。|域控制器上不支持可用性组。|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|确保每台计算机正在运行 x86（非 WOW64）或 x64 Windows Server 2008 或更高版本。|WOW64（Windows 64 位上的 Windows 32 位）不支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|确保每台计算机都是 Windows Server 故障转移群集 (WSFC) 群集中的节点。|[Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|请确保 WSFC 群集包含足够多的节点来支持您的可用性组配置。|对于某一给定可用性组，一个 WSFC 节点只能承载一个可用性副本。 在某一给定 WSFC 节点上， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的一个或多个实例可为许多可用性组承载可用性副本。<br /><br /> 询问您的数据库管理员，了解为支持计划的可用性组的可用性副本，需要多少个 WSFC 节点。<br /><br /> [AlwaysOn 可用性组概述 (SQL Server)](overview-of-always-on-availability-groups-sql-server.md)。|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|确保 WSFC 群集中的每个节点上都安装了所有适用的 Window 修补程序。|**\* 重要 \*\*\*** 对于正在其上部署 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的 WSFC 群集的节点，需要或建议使用许多修补程序。 有关详细信息，请参阅本节后面的[支持 AlwaysOn 可用性组的 Windows 修补程序（Windows 系统）](#WinHotfixes)。|  
  
> [!IMPORTANT]  
>  另外，确保已正确配置了您的环境以连接到可用性组。 有关详细信息，请参阅[AlwaysOn 客户端连接（SQL Server）](always-on-client-connectivity-sql-server.md)。  
  
####  <a name="WinHotfixes"></a>支持 AlwaysOn 可用性组的 windows 修补程序（Windows 系统）  
 根据您的群集拓扑，可能还需要应用其他几个 Windows Server 2008 Service Pack 2 (SP2) 或 Windows Server 2008 R2 修补程序才能支持 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 下表列出了这些修补程序。 可以按任意顺序安装这些修补程序。  
  
||适用于 Windows 2008 SP2|适用于 Windows 2008 R2 SP1|包括在 Windows 2012 中|若要支持 。|修补程序|链接|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|是|**配置最佳 WSFC 仲裁**|在每个 WSFC 节点上，确保安装了在知识库文章 2494036 中介绍的修补程序。<br /><br /> 此修补程序支持使用非自动故障转移目标配置最佳仲裁。 此功能通过使您可以选择哪些节点进行投票，改进了多站点群集。|KB 2494036：[利用修补程序，你可以在 Windows Server 2008 和 Windows Server 2008 R2 中配置不具有仲裁投票的群集节点](https://support.microsoft.com/kb/2494036)<br /><br /> 有关仲裁投票的信息，请参阅 [WSFC 仲裁模式和投票配置 (SQL Server)](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|是|**更有效地使用网络带宽**|在每个 WSFC 节点上，确保安装了在知识库文章 2616514 中介绍的修补程序。<br /><br /> 如果没有安装此修补程序，群集服务将在群集节点间发送不必要的注册表通知。 此行为会限制网络带宽，这对于 [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)]是很严重的问题。|KB 2616514：[群集服务在 Windows Server 2008 或 Windows Server 2008 R2 中的群集节点之间发送不必要的注册表项更改通知](https://support.microsoft.com/kb/2616514)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")||是|不适用|**在不可用于所有 WSFC 节点的磁盘上进行 VPD 存储测试**|如果某一 WSFC 节点正在运行 Windows Server 2008 R2 Service Pack 1 (SP1)，并且在未正确在处于联机状态的磁盘上运行且不可用于 WSFC 群集中的所有节点后“验证 SCSI 设备关键产品数据 (VPD)”存储测试失败，则安装在知识库文章 2531907 中介绍的修补程序。<br /><br /> 此修补程序可避免在磁盘处于联机状态时在验证报告中出现不恰当的警告或错误。|KB 2531907：[安装 Windows Server 2008 R2 SP1 后验证 SCSI 设备重要产品数据（VPD）测试失败](https://support.microsoft.com/kb/2531907)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")||是|是|**更快地故障转移到本地副本**|如果某个 WSFC 节点正在运行 Windows Server 2008 R2 Service Pack 1 (SP1)，请确保安装了在知识库文章 2687741 中介绍的修补程序。<br /><br /> 此修补程序可以改进 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 故障转移到本地副本的性能。|KB 2687741：[用于提高 Windows Server 2008 R2 的 SQL Server 2012 中 "AlwaysOn 可用性组" 功能性能的修补程序](https://support.microsoft.com/KB/2687741)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|是|**非对称存储-用于故障转移群集实例（Fci）**|如果将为 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 启用任何故障转移群集实例 (FCI)，则安装 Windows Server 2008 修补程序 976097。<br /><br /> 此修补程序使故障转移群集管理 Microsoft 管理控制台（MMC）管理单元支持非对称存储共享磁盘，这些磁盘仅在某些 WSFC 节点上可用。|KB 976097：[修补程序，用于将对非对称存储的支持添加到运行 Windows Server 2008 或 Windows Server 2008 R2 的故障转移群集的故障转移群集管理 MMC 管理单元](https://support.microsoft.com/kb/976097)<br /><br /> [AlwaysOn 体系结构指南：使用故障转移群集实例和可用性组生成高可用性和灾难恢复解决方案](https://technet.microsoft.com/library/jj215886.aspx)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|不适用|**Internet 协议安全（IPsec）**|如果您的环境使用 IPsec 连接，则当客户端计算机与虚拟网络名称重新建立 IPsec 连接（在此上下文中将连接到可用性组侦听器）时，可能会出现长时间的延迟（约两到三分钟）。 如果使用 IPsec 连接，我们建议您查看知识库文章 (KB 980915) 中详述的特定应用场景。|KB 980915：[从运行 Windows Server 2003、Windows Vista、Windows Server 2008、Windows 7 或 Windows Server 2008 R2 的计算机重新建立 IPSec 连接时出现长时间延迟](https://support.microsoft.com/kb/980915)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|是|**IPv6**|如果使用 IPv6，根据您的 Windows Server 操作系统，我们建议您查看知识库文章 2578103 或 2578113 中详述的特定应用场景。<br /><br /> 如果 Windows Server 拓扑使用 IP 版本 6 (IPv6)，则 WSFC 群集服务需要大约 30 秒的时间来对 IPv6 IP 地址进行故障转移。 这会导致客户端等待约 30 秒来重新连接该 IPv6 IP 地址。|KB 2578103 （Windows Server 2008）：[在 Windows Server 2008 中，群集服务需要大约30秒的时间来对 IPv6 IP 地址进行故障转移](https://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113 （Windows Server 2008 R2）：**Windows Server 2008 R2：** [在 Windows Server 2008 R2 中，群集服务需要大约30秒的时间来对 IPv6 IP 地址进行故障转移](https://support.microsoft.com/kb/2578113)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是|是|是|**群集和应用程序服务器之间没有路由器**|如果故障转移群集与应用程序服务器之间不存在路由器，则群集服务对网络相关资源进行故障转移的速度会很慢。 这在可用性组执行故障转移之后会延迟客户端重新连接。 在缺少路由器时，我们建议您查看知识库文章 2582281 中详述的特定应用场景并安装该修补程序（如果适用于您的环境）。|KB 2582281：[如果群集与应用程序服务器之间不存在路由器，则故障转移操作的速度会很慢](https://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> 针对承载可用性副本的计算机的建议（Windows 系统）  
  
-   **的系统：** 对于给定的可用性组，所有可用性副本都应在可处理同样的工作负荷的相当的系统上运行。  
  
-   **专用网络适配器：** 为获得最佳性能，请将专用的网络适配器（网络接口卡）用于 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
-   **足够的磁盘空间：** 服务器实例在其上承载可用性副本的每个计算机都必须为该可用性组中的所有数据库拥有足够的磁盘空间。 请记住，在主数据库增长时，其相应的辅助数据库也增长相同量。  
  
###  <a name="PermissionsWindows"></a> 权限（Windows 系统）  
 若要管理 WSFC 群集，用户必须是每个群集节点上的系统管理员。  
  
 有关用于管理群集的帐户的详细信息，请参阅[附录 A：故障转移群集要求](https://technet.microsoft.com/library/dd197454\(WS.10\).aspx)。  
  
###  <a name="RelatedTasksWindows"></a> 相关任务（Windows 系统）  
  
|任务|链接|  
|----------|----------|  
|设置 HostRecordTTL 值。|[更改 HostRecordTTL（使用 Windows PowerShell）](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> 更改 HostRecordTTL（使用 Windows PowerShell）  
  
1.  通过 **“以管理员身份运行”** 打开 PowerShell 窗口。  
  
2.  导入 FailoverClusters 模块。  
  
3.  使用 `Get-ClusterResource` cmdlet 查找网络名称资源，然后使用 `Set-ClusterParameter` cmdlet 设置 `HostRecordTTL` 值，如下所示：  
  
     Get-ClusterResource “\<NetworkResourceName>” | Set-ClusterParameter HostRecordTTL \<TimeInSeconds>  
  
     下面的 PowerShell 示例为名为“`SQL Network Name (SQL35)`”的网络名称资源将 HostRecordTTL 设置为 300 秒。  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  每次您打开新的 PowerShell 窗口时，都需要导入 `FailoverClusters` 模块。  
  
##### <a name="related-content-powershell"></a>相关内容 (PowerShell)  
  
-   [群集和高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) （故障转移群集和网络负载平衡团队博客）  
  
-   [故障转移群集上的 Windows PowerShell 入门](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [群集资源命令和等效的 Windows PowerShell cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> 相关内容（Windows 系统）  
  
-   [在多站点故障转移群集中配置 DNS 设置](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [向网络名称资源注册 DNS](https://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Windows 2008 R2 故障转移多站点群集](https://kiruba4u.blogspot.com/2012/03/failover-clustering-in-windows-server.html)  
  
##  <a name="ServerInstance"></a> SQL Server 实例先决条件和限制  
 每个可用性组均要求称作“可用性副本” [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的一组故障转移伙伴，它们由  的实例承载。 给定的服务器实例可以是独立实例或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例 (FCI)。  
  
 
  
###  <a name="PrerequisitesSI"></a>清单：先决条件（服务器实例）  
  
||先决条件|链接|  
|-|------------------|-----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|主机必须是 Windows Server 故障转移群集 (WSFC) 节点。 承载给定可用性组的可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例必须位于单个 WSFC 群集的单独节点上。 唯一的例外是在迁移到另一个 WSFC 群集时，此时一个可用性组可能会暂时跨两个群集。|[Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [故障转移群集和&#40;AlwaysOn 可用性组 SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|如果您希望将可用性组与 Kerberos 一起使用：<br /><br /> 承载可用性组的可用性副本的所有服务器实例都必须使用相同的 SQL Server 服务帐户。<br /><br /> 域管理员需要在可用性组侦听器的虚拟网络名称 (VNN) 的 SQL Server 服务帐户上使用 Active Directory 手动注册服务主体名称 (SPN)。 如果在 SQL Server 服务帐户之外的帐户上注册 SPN，则身份验证将失败。<br /><br /> **\*\* 重要提示 \*\*** 如果你更改 SQL Server 服务帐户，则域管理员必须重新手动注册 SPN。|[为 Kerberos 连接注册服务主体名称](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **简要说明：**<br /><br /> Kerberos 和 SPN 强制实施相互身份验证。 SPN 将映射到启动 SQL Server 服务的 Windows 帐户。 如果未正确注册 SPN 或注册失败，则 Windows 安全层将无法确定与 SPN 关联的帐户，因而无法使用 Kerberos 身份验证。<br /><br /> 注意:NTLM 没有此要求。|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|如果您计划使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例 (FCI) 承载可用性副本，则请确保您理解 FCI 限制并且满足 FCI 要求。|[使用 SQL Server 故障转移群集实例 (FCI) 承载可用性副本的先决条件和要求](#FciArLimitations) （本主题的后面将介绍）|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|每个服务器实例都必须正在运行 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的 Enterprise Edition。|[SQL Server 2014 各个版本支持的功能](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|为某一可用性组承载可用性副本的所有服务器实例必须都使用相同的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 排序规则。|[设置或更改服务器排序规则](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|对将为任何可用性组承载可用性副本的每个服务器实例都启用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能。 在某一给定计算机上，您可为 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 启用您的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装支持的任意多的服务器实例。|[启用和禁用 AlwaysOn 可用性组 (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> **\*\* 重要提示 \*\*** 如果你删除并重新创建了 WSFC 群集，则必须在每个服务器实例上禁用并重新启用已在原始 WSFC 群集上为 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 启用的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能。|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|每个服务器实例都要求数据库镜像端点。 请注意，此端点由服务器实例上的所有可用性副本以及数据库镜像伙伴和见证服务器共享。<br /><br /> 如果你选择承载可用性副本的服务器实例正在某一域用户帐户下运行并且尚不具有数据库镜像端点，则 [新建可用性组向导](use-the-availability-group-wizard-sql-server-management-studio.md) （或者 [将副本添加到可用性组向导](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)）可以创建该端点并将 CONNECT 权限授予服务器实例的服务帐户。 但是，如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务正在以内置帐户（例如 Local System、Local Service 或 Network Service）或非域帐户运行，您必须使用证书来进行端点身份验证，并且该向导将无法在服务器实例上创建数据库镜像端点。 在此情况下，我们建议您首先手动创建数据库镜像端点，然后启动该向导。<br /><br /> **\*\* 安全说明 \*\*** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的传输安全性与数据库镜像的传输安全性相同。|[数据库镜像终结点 (SQL Server)](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [用于数据库镜像和 AlwaysOn 可用性组&#40;SQL Server 的传输安全性&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|如果使用 FILESTREAM 的任何数据库将添加到某一可用性组，请确保在将承载该可用性组的可用性副本的每个服务器实例上都启用 FILESTREAM。|[启用和配置 FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|如果任何包含的数据库将添加到某一可用性组，请确保在将承载该可用性组的可用性副本的每个服务器实例上将 `contained database authentication` 服务器选项都设置为 `1`。|[contained database authentication 服务器配置选项](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [服务器配置选项 (SQL Server)](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> 可用性组的线程使用情况  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的工作线程具有以下要求：  
  
-   在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的一个空闲实例上， [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 使用 0 线程。  
  
-   可用性组使用的最大线程数为配置的最大服务器线程数（“`max worker threads`”）减去 40。  
  
-   给定服务器实例上承载的可用性副本共享一个线程池。  
  
     线程是按需共享的，如下所示：  
  
    -   一般情况下，存在 3–10 个共享线程，但此数目会根据主副本工作负荷增加。  
  
    -   如果给定线程空闲一段时间，则将释放回常规 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 线程池。 正常情况下，不活动线程在处于不活动状态 15 秒后释放。 但是，根据上一次活动，空闲线程可能保留更长时间。  
  
-   此外，可用性组使用未共享的线程，如下所示：  
  
    -   每个主副本为每个主数据库使用 1 个日志捕获线程。 此外，它为每个辅助数据库使用 1 个日志发送线程。 日志发送线程将在处于不活动状态 15 秒后释放。  
  
    -   每个辅助副本为每个辅助数据库使用 1 个恢复线程。 恢复线程将在处于不活动状态 15 秒后释放。  
  
    -   辅助副本上的备份将在备份操作持续时间内包含主副本上的一个线程。  
  
 有关详细信息，请参阅 [AlwaysON-HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)（CSS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工程师博客）。  
  
###  <a name="PermissionsSI"></a> 权限（服务器实例）  
  
|任务|所需权限|  
|----------|--------------------------|  
|创建数据库镜像端点|要求具有 CREATE ENDPOINT 权限，或者具有 **sysadmin** 固定服务器角色的成员身份。  此外，还要求 CONTROL ON ENDPOINT 权限。 有关详细信息，请参阅 [GRANT 终结点权限 (Transact-SQL)](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)。|  
|启用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|要求本地计算机上 **Administrator** 组中的成员身份以及对 WSFC 群集的完全控制。|  
  
###  <a name="RelatedTasksSI"></a> 相关任务（服务器实例）  
  
|任务|主题|  
|----------|-----------|  
|确定数据库镜像端点是否存在|[sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|创建数据库镜像端点（如果它尚不存在）|[为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [使用数据库镜像终结点证书 (Transact-SQL)](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [为 AlwaysOn 可用性组&#40;创建数据库镜像端点 SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|启用 AlwaysOn 可用性组|[启用和禁用 AlwaysOn 可用性组 (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> 相关内容（服务器实例）  
  
-   [AlwaysON-HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> 网络连接建议  
 强烈建议您为 WSFC 群集成员之间的通信和可用性副本之间的通信使用相同的网络链接。  如果某些链接失败（甚至间歇性断开），使用单独的网络链接可能会导致意外行为。  
  
 例如，要使可用性组支持自动故障转移，作为自动故障转移伙伴的辅助副本必须处于 SYNCHRONIZED 状态。 如果到此辅助副本的网络链接失败（甚至间歇性断开），副本将进入 UNSYNCHRONIZED 状态，并且在该链接恢复之前无法重新同步。 如果在该辅助副本不同步时，WSFC 群集请求自动故障转移，则不会发生自动故障转移。  
  
##  <a name="ClientConnSupport"></a> 客户端连接支持  
 有关客户端连接 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 支持的信息，请参阅[AlwaysOn 客户端连接（SQL Server）](always-on-client-connectivity-sql-server.md)。  
  
##  <a name="FciArLimitations"></a> 使用 SQL Server 故障转移群集实例 (FCI) 承载可用性副本的先决条件和限制  
 
  
###  <a name="RestrictionsFCI"></a> 限制 (FCI)  
  
> [!NOTE]  
>  从 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 中开始，AlwaysOn 故障转移群集实例支持 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 和 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 中的群集共享卷 (CSV)。 有关 CSV 的详细信息，请参阅 [了解故障转移群集中的群集共享卷](https://technet.microsoft.com/library/dd759255.aspx)。  
  
-   FCI 的群集节点仅可以托管给定可用性组的一个副本：如果在 FCI 上添加可用性副本，则可能 FCI 所有者的 WSFC 群集节点不能托管同一个可用性组的另一个副本。  
  
     此外，其他每个副本都必须由同一个 WSFC 群集中不同 WSFC 节点上驻留的 SQL Server 2012 实例承载。 唯一的例外是在迁移到另一个 WSFC 群集时，此时一个可用性组可能会暂时跨两个群集。  
  
-   FCI 不支持可用性组自动故障转移：FCI 不支持通过可用性组来自动进行故障转移，因此只能为手动故障转移配置任何由 FCI 承载的可用性副本。  
  
-   **更改 FCI 网络名称：** 如果你需要更改托管可用性副本的 FCI 的网络名称，则需要从副本的可用性组中删除它，然后将它添加回可用性组中。 您不能删除主副本，因此，如果您在重命名承载主副本的 FCI，则应故障转移到某一辅助副本，然后删除之前的主副本并将其添加回去。 请注意，重命名 FCI 可能会更改其数据库镜像端点的 URL。 当您添加副本时，请确保指定当前端点的 URL。  
  
###  <a name="PrerequisitesFCI"></a>清单：先决条件 (FCI)  
  
||先决条件|链接|  
|-|------------------|----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|在您使用 FCI 承载某一可用性副本之前，请确保系统管理员已安装了知识库文章 KB 976097 中介绍的 Windows Server 2008 修补程序。 此修补程序使故障转移群集管理 Microsoft 管理控制台（MMC）管理单元支持非对称存储共享磁盘，这些磁盘仅在某些 WSFC 节点上可用。|KB 976097：[修补程序，用于将对非对称存储的支持添加到运行 Windows Server 2008 或 Windows Server 2008 R2 的故障转移群集的故障转移群集管理 MMC 管理单元](https://support.microsoft.com/kb/976097)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|请确保每个 SQL Server 故障转移群集实例 (FCI) 都拥有标准 SQL Server 故障转移群集实例安装所要求的共享存储。||  
  
###  <a name="RelatedTasksFCIs"></a> 相关任务 (FCI)  
  
|任务|主题|  
|----------|-----------|  
|安装 SQL Server 故障转移群集|[创建新的 SQL Server 故障转移群集（安装程序）](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|您的现有 SQL Server 故障转移群集的就地升级|[升级 SQL Server 故障转移群集实例（安装程序）](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|维护您的现有 SQL Server 故障转移群集|[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> 相关内容 (FCI)  
  
-   [故障转移群集和&#40;AlwaysOn 可用性组 SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn 体系结构指南：使用故障转移群集实例和可用性组生成高可用性和灾难恢复解决方案](https://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> 可用性组先决条件和限制  

  
###  <a name="RestrictionsAG"></a> 限制（可用性组）  
  
-   **可用性副本必须由一个 WSFC 群集的不同节点承载：** 对于某一给定可用性组，可用性副本必须由在同一 WSFC 群集的不同节点上运行的服务器实例承载。 唯一的例外是在迁移到另一个 WSFC 群集时，此时一个可用性组可能会暂时跨两个群集。  
  
    > [!NOTE]  
    >  同一物理计算机上的多个虚拟机可分别为同一可用性组承载可用性副本，因为每个虚拟机都充当一个单独的计算机。  
  
-   **唯一的可用性组名称：** 每个可用性组名称在 WSFC 群集上必须唯一。 可用性组名称的最大长度为 128 个字符。  
  
-   **可用性副本：** 每个可用性组都支持一个主副本和最多八个辅助副本。 所有副本都可在异步提交模式下运行，或最多三个副本可在同步提交模式下运行（具有两个同步辅助副本的一个主副本）。  
  
-   每台计算机的可用性组和可用性数据库的最大数目：可以在计算机（VM 或物理机）上放置的数据库和可用性组的实际数目取决于硬件和工作负荷，但是没有强制限制。 Microsoft 对每个物理计算机承载 10 个可用性组和 100 个数据库进行了广泛测试。 系统过载的信号可能包括但不限于工作线程用尽、AlwaysOn 系统视图和 DMV 响应时间很长和/或调度程序系统转储停滞。 请务必用接近生产的工作负荷彻底测试您的环境，确保它可以应对您的应用程序 SLA 内的工作负荷蜂值。 考虑 SLA 时，确保考虑故障条件下的负荷以及期望的响应时间。  
  
-   **不要使用故障转移群集管理器来操作可用性组：**  
  
     例如：  
  
    -   不要更改任何可用性组属性，例如可能的所有者。  
  
    -   不要使用故障转移群集管理器来故障转移可用性组。 必须使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
###  <a name="RequirementsAG"></a> 先决条件（可用性组）  
 在创建或重新配置可用性组配置时，请确保您遵守以下要求。  
  
||先决条件|说明|  
|-|------------------|-----------------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|如果您计划使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例 (FCI) 承载可用性副本，则请确保您理解 FCI 限制并且满足 FCI 要求。|[有关使用 SQL Server 故障转移群集实例 (FCI) 承载可用性副本的先决条件和限制](#FciArLimitations) （本主题的前面予以介绍）|  
  
###  <a name="SecurityAG"></a> 安全性（可用性组）  
  
-   安全性是从 Windows Server 故障转移群集 (WSFC) 群集继承的。 WSFC 在整个 WSFC 群集 API 粒度上提供了两个级别的用户安全性：  
  
    -   只读访问  
  
    -   完全控制  
  
         [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 需要完全控制，并且在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 实例上启用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将向其提供对 WSFC 群集的完全控制（通过服务 SID）。  
  
         不能在 WSFC 故障转移群集管理器中直接添加或删除某一服务器实例的安全性。 若要管理 WSFC 安全性会话，请使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中等效的 WMI。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的每个实例都必须具有访问注册表、群集等的权限。  
  
-   我们建议您为承载 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可用性副本的服务器实例之间的连接使用加密。  
  
#### <a name="permissions-availability-groups"></a>权限（可用性组）  
  
|任务|所需权限|  
|----------|--------------------------|  
|创建可用性组|需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
|更改可用性组|对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。<br /><br /> 此外，将数据库联接到可用性组要求具有 **db_owner** 固定服务器角色的成员身份。|  
|删除可用性组|对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。 若要删除并非在本地副本位置上承载的某一可用性组，您需要针对该可用性组的 CONTROL SERVER 权限或 CONTROL 权限。|  
  
###  <a name="RelatedTasksAGs"></a> 相关任务（可用性组）  
  
|任务|主题|  
|----------|-----------|  
|创建可用性组|[使用可用性组（“新建可用性组”向导）](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [创建可用性组 (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [创建可用性组 (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [在添加或修改可用性副本时指定终结点 URL (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|修改可用性副本的数目|[将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [将次要副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|创建可用性组侦听器|[创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)|  
|删除可用性组|[删除可用性组 (SQL Server)](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> 可用性数据库先决条件和限制  
 若要符合添加到可用性组的条件，数据库必须满足以下先决条件和限制。  
  
 
  
###  <a name="RequirementsDb"></a>清单：要求（可用性数据库）  
 为了符合添加到可用性组的条件，数据库必须：  
  
||要求|链接|  
|-|------------------|----------|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是用户数据库。 系统数据库无法属于可用性组。||  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|驻留在您在其中创建可用性组并且对于服务器实例可访问的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上。||  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是读写数据库。 只读数据库不能添加到可用性组。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|是多用户数据库。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|未使用 AUTO_CLOSE。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|使用完整恢复模式。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|拥有至少一个完整的数据库备份。<br /><br /> 注意:将数据库设置为完整恢复模式之后，将需要一个完整的备份来启动完整恢复日志链。|[创建完整数据库备份 (SQL Server)](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|不属于任何现有可用性组。|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|不是为数据库镜像配置的。|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) （如果数据库未参与镜像，则所有带有“mirroring_”前缀的列将为 NULL。）|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|在将使用 FILESTREAM 的数据库添加到某一可用性组之前，请确保在承载或将承载该可用性组的可用性副本的每个服务器实例上都启用 FILESTREAM。|[启用和配置 FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![旁边](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|在将包含的数据库添加到某一可用性组之前，请确保在将承载该可用性组的可用性副本的每个服务器实例上 `contained database authentication` 服务器选项都设置为 `1`。|[contained database authentication 服务器配置选项](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [服务器配置选项 (SQL Server)](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]可使用任何受支持的数据库兼容性级别。  
  
###  <a name="RestrictionsDb"></a> 限制（可用性数据库）  
  
-   如果辅助数据库的文件路径（包括驱动器号）不同于相应主数据库的路径，则以下限制适用：  
  
    -   [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]：不支持“完全”选项（在[选择初始数据同步页](select-initial-data-synchronization-page-always-on-availability-group-wizards.md)页面上），  
  
    -   **RESTORE WITH MOVE：** 若要创建辅助数据库，在承载辅助副本的每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上数据库文件必须是 RESTORED WITH MOVE。  
  
    -   对添加文件操作的影响：以后针对主要副本的添加文件操作在辅助数据库上可能会失败。 此失败可能导致辅助数据库暂停。 而这又会导致辅助副本进入“非同步”状态。  
  
        > [!NOTE]  
        >  有关如何处理失败的添加文件操作的详细信息，请参阅[解决失败的添加文件操作问题（AlwaysOn 可用性组）](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)。  
  
-   您不能删除当前属于可用性组的数据库。  
  
###  <a name="TDEdbs"></a> 关注受 TDE 保护的数据库  
 如果使用透明数据加密 (TDE)，则用于创建和解密其他密钥的证书或非对称密钥在承载可用性组的可用性副本的每个服务器实例上必须相同。 有关详细信息，请参阅 [将受 TDE 保护的数据库移到其他 SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)。  
  
###  <a name="PermissionsDbs"></a> 权限（可用性数据库）  
 需要对数据库拥有 ALTER 权限。  
  
###  <a name="RelatedTasksADb"></a> 相关任务（可用性数据库）  
  
|任务|主题|  
|----------|-----------|  
|准备辅助数据库（手动）|[为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|将辅助数据库联接到可用性组（手动）|[将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|修改可用性数据库的数目|[将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)<br /><br /> [将辅助数据库从可用性组删除 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [Microsoft SQL Server AlwaysOn 解决方案指南以实现高可用性和灾难恢复](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 团队博客：官方 SQL Server AlwaysOn 团队博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
-   [AlwaysON-HADRON 学习系列：启用了 HADRON 的数据库的工作线程池用法](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>请参阅  
 [ &#40;AlwaysOn 可用性组 SQL Server&#41;  概述](overview-of-always-on-availability-groups-sql-server.md)  
 [故障转移群集和&#40;AlwaysOn 可用性组&#41; SQL Server](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 客户端连接（SQL Server）](always-on-client-connectivity-sql-server.md)  
  
  
