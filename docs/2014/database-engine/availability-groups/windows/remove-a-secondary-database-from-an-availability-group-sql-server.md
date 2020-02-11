---
title: 从可用性组中删除辅助数据库 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.unjoindb.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], databases
ms.assetid: 4e51a570-58d7-4f01-9390-4198f3602576
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85cd7335290a619a7dd7b5e2cfcb729879bdaf6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782944"
---
# <a name="remove-a-secondary-database-from-an-availability-group-sql-server"></a>从可用性组中删除辅助数据库 (SQL Server)
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 从 AlwaysOn 可用性组中删除辅助数据库。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要删除辅助数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **跟进：**  [在从可用性组中删除辅助数据库之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a>   
###  <a name="Prerequisites"></a>先决条件和限制  
  
-   只有辅助副本支持该任务。 您必须连接到承载要从中删除数据库的辅助副本的服务器实例。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **从可用性组中删除辅助数据库**  
  
1.  在对象资源管理器中，连接到承载您要从中删除一个或多个辅助数据库的辅助副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  选择可用性组，然后展开 **“可用性数据库”** 节点。  
  
4.  此步骤取决于您是要删除多个数据库组，还是只删除一个数据库，如下所示：  
  
    -   若要删除多个数据库，请使用 **“对象资源管理器详细信息”** 窗格查看并选择所有要删除的数据库。 有关详细信息，请参阅[使用对象资源管理器详细信息监视可用性组 (SQL Server Management Studio)](use-object-explorer-details-to-monitor-availability-groups.md)。  
  
    -   若要删除单个数据库，请在 **“对象资源管理器”** 窗格或 **“对象资源管理器详细信息”** 窗格中选中该数据库。  
  
5.  右键单击选定的一个或多个数据库，然后在命令菜单中选择“删除辅助数据库”****。  
  
6.  在 **“从可用性组删除数据库”** 对话框中，要删除所有列出的数据库，则单击 **“确定”**。 如果您不想删除所有列出的数据库，请单击 **“取消”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **从可用性组中删除辅助数据库**  
  
1.  连接到承载辅助副本的服务器实例。  
  
2.  使用 [ALTER DATABASE 语句的 SET HADR 子句](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) ，如下所述：  
  
     ALTER DATABASE *database_name* SET HADR OFF  
  
     其中， *database_name* 为要从其所属的可用性组中删除的辅助数据库的名称。  
  
     下面的示例将本地辅助数据库 *MyDb2* 从其可用性组中删除。  
  
    ```sql
    ALTER DATABASE MyDb2 SET HADR OFF;  
    GO  
    ```  
  
##  <a name="PowerShellProcedure"></a>使用 PowerShell  
 **从可用性组中删除辅助数据库**  
  
1.  切换目录 (`cd`) 到承载辅助副本的服务器实例。  
  
2.  使用 **Remove-SqlAvailabilityDatabase** cmdlet，指定要从可用性组中删除的可用性数据库的名称。 当您连接到承载辅助副本的服务器实例时，只能从可用性组中删除本地辅助数据库。  
  
     例如，下面的命令从名为 `MyDb8` 的服务器实例承载的次要副本中删除辅助数据库 `SecondaryComputer\Instance`。 与已删除的辅助数据库的数据同步将停止。 此命令将不会影响主数据库或任何其他辅助数据库。  
  
    ```powershell
    Remove-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\SecondaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb8  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置并使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a>跟进：在从可用性组中删除辅助数据库之后  
 删除辅助数据库之后，它不再加入到可用性组中，有关删除的辅助数据库的所有信息都会被可用性组丢弃。 删除的辅助数据库处于 RESTORING 状态。  
  
> [!TIP]  
>  在删除辅助数据库后的较短时间中，您可能能够通过将其重新联接到可用性组，在数据库上重新启动 AlwaysOn 数据同步。 有关详细信息，请参阅 [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
 此时，可以通过多种备选方法处理删除的辅助数据库：  
  
-   如果不再需要该辅助数据库，则可以将其删除。  
  
     有关详细信息，请参阅 [DROP DATABASE (Transact SQL)](/sql/t-sql/statements/drop-database-audit-specification-transact-sql) 或[删除数据库](../../../relational-databases/databases/delete-a-database.md)。  
  
-   如果当辅助数据库已从可用性组中删除后要访问它，则可以恢复此数据库。 但是，如果恢复删除的辅助数据库，则会有两个同名的、独立但不同的数据库处于联机状态。 您必须确保客户端仅可访问当前主数据库。  
  
     有关详细信息，请参阅[恢复数据库而不还原数据 (Transact-SQL)](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [将主数据库从可用性组删除 (SQL Server)](remove-a-primary-database-from-an-availability-group-sql-server.md)  
