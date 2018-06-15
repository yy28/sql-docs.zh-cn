---
title: RESTORE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RESTORE DATABASE
- RESTORE_TSQL
- RESTORE_DATABASE_TSQL
- RESTORE
- RESTORE_LOG_TSQL
- RESTORE LOG
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE DATABASE, see RESTORE statement
- full backups [SQL Server]
- RECOVERY option
- database snapshots [SQL Server], reverting to
- STOPAT syntax
- differential backups, RESTORE statement
- point in time recovery [SQL Server]
- restoring [SQL Server]
- NORECOVERY option
- online restores [SQL Server], RESTORE statement
- moving databases
- RESTORE statement, syntax
- cross-platform restores
- restoring databases [SQL Server], options
- RESTORE statement
- snapshots [SQL Server database snapshots], reverting to
- reverting database snapshots
- transaction log backups [SQL Server], RESTORE statement
- RESTORE LOG, see RESTORE statement
ms.assetid: 877ecd57-3f2e-4237-890a-08f16e944ef1
caps.latest.revision: 248
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1edf0ff22f56446faf5fa316723c4b2a525534cb
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702950"
---
# <a name="restore-statements-transact-sql"></a>RESTORE 语句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  还原使用 BACKUP 命令所做的备份。 通过此命令，您可以执行下列还原方案：  
  
-   基于完整数据库备份还原整个数据库（完整还原）。  
  
-   还原数据库的一部分（部分还原）。  
  
-   将特定文件或文件组还原到数据库（文件还原）。  
  
-   将特定页面还原到数据库（页面还原）。  
  
-   将事务日志还原到数据库（事务日志还原）。  
  
-   将数据库恢复到数据库快照捕获的时间点。  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还原方案的信息，请参阅[还原和恢复概述 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  有关参数说明的详细信息，请参阅 [RESTORE 参数 (Transact-SQL)](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。   从其他实例还原数据库时，请考虑 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)中的信息。
  
> 注意：有关从 Microsoft Azure Blob 存储服务还原的详细信息，请参阅[使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 [ FROM <backup_device> [ ,...n ] ]  
 [ WITH   
   {  
    [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
   | ,  <general_WITH_options> [ ,...n ]  
   | , <replication_WITH_option>  
   | , <change_data_capture_WITH_option>  
   | , <FILESTREAM_WITH_option>  
   | , <service_broker_WITH options>   
   | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence  
-- of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
      ] [ ,...n ]   
[;]  
  
--To Restore Specific Files or Filegroups:   
RESTORE DATABASE { database_name | @database_name_var }   
   <file_or_filegroup> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
   {  
      [ RECOVERY | NORECOVERY ]  
      [ , <general_WITH_options> [ ,...n ] ]  
   } [ ,...n ]   
[;]  
  
--To Restore Specific Pages:   
RESTORE DATABASE { database_name | @database_name_var }   
   PAGE = 'file:page [ ,...n ]'   
 [ , <file_or_filegroups> ] [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
       NORECOVERY     
      [ , <general_WITH_options> [ ,...n ] ]  
[;]  
  
--To Restore a Transaction Log:  
RESTORE LOG { database_name | @database_name_var }  -- Does not apply to SQL Database Managed Instance 
 [ <file_or_filegroup_or_pages> [ ,...n ] ]  
 [ FROM <backup_device> [ ,...n ] ]   
 [ WITH   
   {  
     [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
    | ,  <general_WITH_options> [ ,...n ]  
    | , <replication_WITH_option>  
    | , \<point_in_time_WITH_options—RESTORE_LOG>   
   } [ ,...n ]  
 ]   
[;]  
  
--To Revert a Database to a Database Snapshot:     
RESTORE DATABASE { database_name | @database_name_var }   
FROM DATABASE_SNAPSHOT = database_snapshot_name   
  
<backup_device>::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
 | { DISK    -- Does not apply to SQL Database Managed Instance
     | TAPE  -- Does not apply to SQL Database Managed Instance
     | URL   -- Applies to SQL Server and SQL Database Managed Instance
   } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Windows Azure Blob. Although Windows Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seemless restore experince for all the three devices.  
<files_or_filegroups>::=   
{   
   FILE = { logical_file_name_in_backup | @logical_file_name_in_backup_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }   
 | READ_WRITE_FILEGROUPS  
}   
  
<general_WITH_options> [ ,...n ]::=   
--Restore Operation Options  
   MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
 | REPLACE   
 | RESTART   
 | RESTRICTED_USER  | CREDENTIAL  
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
 | BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }   
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options. Does not apply to SQL Database Managed Instance
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
<replication_WITH_option>::=  
 | KEEP_REPLICATION   
  
<change_data_capture_WITH_option>::=  
 | KEEP_CDC  
  
<FILESTREAM_WITH_option>::=  
 | FILESTREAM ( DIRECTORY_NAME = directory_name )  
  
<service_broker_WITH_options>::=   
 | ENABLE_BROKER   
 | ERROR_BROKER_CONVERSATIONS   
 | NEW_BROKER  
  
\<point_in_time_WITH_options—RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options—RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
  
```  
  
## <a name="arguments"></a>参数  
 有关参数的说明，请参阅 [RESTORE 参数 (Transact-SQL)](../../t-sql/statements/restore-statements-arguments-transact-sql.md)。  
  
## <a name="about-restore-scenarios"></a>关于还原方案  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持各种还原方案：  
  
-   数据库完整还原  
  
     还原整个数据库，将从完整数据库备份开始，然后还原差异数据库备份（和日志备份）。 有关详细信息，请参阅[完整数据库还原（简单恢复模式）](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)或[数据库还原（完整恢复模式）](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)。  
  
-   文件还原  
  
     还原多文件组数据库中的文件或文件组。 请注意，在简单恢复模式下，该文件必须属于只读文件组。 完整文件还原之后，便可还原差异文件备份。 有关详细信息，请参阅[文件还原（完整恢复模式）](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)或[文件还原（简单恢复模式）](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)。  
  
-   页面还原  
  
     还原单个页面。 页面还原仅在完整恢复模式和大容量日志恢复模式下可用。 有关详细信息，请参阅[还原页 (SQL Server)](../../relational-databases/backup-restore/restore-pages-sql-server.md)。  
  
-   段落还原  
  
     从主文件组和一个或多个辅助文件组开始，分阶段还原数据库。 段落还原将从 RESTORE DATABASE 开始，使用 PARTIAL 选项并指定一个或多个要还原的辅助文件组。 有关详细信息，请参阅[段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
-   仅恢复  
  
     恢复那些已经与数据库保持一致且只需使其可用的数据。 有关详细信息，请参阅[恢复数据库而不还原数据 (Transact-SQL)](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)。  
  
-   事务日志还原。  
  
     在完整恢复模式或大容量日志恢复模式下，必须还原日志备份才能到达所需的恢复点。 有关还原日志备份的详细信息，请参阅[应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
-   为 Always On 可用性组准备可用性数据库  
  
     有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)或 PowerShell 将辅助数据库联接到 Always On 可用性组。  
  
-   为数据库镜像准备镜像数据库  
  
     有关详细信息，请参阅 [为镜像准备镜像数据库 (SQL Server)](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)的各版本中均未提供见证服务器实例。  
  
-   联机还原  
  
    > 注意：只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的企业版才允许联机还原。  
  
     在支持联机还原的情况下，如果数据库为联机状态，则文件还原和页面还原将自动为联机还原，同时在段落还原的初始阶段之后，辅助文件组也变为联机还原。  
  
    > 注意：联机还原可能会涉及[延迟的事务](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)。  
  
     有关详细信息，请参阅[联机还原 (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)。  
  
## <a name="additional-considerations-about-restore-options"></a>有关 RESTORE 选项的其他注意事项  
  
### <a name="discontinued-restore-keywords"></a>废止的 RESTORE 关键字  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中已停止使用以下关键字：  
  
|停止使用的关键字|替换为…|替换关键字的示例|  
|--------------------------|------------------|------------------------------------|  
|LOAD|RESTORE|`RESTORE DATABASE`|  
|TRANSACTION|LOG|`RESTORE LOG`|  
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|  
  
### <a name="restore-log"></a>RESTORE LOG  
 RESTORE LOG 可以包括一个文件列表，从而允许在前滚过程中创建文件。 这可用于下列情况：将文件添加到数据库时，日志备份包含了已写入的日志记录。  
  
> 注意：对于使用完全恢复模式或大容量日志恢复模式的数据库，在大多数情况下，必须在还原数据库前备份日志的末尾。 还原数据库而不首先备份日志的末尾将导致错误，除非 RESTORE DATABASE 语句包含 WITH REPLACE 或 WITH STOPAT 子句，此子句必须指定数据备份的结束时间或在数据备份结束之后发生的事务。 有关结尾日志备份的详细信息，请参阅[结尾日志备份 (SQL Server) ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
### <a name="comparison-of-recovery-and-norecovery"></a>RECOVERY 和 NORECOVERY 的比较  
 回滚由 RESTORE 语句通过 [ RECOVERY | NORECOVERY ] 选项控制：  
  
-   NORECOVERY 指定不发生回滚。 从而使前滚按顺序在下一条语句中继续进行。  
  
     在这种情况下，还原顺序可还原其他备份，并执行前滚。  
  
-   RECOVERY（默认值）表示，应在完成当前备份前滚之后执行回滚。  
  
     恢复数据库要求要还原的整个数据集（“前滚集”）必须与数据库一致。 如果前滚集尚未前滚到与数据库保持一致的地步，并且指定了 RECOVERY，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将发出错误。  
  
## <a name="compatibility-support"></a>兼容性支持  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 无法还原使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本创建的 master、model 和 msdb 备份。  
  
> 注意：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份不会还原到比创建了备份的版本还早的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个版本使用的默认路径与早期版本不同。 因此，若要还原在早期版本备份的默认位置创建的数据库，必须使用 MOVE 选项。 有关新的默认路径的信息，请参阅 [SQL Server 的默认实例和命名实例的文件位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 在您将早期版本数据库还原到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]后，将自动升级该数据库。 通常，该数据库将立即可用。 但是，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库具有全文检索，则升级过程将导入、重置或重新生成它们，具体取决于  **upgrade_option** 服务器属性的设置。 如果将升级选项设置为“导入”(**upgrade_option** = 2) 或“重新生成”(**upgrade_option** = 0)，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，如果将升级选项设置为“导入”，并且全文目录不可用，则会重新生成关联的全文索引。 若要更改 **upgrade_option** 服务器属性的设置，请使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)。  
  
 当数据库第一次附加或还原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时，数据库主密钥（由服务主密钥加密）的副本尚未存储在服务器中。 必须使用 **OPEN MASTER KEY** 语句解密数据库主密钥 (DMK)。 一旦 DMK 解密后，通过使用 **ALTER MASTER KEY REGENERATE** 语句向服务器提供 DMK（使用服务主密钥 (SMK) 加密）的副本，即可拥有将来启用自动解密的选项。 当数据库已从较早版本升级后，应重新生成 DMK 以使用更新的 AES 算法。 有关重新生成 DMK 的详细信息，请参阅 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新生成 DMK 密钥以升级到 AES 所需的时间取决于 DMK 保护的对象数。 重新生成 DMK 密钥以升级到 AES 只在必需时执行一次，不影响将来作为密钥循环策略的一部分而重新生成的过程。  
  
## <a name="general-remarks"></a>一般备注  
 在脱机还原过程中，如果指定的数据库正在使用，则在短暂延迟之后，RESTORE 将强制用户离线。 对于非主文件组的联机还原，除非要还原的文件组为脱机状态，否则数据库可以保持使用状态。 指定数据库中的所有数据都将由还原的数据替换。  
  
 有关数据库恢复的详细信息，请参阅[还原和恢复概述 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
 只要操作系统支持数据库排序规则，就可以跨平台执行还原操作，即使这些平台使用不同的处理器类型也不例外。  
  
 RESTORE 在出现错误之后可以重新启动。 此外，您可以指示 RESTORE 继续进行而不必考虑错误，此命令可还原尽可能多的数据（请参阅 CONTINUE_AFTER_ERROR 选项）。  
  
 不允许在显式或隐式事务中使用 RESTORE。  
  
 还原已损坏的 master 数据库需要使用特殊的过程。 有关详细信息，请参阅[备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
 还原数据库将清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计划缓存。 清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含以下信息性消息：“由于某些数据库维护或重新配置操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划高速缓存的一部分)的 %d 次刷新”。 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。  
  
 要还原可用性数据库，首先需要将数据库还原成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，然后再将数据库添加到可用性组。  

## <a name="general-remarks---sql-database-managed-instance"></a>一般注释 - SQL 数据库托管实例

对于异步还原，即使客户端连接中断，还原操作也会继续运行。 如果连接断开，可检查 [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 视图，查看还原操作的状态（以及查看 CREATE 和 DROP 数据库）。 

已设置/覆盖以下数据库选项，这些选项稍后无法进行更改：

- NEW_BROKER（如果 .bak 文件中未启用中转站）
- ENABLE_BROKER（如果 .bak 文件中未启用中转站）
- AUTO_CLOSE=OFF（如果 .bak 文件中的数据库具有 AUTO_CLOSE=ON）
- RECOVERY FULL（如果 .bak 文件中的数据库具有 SIMPLE 或 BULK_LOGGED 恢复模式）
- 如果源 .bak 文件中不存在内存优化文件组，则会添加一个，并将其命名为 XTP。 任何现有内存优化文件组都会重命名为 XTP
- SINGLE_USER 和 RESTRICTED_USER 选项会转换为 MULTI_USER

## <a name="limitations---sql-database-managed-instance"></a>限制 - SQL 数据库托管实例
这些限制包括：

- 无法还原包含多个备份集的 .BAK 文件。
- 无法还原包含多个日志文件的 .BAK 文件。
- 如果 .bak 中包含 FILESTREAM 数据，则还原将失败。
- 如果备份中包含的数据库具有活动的内存中对象，则该备份当前无法还原。
- 如果备份中包含的数据库中某些时候存在内存中对象，则该备份当前无法还原。
- 如果备份包含处于只读模式的数据库，则该备份当前无法还原。 此限制很快就会取消。

有关详细信息，请参阅[托管实例](/azure/sql-database/sql-database-managed-instance)

## <a name="interoperability"></a>互操作性  
  
### <a name="database-settings-and-restoring"></a>数据库设置和还原  
 在还原过程中，可使用 ALTER DATABASE 设置的大多数数据库选项将强制重置为备份结束时的值。  
  
 但是，使用 WITH RESTRICTED_USER 选项将覆盖用户访问选项设置的此行为。 此设置总是通过在 RESTORE 语句后加上 WITH RESTRICTED_USER 选项来设置。  
  
### <a name="restoring-an-encrypted-database"></a>还原加密数据库  
 若要还原已加密的数据库，您必须有权访问用于对数据库进行加密的证书或非对称密钥。 如果没有证书或非对称密钥，数据库将无法还原。 因此，只要需要该备份，就必须保留用于对数据库加密密钥进行加密的证书。 有关详细信息，请参阅 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>还原为 vardecimal 存储启用的数据库  
 使用 vardecimal 存储格式时，备份和还原可正常进行。 有关 vardecimal 存储格式的详细信息，请参阅 [sp_db_vardecimal_storage_format (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)。  
  
### <a name="restore-full-text-data"></a>还原全文数据  
 全文数据与其他数据库数据一同在完全还原过程中还原。 使用常规 `RESTORE DATABASE database_name FROM backup_device` 语法，将全文文件作为数据库文件还原的一部分进行还原。  
  
 RESTORE 语句也可用于对全文数据执行替代位置还原、差异还原、文件和文件组还原，以及差异文件和文件组还原。 此外，RESTORE 可以仅还原全文文件，也可以同时还原数据库数据。  
  
> 注意：从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 导入的全文目录仍被视为数据库文件。 对于这些目录，用于备份全文目录的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 过程仍然适用，只是在备份操作期间不再需要暂停和恢复。 有关详细信息，请参阅[备份和还原全文目录](http://go.microsoft.com/fwlink/?LinkId=107381)。  
  
## <a name="metadata"></a>元数据  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含备份和还原历史记录表，这些表可以跟踪每个服务器实例的备份和还原活动。 执行还原时，还将修改备份历史记录表。 有关这些表的信息，请参阅[备份历史记录和标头信息 (SQL Server)](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)。  
  
##  <a name="REPLACEoption"></a> REPLACE 选项的影响  
 应尽可能避免使用 REPLACE，而且在使用该选项之前必须仔细考虑。 还原一般会防止意外使用一个数据库覆盖另一个数据库。 如果 RESTORE 语句中指定的数据库已存在于当前服务器上，并且指定的数据库系列 GUID 与备份集中记录的数据库系列 GUID 不同，则不还原该数据库。 这是一项重要的安全保护措施。  
  
 使用 REPLACE 选项后，就会忽略还原时通常执行的几项重要安全检查。 忽略的检查如下：  
  
-   还原时使用其他数据库的备份覆盖现有数据库。  
  
     使用 REPLACE 选项后，即使指定的数据库名称与备份集中记录的数据库名称不同，还原也允许您使用备份集中任何一个数据库覆盖现有数据库。 这会导致一个数据库意外覆盖另一个数据库。  
  
-   在没有获取结尾日志备份并也没有使用 STOPAT 选项的情况下，使用完整恢复模式或大容量日志恢复模式对数据库进行还原。  
  
     使用 REPLACE 选项后，由于没有备份最近写入的日志，您会丢失提交的作业。  
  
-   覆盖现有文件。  
  
     例如，可能会错误地覆盖错误类型的文件，如 .xls 文件或非联机状态的其他数据库正在使用的文件等。 如果覆盖现有文件，则即使所还原的数据库是完整的，也有可能丢失某些数据。  
  
## <a name="redoing-a-restore"></a>重新进行还原  
 还原结果是无法撤消的，但可以文件为基础重新开始操作而使数据复制和前滚的结果无效。 若要重新开始，请再次还原所需的文件并执行前滚。 例如，如果您不慎还原了过多的日志备份并超过了预期停止点，则必须重新启动该顺序。  
  
 通过还原受影响文件的全部内容，可以中止并重新启动还原顺序。  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>将数据库恢复到数据库快照  
 “恢复数据库操作”（使用 DATABASE_SNAPSHOT 选项指定）用于及时执行完整的源数据库恢复，该过程将使源数据库恢复到数据库快照时的状态，就是说，用在指定的数据库快照中维护的时间点数据覆盖源数据库。 当前只能存在可以恢复到的快照。 然后，恢复操作重新生成日志（因此，以后无法将已恢复的数据库前滚到用户错误点）。  
  
 丢失的数据仅限于创建快照后数据库更新的数据。 已恢复的数据库的元数据与创建快照时的元数据相同。 但是，恢复到快照将删除所有全文目录。  
  
 从数据库快照恢复不适用于介质恢复。 与定期备份集不同，数据库快照并非数据库文件的完整副本。 如果数据库或数据库快照已损坏，则可能无法从快照恢复。 即便可以恢复，但是如果损坏的话，恢复可能也无法更正该问题。  
  
### <a name="restrictions-on-reverting"></a>对恢复的限制  
 下列情况不支持恢复：  
  
-   源数据库包含任何只读或压缩的文件组。  
  
-   某些在创建快照时处于在线状态的文件已离线。  
  
-   当前存在多个数据库快照。  
  
 有关详细信息，请参阅[将数据库恢复到数据库快照](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)。  
  
## <a name="security"></a>Security  
 在备份时，可以根据需要为介质集、备份集或这两者指定密码。 如果已经在介质集或备份集上定义了密码，则必须在 RESTORE 语句中指定正确的密码。 这些密码可防止未经授权而使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具执行还原操作以及向介质追加备份集。 但是，可以通过 BACKUP 语句的 FORMAT 选项覆盖受密码保护的介质。  
  
> [!IMPORTANT]  
>  此密码提供的安全性较低。 它旨在防止经过授权的用户或未经授权的用户使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具执行不正确的还原操作。 但是不能防止通过其他方式或通过替换密码来读取备份数据。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 保护备份的最佳做法是将备份磁带存储在安全位置，或者备份到由适当的访问控制列表 (ACL) 保护的磁盘文件。 ACL 应设置在创建备份的根目录下。  
>   
>  有关使用 Microsoft Azure Blob 存储进行 SQL Server 备份和还原的特定信息，请参阅[使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
### <a name="permissions"></a>权限  
 如果不存在要还原的数据库，则用户必须有 CREATE DATABASE 权限才能执行 RESTORE。 如果数据库存在，则 RESTORE 权限默认授予 **sysadmin** 和 **dbcreator** 固定服务器角色成员以及数据库的所有者 (**dbo**)（对于 FROM DATABASE_SNAPSHOT 选项，数据库始终存在）。  
  
 RESTORE 权限被授予那些成员身份信息始终可由服务器使用的角色。 因为只有在固定数据库可以访问且没有损坏时（在执行 RESTORE 时并不会总是这样）才能检查固定数据库角色成员身份，所以 **db_owner** 固定数据库角色成员没有 RESTORE 权限。  
  
##  <a name="examples"></a> 示例  
 所有的示例均假定已执行了完整数据库备份。  
  
 RESTORE 示例包括：  
  
-   A. [还原完整数据库](#restoring_full_db)  
  
-   B. [还原完整数据库备份和差异数据库备份](#restoring_full_n_differential_db_backups)  
  
-   C. [使用 RESTART 语法还原数据库](#restoring_db_using_RESTART)  
  
-   D. [还原数据库并移动文件](#restoring_db_n_move_files)  
  
-   E. [使用 BACKUP 和 RESTORE 复制数据库](#copying_db_using_bnr)  
  
-   F. [使用 STOPAT 还原到时间点](#restoring_to_pit_using_STOPAT)  
  
-   G. [将事务日志还原到标记](#restoring_transaction_log_to_mark)  
  
-   H. [使用 TAPE 语法还原](#restoring_using_TAPE)  
  
-   I. [使用 FILE 和 FILEGROUP 语法还原](#restoring_using_FILE_n_FG)  
  
-   J. [从数据库快照还原](#reverting_from_db_snapshot)  
  
-   K. [从 Microsoft Azure Blob 存储服务还原](#Azure_Blob)  
  
> 注意：有关其他示例，请参阅[还原和恢复概述 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md) 中列出的还原操作指南主题。  
  
###  <a name="restoring_full_db"></a> A. 还原完整数据库  
 下面的示例从 `AdventureWorksBackups` 逻辑备份设备还原完整数据库备份。 有关创建此设备的示例，请参阅[备份设备](../../relational-databases/backup-restore/backup-devices-sql-server.md)。  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> 注意：对于使用完全恢复模式或大容量日志恢复模式的数据库，在大多数情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都要求你在还原数据库前备份日志尾部。 有关详细信息，请参阅[结尾日志备份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> B. 还原完整数据库备份和差异数据库备份  
 下面的示例还原完整数据库备份后，从同时还包含差异数据库备份的 `Z:\SQLServerBackups\AdventureWorks2012.bak` 备份设备还原差异备份。 要还原的完整数据库备份是设备上的第六个备份集 (`FILE = 6`)，差异数据库备份是设备上的第九个备份集 (`FILE = 9`)。 在恢复了差异备份之后，便恢复了数据库。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> C. 使用 RESTART 语法还原数据库  
 下面的示例使用 `RESTART` 选项重新启动因服务器电源故障而中断的 `RESTORE` 操作。  
  
```  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> D. 还原数据库并移动文件  
 下面的示例还原完整数据库和事务日志，并将还原后的数据库移动到 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` 目录中。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH NORECOVERY,   
      MOVE 'AdventureWorks2012_Data' TO   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.mdf',   
      MOVE 'AdventureWorks2012_Log'   
TO 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.ldf';  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH RECOVERY;  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="copying_db_using_bnr"></a> E. 使用 BACKUP 和 RESTORE 复制数据库  
 下面的示例使用 `BACKUP` 和 `RESTORE` 语句创建 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的副本。 `MOVE` 语句使数据和日志文件还原到指定的位置。 `RESTORE FILELISTONLY` 语句用于确定待还原数据库内的文件数及名称。 该数据库的新副本称为 `TestDB`。 有关详细信息，请参阅 [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups ;  
  
RESTORE FILELISTONLY   
   FROM AdventureWorksBackups ;  
  
RESTORE DATABASE TestDB   
   FROM AdventureWorksBackups   
   WITH MOVE 'AdventureWorks2012_Data' TO 'C:\MySQLServer\testdb.mdf',  
   MOVE 'AdventureWorks2012_Log' TO 'C:\MySQLServer\testdb.ldf';  
GO  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> F. 使用 STOPAT 还原到时间点  
 下面的示例将数据库还原到它在 `12:00 AM` 的 `April 15, 2020` 的状态，并显示涉及多个日志备份的还原操作。 在备份设备上，要还原的完整数据库备份 `AdventureWorksBackups`是设备上的第三个备份集 (`FILE = 3`)，第一个日志备份是第四个备份集 (`FILE = 4`)，第二个日志备份是第五个备份集 (`FILE = 5`)。  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a> G. 将事务日志还原到标记  
 下面的示例将事务日志还原到名为 `ListPriceUpdate`的标记事务中的标记处。  
  
```  
USE AdventureWorks2012  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master;  
GO  
  
RESTORE DATABASE AdventureWorks2012  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'UPDATE Product list prices';  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_using_TAPE"></a> H. 使用 TAPE 语法还原  
 下面的示例从 `TAPE` 备份设备还原完整数据库备份。  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a> I. 使用 FILE 和 FILEGROUP 语法还原  
 下面的示例还原名为 `MyDatabase` 的数据库，该数据库有两个文件、一个辅助文件组和一个事务日志。 数据库使用完整恢复模式。  
  
 该数据库备份是名为 `MyDatabaseBackups` 的逻辑备份设备上的介质集中的第九个备份集。 接下来，通过使用 `10` 来还原在 `11` 设备上的后续三个备份集（`12`、`MyDatabaseBackups` 和 `WITH NORECOVERY`）中的三个日志备份。 还原最后一个日志备份之后，应当恢复数据库。  
  
> 注意：恢复应当作为单独的步骤执行，以减少在还原所有日志备份之前太早进行恢复的可能性。  
  
 在 `RESTORE DATABASE` 中，请注意有两种 `FILE` 选项类型。 在备份设备名称前面的 `FILE` 选项用于指定要从备份集还原的数据库文件的逻辑文件名；例如，`FILE = 'MyDatabase_data_1'`。 此备份集不是介质集中的第一个数据库备份；因此，应当通过在 `FILE` 子句中使用 `WITH` 选项（即 `FILE=9`）来指示它在介质集中的位置。  
  
```  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'new_customers'  
   FROM MyDatabaseBackups  
   WITH   
      FILE = 9,  
      NORECOVERY;  
GO  
-- Restore the log backups.  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 10,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 11,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 12,   
      NORECOVERY;  
GO  
--Recover the database:  
RESTORE DATABASE MyDatabase WITH RECOVERY;  
GO  
```  
  
 [[示例顶部]](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a> J. 从数据库快照恢复  
 下面的示例将数据库恢复到数据库快照。 该示例假定该数据库当前仅存在一个快照。 有关如何创建此数据库快照的示例，请参阅[创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)。  
  
> 注意：恢复到快照将删除所有全文目录。  
  
```  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
 有关详细信息，请参阅[将数据库恢复到数据库快照](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)。  

 [[示例顶部]](#examples)  
  
###  <a name="Azure_Blob"></a> K. 从 Microsoft Azure Blob 存储服务还原  
以下三个示例都涉及 Microsoft Azure 存储服务的使用。  存储帐户名称为 `mystorageaccount`。  数据文件的容器称为 `myfirstcontainer`。  备份文件的容器称为 `mysecondcontainer`。  已为每个容器创建具有读取、写入、删除和列表权限的存储访问策略。  已使用与存储访问策略相关联的共享访问签名创建 SQL Server 凭据。  针对使用 Microsoft Azure Blob 存储进行 SQL Server 备份和还原的信息，请参阅[使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  

**K1.从 Microsoft Azure 存储服务还原完整数据库备份**  
位于 `mysecondcontainer` 的 `Sales` 的完整数据库备份将还原到 `myfirstcontainer`。  `Sales` 当前不在服务器上。 
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2.将完整数据库备份从 Microsoft Azure 存储服务还原到本地存储**  
位于 `mysecondcontainer` 的 `Sales` 的完整数据库备份将还原到本地存储。  `Sales` 当前不在服务器上。
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3.将完整数据库备份从本地存储还原到 Microsoft Azure 存储服务**  
```
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
 [[示例顶部]](#examples)  
  
## <a name="much-more-information"></a>更多信息！！  
 - [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [系统数据库的备份和还原 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
 - [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
 - [备份和还原全文目录和索引](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 - [备份和还原复制的数据库](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 - [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 - [媒体集、媒体簇和备份集 (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 - [RESTORE REWINDONLY (Transact-SQL)](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 - [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 - [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
 - [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
 - [备份历史记录和标头信息 (SQL Server)](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
