---
title: "DBCC SHRINKFILE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
caps.latest.revision: "87"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 94ad5652920129790045e33c93e2a8fbb83816bd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

收缩当前数据库的指定数据或日志文件的大小，或通过将数据从指定的文件移动到相同文件组中的其他文件来清空文件，以允许从数据库中删除该文件。 文件大小可以收缩到比创建该文件时所指定的大小更小。 这样会将最小文件大小重置为新值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
*file_name*  
要收缩的文件的逻辑名称。
  
*file_id*  
要收缩的文件的标识 (ID) 号。 若要获取文件 ID，请使用[FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)系统函数或查询[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)目录视图中当前的数据库。
  
*target_size*  
用兆字节表示的文件大小（用整数表示）。 如果未指定，则 DBCC SHRINKFILE 将文件大小减少到默认文件大小。 默认大小为创建文件时指定的大小。
  
> [!NOTE]  
>  你可以通过使用 DBCC SHRINKFILE 减少的空文件的默认大小*target_size*。 例如，如果创建一个 5 MB 的文件，然后在文件仍然为空的时候将文件收缩为 3 MB，默认文件大小将设置为 3 MB。 这只适用于永远不会包含数据的空文件。  
  
FILESTREAM 文件组容器不支持此选项。  
如果*target_size*指定，DBCC SHRINKFILE 尝试将文件收缩到指定的大小。 将要释放的文件部分中的已使用页重新定位到保留的文件部分中的可用空间。 例如，如果没有 10 MB 的数据文件，DBCC SHRINKFILE 操作*target_size* 8 原因的所有页中使用最后一个的 2 MB 的文件可以重新分配到第一个 8 MB 的文件中任何未分配的页。 DBCC SHRINKFILE 不会将文件收缩到小于存储文件中的数据所需要的大小。 例如，如果使用 7 MB 的 10 MB 的数据文件时，具有的 DBCC SHRINKFILE 语句*target_size*的 6 将文件收缩到仅 7 MB，可不 6 MB。
  
EMPTYFILE  
将所有数据从指定的文件都迁移到其他文件**相同的文件组**。 换而言之，清空文件将迁移数据，从指定的文件到同一个文件组中的其他文件。 清空文件可确保你没有新数据将添加到文件。可以通过删除该文件[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)语句。
对于 FILESTREAM 文件组容器，将无法使用 ALTER DATABASE 删除该文件，直到已运行垃圾收集器并删除了 EMPTYFILE 已复制到其他容器的所有多余文件组容器文件。 有关详细信息，请参阅[sp_filestream_force_garbage_collection &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  有关删除 FILESTREAM 容器的信息，请参阅中的相应部分[ALTER DATABASE 文件和文件组选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
NOTRUNCATE  
移动到未分配的页前面或还未指定的文件从数据文件的末尾分配页*target_percent*。 文件末尾的可用空间不会返回给操作系统，文件的物理大小也不会更改。 因此，指定 NOTRUNCATE 时，文件看起来未收缩。
NOTRUNCATE 只适用于数据文件。 日志文件不受影响。   FILESTREAM 文件组容器不支持此选项。
  
TRUNCATEONLY  
将文件末尾的所有可用空间释放给操作系统，但不在文件内部执行任何页移动。 数据文件只收缩到最后分配的区。
*target_size*如果使用 TRUNCATEONLY 指定将被忽略。  
TRUNCATEONLY 选项不会移动日志中的信息，但会删除日志文件末尾的失效 VLF。 FILESTREAM 文件组容器不支持此选项。
  
WITH NO_INFOMSGS  
取消显示所有信息性消息。
  
## <a name="result-sets"></a>结果集  
下表对结果集中的列进行了说明。
  
|列名|Description|  
|---|---|
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]试图收缩的文件的数据库标识号。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]试图收缩的文件的文件标识号。|  
|**CurrentSize**|文件当前占用的 8 KB 页数。|  
|**MinimumSize**|文件最低可以占用的 8 KB 页数。 这与文件的最小大小或最初创建时的大小相对应。|  
|**UsedPages**|文件当前使用的 8 KB 页数。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]估计文件能够收缩到的 8 KB 页数。|  
  
## <a name="remarks"></a>注释  
DBCC SHRINKFILE 适用于当前数据库中的文件。 有关如何更改当前数据库的详细信息，请参阅[使用 &#40;Transact SQL &#41;](../../t-sql/language-elements/use-transact-sql.md).
  
可在进程中的任一点停止 DBCC SHRINKFILE 操作，任何已完成的工作都将保留。
  
当的 DBCC SHRINKFILE 操作失败时，将引发错误。
  
 要收缩的数据库不必在单用户模式下；收缩文件时，其他用户也可使用该数据库。 不必在单用户模式下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以对系统数据库进行收缩。  
  
## <a name="shrinking-a-log-file"></a>收缩日志文件  
为日志文件，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用*target_size*来计算目标大小的整个日志; 因此， *target_size*后收缩操作日志中的可用空间量。 然后，整个日志的目标大小被转换为每个日志文件的目标大小。 DBCC SHRINKFILE 尝试立即将每个物理日志文件收缩到其目标大小。 但是，如果部分逻辑日志位于超出目标大小的虚拟日志中，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将释放尽可能多的空间，并发出一条信息性消息。 该消息说明需要执行哪些操作来将逻辑日志移出位于文件末尾的虚拟日志。 执行这些操作以后，DBCC SHRINKFILE 可用于释放剩余空间。
  
因为日志文件只能收缩到虚拟日志文件边界，所以可能无法将日志文件收缩到比虚拟日志文件更小（即使现在没有使用该文件）。 虚拟日志文件的大小在创建或扩展这些日志文件时由[!INCLUDE[ssDE](../../includes/ssde-md.md)]动态选择。
  
## <a name="best-practices"></a>最佳实践  
在计划收缩文件时，请考虑以下信息：
-   在执行会产生许多未使用空间的操作（如截断表或删除表操作）后，执行收缩操作最有效。  
-   大多数数据库都需要一些可用空间，以供常规日常操作使用。 如果反复收缩数据库并注意到数据库大小变大，则表明收缩的空间是常规操作所必需的。 在这种情况下，反复收缩数据库是一种无谓的操作。  
-   收缩操作不会保留数据库中索引的碎片状态，通常还会在一定程度上增加碎片。 这是不要反复收缩数据库的另一个原因。  
-   按顺序而非同时缩小同一数据库中的多个文件。 系统表上的连接可能会因为阻止而导致延迟。  
  
## <a name="troubleshooting"></a>故障排除  
本部分介绍如何诊断和更正在运行 DBCC SHRINKFILE 命令时可能发生的问题。
  
### <a name="the-file-does-not-shrink"></a>文件不收缩  
如果收缩操作运行时未出现错误，但文件大小看起来没有发生更改，则请执行下列操作之一以验证文件是否有足够的可用空间可供删除：
- 运行以下查询。  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   运行[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)命令中来返回用于事务日志的空间。  
如果可用空间不足，则收缩操作无法进一步减小文件大小。
  
通常，日志文件看起来不收缩。 这通常是由于未截断日志文件的原因造成的。 可以通过将数据库恢复模式设置为 SIMPLE 或者通过备份日志然后再次运行 DBCC SHRINKFILE 操作来截断日志。
  
### <a name="the-shrink-operation-is-blocked"></a>收缩操作被阻塞  
收缩操作才会被阻止下运行的事务可能[行基于版本控制的隔离级别](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。 例如，执行 DBCC SHRINK DATABASE 操作时，如果在基于行版本控制的隔离级别下运行的大型删除操作正在进行中，则收缩操作将等到删除操作完成才会收缩文件。 出现这种情况时，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 操作会在第一个小时每五分钟将信息性消息（对于 SHRINKDATABASE 为 5202，对于 SHRINKFILE 为 5203）输出到 SQL Server 错误日志，之后每一个小时输出一次。 例如，如果错误日志包含以下错误消息，则会发生以下错误：
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
这意味着收缩操作被时间戳早于 109 的快照事务阻塞，它是收缩操作所完成的上一事务。 它还指示**transaction_sequence_num**，或**first_snapshot_sequence_num**中的列[sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)动态管理视图包含值为 15。 如果任一**transaction_sequence_num**，或**first_snapshot_sequence_num**列在视图中的包含的数字小于最后一个事务已完成通过执行收缩操作 (109)收缩操作将等待这些事务完成。
  
若要解决此问题，请执行下列任务之一：
-   终止阻塞收缩操作的事务。
-   终止收缩操作。 如果终止收缩操作，则会保留任何已完成的工作。  
-   不执行任何操作，并允许收缩操作等到阻塞事务完成。  
  
## <a name="permissions"></a>权限  
要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。
  
## <a name="examples"></a>示例  
  
### <a name="a-shrinking-a-data-file-to-a-specified-target-size"></a>A. 将数据文件收缩到指定的目标大小  
下面的示例收缩的名为的数据文件大小`DataFile1`中`UserDB`到 7 MB 的用户数据库。
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="b-shrinking-a-log-file-to-a-specified-target-size"></a>B. 将日志文件收缩到指定的目标大小  
以下示例将 `AdventureWorks` 数据库中的日志文件收缩到 1 MB。 若要允许 DBCC SHRINKFILE 命令收缩文件，首先需要通过将数据库恢复模式设置为 SIMPLE 来截断该文件。
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. 截断数据文件  
下面的示例将截断 `AdventureWorks` 数据库中的主数据文件。 需要查询 `sys.database_files` 目录视图以获得数据文件的 `file_id`。
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. 清空文件  
以下示例演示了清空文件以便从数据库中将其删除的步骤。 针对此示例，首先创建一个数据文件，并假设该文件包含数据。
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40;Transact SQL &#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[收缩文件](../../relational-databases/databases/shrink-a-file.md)
  
  
