---
title: "使用故障转移可用性组向导 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.failoverwizard.connecttoreplicas.f1"
  - "sql13.swb.failoverwizard.progress.f1"
  - "sql13.swb.failoverwizard.selectnewprimary.f1"
  - "sql13.swb.failoverwizard.f1"
  - "sql13.swb.failoverwizard.confirmdataloss.f1"
helpviewer_keywords: 
  - "故障转移 [SQL Server], 故障转移"
  - "可用性组 [SQL Server], 向导"
  - "可用性组 [SQL Server], 配置"
ms.assetid: 4a602584-63e4-4322-aafc-5d715b82b834
caps.latest.revision: 26
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 26
---
# 使用故障转移可用性组向导 (SQL Server Management Studio)
  本主题介绍了如何在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 来对 AlwaysOn 可用性组执行计划的手动故障转移或强制的手动故障转移（强制故障转移）。 可用性组在可用性副本级别进行故障转移。 如果故障转移到一个处于 SYNCHRONIZED 状态的辅助副本，则向导将执行计划的手动故障转移（不会造成数据丢失）。 如果故障转移到一个处于 UNSYNCHRONIZED 或 NOT SYNCHRONIZING 状态的次要副本，则向导将执行强制的手动故障转移（这也称为“强制故障转移”，可能造成数据丢失）。 这两种形式的手动故障转移均会将您所连接的辅助副本转换为主角色。 计划的手动故障转移当前会将先前的主副本转换为辅助角色。 在强制故障转移之后，一旦先前的主要副本联机，它就会转换为辅助角色。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [使用“故障转移可用性组向导”的先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要对可用性组执行故障转移，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **[!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] 页：**  
  
     [“选择新主要副本”页](#SelectNewPrimaryReplica)（将在本主题的后面介绍）  
  
     [“连接到副本”页](#ConnectToReplica)（将在本主题的后面介绍）  
  
     “确认可能丢失数据”页[](#ConfirmPotentialDataLoss)（将在本主题的后面介绍）  
  
     [“摘要”页（AlwaysOn 可用性组向导）](../../../database-engine/availability-groups/windows/summary-page-always-on-availability-group-wizards.md)  
  
     [“进度”页（AlwaysOn 可用性组向导）](../../../database-engine/availability-groups/windows/progress-page-always-on-availability-group-wizards.md)  
  
     [“结果”页（AlwaysOn 可用性组向导）](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 在你首次执行计划的手动故障转移之前，请参阅[执行可用性组的计划手动故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md) 中的“开始之前”部分。  
  
 在你首次执行强制故障转移之前，请参阅[执行可用性组的强制手动故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) 中的“开始之前”和“跟进：强制故障转移之后的重要任务”部分。  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   故障转移命令将在目标辅助副本接受它之后立即返回。 但是，在可用性组完成故障转移之后，数据库恢复操作将以异步方式执行。  
  
-   故障转移时，可能不维护可用性组中数据库间的跨数据库一致性。  
  
    > [!NOTE]  
    >  对跨数据库和分布式事务的支持因 SQL Server 和操作系统版本而异。 有关详细信息，请参阅[用于 AlwaysOn 可用性组和数据库镜像的跨数据库事务和分布式事务 (SQL Server)](../../../database-engine/availability-groups/windows/transactions - always on availability and database mirroring.md)。  
  
###  <a name="Prerequisites"></a> 使用“故障转移可用性组向导”的先决条件  
  
-   必须连接到承载当前可用的可用性副本的服务器实例。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **使用“故障转移可用性组向导”**  
  
1.  在对象资源管理器中，连接到承载需要进行故障转移的可用性组的辅助副本的服务器实例，然后展开服务器树。  
  
2.  依次展开“Always On 高可用性”节点和“可用性组”节点。  
  
3.  若要启动故障转移可用性组向导，请右键单击你要进行故障转移的可用性组，然后选择“故障转移”。  
  
4.  **“简介”** 页面所显示的信息取决于是否有任何辅助副本可用于计划的故障转移。 如果此页面显示“**执行此可用性组的计划故障转移**”，则您可在不造成数据丢失的情况下对可用性组进行故障转移。  
  
5.  在“选择新主要副本”页上，在你选择将成为新的主要副本的次要副本（即故障转移目标）之前，你可查看当前主要副本和 WSFC 仲裁的状态。 对于计划的手动故障转移，确保选择其 **“故障转移就绪”** 值为“**无数据丢失**”的辅助副本。 对于强制故障转移的所有可能的故障转移目标，此值将为“**数据丢失，警告(***#***)**”，其中 *#* 指示给定次要副本存在的警告数。 若要查看给定故障转移目标的警告，请单击其“故障转移就绪”值。  
  
     有关详细信息，请参阅本主题后面的 [“选择新主副本”页](#SelectNewPrimaryReplica)。  
  
6.  在 **“连接到副本”** 页上，连接到故障转移目标。 有关详细信息，请参阅本主题后面的 [“连接到副本”页](#ConnectToReplica)。  
  
7.  如果您正在执行强制故障转移，则向导将显示 **“确认可能丢失数据”** 页。 若要继续执行故障转移，则必须选择 **“单击此处以确认故障转移可能丢失数据”**。 有关详细信息，请参阅本主题后面的[“确认可能丢失数据”页](#ConfirmPotentialDataLoss)。  
  
8.  在 **“摘要”** 页上，查看故障转移到选定的辅助副本的含义。  
  
     如果您满意所做的选择，可以选择单击 **“脚本”** 以创建向导将执行的步骤的脚本。 然后，若要将可用性组故障转移到选定的辅助副本，请单击 **“完成”**。  
  
9. **“进度”** 页将显示对可用性组进行故障转移的进度。  
  
10. 当故障转移操作完成之后， **“结果”** 页将显示结果。 完成向导后，单击 **“关闭”** 以退出安装向导。  
  
     有关详细信息，请参阅[“结果”页（AlwaysOn 可用性组向导）](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md)。  
  
11. 在强制故障转移之后，请参阅 [执行可用性组的强制手动故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)中的“跟进：在强制故障转移之后”部分。  
  
## 有关此向导独有的页面的帮助  
 本节介绍 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]独有的页面。  
  
 **本节内容**  
  
-   [“选择新主副本”页](#SelectNewPrimaryReplica)  
  
-   [“连接到副本”页](#ConnectToReplica)  
  
-   [“确认可能丢失数据”页](#ConfirmPotentialDataLoss)  
  
 此向导的其他页面与一个或多个其他 AlwaysOn 可用性组向导共享帮助，并且在不同的 F1 帮助主题中进行了介绍。  
  
###  <a name="SelectNewPrimaryReplica"></a> “选择新主副本”页  
 本节介绍 **“选择新主副本”** 页的选项。 可使用此页选择可用性组将要故障转移到的辅助副本（即“故障转移目标”）。 此副本将成为新的主副本。  
  
#### 页选项  
 **当前主副本**  
 显示当前主副本的名称（如果它处于联机状态的话）。  
  
 **主副本状态**  
 显示当前主副本的状态（如果它处于联机状态的话）。  
  
 **仲裁状态**  
 显示可用性副本的以下 WSFC 仲裁状态之一：  
  
|值|说明|  
|-----------|-----------------|  
|**标准仲裁**|群集已开始标准仲裁。|  
|**强制仲裁 (Forced quorum)**|群集已开始强制仲裁。|  
|**未知仲裁**|群集仲裁状态不可用。|  
|**不适用**|承载可用性副本的节点不包含任何仲裁。|  
  
 有关详细信息，请参阅 [WSFC 仲裁模式和投票配置 (SQL Server)](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)。  
  
 **选择新主副本**  
 可使用此网格选择一个将成为新的主副本的辅助副本。 此网格中的列如下所示：  
  
 **服务器实例**  
 显示承载辅助副本的服务器实例的名称。  
  
 **可用性模式**  
 显示服务器实例的以下可用性模式之一：  
  
|值|说明|  
|-----------|-----------------|  
|**同步提交**|在同步提交模式下，在提交事务之前，同步提交主副本要等待同步提交辅助副本确认它已完成硬化日志。 同步提交模式可确保在给定的辅助数据库与主数据库同步时，充分保护已提交的事务。|  
|**异步提交**|在异步提交模式下，主副本无需等待确认异步提交辅助副本已硬化日志，便可提交事务。 异步提交模式可最大限度地减少辅助数据库上的事务滞后时间，但允许它们滞后于主数据库，因此可能会导致某些数据丢失。|  
  
 有关详细信息，请参阅[可用性模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)。  
  
 **故障转移模式**  
 显示服务器实例的以下故障转移模式之一：  
  
|值|说明|  
|-----------|-----------------|  
|**自动**|只要辅助副本与主副本进行同步，配置为进行自动故障转移的辅助副本也会支持计划的手动故障转移。|  
|**Manual**|存在两种类型的手动故障转移：计划的（不会造成数据丢失）和强制的（可能造成数据丢失）。 对于给定的辅助副本，仅支持这两种类型中的一种，具体取决于可用性模式，而对于同步提交模式，则取决于辅助副本的同步状态。 若要确定给定的辅助副本当前所支持的手动故障转移的形式，请参阅此网格的 **“故障转移就绪”** 列。|  
  
 有关详细信息，请参阅[故障转移和故障转移模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。  
  
 **故障转移就绪**  
 显示辅助副本的以下故障转移就绪情况之一：  
  
|值|说明|  
|-----------|-----------------|  
|**无数据丢失**|此辅助副本当前支持计划的故障转移。 只有当同步提交模式的辅助副本当前与主副本进行同步时，才会出现此值。|  
|**数据丢失，警告(** *#* **)**|此辅助副本当前支持强制故障转移（可能造成数据丢失）。 只要辅助副本不与主副本进行同步，就会出现此值。 有关可能的数据丢失的信息，请单击数据丢失警告链接。|  
  
 **刷新**  
 单击此按钮可更新网格。  
  
 **取消**  
 单击此选项可取消向导操作。 在 **“选择新主副本”** 页上，取消此向导将会导致其退出而不执行任何操作。  
  
###  <a name="ConfirmPotentialDataLoss"></a> “确认可能丢失数据”页  
 本节介绍 **“确认可能丢失数据”** 页（只有在执行强制故障转移时才会显示）的选项。 本主题仅供 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]使用。 可使用此页指示您是否愿意为强制对可用性组进行故障转移而承担可能造成数据丢失的风险。  
  
#### “确认可能丢失数据”选项  
 如果选定的辅助副本未与主副本进行同步，则向导将显示警告，指出故障转移到此辅助副本可能造成一个或多个数据库上的数据丢失。  
  
 **单击此处以确认故障转移可能丢失数据。**  
 如果您愿意为了使此可用性组中的数据库对用户可用而承担数据丢失的风险，则单击此复选框。 如果您不愿意承担数据丢失的风险，则可单击 **“上一步”** 返回到 **“选择新主副本”** 页，或单击 **“取消”** 以退出向导，而不对可用性组进行故障转移。  
  
 **取消**  
 单击此选项可取消向导操作。 在 **“确认可能丢失数据”** 页上，取消此向导将导致其退出而不执行任何操作。  
  
###  <a name="ConnectToReplica"></a> “连接到副本”页  
 本节介绍 **的** “连接到副本” [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]页的选项。 只有当您尚未连接到目标辅助副本时才会显示此页。 可使用此页连接到您已选择作为新的主副本的辅助副本。  
  
#### 页选项  
 **网格列：**  
 **服务器实例**  
 显示将承载可用性副本的服务器实例的名称。  
  
 **连接为**  
 显示在建立了连接后连接到服务器实例的帐户。 如果对于给定的服务器实例此列显示“**未连接**”，则您将需要单击 **“连接”** 按钮。  
  
 **Connect**  
 如果此服务器实例正基于与您将需要连接到的其他服务器实例不同的帐户运行，则单击此选项。  
  
 **取消**  
 单击此选项可取消向导操作。 在 **“连接到副本”** 页上，取消此向导将导致其退出而不执行任何操作。  
  
## 另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [故障转移和故障转移模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [执行可用性组的计划手动故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)   
 [执行可用性组的强制手动故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)   
 [通过强制仲裁进行 WSFC 灾难恢复 (SQL Server)](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  