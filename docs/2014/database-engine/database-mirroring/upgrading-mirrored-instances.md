---
title: 升级服务器实例时，尽量减少镜像数据库的停机时间 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server, rolling upgrade of mirrored databases
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
ms.assetid: 0e73bd23-497d-42f1-9e81-8d5314bcd597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 857e18b1b956d3d8c9d2fc4c5692dbf022bf85fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754272"
---
# <a name="minimize-downtime-for-mirrored-databases-when-upgrading-server-instances"></a>在升级服务器实例时最大限度地减少镜像数据库的停机时间
  升级到的服务器实例时[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，你可以减少每个镜像数据库的停机时间仅一次的手动故障转移到按顺序进行升级，称为*滚动升级*。 滚动升级是一个多阶段过程，其最简单的形式如下：升级当前在镜像会话中充当镜像服务器的服务器实例，然后对镜像数据库进行手动故障转移，升级以前的主体服务器，恢复镜像。 实际上，确切过程将取决于运行模式以及在所升级的服务器实例上运行的镜像会话的编号和布局。  
  
> [!NOTE]  
>  有关执行滚动升级，以安装 service pack 或修补程序的信息，请参阅[为镜像数据库停机时间最短的系统上安装 Service Pack](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)。  
  
 **建议的准备工作 （最佳实践）**  
  
 在开始滚动升级之前，建议您：  
  
1.  至少对一个镜像会话执行实际手动故障转移：  
  
    -   [手动故障转移数据库镜像会话 (SQL Server Management Studio)](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [手动故障转移数据库镜像会话 (Transact-SQL)](manually-fail-over-a-database-mirroring-session-transact-sql.md)。  
  
    > [!NOTE]  
    >  有关手动故障转移如何实现的详细信息，请参阅[数据库镜像会话期间的角色切换 (SQL Server)](role-switching-during-a-database-mirroring-session-sql-server.md) 。  
  
2.  保护数据：  
  
    1.  对每个主体数据库执行完整数据库备份：  
  
         [创建完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
    2.  在每个主体服务器上运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
 **滚动升级的阶段**  
  
 滚动升级的具体步骤取决于镜像配置的运行模式。 不过基本阶段是相同的。  
  
> [!NOTE]  
>  有关运行模式的详细信息，请参阅 [数据库镜像运行模式](database-mirroring-operating-modes.md)。  
  
 下图是显示各个运行模式的滚动升级基本阶段的流程图。 该图后面的内容介绍了对应的步骤。  
  
 ![显示滚动升级步骤的流程图](../media/dbm-rolling-upgrade.gif "显示滚动升级步骤的流程图")  
  
> [!IMPORTANT]  
>  在并发镜像会话中，一个服务器实例可能扮演不同的镜像角色（主体服务器、镜像服务器或见证服务器）。 在这种情况下，必须相应地调整基本滚动升级过程。 有关详细信息，请参阅 [数据库镜像会话期间的角色切换 (SQL Server)](role-switching-during-a-database-mirroring-session-sql-server.md)的各版本中均未提供见证服务器实例。  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>将会话从高性能模式更改为高安全模式  
  
1.  如果镜像会话在高性能模式下运行，则在执行滚动升级之前，将运行模式更改为不带自动故障转移功能的高安全模式。  
  
    > [!IMPORTANT]  
    >  如果镜像服务器与主体服务器在地理位置上存有一定距离，则可能不适宜进行滚动升级。  
  
    -   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中：使用“数据库属性”对话框中的[镜像页](../../relational-databases/databases/database-properties-mirroring-page.md)将“操作模式”选项更改为“不带自动故障转移功能的高安全(同步)”。 有关如何访问此页的详细信息，请参阅[启动配置数据库镜像安全向导 (SQL Server Management Studio)](start-the-configuring-database-mirroring-security-wizard.md)。  
  
    -   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中：将事务安全设置为 FULL。 有关详细信息，请参阅[更改数据库镜像会话中的事务安全 (Transact-SQL)](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
### <a name="to-remove-a-witness-from-a-session"></a>从会话中删除见证服务器  
  
1.  如果镜像会话包括见证服务器，则建议您在执行滚动升级之前删除该见证服务器。 否则，在升级镜像服务器实例时，数据库的可用性将取决于仍然连接至主体服务器实例的见证服务器。 删除见证服务器之后，可以在滚动升级过程中随时对其进行升级，而不会有数据库停机的风险。  
  
    > [!NOTE]  
    >  有关详细信息，请参阅[仲裁：见证服务器如何影响数据库可用性（数据库镜像）](quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
    -   [从数据库镜像会话删除见证服务器 (SQL Server)](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-perform-the-rolling-upgrade"></a>执行滚动升级  
  
1.  为了最大限度地减少停机时间，我们建议：通过更新任何当前在其所有镜像会话中均为镜像服务器的镜像伙伴开始滚动升级。 此时，可能需要更新多个服务器实例。  
  
    > [!NOTE]  
    >  在滚动升级过程中可以随时升级见证服务器。 例如，如果某个服务器实例在会话 1 中为镜像服务器，在会话 2 中为见证服务器，则可以立即升级此服务器实例。  
  
     要首先升级的服务器实例是由镜像会话的当前配置决定的，如下所示：  
  
    -   如果任何服务器实例在其所有镜像会话中均已为镜像服务器，则将此服务器实例升级为新版本。  
  
    -   如果在任何镜像会话中所有服务器实例当前都是主体服务器，则选择一个要首先升级的服务器实例。 然后，对其每个主体数据库进行手动故障转移并升级该服务器实例。  
  
     升级完成后，服务器实例将自动重新加入其每个镜像会话。  
  
2.  对于其镜像服务器实例刚完成升级的每个镜像会话，请等待会话进行同步。 然后，连接到主体服务器实例并对会话进行手动故障转移。 故障转移后，已升级的服务器实例成为该会话的主体服务器，而以前的主体服务成为镜像服务器。  
  
     此步骤的目的是让其他服务器实例在其作为伙伴的每个镜像会话中成为镜像服务器。  
  
     **在出现故障时转移到已升级的服务器实例后的限制。**  
  
     在从早期服务器实例故障转移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器实例后，数据库会话将挂起。 直到升级完其他伙伴后，此会话才能继续。 但主体服务器仍然接受连接，并允许对主体数据库进行数据访问和修改。  
  
    > [!NOTE]  
    >  如果建立新镜像会话，则要求所有服务器实例运行相同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
3.  故障转移后，我们建议你运行[DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) theprincipal 数据库命令。  
  
4.  升级在其作为伙伴的所有镜像会话中目前为镜像服务器的每个服务器实例。 此时，可能需要更新多个服务器。  
  
    > [!IMPORTANT]  
    >  在复杂的镜像配置中，某个服务器实例在一个或多个镜像会话中可能仍作为原始主体服务器。 对这些服务器实例重复步骤 2-4，直至涉及的所有实例均已升级。  
  
5.  继续镜像会话。  
  
    > [!NOTE]  
    >  升级完见证服务器并将其重新添加到镜像会话中之后，自动故障转移功能才会起作用。  
  
6.  升级在其所有镜像会话中为见证服务器的任何剩余服务器实例。 在已升级的见证服务器重新加入镜像会话之后，自动故障转移功能将重新变为可用。 此时，可能需要更新多个服务器。  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>将会话恢复为高性能模式  
  
1.  可以选择使用下列方法之一返回高性能模式：  
  
    -   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中：使用“数据库属性”对话框中的[镜像页](../../relational-databases/databases/database-properties-mirroring-page.md)将“操作模式”选项更改为“高性能(同步)”。  
  
    -   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中：使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) 将事务安全设置为 OFF。  
  
### <a name="to-add-a-witness-back-into-a-mirroring-session"></a>将见证服务器重新添加到镜像会话中  
  
1.  在高安全模式下，可以选择让见证服务器重新回到每个镜像会话中。  
  
     **返回见证服务器**  
  
    -   [添加或替换数据库镜像见证服务器 (SQL Server Management Studio)](add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [使用 Windows 身份验证添加数据库镜像见证服务器 (Transact-SQL)](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [查看镜像数据库的状态 (SQL Server Management Studio)](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)   
 [镜像数据库停机时间最短的系统上安装的 Service Pack](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)   
 [数据库镜像会话期间的角色切换 (SQL Server)](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [在数据库镜像会话中强制服务 (Transact-SQL)](force-service-in-a-database-mirroring-session-transact-sql.md)   
 [启动数据库镜像监视器 (SQL Server Management Studio)](start-database-mirroring-monitor-sql-server-management-studio.md)   
 [数据库镜像运行模式](database-mirroring-operating-modes.md)  
  
  
