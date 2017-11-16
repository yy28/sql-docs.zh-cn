---
title: "更改可用性副本的可用性模式 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 76edaa54ec25923e776324538934b0dd35a4ffac
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="change-the-availability-mode-of-an-availability-replica-sql-server"></a>更改可用性副本的可用性模式 (SQL Server)
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 PowerShell 来更改 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中 AlwaysOn 可用性组的可用性副本的可用性模式。 可用性模式是一个副本属性，用于控制以异步还是同步方式提交副本。 异步提交模式可使性能最大化，但要牺牲高可用性；它仅支持强制手动故障转移（有可能丢失数据），该故障转移一般称为*强制故障转移*。 *同步提交模式* 更多地强调高可用性而不是性能，并且一旦同步次要副本，即支持手动故障转移（也可以支持自动故障转移）。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要更改可用性副本的可用性模式，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   您必须连接到承载主副本的服务器实例。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **更改可用性组的可用性模式**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开“Always On 高可用性”节点和“可用性组”节点。  
  
3.  单击要更改其副本的可用性组。  
  
4.  右键单击该副本，然后单击“属性”。  
  
5.  在 **“可用性副本属性”** 对话框中，使用 **“可用性模式”** 下拉列表更改此副本的可用性模式。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **更改可用性组的可用性模式**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     其中， *group_name* 为可用性组的名称， *server_name* 为承载要修改的副本的服务器实例的名称。  
  
    > [!NOTE]  
    >  仅在你还指定了 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 的情况下，才支持 FAILOVER_MODE = AUTOMATIC。  
  
     在 `AccountsAG` 可用性组的主副本上输入的以下示例，针对 `INSTANCE09` 服务器实例承载的副本，将可用性模式和故障转移模式分别更改为同步提交和自动故障转移。  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **更改可用性组的可用性模式**  
  
1.  将目录 (**cd**) 更改为托管主副本的服务器实例。  
  
2.  结合使用 **Set-SqlAvailabilityReplica** cmdlet 与 **AvailabilityMode** 参数和 **FailoverMode** 参数（可选）。  
  
     例如，以下命令将修改可用性组 `MyReplica` 中的副本 `MyAg` 以使用同步提交可用性模式和支持自动故障转移。  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 **PowerShell 环境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [故障转移和故障转移模式（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
