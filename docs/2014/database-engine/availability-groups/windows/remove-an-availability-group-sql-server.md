---
title: 删除可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4227b0af8453a40e9dd63b4aef170d52f8115b2
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782929"
---
# <a name="remove-an-availability-group-sql-server"></a>删除可用性组 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中删除 AlwaysOn 可用性组。 如果在删除某一可用性组时承载可用性副本之一的服务器实例处于脱机状态，则在联机后，该服务器实例将删除本地可用性副本。 删除可用性组时，将删除任何关联的可用性组侦听器。  
  
 请注意，如果需要，您可以从拥有某一可用性组的正确安全凭据的任何 Windows Server 故障转移群集 (WSFC) 节点删除该可用性组。 因此，在某一可用性组未保留任何可用性副本时，您可以删除该可用性组。  
  
> [!IMPORTANT]  
>  如果可能，请仅在连接到承载主副本的服务器实例时删除此可用性组。 从主副本中删除此可用性组时，允许对以前的主数据库进行更改（不具有高可用性保护）。 从辅助副本中删除可用性组会使主副本处于 RESTORING 状态，且不允许对此数据库进行更改。  
  
-   **开始之前：**  
  
     [限制和建议](#Restrictions)  
  
     [安全性](#Security)  
  
-   **删除可用性组，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相关内容](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和建议  
  
-   当可用性组处于联机状态时，从辅助副本删除它会导致主副本转换为 RESTORING 状态。 因此，如果可能，请仅从承载主副本的服务器实例中删除此可用性组。  
  
-   如果您从已被 WSFC 故障转移群集删除或逐出的计算机删除某一可用性组，则该可用性组仅在本地删除。  
  
-   如果 Windows Server 故障转移群集 (WSFC) 群集没有仲裁，则避免删除可用性组。 如果在群集缺少仲裁时必须删除可用性组，则不删除群集中存储的元数据可用性组。 在群集重新获得仲裁后，将需要再次删除此可用性组以便将其从 WSFC 群集中删除。  
  
-   在辅助副本上，DROP AVAILABILITY GROUP 应仅用于紧急情况。 这是因为删除可用性组会使该可用性组脱机。 如果您从辅助副本中删除该可用性组，则主副本无法确定出现 OFFLINE 状态是因为仲裁丢失、强制故障转移还是 DROP AVAILABILITY GROUP 命令。 主副本将转换为 RESTORING 状态以避免出现可能的裂脑情况。 有关详细信息，请参阅 [工作方式：DROP AVAILABILITY GROUP 行为](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) （CSS SQL Server 工程师博客）。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。 若要删除并非由本地服务器实例承载的某一可用性组，您需要针对该可用性组的 CONTROL SERVER 权限或 CONTROL 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **删除可用性组**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，如果可能，还可以连接到 WSFC 节点（该节点拥有可用性组的正确安全凭据）上为 AlwaysOn 可用性组启用的另一个服务器实例。 展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  此步骤取决于您是要删除多个可用性组还是只删除一个可用性组，如下所示：  
  
    -   若要删除多个可用性组（其主要副本位于连接的服务器实例上），请使用“对象资源管理器详细信息”窗格查看和选择要删除的所有可用性组。 有关详细信息，请参阅[使用对象资源管理器详细信息监视可用性组 (SQL Server Management Studio)](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   若要删除单个可用性组，请在 **“对象资源管理器”** 窗格或 **“对象资源管理器详细信息”** 窗格中选择它。  
  
4.  右键单击所选的可用性组，然后选择“删除”命令。  
  
5.  在 **“删除可用性组”** 对话框中，若要删除所有列出的可用性组，请单击 **“确定”** 。 如果您不想删除所有列出的可用性组，请单击 **“取消”** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **删除可用性组**  
  
1.  连接到承载主副本的服务器实例，如果可能，还可以连接到 WSFC 节点（该节点拥有可用性组的正确安全凭据）上为 AlwaysOn 可用性组启用的另一个服务器实例。  
  
2.  按如下所示使用 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) 语句  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     其中， *group_name* 是要删除的可用性组的名称。  
  
     下面的示例将删除 `MyAG` 可用性组。  
  
    ```sql
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **删除可用性组**  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 提供程序中：  
  
1.  将目录切换 (`cd`) 到承载主副本的服务器实例，如果可能，还可以切换到 WSFC 节点（该节点拥有可用性组的正确安全凭据）上为 AlwaysOn 可用性组启用的另一个服务器实例。  
  
2.  使用 **Remove-SqlAvailabilityGroup** cmdlet。  
  
     例如，下面的命令删除名为 `MyAg`的可用性组。 可以对承载可用性组的可用性副本的任何服务器实例执行此命令。  
  
    ```powershell
    Remove-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [工作方式：DROP AVAILABILITY GROUP 行为](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) （CSS SQL Server 工程师博客）  
  
## <a name="see-also"></a>另请参阅  
 [ &#40;AlwaysOn 可用性组 SQL Server&#41;  概述](overview-of-always-on-availability-groups-sql-server.md)  
 [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)  
