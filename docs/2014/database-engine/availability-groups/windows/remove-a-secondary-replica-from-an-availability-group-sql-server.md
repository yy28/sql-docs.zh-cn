---
title: 从可用性组中删除次要副本 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removesecondaryar.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 91a19eebfb03019fdbd928a340c139a23d9f27d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814073"
---
# <a name="remove-a-secondary-replica-from-an-availability-group-sql-server"></a>从可用性组中删除辅助副本 (SQL Server)
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 从 AlwaysOn 可用性组中删除辅助副本。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要删除辅助副本，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **跟进：**[在删除次要副本之后](#PostBestPractices)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   只有主副本支持该任务。  
  
-   从可用性组中仅可删除辅助副本。  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   您必须连接到承载可用性组的主副本的服务器实例。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **删除辅助副本**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  选择可用性组，然后展开 **“可用性副本”** 节点。  
  
4.  此步骤取决于您是要删除多个副本，还是只删除一个副本，如下所示：  
  
    -   若要删除多个副本，请使用 **“对象资源管理器详细信息”** 窗格查看并选择所有要删除的副本。 有关详细信息，请参阅[使用对象资源管理器详细信息监视可用性组 (SQL Server Management Studio)](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   若要删除单个副本，请在 **“对象资源管理器”** 窗格或 **“对象资源管理器详细信息”** 窗格中选中此副本。  
  
5.  右键单击选定的一个或多个次要副本，然后在命令菜单中选择“从可用性组中删除”。  
  
6.  在 **“从可用性组删除辅助副本”** 对话框中，要删除所有列出的辅助副本，请单击 **“确定”**。 如果您不想删除所有列出的副本，请单击 **“取消”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **删除辅助副本**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP group_name REMOVE REPLICA ON 'instance_name' [,...n]  
  
     其中，group_name 为可用性组的名称，instance_name 为该次要副本所在的服务器实例。  
  
     下面的示例将次要副本从 *MyAG* 可用性组中删除。 目标次要副本位于名为 COMPUTER02 的计算机上的服务器实例（名为 HADR_INSTANCE）上。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **删除辅助副本**  
  
1.  将目录 (`cd`) 更改为承载主副本的服务器实例。  
  
2.  使用 **Remove-SqlAvailabilityReplica** cmdlet。  
  
     例如，下面的命令从名为 `MyReplica` 的可用性组中删除服务器 `MyAg`上的可用性副本。  此命令必须在承载可用性组的主副本的服务器实例上运行。  
  
    ```  
    Remove-SqlAvailabilityReplica `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="PostBestPractices"></a>跟进：在删除次要副本之后  
 如果您指定一个当前不可用的副本，则在该副本联机时，将发现该副本已被删除。  
  
 删除副本会导致它停止接收数据。 在某个辅助副本确认其已从全局存储中删除之后，该副本将从其数据库（在本地服务器实例上保留为 RECOVERING 状态）中删除可用性组设置。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [将次要副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [删除可用性组 (SQL Server)](remove-an-availability-group-sql-server.md)  
  
  
