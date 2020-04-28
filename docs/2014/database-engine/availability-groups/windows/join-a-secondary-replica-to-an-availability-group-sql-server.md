---
title: 将次要副本联接到可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39ee8bfc079445e177aa9b175019ae385b9f9f36
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797656"
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>将辅助副本联接到可用性组 (SQL Server)
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 来将辅助副本联接到 AlwaysOn 可用性组。 在将某一辅助副本添加到一个 AlwaysOn 可用性组后，这个辅助副本必须联接到该可用性组。 该联接副本操作必须在承载辅助副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上执行。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要准备辅助数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **跟进：** [配置辅助数据库](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   该可用性组的主副本当前必须处于联机状态。  
  
-   您必须连接到承载尚未联接到该可用性组的辅助副本的服务器实例。  
  
-   本地服务器实例必须能够连接到承载主副本的服务器实例的数据库镜像端点。  
  
> [!IMPORTANT]  
>  如果不满足任何先决条件，联接操作将会失败。 在联接尝试失败之后，您可能需要连接到承载主副本的服务器实例以删除并重新添加辅助副本，然后您才可以将其联接到可用性组。 有关详细信息，请参阅[将辅助副本从可用性组删除 (SQL Server)](remove-a-secondary-replica-from-an-availability-group-sql-server.md) 和[将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **将可用性副本联接到可用性组**  
  
1.  在对象资源管理器中，连接到承载辅助副本的服务器实例，然后单击服务器名称以便展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  选择您连接到辅助副本的可用性组。  
  
4.  右键单击辅助副本，然后单击****“联接到可用性组”。  
  
5.  这将打开 **“将副本联接到可用性组”** 对话框。  
  
6.  若要将辅助副本联接到可用性组，请单击 **“确定”**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **将可用性副本联接到可用性组**  
  
1.  连接到承载辅助副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     其中， *group_name* 是可用性组的名称。  
  
     下面的示例将辅助副本联接到 `MyAG` 可用性组。  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  若要查看此用于上下文的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，请参阅[创建可用性组 (Transact-SQL)](create-an-availability-group-transact-sql.md)。  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
 **将可用性副本联接到可用性组**  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 提供程序中：  
  
1.  切换目录 (`cd`) 到承载辅助副本的服务器实例。  
  
2.  通过使用可用性组的名称执行 **Join-SqlAvailabilityGroup** cmdlet，将辅助副本联接到可用性组。  
  
     例如，以下命令将由位于指定路径的服务器实例承载的辅助副本联接到名为 `MyAg`的可用性组。  此服务器实例必须承载此可用性组中的辅助副本。  
  
    ```powershell
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-configure-secondary-databases"></a><a name="FollowUp"></a>跟进：配置辅助数据库  
 对于该可用性组中的每个数据库，您在承载辅助副本的服务器实例上需要辅助数据库。 您可以在将辅助副本联接到可用性组之前或之后，按如下所述配置辅助数据库：  
  
1.  通过将 RESTORE WITH NORECOVERY 用于每个还原操作，将各个主数据库的最近数据库和日志备份还原到承载辅助副本的服务器实例。 有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)或 PowerShell 将辅助数据库联接到 Always On 可用性组。  
  
2.  将每个辅助数据库联接到可用性组。 有关详细信息，请参阅 [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQL Server&#41;创建和配置可用性组](creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [&#41;删除 AlwaysOn 可用性组配置 &#40;SQL Server 的疑难解答](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
