---
title: 更改可用性副本的故障转移模式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover modes [SQL Server]
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover modes
- Availability Groups [SQL Server], configuring
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6750456d708d68e57aadd4b1139f6e108a93b9ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783021"
---
# <a name="change-the-failover-mode-of-an-availability-replica-sql-server"></a>更改可用性副本的故障转移模式 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 PowerShell 更改 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中 AlwaysOn 可用性组的可用性副本的故障转移模式。 故障转移模式是一个副本属性，用于确定在同步提交可用性模式下运行的副本的故障转移模式。 有关详细信息，请参阅[故障转移和故障转移模式（AlwaysOn 可用性组）](failover-and-failover-modes-always-on-availability-groups.md)和[可用性模式（AlwaysOn 可用性组）](availability-modes-always-on-availability-groups.md)。  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> 先决条件和限制  
  
-   只有主副本支持该任务。 您必须连接到承载主副本的服务器实例。  
  
-   SQL Server 故障转移群集实例 (FCI) 不支持通过可用性组来自动进行故障转移，因此，只能为手动故障转移配置任何由 FCI 承载的可用性副本。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **更改可用性副本的故障转移模式**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  单击要更改其副本的可用性组。  
  
4.  右键单击该副本，然后单击“属性”****。  
  
5.  在 **“可用性副本属性”** 对话框中，使用 **“故障转移模式”** 下拉列表更改此副本的故障转移模式。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **更改可用性副本的故障转移模式**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     }  )  
  
     where  
  
    -   其中，*group_name* 是可用性组的名称。  
  
    -   {'*system_name*[\\*instance_name*] "|"*FCI_network_name*[\\*instance_name*]"}  
  
         指定承载要更改的可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的地址。 此地址由以下部分组成：  
  
         *system_name*  
         为独立服务器实例所在的计算机系统的 NetBIOS 名称。  
  
         *FCI_network_name*  
         为用于访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集的网络名称，在此群集中目标服务器实例为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移伙伴 (FCI)。  
  
         *instance_name*  
         为承载目标可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 对于默认服务器实例， *instance_name* 是可选的。  
  
     有关这些参数的详细信息，请参阅 [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)。  
  
     以下示例（在 *MyAG* 可用性组的主要副本上输入）在可用性副本上（位于名为 *COMPUTER01*的计算机的默认服务器实例上）将故障转移模式更改为自动故障转移。  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-change-the-failover-mode-of-an-availability-replica"></a>更改可用性副本的故障转移模式
  
1.  将目录 (`cd`) 更改为承载主副本的服务器实例。  
  
2.  将 `Set-SqlAvailabilityReplica` cmdlet 与 `FailoverMode` 参数一起使用。 在将某一副本设置为自动故障转移时，您可能需要使用 `AvailabilityMode` 参数将该副本更改为同步提交可用性模式。  
  
     例如，以下命令将修改可用性组 `MyReplica` 中的副本 `MyAg` 以使用同步提交可用性模式和支持自动故障转移。  
  
    ```powershell
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `
     -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
若要设置并使用 SQL Server PowerShell 提供程序，请参阅[SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)。
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)  
 [可用性模式 &#40;AlwaysOn 可用性组&#41;](availability-modes-always-on-availability-groups.md)   
 [故障转移和故障转移模式 &#40;AlwaysOn 可用性组&#41;](failover-and-failover-modes-always-on-availability-groups.md) 
