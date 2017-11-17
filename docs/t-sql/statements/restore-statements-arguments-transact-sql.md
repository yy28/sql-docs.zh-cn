---
title: "还原自变量 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE statement, arguments
- RESTORE statement
ms.assetid: 4bfe5734-3003-4165-afd4-b1131ea26e2b
caps.latest.revision: 154
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 8a5997cc7692e7cce1459dc64401397cc3b07eaf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---
# <a name="restore-statements---arguments-transact-sql"></a>还原语句的自变量 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题记录了在 RESTORE {DATABASE|LOG} 语句和如后所示的关联辅助语句的“语法”部分中说明的参数：RESTORE FILELISTONLY、RESTORE HEADERONLY、RESTORE LABELONLY、RESTORE REWINDONLY 和 RESTORE VERIFYONLY。 大多数参数都仅由这六个语句中的一部分支持。 每个参数的说明中都指示了相应的支持信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
 有关语法，请参阅下列主题：  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="arguments"></a>参数  
 DATABASE  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定目标数据库。 如果指定了文件和文件组列表，则只还原那些文件和文件组。  
  
 对于使用完全恢复模式或大容量日志恢复模式的数据库，在大多数情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都要求您在还原数据库前备份日志尾部。 还原数据库而不首先备份日志的末尾将导致错误，除非 RESTORE DATABASE 语句包含 WITH REPLACE 或 WITH STOPAT 子句，此子句必须指定数据备份的结束时间或在数据备份结束之后发生的事务。 有关结尾日志备份的详细信息，请参阅[结尾日志备份 (SQL Server) ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
 LOG  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指示对该数据库应用事务日志备份。 必须按顺序应用事务日志。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检查已备份的事务日志，以确保按正确的序列将事务加载到正确的数据库。 若要应用多个事务日志，请在除上一个外的所有还原操作中使用 NORECOVERY 选项。  
  
> [!NOTE]  
>  上一个还原的日志通常是结尾日志备份。 A*结尾日志备份*进行日志备份右之前还原数据库，通常在数据库上出现故障后。 从可能已损坏的数据库备份结尾日志可以捕获尚未备份的日志（日志的尾部），从而防止工作丢失。 有关详细信息，请参阅[结尾日志备份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
 有关详细信息，请参阅[应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
 { *database_name* | **@***database_name_var*}  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 是将日志或整个数据库还原到的数据库。 如果为变量提供 (**@***database_name_var*)，此名称可以是指定为字符串常量 ( **@**  *database_name_var* = *数据库*_*名称*) 或作为变量的字符字符串数据类型，除**ntext**或**文本**数据类型。  
  
 \<file_or_filegroup_or_page > [ **，**...*n* ]  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定要包含在 RESTORE DATABASE 或 RESTORE LOG 语句中的逻辑文件或文件组或页面的名称。 您可以指定文件或文件组列表。  
  
 对于使用简单恢复模式数据库，仅当目标文件组只读字段，或如果这是部分还原允许的文件和文件组选项 (这将导致[失效的文件组](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md))。  
  
 对于使用完全恢复模式或大容量日志记录恢复模式的数据库而言，在使用 RESTORE DATABASE 还原了一个或多个文件、文件组和/或页面之后，通常必须将事务日志应用于包含已还原数据的文件，以使这些文件与数据库的剩余部分保持一致。 不过，有时不需要应用事务日志，具体情况如下：  
  
-   如果要还原的文件是只读的那些自从上次备份之前 — 事务日志没有要应用，然后还原语句会通知你这种情况。  
  
-   如果备份中包含主文件组，则会执行部分还原。 在这种情况下，由于日志可从备份集中自动还原，因此不需要还原日志。  
  
文件 **=**  { *logical_file_name_in_backup*| **@***logical_file_name_in_backup_var*}  
 命名一个要包含在数据库还原任务中的文件。  
  
文件组 **=**  { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
 命名一个要包含在数据库还原任务中的文件组。  
  
 **请注意**文件组允许在简单恢复模式中，仅当指定的文件组是只读的且 （即，如果使用 WITH PARTIAL），这是部分还原。 任何未还原的读写文件组将被标记为失效，而且以后无法被还原到最终的数据库中。  
  
READ_WRITE_FILEGROUPS  
 选择所有读写文件组。 如果希望在还原读写文件组之后，并在还原只读文件组之前还原某些只读文件组，该选项尤其有用。  
  
页 = *文件***:***页*[ **，**...*n* ]**'**  
 指定用于页面还原的一页或多页列表（只有使用完整恢复模式或大容量日志恢复模式的数据库支持页面还原）。 这些值如下所示：  
  
PAGE  
 指示一个由一个或多个文件和页面构成的列表。  
  
 *文件*  
 文件的文件 ID，该文件包含要还原的特定页面。  
  
 *页*  
 文件中要还原的页面的页 ID。  
  
 *n*  
 指示可以指定多个页面的占位符。  
  
 可按还原顺序还原到任何单个文件中的最大页面数是 1000。 然而，如果文件中损坏的页面过多，则应考虑还原整个文件而不是还原这些页面。  
  
> [!NOTE]  
>  永远不会恢复页面还原。  
  
 有关页面还原的详细信息，请参阅[还原页 &#40;SQL server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
 [ **,**...*n* ]  
 一个占位符，表示可以在以逗号分隔的列表中指定多个文件、文件组和页。 数量不受限制。  
  
从 { \<backup_device > [ **，**...*n* ]|\<database_snapshot >}通常情况下，指定要从中还原备份的备份设备。 此外，在 RESTORE DATABASE 语句中，FROM 子句可以指定要向哪个数据库快照还原数据库，在这种情况下不允许使用 WITH 子句。  
  
 如果省略了 FROM 子句，将不会还原备份， 而是会恢复数据库。 这样，您就可以恢复用 NORECOVERY 选项还原的数据库，或者转到一个备用服务器。 如果省略 FROM 子句，则必须在 WITH 子句中指定 NORECOVERY、RECOVERY 或 STANDBY。  
  
 \<backup_device > [ **，**... *n*  ] 指定要用于还原操作的逻辑或物理备份设备。  
  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)， [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 \<backup_device >:: = 指定逻辑或物理备份设备用于备份操作，，如下所示：  
  
 { *logical_backup_device_name* | **@***logical_backup_device_name_var* }  
 是逻辑名称，必须遵循标识符规则，所创建的备份设备的**sp_addumpdevice**从还原数据库。 如果为变量提供 (**@***logical_backup_device_name_var*)，备份设备名称可以是指定为字符串常量 ( **@** *logical_backup_device_name_var* = *logical_backup_device_name*) 或作为变量的字符字符串数据类型，除**ntext**或**文本**数据类型。  
  
 {磁盘 |磁带}  **=**  { *physical_backup_device_name*  |   **@** *physical_backup_device_name_var* }  
 允许从指定的磁盘或磁带设备还原备份。 应使用设备的实际名称 （例如，完整路径和文件名称） 指定的磁盘和磁带的设备类型：`DISK ='Z:\SQLServerBackups\AdventureWorks.bak'`或`TAPE ='\\\\.\TAPE0'`。 如果指定为一个变量 (**@***physical_backup_device_name_var*)，可以是设备名称指定为字符串常量 ( **@**  *physical_backup_device_name_var* =*physcial_backup_device_name*) 或作为变量的字符字符串数据类型，除**ntext**或**文本**数据类型。  
  
 如果使用的是具有 UNC 名称（必须包含计算机名称）的网络服务器，请指定磁盘的设备类型。 有关如何使用 UNC 名称的详细信息，请参阅[备份设备 &#40;SQL server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时所使用的帐户必须具有对远程计算机或网络服务器的 READ 访问权，这样才能执行 RESTORE 操作。  
  
 *n*  
 一个占位符，表示可以在以逗号分隔的列表中最多指定 64 个备份设备。  
  
 还原顺序是否要求备份设备的数量与创建备份所属的介质集时所用的数量相同，这取决于还原是脱机还原还是联机还原，如下所示：  
  
-   脱机还原允许还原所用的设备少于创建备份时所用的设备。  
  
-   联机还原要求使用备份的所有备份设备。 使用较少的设备进行还原将会失败。  
  
 例如，假设将某个数据库备份到与服务器连接的四个磁带机上。 联机还原要求有四个连接到服务器的磁带机，但是即使机器上的磁带机不足四个，脱机还原也允许还原备份。  
  
> [!NOTE]  
>  从镜像介质集中还原备份时，对于每个介质簇，只能指定一个镜像。 不过，在出现错误的情况下，如果具有其他镜像则可快速解决某些还原问题。 您可以使用其他镜像服务器中的相应卷替换损坏的介质卷。 请注意，为脱机还原你可以还原从较少的设备，介质簇，但每个系列处理仅一次。  
  
\<database_snapshot >:: =  
**支持：**[还原数据库  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
DATABASE_SNAPSHOT  **=**  *database_snapshot_name*  
 将恢复到指定的数据库快照数据库*database_snapshot_name*。 DATABASE_SNAPSHOT 选项只能用于完整数据库还原。 在还原操作中，数据库快照将取代完整数据库备份。  
  
 还原操作要求指定的数据库快照是数据库中的唯一快照。 在还原操作过程中，数据库快照和目标数据库都会被标记为 `In restore`。 有关详细信息，请参阅中的"备注"部分[RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
### <a name="with-options"></a>WITH 选项  
 指定还原操作要使用的选项。 有关语句对各个选项的支持的摘要信息，请参阅本主题后面的“WITH 选项支持摘要”。  
  
> [!NOTE]  
>  使用选项分为此处如中的"语法"一节中所示的相同顺序[还原 {数据库 |日志}](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
 PARTIAL  
 **支持：**[还原数据库  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定还原主文件组和指定的任意辅助文件组的部分还原操作。 PARTIAL 选项将隐式选择主文件组；无需指定 FILEGROUP = 'PRIMARY'。 若要还原辅助文件组，必须使用 FILE 选项或 FILEGROUP 选项明确指定文件组。  
  
 PARTIAL 选项不能在 RESTORE LOG 语句中使用。  
  
 PARTIAL 选项会启动最初阶段的段落还原，这样将允许剩余的文件组稍后还原。 有关详细信息，请参阅[段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
 [**恢复**|NORECOVERY |STANDBY]  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **恢复**  
 指示还原操作回滚任何未提交的事务。 在恢复进程后即可随时使用数据库。 如果既没有指定 NORECOVERY 和 RECOVERY，也没有指定 STANDBY，则默认为 RECOVERY。  
  
 如果安排了后续 RESTORE 操作（RESTORE LOG 或从差异数据库备份 RESTORE DATABASE），则应改为指定 NORECOVERY 或 STANDBY。  
  
 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中还原备份集时，可能要求将数据库升级。 如果指定了 WITH RECOVERY，升级将自动进行。 有关详细信息，请参阅[应用事务日志备份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
> [!NOTE]  
>  如果省略 FROM 子句，则必须在 WITH 子句中指定 NORECOVERY、RECOVERY 或 STANDBY。  
  
 NORECOVERY  
 指示还原操作不回滚任何未提交的事务。 如果稍后必须应用另一个事务日志，则应指定 NORECOVERY 或 STANDBY 选项。 如果既没有指定 NORECOVERY 和 RECOVERY，也没有指定 STANDBY，则默认为 RECOVERY。 使用 NORECOVERY 选项执行脱机还原操作时，数据库将无法使用。  
  
 还原数据库备份和一个或多个事务日志时，或者需要多个 RESTORE 语句（例如还原一个完整数据库备份并随后还原一个差异数据库备份）时，RESTORE 需要对所有语句使用 WITH NORECOVERY 选项，但最后的 RESTORE 语句除外。 最佳方法是按多步骤还原顺序对所有语句都使用 WITH NORECOVERY，直到达到所需的恢复点为止，然后仅使用单独的 RESTORE WITH RECOVERY 语句执行恢复。  
  
 当 NORECOVERY 选项用于文件或文件组还原操作时，它会强制数据库在还原操作结束后保持还原状态。 这在以下情况中很有用：  
  
-   还原脚本正在运行且始终需要应用日志。  
  
-   使用文件还原序列，并且在两次还原操作之间不能使用数据库。  
  
 在某些情况下，RESTORE WITH NORECOVERY 会将前滚集滚动到足够靠前的位置，使它与数据库一致。 在这种情况下将不会出现回滚，数据仍会保持脱机状态，正如使用该选项预期出现的情况一样。 但[!INCLUDE[ssDE](../../includes/ssde-md.md)]会发出一条信息性消息，表明现在可以用 RECOVERY 选项恢复前滚集。  
  
备用 **=**  *standby_file_name*  
 指定一个允许撤消恢复效果的备用文件。 STANDBY 选项可以用于脱机还原（包括部分还原）， 但不能用于联机还原。 尝试为联机还原操作指定 STANDBY 选项将会导致还原操作失败。 如果必须升级数据库，也不允许使用 STANDBY 选项。  
  
 备用文件用于为 RESTORE WITH STANDBY 的撤消过程中修改的页面保留一个“写入时副本”预映像。 备用文件允许用户在事务日志还原期间以只读方式访问数据库，并允许数据库用于备用服务器情形，或用于需要在日志还原操作之间检查数据库的特殊恢复情形。 执行完 RESTORE WITH STANDBY 操作之后，下一个 RESTORE 操作会自动删除撤消文件。 如果在下一个 RESTORE 操作之前手动删除了这个备用文件，则必须重新还原整个数据库。 当数据库处于 STANDBY 状态时，您应将这个备用文件视为和任何其他数据库文件同样重要。 该文件与其他数据库文件不同，[!INCLUDE[ssDE](../../includes/ssde-md.md)]仅在活动还原操作过程中持续打开该文件。  
  
 *Standby_file_name*指定备用文件的位置存储在数据库的日志。 如果某个现有文件使用了指定的名称，该文件将被覆盖，否则[!INCLUDE[ssDE](../../includes/ssde-md.md)]会创建该文件。  
  
 给定备用文件的大小要求取决于由还原操作过程中未提交的事务所导致的撤消操作数。  
  
> [!IMPORTANT]  
>  如果指定备用文件所在的驱动器上的磁盘空间已满，还原操作将停止。  
  
 有关恢复和 NORECOVERY 的比较，请参阅中的"备注"部分[还原](../../t-sql/statements/restore-statements-transact-sql.md)。  
  
LOADHISTORY  
 **支持：**[RESTORE VERIFYONLY  ](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 指定的还原操作将信息加载到**msdb**历史记录表。 LOADHISTORY 选项加载的信息，单个备份设置正在验证大约[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储媒体上的备份设置为备份和还原历史记录表中的**msdb**数据库。 有关历史记录表的详细信息，请参阅[系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md).  
  
#### <a name="generalwithoptions--n-"></a>\<general_WITH_options > [，...n]  
 RESTORE DATABASE 和 RESTORE LOG 语句均支持常规 WITH 选项。 其中某些选项也支持一个或多个辅助语句，以下所述。  
  
##### <a name="restore-operation-options"></a>还原操作选项  
 这些选项影响还原操作的行为。  
  
移动*logical_file_name_in_backup*收件人*operating_system_file_name* **'** [ ...*n* ]  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)和[RESTORE VERIFYONLY  ](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 指定的数据或日志文件的逻辑名称由指定*logical_file_name_in_backup*应通过将其还原到指定的位置移动*operating_system_file_name*。 创建备份集时，备份集中的数据或日志文件的逻辑文件名与其在数据库中的逻辑名称匹配。  
  
*n*指示可以指定其他 MOVE 语句的占位符。 请为每个要从备份集还原到新位置的逻辑文件指定 MOVE 语句。 默认情况下， *logical_file_name_in_backup*文件还原到其原始位置。  
  
> [!NOTE]  
>  若要从备份集中获取逻辑文件列表，请使用 RESTORE FILELISTONLY。  
  
 如果使用 RESTORE 语句将数据库重新定位到同一个服务器或将其复制到不同的服务器上，则最好使用 MOVE 选项重新定位数据库文件以避免与现有文件冲突。  
  
 与 RESTORE LOG 配合使用时，MOVE 选项只能用来重新定位在还原日志的那段时间内添加的文件。 例如，如果日志备份中包含一个添加 `file23` 文件的操作，系统将使用 RESTORE LOG 的 MOVE 选项重新定位该文件。  
  
 一起使用时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]快照备份可以使用 MOVE 选项只是为了将文件重新定位到 Azure 中作为原始 blob 相同的存储帐户的 blob。 移动选项无法用于将快照备份还原到本地文件或其他存储帐户。  
  
 如果使用 RESTORE VERIFYONLY 语句将数据库重新定位到同一个服务器或复制到不同的服务器上，则最好使用 MOVE 选项来验证目标服务器上是否有足够的空间并找出可能与现有文件存在的冲突。  
  
 有关详细信息，请参阅 [通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)。  
  
CREDENTIAL  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 SP1 CU2[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 仅当从 Microsoft Azure Blob 存储服务还原备份时，才使用。  
  
> [!NOTE]  
>  与[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]直到 SP1 CU2 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，你可以仅从一台设备时还原从 URL 还原。 若要从你必须使用的 URL 中还原时从多个设备还原[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))，并且必须使用共享访问签名 (SAS) 令牌。 有关详细信息，请参阅[启用 SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)和[简化使用 powershell 的 Azure 存储空间上的共享访问签名 (SAS) 令牌创建 SQL 凭据](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)。  
  
 REPLACE  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定即使存在另一个具有相同名称的数据库，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也应该创建指定的数据库及其相关文件。 在这种情况下将删除现有的数据库。 如果不指定 REPLACE 选项，则会执行安全检查。 这样可以防止意外覆盖其他数据库。 安全检查可确保在以下条件同时存在的情况下，RESTORE DATABASE 语句不会将数据库还原到当前服务器：  
  
-   在 RESTORE 语句中命名的数据库已存在于当前服务器中，并且  
  
-   该数据库名称与备份集中记录的数据库名称不同。  
  
 若无法验证现有文件是否属于正在还原的数据库，则 REPLACE 也允许 RESTORE 覆盖该文件。 RESTORE 通常拒绝覆盖已存在的文件。 WITH REPLACE 也可以同样的方式用于 RESTORE LOG 选项。  
  
 REPLACE 还会覆盖在恢复数据库之前备份尾日志的要求。  
  
 使用 REPLACE 选项的信息的影响，请参阅[还原 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
RESTART  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应重新启动被中断的还原操作。 RESTART 从中断点重新启动还原操作。  
  
RESTRICTED_USER  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)。    
  
 将新还原的数据库的访问权限的成员于**db_owner**， **dbcreator**，或**sysadmin**角色。  RESTRICTED_USER 替换了 DBO_ONLY 选项。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中已停止使用 DBO_ONLY。  
  
 该选项可与 RECOVERY 选项一起使用。  
  
##### <a name="backup-set-options"></a>备份集选项  
 这些选项作用于包含要还原的备份的备份集。  
  
文件 **=** { *backup_set_file_number* | **@***backup_set_file_number* }  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 标识要还原的备份集。 例如， *backup_set_file_number* 为 **1** 指示备份介质中的第一个备份集， *backup_set_file_number* 为 **2** 指示第二个备份集。 你可以通过使用 *RESTORE HEADERONLY* 语句来获取备份集的 [backup_set_file_number](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 。  
  
 如果未指定，默认值是**1**，除外 RESTORE HEADERONLY 在这种情况下处理在介质集中的所有备份集。 有关详细信息，请参阅本主题后面的“指定备份集”。  
  
> [!IMPORTANT]  
>  此文件选项与用于指定数据库文件，文件的文件选项无关 **=**  { *logical_file_name_in_backup*  |   **@** *logical_file_name_in_backup_var* }。  
  
 密码 **=**  {*密码* | **@***password_variable* }  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 提供备份集的密码。 备份集密码是一个字符串。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 如果在创建备份集时指定了密码，则从备份集执行任何还原操作时必须提供该密码。 指定错误的密码或在备份集没有密码的情况下指定一个密码时将会出错。  
  
> [!IMPORTANT]  
>  此密码只能为介质集提供弱保护。 有关详细信息，请参阅相关语句的“权限”部分。  
  
##### <a name="media-set-options"></a>介质集选项  
 这些选项作为一个整体对介质集进行操作。  
  
 MEDIANAME  **=**  { *media_name* | **@***media_name_variable*}  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 指定介质名称。 如果提供了介质名称，该名称必须与备份卷上的介质名称相匹配，否则还原操作将终止。 如果 RESTORE 语句中没有给出介质名称，将不会对备份卷执行介质名称匹配检查。  
  
> [!IMPORTANT]  
>  在备份和还原操作中使用一致的介质名称可以为用于还原操作的介质提供额外的安全检查。  
  
 MEDIAPASSWORD  **=**  { *mediapassword* | **@***mediapassword_variable* }  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 提供介质集的密码。 介质集密码是一个字符串。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 如果格式化介质集时提供了密码，则访问该介质集上的任何备份集时都必须提供该密码。 指定错误的密码或在介质集没有密码的情况下指定一个密码时将会出错。  
  
> [!IMPORTANT]  
>  此密码只能为介质集提供弱保护。 有关详细信息，请参阅相关的语句的"权限"部分。  
  
 BLOCKSIZE  **=**  { *blocksize* | **@***blocksize_variable* }  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 用字节数来指定物理块的大小。 支持的大小是 512、1024、2048、4096、8192、16384、32768 和 65536 (64 KB) 字节。 对于磁带设备默认为 65536，其他情况为 512。 通常，由于 RESTORE 自动选择适合于设备的块大小，因此不需要此选项。 显式声明块大小将覆盖自动选择块大小。  
  
 如果要从 CD-ROM 中还原备份，请指定 BLOCKSIZE=2048。  
  
> [!NOTE]  
>  通常，只有从磁带设备中读取数据时，此选项才会影响性能。  
  
##### <a name="data-transfer-options"></a>数据传输选项  
 该选项使您可以优化与备份设备之间的数据传输。  
  
 BUFFERCOUNT  **=**  { *buffercount* | **@***buffercount_variable* }  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定用于还原操作的 I/O 缓冲区总数。 可以指定任何正整数；但是，较大的缓冲区数可能导致由于 Sqlservr.exe 进程中的虚拟地址空间不足而发生“内存不足”错误。  
  
 所使用的缓冲区的总空间由： *buffercount***\****maxtransfersize*。  
  
 MAXTRANSFERSIZE  **=**  { *maxtransfersize* | **@***maxtransfersize_variable* }  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 指定要在备份介质和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之间使用的最大传输单元（以字节为单位）。 可能的值是 65536 字节 (64 KB) 的倍数，最多可到 4194304 字节 (4 MB)。  
> [!NOTE]  
>  当数据库具有配置 FILESTREAM，或包括或内存中 OLTP 文件组，`MAXTRANSFERSIZE`在还原时应大于或等于什么时创建备份时使用。  
  
##### <a name="error-management-options"></a>错误管理选项  
 这些选项允许你以确定是否为还原操作启用备份校验和和该操作是否停止上遇到错误。    
  
 { CHECKSUM | NO_CHECKSUM }  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 默认行为是在存在校验和时验证校验和，在不存在校验和时不进行验证并继续执行操作。  
  
 CHECKSUM  
 指定必须验证备份校验和，在备份缺少备份校验和的情况下，该选项将导致还原操作失败，并会发出一条消息表明校验和不存在。  
  
> [!NOTE]  
>  仅当使用备份校验和时，页校验和才与备份操作相关。  
  
 默认情况下，当遇到无效的校验和时，RESTORE 会报告校验和错误并停止。 然而，如果指定了 CONTINUE_AFTER_ERROR，RESTORE 会在返回校验和错误以及包含无效校验和的页面编号之后继续。  
  
 有关使用备份校验和的详细信息，请参阅[可能媒体错误期间备份和还原 &#40;SQL server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 NO_CHECKSUM  
 显式禁用还原操作的校验和验证功能。  
  
 { **STOP_ON_ERROR** |CONTINUE_AFTER_ERROR}  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 STOP_ON_ERROR  
 指定还原操作在遇到第一个错误时停止。 这是 RESTORE 的默认行为，但对于 VERIFYONLY 例外，后者的默认值是 CONTINUE_AFTER_ERROR。  
  
 CONTINUE_AFTER_ERROR  
 指定遇到错误后继续执行还原操作。  
  
 如果备份中包含损坏的页，则最好使用不包含错误的备用备份（例如，在页损坏之前进行的备份）来重复执行还原操作。 但是，作为最后的手段，您可以使用还原语句的 CONTINUE_AFTER_ERROR 选项来还原损坏的备份并尝试补救数据。  
  
##### <a name="filestream-options"></a>FILESTREAM 选项  
 FILESTREAM (DIRECTORY_NAME =*directory_name* )  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)和[RESTORE VERIFYONLY  ](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 与 Windows 兼容的目录名称。 此名称应在该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有数据库级 FILESTREAM 目录名称中保持唯一。 无论 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则如何设置，都应通过不区分大小写的形式进行唯一性比较。  
  
##### <a name="monitoring-options"></a>监视选项  
 这些选项使您可以监视与备份设备之间的数据传输。  
  
 统计信息 [  **=**  *百分比*]  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)和[RESTORE VERIFYONLY  ](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 每当另一个百分比完成时显示一条消息，并用于测量进度。 如果*百分比*省略，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每个 10%（大约） 完成后显示一条消息。  
  
 STATS 选项报告截止报告下一个间隔的阈值时的完成百分比。 此百分比接近于指定的百分比；例如，STATS=10 时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将按近似值报告该间隔；例如，此选项可能显示 43%，而不是精确地显示 40%。 对于大型的备份集，这不是问题因为非常缓慢已完成的 I/O 调用之间移动时完成百分比。  
  
##### <a name="tape-options"></a>磁带选项  
 这些选项只用于 TAPE 设备。 如果使用的是非磁带设备，则会忽略这些选项。  
  
 { **REWIND** | NOREWIND }  
 这些选项只用于 TAPE 设备。 如果正在使用非磁带设备，则忽略这些选项。  
  
 REWIND  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将释放和重绕磁带。 REWIND 是默认设置。  
  
 NOREWIND  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)和[RESTORE VERIFYONLY  ](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 指定任何其他还原语句中的 NOREWIND 都将生成错误。  
  
 指定在备份操作之后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 让磁带一直处于打开状态。 在对磁带执行多个备份操作时，可以使用此选项来改进性能。  
  
 NOREWIND 表示 NOUNLOAD，并且这些选项在单个 RESTORE 语句中不兼容。  
  
> [!NOTE]  
>  如果你使用 NOREWIND，实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前相同的进程中运行的备份或还原语句使用的后退或卸载选项，或服务器实例关闭的情况下一直保留磁带驱动器的所有权。 磁带保持打开将防止其他进程访问磁带。 有关如何显示打开的磁带列表以及如何关闭打开的磁带的信息，请参阅[备份设备 &#40;SQL server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 {**卸载**|NOUNLOAD}  
 **支持：**[还原](../../t-sql/statements/restore-statements-transact-sql.md)， [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)， [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)， [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)， [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)，和[RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。    
  
 这些选项只用于 TAPE 设备。 如果正在使用非磁带设备，则忽略这些选项。  
  
> [!NOTE]  
>  UNLOAD/NOUNLOAD 这一会话设置可在整个会话期间存在，或者在通过指定其他设置而进行重置之前一直存在。  
  
 UNLOAD  
 指定在备份完成后自动重绕并卸载磁带。 会话开始时 UNLOAD 是默认值。  
  
 NOUNLOAD  
 指定在之后，还原操作磁带保持加载磁带驱动器上。  
  
#### <a name="replicationwithoption"></a>< replication_WITH_option >  
 此选项只适用于在创建备份时对数据库进行了复制的情况。  
  
 KEEP_REPLICATION  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
使用 KEEP_REPLICATION 设置复制时要使用日志传送。 这样，在备用服务器上还原数据库或日志备份并恢复数据库时，可防止删除复制设置。 当使用 NORECOVERY 选项还原备份时，不允许指定此选项。 要确保复制功能在还原之后正常发挥作用，必须满足以下条件：  
  
-   **Msdb**和**master**温备用服务器上的数据库必须与同步**msdb**和**master**在主数据库服务器。  
  
-   必须重命名备用服务器，以使用与主服务器同样的名称。  
  
#### <a name="changedatacapturewithoption"></a>< change_data_capture_WITH_option >  
 此选项只适用于在创建备份时对数据库启用了变更数据捕获的情况。  
  
 KEEP_CDC  
 **支持：**[还原  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 KEEP_CDC 应该用于防止在其他服务器中还原数据库备份或日志备份并恢复数据库时删除变更数据捕获设置。 当使用 NORECOVERY 选项还原备份时，不允许指定此选项。  
  
 还原 KEEP_CDC 的数据库不会创建变更数据捕获作业。 若要在还原数据库后从日志中提取更改，请为还原的数据库重新创建捕获进程作业和清除作业。 有关信息，请参阅[sys.sp_cdc_add_job &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).  
  
 有关数据库镜像使用变更数据捕获的信息，请参阅[变更数据捕获和其他 SQL Server 功能](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)。  
  
#### <a name="servicebrokerwithoptions"></a>\<service_broker_WITH_options >  
 启用或禁用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息传递，或者设置新的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 标识符。 此选项只适用于在创建备份时为数据库启用（激活）了 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的情况。  
  
 {ENABLE_BROKER || ERROR_BROKER_CONVERSATIONS |NEW_BROKER}  
 **支持：**[还原数据库  ](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ENABLE_BROKER  
 指定[!INCLUDE[ssSB](../../includes/sssb-md.md)]消息传递时处于启用状态的末尾还原，以便可以立即发送消息。 默认情况下，还原期间禁用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息传递。 数据库保留现有的 Service Broker 标识符。  
  
 ERROR_BROKER_CONVERSATIONS  
 结束所有会话，并产生一个错误指出数据库已附加或还原。 这样，您的应用程序即可为现有会话执行定期清理。 在此操作完成之前，Service Broker 消息传递始终处于禁用状态，此操作完成后即处于启用状态。 数据库保留现有的 Service Broker 标识符。  
  
 NEW_BROKER  
 指定为数据库分配新的 Service Broker 标识符。 由于该数据库被视为新的 Service Broker，因此将立即删除数据库中的现有会话，而不生成结束对话框消息。 必须使用新标识符重新创建任何引用旧 Service Broker 标识符的路由。  
  
#### <a name="pointintimewithoptions"></a>\<point_in_time_WITH_options >  
 **支持：**[还原 {数据库 |日志}](../../t-sql/statements/restore-statements-transact-sql.md) ，并且仅用于完整或大容量日志恢复模式。    
  
 通过在 STOPAT、STOPATMARK 或 STOPBEFOREMARK 子句中指定目标恢复点，可以将数据库还原到特定时间点或事务点。 指定的时间或事务始终从日志备份还原。 在还原序列的每个 RESTORE LOG 语句中，必须在相同的 STOPAT、STOPATMARK 或 STOPBEFOREMARK 子句中指定目标时间或事务。  
  
 作为时点还原的先决条件，必须首先还原其端点早于目标恢复点的完整数据库备份。 为帮助识别要还原哪个数据库备份，您可以选择在 RESTORE DATABASE 语句中指定 WITH STOPAT、STOPATMARK 或 STOPBEFOREMARK 子句，以便在数据备份太靠近指定的目标时间的情况下引发错误。 但将始终还原完整数据备份，即使它包含目标时间。  
  
> [!NOTE]  
>  RESTORE_DATABASE 和 RESTORE_LOG 时间点 WITH 选项相似，但仅还原日志支持*mark_name*自变量。  
  
 { STOPAT | STOPATMARK | STOPBEFOREMARK }   
 
 STOPAT  **=**  { *datetime*  |   **@** *datetime_var* }  
 指定数据库还原到截至日期和指定的时间的状态*datetime*或 **@**  *datetime_var*参数。 有关指定的日期和时间的信息，请参阅[日期和时间数据类型和函数 &#40;Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 如果变量用于 STOPAT，该变量必须是**varchar**， **char**， **smalldatetime**，或**datetime**数据类型。 只有在指定的日期和时间前写入的事务日志记录才能应用于数据库。  
  
> [!NOTE]  
>  如果指定的 STOPAT 时间是在最后日志备份之后，则数据库将继续处于未恢复状态，如同以 NORECOVERY 运行 RESTORE LOG 时的情况。  
  
 有关详细信息，请参阅[将 SQL Server 数据库还原到某个时间点（完整恢复模式）](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
 STOPATMARK  **=**  { *mark_name* | lsn:*lsn_number* } [AFTER *datetime* ]  
 指定恢复至指定的恢复点。 恢复中包括指定的事务，但是，仅当该事务最初于实际生成事务时已获得提交，才可进行本次提交。  
  
 还原数据库和还原日志支持*lsn_number*参数。 该参数指定了一个日志序列号。  
  
 *Mark_name*参数仅受 RESTORE LOG 语句。 此参数在日志备份中标识一个事务标记。  
  
 在 RESTORE LOG 语句中，如果后的*datetime*是省略，在具有指定名称的第一个标记处停止恢复。 如果之后*datetime*指定，在具有指定的名称时或之后的第一个标记处停止恢复*datetime*。  
  
> [!NOTE]  
>  如果指定的标记、LSN 或时间是在最后日志备份之后，则数据库将继续处于未恢复状态，如同以 NORECOVERY 运行 RESTORE LOG 的情况。  
  
 有关详细信息，请参阅[使用标记的事务一致恢复相关数据库 &#40;完整恢复模式 &#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)和[恢复到日志序列号 &#40;SQL server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md).  
  
 STOPBEFOREMARK  **=**  { *mark_name* | lsn:*lsn_number* } [AFTER *datetime* ]  
 指定恢复至指定的恢复点为止。 在恢复中不包括指定的事务，且在使用 WITH RECOVERY 时将回滚。  
  
 还原数据库和还原日志支持*lsn_number*参数。 该参数指定了一个日志序列号。  
  
 *Mark_name*参数仅受 RESTORE LOG 语句。 此参数在日志备份中标识一个事务标记。  
  
 在 RESTORE LOG 语句中，如果后的*datetime*省略，则恢复将只在具有指定名称的第一个标记之前停止。 如果之后*datetime*恢复停止只是第一个标记具有指定的名称时之前或之后的指定*datetime*。  
  
> [!IMPORTANT]  
>  如果部分还原顺序不包括任何 FILESTREAM 文件组，则不支持时点还原。 可以强制该还原顺序以继续执行操作。 但是，还原语句中省略的 FILESTREAM 文件组永远无法还原。 若要强制进行时点还原，请将 CONTINUE_AFTER_ERROR 选项与 STOPAT、STOPATMARK 或 STOPBEFOREMARK 选项一起指定。 如果指定 CONTINUE_AFTER_ERROR，则部分还原顺序将成功，但 FILESTREAM 文件组将不可恢复。  
  
## <a name="result-sets"></a>结果集  
 有关结果集，请参阅下列主题：  
  
-   [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
## <a name="remarks"></a>注释  
 有关其他备注，请参阅下列主题：  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="specifying-a-backup-set"></a>指定备份集  
 A*备份集*包含来自单个、 成功的备份操作的备份。 RESTORE、RESTORE FILELISTONLY、RESTORE HEADERONLY 和 RESTORE VERIFYONLY 语句对指定的一个或多个备份设备上的介质集中的单个备份集进行操作。 应从介质集中指定您需要的备份。 你可以通过使用 *RESTORE HEADERONLY* 语句来获取备份集的 [backup_set_file_number](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 。  
  
 用于指定要还原的备份集的选项是：  
  
 文件 **=** { *backup_set_file_number* | **@***backup_set_file_number* }  
  
 其中*backup_set_file_number*指示备份在介质集中的位置。 A *backup_set_file_number*的 1 (文件 = 1) 指示的第一个备份集在备份介质上和*backup_set_file_number*的 2 (文件 = 2) 表示第二个备份集，依此类推。  
  
 此选项的行为而异语句下, 表中所述：  
  
|。|备份集 FILE 选项的行为|  
|---------------|-----------------------------------------|  
|RESTORE|默认备份集文件号为 1。 一个 RESTORE 语句中只允许使用一个备份集 FILE 选项。 一定要按顺序指定备份集。|  
|RESTORE FILELISTONLY|默认备份集文件号为 1。|  
|RESTORE HEADERONLY|默认情况下，对介质集中的所有备份集进行处理。 RESTORE HEADERONLY 的结果集返回有关每个备份集的信息包括其**位置**中的媒体设置。 若要返回上给定的备份集的信息，请使用作为其位置数目*backup_set_file_number*文件选项中的值。<br /><br /> 注意： 对于磁带媒体还原标头仅处理加载的磁带上的备份集。|  
|RESTORE VERIFYONLY|默认值*backup_set_file_number*为 1。|  
  
> [!NOTE]  
>  用于指定备份集的文件选项与用于指定数据库文件，文件的文件选项无关 **=**  { *logical_file_name_in_backup*  |  **@**  *logical_file_name_in_backup_var* }。  
  
## <a name="summary-of-support-for-with-options"></a>WITH 选项支持摘要  
 仅还原语句支持以下选项： 块大小、 BUFFERCOUNT、 MAXTRANSFERSIZE、 部分、 KEEP_REPLICATION，{恢复 |NORECOVERY |待机状态}，替换、 重新启动、 RESTRICTED_USER，和 {STOPAT |STOPATMARK |STOPBEFOREMARK}  
  
> [!NOTE]  
>  PARTIAL 选项仅受 RESTORE DATABASE 支持。  
  
 下表列出了受一个或多个语句支持的 WITH 选项，并指明每个选项受哪些语句的支持。 选中标记 (√) 表示支持选项；短划线 (—) 表示不支持选项。  
  
|WITH 选项|RESTORE|RESTORE FILELISTONLY|RESTORE HEADERONLY|RESTORE LABELONLY|RESTORE REWINDONLY|RESTORE VERIFYONLY|  
|-----------------|-------------|--------------------------|------------------------|-----------------------|------------------------|------------------------|  
|{ CHECKSUM<br /><br /> &#124;NO_CHECKSUM}|√|√|√|√|—|√|  
|{ CONTINUE_AFTER_ERROR<br /><br /> &#124;STOP_ON_ERROR}|√|√|√|√|—|√|  
|文件<sup>1</sup>|√|√|√|—|—|√|  
|LOADHISTORY|—|—|—|—|—|√|  
|MEDIANAME|√|√|√|√|—|√|  
|MEDIAPASSWORD|√|√|√|√|—|√|  
|MOVE|√|—|—|—|—|√|  
|PASSWORD|√|√|√|—|—|√|  
|{后退 &#124;NOREWIND}|√|仅限 REWIND|仅限 REWIND|仅限 REWIND|—|√|  
|STATS|√|—|—|—|—|√|  
|{卸载 &#124;NOUNLOAD}|√|√|√|√|√|√|  
  
 <sup>1</sup>文件 **=**  *backup_set_file_number*，即不同于 {文件 |文件组}。  
  
## <a name="permissions"></a>Permissions  
 有关权限，请参阅下列主题：  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="examples"></a>示例  
 有关示例，请参阅下列主题：  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY (Transact-SQL)](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE REWINDONLY (Transact-SQL)](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)  
  
  


