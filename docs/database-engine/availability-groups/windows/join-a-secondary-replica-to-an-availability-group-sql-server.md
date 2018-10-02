---
title: 将次要副本联接到可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0c3bbe1e99f11626b42a1bf6aee0b54e823a7fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632805"
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>将辅助副本联接到可用性组 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 来将辅助副本联接到 Always On 可用性组。 在将某一辅助副本添加到一个 Always On 可用性组后，这个辅助副本必须联接到该可用性组。 该联接副本操作必须在承载辅助副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上执行。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **若要准备辅助数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **跟进：**[配置辅助数据库](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   该可用性组的主副本当前必须处于联机状态。  
  
-   您必须连接到承载尚未联接到该可用性组的辅助副本的服务器实例。  
  
-   本地服务器实例必须能够连接到承载主副本的服务器实例的数据库镜像端点。  
  
> [!IMPORTANT]  
>  如果不满足任何先决条件，联接操作将会失败。 在联接尝试失败之后，您可能需要连接到承载主副本的服务器实例以删除并重新添加辅助副本，然后您才可以将其联接到可用性组。 有关详细信息，请参阅[将辅助副本从可用性组删除 (SQL Server)](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md) 和[将辅助副本添加到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **将可用性副本联接到可用性组**  
  
1.  在对象资源管理器中，连接到承载辅助副本的服务器实例，然后单击服务器名称以便展开服务器树。  
  
2.  依次展开“Always On 高可用性”节点和“可用性组”节点。  
  
3.  选择您连接到辅助副本的可用性组。  
  
4.  右键单击辅助副本，然后单击“联接到可用性组”。  
  
5.  这将打开 **“将副本联接到可用性组”** 对话框。  
  
6.  若要将辅助副本联接到可用性组，请单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **将可用性副本联接到可用性组**  
  
1.  连接到承载辅助副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     其中， *group_name* 是可用性组的名称。  
  
     下面的示例将辅助副本联接到 `MyAG` 可用性组。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  若要查看此用于上下文的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，请参阅[创建可用性组 (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **将可用性副本联接到可用性组**  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 提供程序中：  
  
1.  将目录 (**cd**) 更改为托管辅助副本的服务器实例。  
  
2.  通过使用可用性组的名称执行 **Join-SqlAvailabilityGroup** cmdlet，将辅助副本联接到可用性组。  
  
     例如，以下命令将由位于指定路径的服务器实例承载的辅助副本联接到名为 `MyAg`的可用性组。  此服务器实例必须承载此可用性组中的辅助副本。  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 **PowerShell 环境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> 跟进：配置辅助数据库  
 对于该可用性组中的每个数据库，您在承载辅助副本的服务器实例上需要辅助数据库。 您可以在将辅助副本联接到可用性组之前或之后，按如下所述配置辅助数据库：  
  
1.  通过将 RESTORE WITH NORECOVERY 用于每个还原操作，将各个主数据库的最近数据库和日志备份还原到承载辅助副本的服务器实例。 有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)或 PowerShell 将辅助数据库联接到 Always On 可用性组。  
  
2.  将每个辅助数据库联接到可用性组。 有关详细信息，请参阅 [将辅助数据库联接到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建和配置可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组配置故障排除 (SQL Server)](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
