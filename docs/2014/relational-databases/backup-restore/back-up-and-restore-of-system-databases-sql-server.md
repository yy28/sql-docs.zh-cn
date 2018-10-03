---
title: 系统数据库的备份和还原 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83dd88ee1c95f5d88319a60b0c17e4ddc2882ef4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129149"
---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>系统数据库的备份和还原 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 维护一组系统级数据库（称为“系统数据库”），这些数据库对于服务器实例的运行至关重要。 每次进行大量更新后，都必须备份多个系统数据库。 必须备份的系统数据库包括 **msdb**、 **master**和 **model**。 如果有任何数据库在服务器实例上使用了复制，则还必须备份 **distribution** 系统数据库。 备份这些系统数据库，就可以在发生系统故障（例如硬盘丢失）时还原和恢复 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统。  
  
 下表概述了所有的系统数据库。  
  
|系统数据库|Description|是否需要备份？|恢复模式|注释|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[master](../databases/master-database.md)|记录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统的所有系统级信息的数据库。|用户帐户控制|Simple|必须经常备份 **master** ，以便根据业务需要充分保护数据。 建议使用定期备份计划，这样在大量更新之后可以补充更多的备份。|  
|[model](../databases/model-database.md)|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上为所有数据库创建的模板。|用户帐户控制|用户可配置<sup>1</sup>|仅在业务需要时备份 **model** ，例如自定义其数据库选项后立即备份。<br /><br /> **最佳方法：** 建议您仅根据需要创建 **model**的完整数据库备份。 由于 **model** 较小而且很少更改，因此无需备份日志。|  
|[msdb](../databases/msdb-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理用来安排警报和作业以及记录操作员信息的数据库。 **msdb** 还包含历史记录表，例如备份和还原历史记录表。|用户帐户控制|简单（默认值）|更新时备份 **msdb** 。|  
|[Resource](../databases/resource-database.md) (RDB)|包含附带的所有系统对象副本的只读数据库 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|否|—|**Resource** 数据库位于 mssqlsystemresource.mdf 文件中，该文件仅包含代码。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能备份 **Resource** 数据库。<br /><br /> 注意：通过将 mssqlsystemresource.mdf 文件作为二进制 (.exe) 文件而不是作为数据库文件处理，可以对该文件执行基于文件的备份或基于磁盘的备份。 但是不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还原这些备份。 只能手动还原 mssqlsystemresource.mdf 的备份副本，并且必须谨慎，不要使用过时版本或可能不安全的版本覆盖当前的 **Resource** 数据库。|  
|[tempdb](../databases/tempdb-database.md)|用于保存临时或中间结果集的工作空间。 每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时都会重新创建此数据库。 服务器实例关闭时，将永久删除 **tempdb** 中的所有数据。|否|Simple|无法备份 **tempdb** 系统数据库。|  
|[配置分发](../replication/configure-distribution.md)|只有将服务器配置为复制分发服务器时才存在此数据库。 此数据库存储元数据、各种复制的历史记录数据以及用于事务复制的事务。|用户帐户控制|Simple|有关何时备份 **distribution** 数据库的信息，请参阅[备份和还原复制的数据库](../replication/administration/back-up-and-restore-replicated-databases.md)。|  
  
 <sup>1</sup>若要了解模型的当前恢复模式，请参阅[查看或更改数据库的恢复模式&#40;SQL Server&#41; ](view-or-change-the-recovery-model-of-a-database-sql-server.md)或[sys.databases &#40;-&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
## <a name="limitations-on-restoring-system-databases"></a>对还原系统数据库的限制  
  
-   只能从在服务器实例当前运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本上创建的备份中还原系统数据库。 例如，若要还原系统数据库运行的服务器实例上[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP1。  
  
-   若要还原任何数据库，必须运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] master **数据库可供访问且至少部分可用时，才能启动** 实例。 如果 **master** 数据库不可用，则可以通过下列两种方式之一将该数据库返回到可用状态：  
  
    -   从当前数据库备份还原 **master** 。  
  
         如果你可以启动服务器实例，则应该能够从完整数据库备份还原 **master** 。  
  
    -   完全重新生成 **master** 。  
  
         如果由于 **master** 严重损坏而无法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则必须重新生成 **master**。 有关详细信息，请参阅 [重新生成系统数据库](../databases/system-databases.md)。  
  
        > [!IMPORTANT]  
        >  重新生成 **master** 将重新生成所有系统数据库。  
  
-   某些情况下，恢复模型数据库时发生的问题可能需要重新生成系统数据库或替换模型数据库的 mdf 和 ldf 文件。 有关详细信息，请参阅 [重新生成系统数据库](../databases/system-databases.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [完整数据库还原（简单恢复模式）](complete-database-restores-simple-recovery-model.md)  
  
-   [还原 master 数据库 (Transact-SQL)](restore-the-master-database-transact-sql.md)  
  
-   [查看或更改数据库的恢复模式 (SQL Server)](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [移动系统数据库](../databases/move-system-databases.md)  
  
## <a name="see-also"></a>请参阅  
 [分发数据库](../../relational-databases/replication/distribution-database.md)   
 [master 数据库](../databases/master-database.md)   
 [msdb 数据库](../databases/msdb-database.md)   
 [model 数据库](../databases/model-database.md)   
 [Resource 数据库](../databases/resource-database.md)   
 [tempdb 数据库](../databases/tempdb-database.md)  
  
  
