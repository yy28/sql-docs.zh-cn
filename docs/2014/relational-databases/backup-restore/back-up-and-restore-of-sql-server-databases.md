---
title: SQL Server 数据库的备份和还原 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96eab9a3b388c8cb68203dce22e8bd1abc013e4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922933"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>SQL Server 数据库的备份和还原
  本主题介绍备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的优点、基本的备份和还原术语，还介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的备份和还原策略以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份和还原的安全注意事项。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份和还原组件为保护存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的关键数据提供了基本安全保障。 为了最大限度地降低灾难性数据丢失的风险，您需要定期备份数据库以保留对数据所做的修改。 规划良好的备份和还原策略有助于防止数据库因各种故障而造成数据丢失。 通过还原一组备份，然后恢复数据库来测试您的策略，以便为有效地应对灾难做好准备。  
  
 除了在本地存储中存储备份外，SQL Server 还支持备份到 Windows Azure Blob 存储服务和从其还原。 有关详细信息，请参阅 [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  

  
##  <a name="Benefits"></a> 优势  
  
-   备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库、在备份上运行测试还原过程以及在另一个安全位置存储备份副本可防止可能的灾难性数据丢失。  
  
    > [!IMPORTANT]  
    >  这是可靠地保护您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据的唯一方法。  
  
     使用有效的数据库备份，可从多种故障中恢复数据，例如：  
  
    -   介质故障。  
  
    -   用户错误（例如，误删除了某个表）。  
  
    -   硬件故障（例如，磁盘驱动器损坏或服务器报废）。  
  
    -   自然灾难。 通过使用 SQL Server 备份到 Windows Azure Blob 存储服务，您可以在本地位置之外的其他区域创建一个站外备份，这样在发生影响您的本地位置的自然灾难时仍可以使用数据库。  
  
-   此外，数据库备份对于进行日常管理（如将数据库从一台服务器复制到另一台服务器、设置 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 或数据库镜像以及进行存档）非常有用。  
  

  
##  <a name="TermsAndDefinitions"></a> 组件和概念  
 备份 [动词] (back up)  
 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库或其事务日志中将数据或日志记录复制到备份设备（如磁盘），以创建数据备份或日志备份。  
  
 备份 [名词] (backup)  
 可用于在出现故障后还原或恢复数据的数据副本。 数据库备份还可用于将数据库副本还原到新位置。  
  
 备份设备 (backup device)  
 要写入 SQL Server 备份及能从中还原这些备份的磁盘或磁带设备。 SQL Server 备份也可以写入 Windows Azure Blob 存储服务，并且使用 **URL** 格式来指定备份文件的目标和名称。 有关详细信息，请参阅 [SQL Server Backup and Restore with Windows Azure Blob Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 备份介质  
 已写入一个或多个备份的一个或多个磁带或磁盘文件。  
  
 数据备份 (data backup)  
 完整数据库的数据备份（数据库备份）、部分数据库的数据备份（部分备份）或一组数据文件或文件组（文件备份）。  
  
 数据库备份 (database backup)  
 数据库的备份。 完整数据库备份表示备份完成时的整个数据库。 差异数据库备份只包含自最近完整备份以来对数据库所做的更改。  
  
 差异备份 (differential backup)  
 一种数据备份，基于完整数据库或部分数据库或一组数据文件或文件组（差异基准）的最新完整备份，并且仅包含自确定差异基准以来发生更改的数据。  
  
 完整备份 (full backup)  
 一种数据备份，包含特定数据库或者一组特定的文件组或文件中的所有数据，以及可以恢复这些数据的足够的日志。  
  
 日志备份 (log backup)  
 包括以前日志备份中未备份的所有日志记录的事务日志备份。 （完整恢复模式）  
  
 恢复 (recover)  
 将数据库恢复到稳定且一致的状态。  
  
 recovery  
 将数据库恢复到事务一致状态的数据库启动阶段或 Restore With Recovery 阶段。  
  
 恢复模式  
 用于控制数据库上的事务日志维护的数据库属性。 有三种恢复模式：简单恢复模式、完整恢复模式和大容量日志恢复模式。 数据库的恢复模式确定其备份和还原要求。  
  
 还原 (restore)  
 一种包括多个阶段的过程，用于将指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份中的所有数据和日志页复制到指定数据库，然后通过应用记录的更改使该数据在时间上向前移动，以前滚备份中记录的所有事务。  
  

  
##  <a name="BnrStrategies"></a> 备份和还原策略简介  
 备份和还原数据必须根据特定环境进行自定义，并且必须使用可用资源。 因此，可靠使用备份和还原以实现恢复需要有一个备份和还原策略。 设计良好的备份和还原策略在考虑到特定业务要求的同时，可以尽量提高数据的可用性并尽量减少数据的丢失。  
  
> [!IMPORTANT]  
>  请将数据库和备份放置在不同的设备上。 否则，如果包含数据库的设备失败，备份也将不可用。 此外，将数据和备份放置在不同的设备上还可以提高写入备份和使用数据库时的 I/O 性能。  
  
 备份和还原策略包含备份部分和还原部分。 策略的备份部分定义备份的类型和频率、备份所需硬件的特性和速度、备份的测试方法以及备份介质的存储位置和方法（包括安全注意事项）。 策略的还原部分定义负责执行还原的人员以及如何执行还原以满足数据库可用性和尽量减少数据丢失的目标。 建议您将备份和还原过程记录下来并在运行手册中保留记录文档的副本。  
  
 设计有效的备份和还原策略需要仔细计划、实现和测试。 测试是必需环节。 直到成功还原了还原策略中所有组合内的备份后，才会生成备份策略。 必须考虑各种因素。 其中包括：  
  
-   您的组织对数据库的生产目标，尤其是对可用性和防止数据丢失的要求。  
  
-   每个数据库的特性，包括：大小、使用模式、内容特性以及数据要求等。  
  
-   对资源的约束，例如：硬件、人员、备份介质的存储空间以及所存储介质的物理安全性等。  
  
    > [!NOTE]  
    >  在 64 位和 32 位环境中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘存储格式均相同。 因此，可以将 32 位环境中的备份还原到 64 位环境中，反之亦然。 在运行在某个环境中的服务器实例上，可以还原在运行在另一个环境中的服务器实例上创建的备份。  
  

  
### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>恢复模式对备份和还原的影响  
 备份和还原操作发生在恢复模式的上下文中。 恢复模式是一种数据库属性，用于控制事务日志的管理方式。 此外，数据库的恢复模式还决定数据库支持的备份类型和还原方案。 通常，数据库使用简单恢复模式或完整恢复模式。 可以在执行大容量操作之前切换到大容量日志恢复模式，以补充完整恢复模式。 有关这些恢复模式以及它们是如何影响事务日志管理方式的说明，请参阅[事务日志 (SQL Server)](../logs/the-transaction-log-sql-server.md)。  
  
 数据库的最佳恢复模式取决于您的业务要求。 若要免去事务日志管理工作并简化备份和还原，请使用简单恢复模式。 若要在管理开销一定的情况下使工作丢失的可能性降到最低，请使用完整恢复模式。 有关恢复模式对备份和还原存在哪些影响的信息，请参阅[备份概述 (SQL Server)](backup-overview-sql-server.md)。  
  
### <a name="design-the-backup-strategy"></a>设计备份策略  
 当为特定数据库选择了满足业务要求的恢复模式后，需要计划并实现相应的备份策略。 最佳备份策略取决于各种因素，以下因素尤其重要：  
  
-   一天中应用程序访问数据库的时间有多长？  
  
     如果存在一个可预测的非高峰时段，则建议您将完整数据库备份安排在此时段。  
  
-   更改和更新可能发生的频率如何？  
  
     如果更改经常发生，请考虑下列事项：  
  
    -   在简单恢复模式下，请考虑将差异备份安排在完整数据库备份之间。 差异备份只能捕获自上次完整数据库备份之后的更改。  
  
    -   在完整恢复模式下，应安排经常的日志备份。 在完整备份之间安排差异备份可减少数据还原后需要还原的日志备份数，从而缩短还原时间。  
  
-   可能只是更改数据库的小部分内容，还是需要更改数据库的大部分内容？  
  
     对于更改集中于部分文件或文件组的大型数据库，部分备份和/或文件备份非常有用。 有关详细信息，请参阅[部分备份 (SQL Server)](partial-backups-sql-server.md) 和[完整文件备份 (SQL Server)](full-file-backups-sql-server.md)。  
  
-   完整数据库备份需要多少磁盘空间？  
  
     有关详细信息，请参阅本部分后面的 [估计完整数据库备份的大小](#EstimateDbBuSize)。  
  
####  <a name="EstimateDbBuSize"></a> 估计完整数据库备份的大小  
 在实现备份与还原策略之前，应当估计完整数据库备份将使用的磁盘空间。 备份操作会将数据库中的数据复制到备份文件。 备份仅包含数据库中的实际数据，而不包含任何未使用的空间。 因此，备份通常小于数据库本身。 你可以使用 **sp_spaceused** 系统存储过程估计完整数据库备份的大小。 有关详细信息，请参阅 [sp_spaceused (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)。  
  
### <a name="schedule-backups"></a>计划备份  
 执行备份操作对运行中的事务影响很小，因此可以在正常操作过程中执行备份操作。 您可以在对生产工作负荷的影响很小的情况下执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份。  
  
> [!NOTE]  
>  有关备份过程中的并发限制的信息，请参阅 [备份概述 (SQL Server)](backup-overview-sql-server.md)。  
  
 确定所需的备份类型和必须执行每种备份类型的频率后，建议您将定期备份计划为数据库维护计划的一部分。 有关维护计划以及如何为数据库备份和日志备份创建维护计划的信息，请参阅 [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  
### <a name="test-your-backups"></a>测试备份  
 直到完成备份测试后，才会生成还原策略。 必须通过将数据库副本还原到测试系统，针对每个数据库的备份策略进行全面测试。 您必须对每种要使用的备份类型进行还原测试。  
  
 建议您为每个数据库维护一个操作手册。 此操作手册应记录备份的位置、备份设备名称（如果有），以及还原测试备份所需的时间。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
### <a name="scheduling-backup-jobs"></a>计划备份作业  
  
-   [创建维护计划](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   [创建作业](../../ssms/agent/create-a-job.md)  
  
-   [安排作业计划](../../ssms/agent/schedule-a-job.md)  
  
### <a name="working-with-backup-devices-and-backup-media"></a>使用备份设备和备份介质  
  
-   [为磁盘文件定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [为磁带驱动器定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [将磁盘或磁带指定为备份目标 (SQL Server)](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [删除备份设备 (SQL Server)](delete-a-backup-device-sql-server.md)  
  
-   [设置备份的过期日期 (SQL Server)](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [查看备份磁带或文件的内容 (SQL Server)](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [查看备份集中的数据文件和日志文件 (SQL Server)](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [查看逻辑备份设备的属性和内容 (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [从设备还原备份 (SQL Server)](restore-a-backup-from-a-device-sql-server.md)  
  
### <a name="creating-backups"></a>创建备份  
  
> [!NOTE]  
>  对于部分备份或仅复制备份，必须分别使用带 PARTIAL 或 COPY_ONLY 选项的 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) 语句。  
  
 **使用 SQL Server Management Studio**  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
-   [备份文件和文件组 (SQL Server)](back-up-files-and-filegroups-sql-server.md)  
  
-   [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
 **使用 Transact-SQL**  
  
-   [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [在数据库损坏时备份事务日志 (SQL Server)](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [在备份或还原期间启用或禁用备份校验和 (SQL Server)](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [指定备份或还原操作在遇到错误后是继续还是停止 (SQL Server)](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  

  
### <a name="restoring-data-backups"></a>还原数据备份  
 **使用 SQL Server Management Studio**  
  
-   [还原数据库备份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [将数据库还原到新位置 (SQL Server)](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [还原差异数据库备份 (SQL Server)](restore-a-differential-database-backup-sql-server.md)  
  
-   [还原文件和文件组 (SQL Server)](restore-files-and-filegroups-sql-server.md)  
  
 **使用 Transact-SQL**  
  
-   [在简单恢复模式下还原数据库备份 (Transact-SQL)](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [在完整恢复模式下将数据库还原到故障点 (Transact-SQL)](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [在现有文件上还原文件和文件组 (SQL Server)](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [将文件还原到新位置 (SQL Server)](restore-files-to-a-new-location-sql-server.md)  
  
-   [还原 master 数据库 (Transact-SQL)](restore-the-master-database-transact-sql.md)  
  

  
### <a name="restoring-transaction-logs-full-recovery-model"></a>还原事务日志（完整恢复模式）  
 **使用 SQL Server Management Studio**  
  
-   [将数据库还原到标记的事务 (SQL Server Management Studio)](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
-   [将 SQL Server 数据库还原到某个时间点（完整恢复模式）](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 **使用 Transact-SQL**  
  
-   [将 SQL Server 数据库还原到某个时间点（完整恢复模式）](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  

  
### <a name="additional-restore-tasks"></a>其他还原任务  
 **使用 Transact-SQL**  
  
-   [重新启动中断的还原操作 (Transact-SQL)](restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [恢复数据库但不还原数据 (Transact-SQL)](recover-a-database-without-restoring-data-transact-sql.md)  
  

  
## <a name="see-also"></a>请参阅  
 [备份概述 (SQL Server)](backup-overview-sql-server.md)   
 [还原和恢复概述 (SQL Server)](restore-and-recovery-overview-sql-server.md)   
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [备份和还原全文目录和索引](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [备份和还原复制的数据库](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [事务日志 (SQL Server)](../logs/the-transaction-log-sql-server.md)   
 [恢复模式 (SQL Server)](recovery-models-sql-server.md)   
 [媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
