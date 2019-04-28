---
title: 将数据库添加到可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69d148f9ef780e28300a6d3e233f2b680f0d37d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62791941"
---
# <a name="add-a-database-to-an-availability-group-sql-server"></a>将数据库添加到可用性组 (SQL Server)
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 将数据库添加到 AlwaysOn 可用性组。  
  
-   **开始之前：**  
  
     [先决条件和限制](#Prerequisites)  
  
     [权限](#Permissions)  
  
-   **若要将数据库添加到可用性组，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件和限制  
  
-   您必须连接到承载主副本的服务器实例。  
  
-   数据库必须位于承载主副本的服务器实例上并符合可用性数据库的先决条件和限制。 有关详细信息，请参阅[针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
###  <a name="Security"></a> 安全性  
  
###  <a name="Permissions"></a> Permissions  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **将数据库添加到可用性组**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  右键单击可用性组，然后选择下列命令之一：  
  
    -   若要启动“将数据库添加到可用性组向导”，请选择 **“添加数据库”** 命令。 有关详细信息，请参阅[使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](availability-group-add-database-to-group-wizard.md)。  
  
    -   若要通过在 **“可用性组属性”** 对话框中指定一个或多个数据库来进行添加，则选择 **“属性”** 命令。 添加数据库的步骤如下所示：  
  
        1.  在 **“可用性数据库”** 窗格中，单击 **“添加”** 按钮。 这将创建并选择一个空数据库字段。  
  
        2.  输入符合可用性数据库先决条件的数据库的名称。  
  
         若要添加其他数据库，请重复前面的步骤。 当您完成指定数据库后，请单击 **“确定”** 以完成此操作。  
  
         在您使用 **“可用性组属性”** 对话框将数据库添加到可用性组后，需要在承载辅助副本的每个服务器实例上配置相应的辅助数据库。 有关详细信息，请参阅[启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **将数据库添加到可用性组**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* ADD DATABASE *database_name* [,...*n*]  
  
     其中 *group_name* 是可用性组的名称， *database_name* 是要添加到该组的数据库的名称。  
  
     以下示例添加 *MyDb3* 数据库到 *MyAG* 可用性组。  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  在您将数据库添加到可用性组后，需要在承载辅助副本的每个服务器实例上配置相应的辅助数据库。 有关详细信息，请参阅[启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **将数据库添加到可用性组**  
  
1.  将目录 (`cd`) 更改为承载主副本的服务器实例。  
  
2.  使用 `Add-SqlAvailabilityDatabase` cmdlet。  
  
     例如，以下命令将添加辅助数据库 `MyDd` 到 `MyAG` 可用性组中，其主副本由 `PrimaryServer\InstanceName`承载。  
  
    ```  
  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
3.  在您将数据库添加到可用性组后，需要在承载辅助副本的每个服务器实例上配置相应的辅助数据库。 有关详细信息，请参阅[启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
 有关完整示例，请参阅下面的 [示例 (PowerShell)](#PSExample)。  
  
###  <a name="PSExample"></a> 示例 (PowerShell)  
 下面的示例说明了一个完整过程：从承载可用性组主副本的服务器实例上的一个数据库中准备一个辅助数据库，将此数据库添加到可用性组（作为主数据库），然后将此辅助数据库加入可用性组。 首先，该示例备份数据库及其事务日志。 然后，此示例将数据库和日志备份还原到承载辅助副本的服务器实例。  
  
 此示例调用两次 `Add-SqlAvailabilityDatabase`：第一次是针对主副本调用，以便将数据库添加到可用性组；然后对辅助副本调用，以便将该副本上的辅助数据库加入到可用性组。 如果您有多个辅助副本，则对其中每个副本还原和加入辅助数据库。  
  
```  
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"  
  
```  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)   
 [使用 AlwaysOn 仪表板&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [监视可用性组 (Transact-SQL)](monitor-availability-groups-transact-sql.md)  
  
  
