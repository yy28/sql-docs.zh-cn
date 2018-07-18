---
title: 事务日志 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdaae11d21d1018e0c855036c4c82221c57a905d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223320"
---
# <a name="the-transaction-log-sql-server"></a>事务日志 (SQL Server)
  每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库都具有事务日志，用于记录所有事务以及每个事务对数据库所做的修改。 必须定期截断事务日志以避免它被填满。 但是，一些因素可能延迟日志截断，因此监视日志大小很重要。 某些操作可以最小日志量进行记录以减少其对事务日志大小的影响。  
  
 事务日志是数据库的重要组件，如果系统出现故障，则可能需要使用事务日志将数据库恢复到一致状态。 删除或移动事务日志以前，必须完全了解此操作带来的后果。  
  
> [!NOTE]  
>  检查点会创建一些正常点，在数据库恢复期间将从这些正常点开始应用事务日志。 有关详细信息，请参阅[数据库检查点 (SQL Server)](database-checkpoints-sql-server.md)。  
  
 **本主题内容：**  
  
-   [支持的事务日志的优势： 操作](#Benefits)  
  
-   [事务日志截断](#Truncation)  
  
-   [可能延迟日志截断的因素](#FactorsThatDelayTruncation)  
  
-   [可以按最小方式记录的操作](#MinimallyLogged)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="Benefits"></a> 支持的事务日志的优势： 操作  
 事务日志支持以下操作：  
  
-   恢复个别的事务。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动时恢复所有未完成的事务。  
  
-   将还原的数据库、文件、文件组或页前滚至故障点。  
  
-   支持事务复制。  
  
-   支持高可用性和灾难恢复解决方案： [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]、数据库镜像和日志传送。  
  
##  <a name="Truncation"></a> 事务日志截断  
 日志截断将释放日志文件的空间，以便由事务日志重新使用。 日志截断主要用于阻止日志填充。 日志截断可从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的逻辑事务日志中删除不活动的虚拟日志文件，释放逻辑日志中的空间以便物理事务日志重用这些空间。 如果事务日志从不截断，它最终将填满分配给物理日志文件的所有磁盘空间。  
  
 为了避免这个问题，除非由于某些原因延迟日志截断，否则将在以下事件后自动进行截断：  
  
-   简单恢复模式下，在检查点之后发生。  
  
-   在完整恢复模式或大容量日志恢复模式下，如果自上一次备份后生成检查点，则在日志备份后进行截断（除非是仅复制日志备份）。  
  
 有关详细信息，请参阅本主题后面的 [可能延迟日志截断的因素](#FactorsThatDelayTruncation)。  
  
> [!NOTE]  
>  日志截断并不减小物理日志文件的大小。 若要减少物理日志文件的物理大小，需要收缩日志文件。 有关收缩物理日志文件大小的信息，请参阅 [管理事务日志文件的大小](manage-the-size-of-the-transaction-log-file.md)。  
  
##  <a name="FactorsThatDelayTruncation"></a> 可能延迟日志截断的因素  
 在日志记录长时间处于活动状态时，事务日志截断将延迟，事务日志可能填满。  
  
> [!IMPORTANT]  
>  有关如何响应已满事务日志的信息，请参阅[解决事务日志已满的问题（SQL Server 错误 9002）](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)。  
  
 日志截断会由于多种因素发生延迟。 可以查询 **sys.databases** 目录视图的 **log_reuse_wait** 和 [log_reuse_wait_desc](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列来发现是哪些因素（如果有）阻止截断日志。 下表对这些列的值进行了说明。  
  
|log_reuse_wait 值|log_reuse_wait_desc 值|Description|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|当前有一个或多个可重复使用的虚拟日志文件。|  
|@shouldalert|CHECKPOINT|自上次日志截断之后，尚未生成检查点，或者日志头尚未跨一个虚拟日志文件移动。 （所有恢复模式）<br /><br /> 这是日志截断延迟的常见原因。 有关详细信息，请参阅[数据库检查点 (SQL Server)](database-checkpoints-sql-server.md)。|  
|2|LOG_BACKUP|在截断事务日志前，需要进行日志备份。 （仅限完整恢复模式或大容量日志恢复模式）<br /><br /> 完成下一个日志备份后，一些日志空间可能变为可重复使用。|  
|3|ACTIVE_BACKUP_OR_RESTORE|数据备份或还原正在进行（所有恢复模式）。<br /><br /> 如果数据备份阻止了日志截断，则取消备份操作可能有助于解决备份直接导致的此问题。|  
|4|ACTIVE_TRANSACTION|事务处于活动状态（所有恢复模式）。<br /><br /> 一个长时间运行的事务可能存在于日志备份的开头。 在这种情况下，可能需要进行另一个日志备份才能释放空间。 请注意，长时间运行的事务将阻止所有恢复模式，包括简单恢复模式，在其下截断事务日志是通常在每个自动检查点模式下的日志截断。<br /><br /> 延迟事务。 “延迟的事务  ”是有效的活动事务，因为某些资源不可用，其回滚受阻。 有关导致事务延迟的原因以及如何使它们摆脱延迟状态的信息，请参阅[延迟的事务 (SQL Server)](../backup-restore/deferred-transactions-sql-server.md)。 <br /><br />长时间运行的事务也可能会填满 tempdb 的事务日志。 Tempdb 由用户事务隐式用于内部对象，例如用于排序的工作表、用于哈希的工作文件、游标工作表，以及行版本控制。 即使用户事务只包括读取数据 （SELECT 查询），可能会创建内部对象，并在用户事务中使用。 然后就会填充 tempdb 事务日志。|  
|5|DATABASE_MIRRORING|数据库镜像暂停，或者在高性能模式下，镜像数据库明显滞后于主体数据库。 （仅限完整恢复模式）<br /><br /> 有关详细信息，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。|  
|6|REPLICATION|在事务复制过程中，与发布相关的事务仍未传递到分发数据库。 （仅限完整恢复模式）<br /><br /> 有关事务复制的信息，请参阅 [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md)。|  
|7|DATABASE_SNAPSHOT_CREATION|正在创建数据库快照。 （所有恢复模式）<br /><br /> 这是日志截断延迟的常见原因，通常也是主要原因。|  
|8|LOG_SCAN|发生日志扫描。 （所有恢复模式）<br /><br /> 这是日志截断延迟的常见原因，通常也是主要原因。|  
|9|AVAILABILITY_REPLICA|可用性组的辅助副本正将此数据库的事务日志记录应用到相应的辅助数据库。 （完整恢复模式）<br /><br /> 有关详细信息，请参阅[AlwaysOn 可用性组的概述&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。|  
|10|—|仅供内部使用|  
|11|—|仅供内部使用|  
|12|—|仅供内部使用|  
|13|OLDEST_PAGE|如果将数据库配置为使用间接检查点，数据库中最早的页可能比检查点 LSN 早。 在这种情况下，最早的页可以延迟日志截断。 （所有恢复模式）<br /><br /> 有关间接检查点的信息，请参阅[数据库检查点 (SQL Server)](database-checkpoints-sql-server.md)。|  
|14|OTHER_TRANSIENT|当前未使用此值。|  
|16|XTP_CHECKPOINT|当数据库具有内存优化文件组时，事务日志可能不会截断之前自动[!INCLUDE[hek_2](../../includes/hek-2-md.md)]（这种情况发生在每个 512 MB 的日志增长） 触发检查点。<br /><br /> 注意： 512 MB 大小之前的事务日志截断，触发手动对所讨论数据库的检查点命令。|  
  
##  <a name="MinimallyLogged"></a> 可以按最小方式记录的操作  
 最小日志记录是指只记录在不支持时间点恢复的情况下恢复事务所需的信息。 本主题介绍在大容量日志恢复模式下（以及简单恢复模式下）按最小方式记录、但在运行备份时例外的操作。  
  
> [!NOTE]  
>  内存优化表不支持最小日志记录。  
  
> [!NOTE]  
>  在完整恢复模式下，所有大容量操作都将被完整地记录下来。 但是，可以通过将数据库暂时切换到用于大容量操作的大容量日志恢复模式，最小化一组大容量操作的日志记录。 最小日志记录比完整日志记录更为有效，并在大容量事务期间，降低了大规模大容量操作填满可用的事务日志空间的可能性。 不过，如果在最小日志记录生效时数据库损坏或丢失，则无法将数据库恢复到故障点。  
  
 下列操作在完整恢复模式下执行完整日志记录，而在简单和大容量日志恢复模式下按最小方式记录日志：  
  
-   批量导入操作（[bcp](../../tools/bcp-utility.md)、[BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 和 [INSERT...SELECT](/sql/t-sql/statements/insert-transact-sql)）。 有关在何时对大容量导入表按最小方式进行记录的详细信息，请参阅 [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
    > [!NOTE]  
    >  启用事务复制时，将完全记录 BULK INSERT 操作，即使处于大容量日志恢复模式下。  
  
-   SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) 操作。  
  
    > [!NOTE]  
    >  启用事务复制时，将完全记录 SELECT INTO 操作，即使处于大容量日志恢复模式下。  
  
-   插入或追加新数据时，使用 [UPDATE](/sql/t-sql/queries/update-transact-sql) 语句中的 .WRITE 子句部分更新到大型值数据类型。 注意，在更新现有值时没有使用最小日志记录。 有关大型值数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)。  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql)并[UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql)语句插入或追加新数据时`text`， `ntext`，并`image`数据类型列。 注意，在更新现有值时没有使用最小日志记录。  
  
    > [!NOTE]  
    >  不推荐使用 WRITETEXT 语句和 UPDATETEXT 语句，因此应该避免在新的应用程序中使用这些语句。  
  
-   如果数据库设置为简单或大容量日志恢复模式，则无论是脱机还是联机执行操作，都会按最小方式记录一些索引 DDL 操作。 按最小方式记录的索引操作如下：  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 操作（包括索引视图）。  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD 或 DBCC DBREINDEX 操作。  
  
        > [!NOTE]  
        >  不推荐使用 DBCC DBREINDEX 语句，因此应该避免在新的应用程序中使用该语句。  
  
    -   DROP INDEX 新堆重新生成（如果适用）。  
  
        > [!NOTE]  
        >  索引页的释放期间[DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql)操作将始终完整记录。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 `Managing the transaction log`  
  
-   [管理事务日志文件的大小](manage-the-size-of-the-transaction-log-file.md)  
  
-   [解决事务日志已满的问题（SQL Server 错误 9002）](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **备份事务日志（完整恢复模式）**  
  
-   [备份事务日志 (SQL Server)](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **还原事务日志（完整恢复模式）**  
  
-  [还原事务日志备份](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>请参阅  
 [控制事务持续性](control-transaction-durability.md)   
 [在批量导入中按最小方式记录日志的前提条件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [SQL Server 数据库的备份和还原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [数据库检查点 (SQL Server)](database-checkpoints-sql-server.md)   
 [查看或更改数据库的属性](../databases/view-or-change-the-properties-of-a-database.md)   
 [恢复模式 (SQL Server)](../backup-restore/recovery-models-sql-server.md)  
  
  
