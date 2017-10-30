---
title: "DBCC SHRINKDATABASE (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: 62
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7f6e9fa3feea20bfeb82037cb9358370c67aaa0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

收缩指定数据库中的数据文件和日志文件的大小。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 *database_name* | *database_id* | 0  
 要收缩的数据库的名称或 ID。 如果指定 0，则使用当前数据库。  
  
 *target_percent*  
 数据库收缩后的数据库文件中所需的剩余可用空间百分比。  
  
 NOTRUNCATE  
 通过将已分配的页从文件末尾移动到文件前面的未分配页来压缩数据文件中的数据。 *target_percent*是可选的。  
  
 文件末尾的可用空间不会返回给操作系统，文件的物理大小也不会更改。 因此，指定 NOTRUNCATE 时，数据库看起来未收缩。  
  
 NOTRUNCATE 只适用于数据文件。 日志文件不受影响。  
  
 TRUNCATEONLY  
 将文件末尾的所有可用空间释放给操作系统，但不在文件内部执行任何页移动。 数据文件只收缩到最后分配的区。 *target_percent*如果使用 TRUNCATEONLY 指定将被忽略。  
  
 TRUNCATEONLY 将影响日志文件。 若要仅截断数据文件，请使用 DBCC SHRINKFILE。  
  
 WITH NO_INFOMSGS  
 取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
下表对结果集中的列进行了说明。
  
|列名|Description|  
|-----------------|-----------------|  
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]试图收缩的文件的数据库标识号。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]尝试收缩的文件的文件标识号。|  
|**CurrentSize**|文件当前占用的 8 KB 页数。|  
|**MinimumSize**|文件最低可以占用的 8 KB 页数。 这与文件的最小大小或最初创建时的大小相对应。|  
|**UsedPages**|文件当前使用的 8 KB 页数。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]估计文件能够收缩到的 8 KB 页数。|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]不显示未收缩的文件的行。  
  
## <a name="remarks"></a>注释  
若要收缩特定数据库的所有数据和日志文件，请执行 DBCC SHRINKDATABASE 命令。 若要收缩一个数据或同时为特定数据库日志文件，执行[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)命令。
  
若要查看数据库中的当前可用 （未分配） 空间量，运行[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)。
  
可在进程中的任一点停止 DBCC SHRINKDATABASE 操作，任何已完成的工作都将保留。
  
收缩后的数据库不能小于数据库的最小大小。 最小大小是在数据库最初创建时指定的大小，或是使用文件大小更改操作（如 DBCC SHRINKFILE 或 ALTER DATABASE）显式设置的最后大小。 例如，如果数据库最初创建大小为 10 MB 的大小，并可增长到 100 MB，最小的数据库可缩减为 10 MB，即使是在数据库中的所有数据都已都删除。
  
运行 DBCC SHRINKDATABASE 而不指定 NOTRUNCATE 选项或 TRUNCATEONLY 选项等价于带 NOTRUNCATE 运行 DBCC SHRINKDATABASE 操作，然后再带 TRUNCATEONLY 运行 DBCC SHRINKDATABASE 操作。
  
要收缩的数据库不必在单用户模式下；其他的用户仍可以在数据库收缩时对其进行工作。 这也包括系统数据库。
  
不能在备份数据库时收缩数据库。 反之，也不能在数据库执行收缩操作时备份数据库。
  
## <a name="how-dbcc-shrinkdatabase-works"></a>DBCC SHRINKDATABASE 的工作原理  
DBCC SHRINKDATABASE 以每个文件为单位对数据文件进行收缩。然而，DBCC SHRINKDATABASE 在对日志文件进行收缩时，它将视为所有的日志文件都存在于一个连续的日志池中。 文件始终从末尾开始收缩。
  
假定一个名为数据库**mydb**使用数据的文件和两个日志文件。 数据和日志文件为 10 MB 和数据文件将包含 6 MB 的数据。
  
对于每个文件，[!INCLUDE[ssDE](../../includes/ssde-md.md)]都会计算一个目标大小。 这就是文件将要收缩到的大小。 当使用指定的 DBCC SHRINKDATABASE *target_percent*、[!INCLUDE[ssDE](../../includes/ssde-md.md)]计算目标大小*target_percent*收缩后文件中的可用空间量。 例如，如果你指定*target_percent*收缩的 25 个**mydb**、[!INCLUDE[ssDE](../../includes/ssde-md.md)]计算为 8 MB （6 MB 的数据加上 2 MB 的可用空间） 的数据文件的目标大小。 因此，[!INCLUDE[ssDE](../../includes/ssde-md.md)]从最后一个的 2 MB 的数据文件的任何数据移动到任何在第一个 8 MB 的数据文件的可用空间并将文件然后收缩。
  
假定数据文件的**mydb**包含 7 MB 的数据。 指定*target_percent* 30 的允许用于此数据文件收缩到免费的 30 百分比。 但是，指定*target_percent*的 40 不收缩数据文件，因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]不将将文件收缩到小于数据当前占用的大小。 您也可以将此问题的另一种方法： 40%想可用空间 + 70%完整的数据文件 (带 10 MB 的 7 MB) 为多个 100%。 因为免费是您想要的百分比和当前数据文件所占的百分比大于 100%（以 10%) 的任何*target_size*大于 30 将不会收缩数据文件。
  
为日志文件，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用*target_percent*来计算目标大小的整个日志; 因此， *target_percent*后收缩操作日志中的可用空间量。 之后，整个日志的目标大小转换为每个日志文件的目标大小。
  
DBCC SHRINKDATABASE 尝试立即将每个物理日志文件收缩到其目标大小。 如果虚拟日志中的所有逻辑日志部分都没有超出日志文件的目标大小，则该文件将成功截断，DBCC SHRINKDATABASE 完成且不显示任何消息。 但是，如果部分逻辑日志位于超出目标大小的虚拟日志中，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将释放尽可能多的空间，并发出一条信息性消息。 该消息说明需要执行哪些操作来将逻辑日志移出位于文件末尾的虚拟日志。 执行该操作以后，DBCC SHRINKDATABASE 可用于释放剩余空间。
  
因为日志文件只能收缩到虚拟日志文件边界，所以可能无法将日志文件收缩到比虚拟日志文件更小（即使现在没有使用该文件）。 虚拟日志文件的大小在创建或扩展这些日志文件时由[!INCLUDE[ssDE](../../includes/ssde-md.md)]动态选择。
  
## <a name="best-practices"></a>最佳实践  
当您计划收缩数据库时，请考虑以下信息：
-   在执行会产生许多未使用空间的操作（如截断表或删除表操作）后，执行收缩操作最有效。  
-   大多数数据库都需要一些可用空间，以供常规日常操作使用。 如果反复收缩数据库并注意到数据库大小变大，则表明收缩的空间是常规操作所必需的。 在这种情况下，反复收缩数据库是一种无谓的操作。  
-   收缩操作不会保留数据库中索引的碎片状态，通常还会在一定程度上增加碎片。 这是不要反复收缩数据库的另一个原因。  
-   除非有特定要求，否则不要将 AUTO_SHRINK 数据库选项设置为 ON。  
  
## <a name="troubleshooting"></a>故障排除  
 收缩操作才会被阻止下运行的事务可能[行基于版本控制的隔离级别](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。 例如，执行 DBCC SHRINK DATABASE 操作时，如果在基于行版本控制的隔离级别下运行的大型删除操作正在进行中，则收缩操作将等到删除操作完成才会收缩文件。 出现这种情况时，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 操作会在第一个小时每五分钟将信息性消息（对于 SHRINKDATABASE 为 5202，对于 SHRINKFILE 为 5203）输出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志，之后每一个小时输出一次。 例如，如果错误日志包含以下错误消息：  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
这意味着收缩操作被时间戳早于 109 的快照事务阻塞，它是收缩操作所完成的上一事务。 它还指示**transaction_sequence_num**，或**first_snapshot_sequence_num**中的列[sys.dm_tran_active_snapshot_database_transactions &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)动态管理视图包含值为 15。 如果任一**transaction_sequence_num**，或**first_snapshot_sequence_num**列在视图中的包含的数字小于最后一个事务已完成通过执行收缩操作 (109)收缩操作将等待这些事务完成。
  
若要解决此问题，你可以执行以下任务之一：
-   终止阻塞收缩操作的事务。  
-   终止收缩操作。 将保留任何已完成的工作。  
-   不执行任何操作，并允许收缩操作等到阻塞事务完成。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. 收缩数据库并指定可用空间的百分比  
 以下示例将减小 `UserDB` 用户数据库中数据文件和日志文件的大小，以便在数据库中留出 10% 的可用空间。  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. 截断数据库  
 以下示例使 `AdventureWorks` 示例数据库中的数据和日志文件收缩到最后分配的区。  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[收缩数据库](../../relational-databases/databases/shrink-a-database.md)
  
  

