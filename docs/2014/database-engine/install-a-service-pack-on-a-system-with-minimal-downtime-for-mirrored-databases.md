---
title: 镜像数据库停机时间最短的系统上安装的 Service Pack |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779591"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>在系统上安装 Service Pack 并且尽量缩短镜像数据库停机时间
  本主题介绍了如何在安装 Service Pack 和修补程序时尽量减少镜像服务器的停机时间。 此过程包括按顺序升级参与数据库镜像的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 实例。 这种形式的更新，这被称为*滚动更新*，停机时间减少为仅一次故障转移。 请注意，对于高性能模式会话中的镜像服务器与主体服务器从地理上遥远，滚动更新可能不合适。  
  
 滚动更新是包含下列阶段的一个多阶段过程：  
  
-   保护数据。  
  
-   如果会话包括见证服务器，建议您删除见证服务器。 否则，在更新镜像服务器实例时，数据库的可用性将取决于仍然连接至主体服务器实例的见证服务器。 删除见证服务器之后，可以在滚动更新过程中随时对其进行更新，而不会有数据库停机的风险。  
  
    > [!NOTE]  
    >  有关详细信息，请参阅[仲裁：见证服务器如何影响数据库可用性（数据库镜像）](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
-   如果会话在高性能模式下运行，则将运行模式更改为高安全模式。  
  
-   更新数据库镜像中涉及的每个服务器实例。 滚动更新包括升级当前作为镜像服务器的服务器实例，对其每个镜像数据库进行手动故障转移以及升级最初作为主体服务器（现在作为新镜像服务器）的服务器实例。 此时，必须继续镜像。  
  
    > [!NOTE]  
    >  在开始滚动更新之前，建议您至少对一个镜像会话执行实际手动故障转移。  
  
-   如有必要，则恢复为高性能模式。  
  
-   如有必要，则将见证服务器返回镜像会话。  
  
 下面将介绍各个阶段的过程。  
  
> [!IMPORTANT]  
>  在并发镜像会话中，一个服务器实例可能扮演不同的镜像角色（主体服务器、镜像服务器或见证服务器）。 在这种情况下，必须相应地调整基本滚动更新过程。  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>在更新之前保护数据（最佳做法）  
  
1.  对每个主体数据库执行完整数据库备份。  
  
     **备份数据库**  
  
    -   [创建完整数据库备份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
2.  在每个主体服务器上运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
### <a name="to-remove-a-witness-from-a-session"></a>从会话中删除见证服务器  
  
1.  如果镜像会话包括见证服务器，则建议您在执行滚动更新之前删除该见证服务器。  
  
     **删除见证服务器**  
  
    -   [从数据库镜像会话删除见证服务器 (SQL Server)](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>将会话从高性能模式更改为高安全模式  
  
1.  如果镜像会话在高性能模式下运行，则在执行滚动更新之前，将运行模式更改为不带自动故障转移功能的高安全模式。 使用下列方法之一：  
  
    -   在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:更改**操作模式**选项设为**不带自动故障转移 （同步） 的高安全性**通过[镜像页](../relational-databases/databases/database-properties-mirroring-page.md)的**数据库属性**对话框。 有关如何访问此页的详细信息，请参阅[启动配置数据库镜像安全向导 (SQL Server Management Studio)](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)。  
  
    -   在[!INCLUDE[tsql](../includes/tsql-md.md)]:将事务安全设置为 FULL。 有关详细信息，请参阅[更改数据库镜像会话中的事务安全 (Transact-SQL)](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)。  
  
### <a name="to-perform-the-rolling-update"></a>执行滚动更新  
  
1.  若要尽量减少停机时间，我们建议：通过更新任何镜像服务器目前在其所有镜像会话的镜像伙伴开始滚动更新。 此时，可能需要更新多个服务器实例。  
  
    > [!NOTE]  
    >  在滚动更新过程中可以随时更新见证服务器。 例如，如果某个服务器实例在会话 1 中为镜像服务器，在会话 2 中为见证服务器，则可以立即更新此服务器实例。  
  
     要首先更新的服务器实例是由镜像会话的当前配置决定的，如下所示：  
  
    -   如果有任何服务器实例已经是其所有镜像会话中的镜像服务器，则在该服务器实例上安装 Service Pack 或修补程序。  
  
    -   如果在任何镜像会话中所有服务器实例当前都是主体服务器，则选择一个服务器实例首先更新。 然后，对其每个主体数据库进行手动故障转移，并通过安装 Service Pack 或修补程序来更新该数据库实例。  
  
     更新完成后，服务器实例将自动重新加入其每个镜像会话。  
  
     **执行手动故障转移**  
  
    -   [手动故障转移数据库镜像会话 (SQL Server Management Studio)](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [手动故障转移数据库镜像会话 (Transact-SQL)](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md)。  
  
     有关手动故障转移如何实现的详细信息，请参阅[数据库镜像会话期间的角色切换 (SQL Server)](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md) 。  
  
2.  对于其镜像服务器实例刚完成更新的每个镜像会话，请等待会话进行同步。 然后，连接到主体服务器实例并对会话进行手动故障转移。 故障转移后，已更新的服务器实例成为该会话的主体服务器，而以前的主体服务成为镜像服务器。  
  
     此步骤的目的是让其他服务器实例在其作为伙伴的每个镜像会话中成为镜像服务器。  
  
3.  完成故障转移后，我们建议您在主体数据库上运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 命令。  
  
4.  对于在其作为伙伴的所有镜像会话中目前为镜像服务器的每个服务器实例，在该服务器实例上安装 Service Pack 或修补程序。 此时，可能需要更新多个服务器。  
  
    > [!IMPORTANT]  
    >  在复杂的镜像配置中，某个服务器实例在一个或多个镜像会话中可能仍作为原始主体服务器。 对于这些服务器实例重复步骤 2-4，直至涉及的所有实例都已都更新。  
  
5.  继续镜像会话。  
  
    > [!NOTE]  
    >  更新完见证服务器后，自动故障转移功能才会起作用。  
  
6.  对于在其所有镜像会话中为见证服务器的任何剩余服务器实例，在该服务器实例上安装 Service Pack 或修补程序。 在已更新的见证服务器重新加入镜像会话之后，自动故障转移功能将重新变为可用。 此时，可能需要更新多个服务器。  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>将会话恢复为高性能模式  
  
1.  可以选择使用下列方法之一返回高性能模式：  
  
    -   在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:更改**操作模式**选项设为**高性能 （异步）** 通过[镜像页](../relational-databases/databases/database-properties-mirroring-page.md)的**数据库属性**对话框。  
  
    -   在[!INCLUDE[tsql](../includes/tsql-md.md)]:使用[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)将事务安全设置为 OFF。  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>将见证服务器返回镜像会话  
  
1.  在高安全模式下，可以选择让见证服务器重新回到每个镜像会话中。  
  
     **若要重新建立见证服务器**  
  
    -   [添加或替换数据库镜像见证服务器 (SQL Server Management Studio)](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [使用 Windows 身份验证添加数据库镜像见证服务器 (Transact-SQL)](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [数据库镜像 (SQL Server)](database-mirroring/database-mirroring-sql-server.md)   
 [数据库镜像运行模式](database-mirroring/database-mirroring-operating-modes.md)   
 [数据库镜像会话期间的角色切换 (SQL Server)](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [启动数据库镜像监视器 (SQL Server Management Studio)](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [查看镜像数据库的状态 (SQL Server Management Studio)](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
